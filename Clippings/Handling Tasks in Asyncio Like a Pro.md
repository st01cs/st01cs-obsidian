---
title: "Handling Tasks in Asyncio Like a Pro"
source: "https://jacobpadilla.com/articles/handling-asyncio-tasks"
author:
  - "[[Jacob Padilla]]"
published: 2024-02-14
created: 2025-09-30
description: "I first go over the basics of an Asyncio task object and then talk about all of the various ways to handle them and the pros and cons of each."
tags:
  - "clippings"
---
Python’s Asyncio module is a great way to handle IO-bound jobs and has seen many improvements in recent Python updates. However, there are so many ways to handle async tasks that figuring out which method to use for different scenarios can be a bit confusing. In this article, I’ll first go over the basics of what a task object is and then talk about all of the different ways to handle them and the pros and cons of each.

## What's a Task

Before talking about tasks, it’s important to understand how Asyncio coroutines work since a task object is just a coroutine wrapper that can run asynchronously.

## Coroutines

To create a coroutine object, all you need to do is add the `async` keyword to the front of a function/method definition. This signifies that the function is able to be stopped and started via the event loop (if the coroutine has its own `await` keywords). When calling a coroutine function, instead of the actual function being run, a coroutine object is created. This object then needs to be waited upon with the `await` keyword, which will then run the code in the coroutine.

Below is an example of how to create a coroutine and then run the code inside of the coroutine object using `await`:

```python
import asyncio

async def my_function():
    print(‘Hello World’)

async def main():
    coro = my_function()
    print(type(coro))

    await coro

asyncio.run(main())
```

In the example, we first call `my_function`, which creates the coroutine object, which we can see via the print statement. Then to print “Hello World,” we use the `await` keyword to pause the execution of `main` and run `my_function`. The full output is:

```
<class ‘coroutine’>
Hello World
```

## Scheduled Coroutines

After making a coroutine, you generally want to wrap it in an `asyncio.Task` object. Creating a task will automatically schedule the coroutine to be run by appending the task object to the event loop (basically just a list of task objects). To create a task object, you can use the `asyncio.create_task(coro, *, name=None, context=None)` function. This function takes a coroutine object as well as two optional keyword arguments. The first optional argument is `name`, which lets you give the task object a name so that you can remember what it does. You can also set the name after creating the task object via `Task.set_name(name)` and then get the task name via `Task.get_name()`. The other keyword argument, added in 3.11, is `context`, which lets you give the task a [context variable](https://superfastpython.com/asyncio-context-variables/)  to implement local storage inside the task (sort of similar to the `Threading.local()` object but for async tasks). The `name` argument can be pretty useful, but `context` is pretty rarely used.

Another important thing to note is that the event loop only stores [weak references](https://stackoverflow.com/questions/9908013/weak-references-in-python)  to the task objects. So, if you just write `asyncio.create_task(my_function())`, the garbage collector will destroy the task. Instead, you need to store a non-weak reference to all tasks by storing the task object returned from `create_task` in either a variable or other object.

Here’s a basic example of using a task object:

```python
import asyncio

async def my_function():
    print(‘Hello World’)

async def main():
    task = asyncio.create_task(my_function())
    print(type(task))
    await task

asyncio.run(main())
```

Output:

```
<class ‘_asyncio.Task’>
Hello World
```

Besides just waiting for the task to finish, you can also cancel it with `Task.cancel()`, add a callback function to be called when the task finishes with `Task.add_done_callback(cb)`, manually check if the coroutine is done running with `Task.done()`, or get the result of the wrapped coroutine when the task is done with `Task.result()`; checkout the complete list of [Task methods in Python’s documentation](https://docs.python.org/3/library/asyncio-task.html#asyncio.Task).

Here’s the same example from above, but with some of these task methods in use:

```python
import asyncio

async def my_function():
    return ‘Hello World!‘

async def main():
    task = asyncio.create_task(my_function())
    
    print(task.done())  # Will print False
    await task
    print(task.done())  # Will print True
    
    print(task.result())  # Will print Hello World!

asyncio.run(main())
```

While we generally create tasks and then use some method to wait for them to be done, if you want to create a task and then simply forget about it, you can utilize the following pattern. This is straight out of the Asyncio documentation; it creates tasks, adds them to a set so that there is a reference to them, and then when the task is done, it is discarded from the set via a callback.

```python
background_tasks = set()

for _ in range(10):
    task = asyncio.create_task(some_coro())
    background_tasks.add(task)
    task.add_done_callback(background_tasks.discard)
```

## Wait for a Single Task

Now that we've discussed coroutines and task objects, we're ready to talk about ways to manage them more elegantly. While the `await` keyword is fundamental for pausing the current coroutine until the awaitable (such as a coroutine, task, or future) being waited upon with `await` completes, it inherently focuses on one operation at a time. This article is leading towards using Asyncio's built-in functions to aggregate multiple tasks into a single awaitable object and then use `await` on that single object.

While most of Asyncio’s functions are for waiting on multiple tasks, there’s one function meant to wait for a single awaitable called `wait_for`. Let’s talk about that one first:

## asyncio.wait\_for

The next step up from a simple `await` is the `wait_for` function.

```
asyncio.wait_for(aw, timeout)
```

This function takes in a single awaitable object (it automatically wraps coroutines in a task object so that it can be run on the event loop) and waits for it to be done. But unlike a simple `await`, It also allows you to add a timeout - if the task takes longer than the allotted time to finish, a `TimeoutError` will be raised, and the task inside of `wait_for` is canceled.

```python
async def slow_function():
    await asyncio.sleep(100)

async def main():
    try:
        await asyncio.wait_for(slow_function(), timeout=5.0)
    except TimeoutError:
        print(‘Function was too slow :(‘)

asyncio.run(main())
```

Because the coroutine function tried to sleep for 100 seconds, a TimeoutError was raised since the timeout in `wait_for` was only set to 5 seconds:

```
Function was too slow :(
```

## Wait for Multiple Tasks

Now, let’s get to the interesting stuff - awaiting multiple tasks! There are three main ways to wait for a collection of tasks; each has its pros and cons and can be helpful in different scenarios.

## asyncio.wait

Our first option is similar to `wait_for` but for a collection (such as a list, tuple, or set) of either task or lower-level future objects.

```
asyncio.wait(collection_of_tasks, *, timeout=None, return_when=ALL_COMPLETED)
```

This function returns a tuple containing two sets; the first set is the finished tasks, and the second are the ones that aren’t done yet. Tasks that are finished before the timeout or the `return_when` directive go into the finished task set, and ones that aren’t are put in the second set, often called `pending`  or `_` if you don’t plan on using them. However, unlike ‘asyncio.wait\`, the unfinished tasks are not canceled when a timeout occurs.

The `return_when` argument lets you tell `asyncio.wait` to return when one of the following three things happen:

- `FIRST_COMPLETED` returns when the first task finishes or is canceled.
- `FIRST_EXCEPTION` returns when one of the tasks causes an exception or they all finish.
- `ALL_COMPLETED` is the default and will return when all futures are finished or canceled.

Let’s see this in action:

```python
import asyncio
import random

async def job():
    await asyncio.sleep(random.randint(1, 5))

async def main():
    tasks = [
        asyncio.create_task(job(), name=index)
        for index in range(1, 5)
    ]

    done, pending = await asyncio.wait(tasks, return_when=asyncio.FIRST_COMPLETED)

    print(f’The first task completed was {done.pop().get_name()}’)

asyncio.run(main())
```

Output:

```
The first task completed was 4
```

## asyncio.gather

Next, let’s take a look at `asyncio.gather(*aws, return_exceptions=False)`.

Unlike `wait_for`, which takes a collection of only tasks or future objects, `gather` takes any number of tasks, futures, or even coroutine objects as a bunch of positional arguments. However, any coroutine objects passed into the function are automatically scheduled as task objects so that they can run on the event loop. Once all the tasks are finished, all return values, obtained via `Task.result()`, are returned as a single list. One of the nicest things about `gather` is that the list being returned holds the tasks in the exact order in which they were passed into the function!

Another nice thing about `gather` is that it’s the only one of the three functions that can gracefully return exceptions. If the `return_exceptions` keyword argument is set to `True`, the returned list will contain any exception caused by the tasks in place of where the task’s result value would have been.

Let’s look at an example of how this works:

```python
import asyncio
import random

async def job(id):
    print(f’Starting job {id}’)
    await asyncio.sleep(random.randint(1, 3))
    print(f’Finished job {id}’)
    return id

async def main():
    # create a list of worker tasks
    coros = [job(i) for i in range(4)]
    
    # gather the results of all worker tasks
    results = await asyncio.gather(*coros)
    
    # print the results
    print(f’Results: {results}’)

asyncio.run(main())
```

First, we make a list of coroutine objects and then use the `*` symbol to unpack them into positional arguments for the `gather` function to accept. Awaiting the object returned by `gather` will then start running the tasks until they are eventually all done. Notice how the resulting list of return values matches the order in which the tasks were put into `gather` despite the tasks finishing in a random order due to `await asyncio.sleep(random.randint(1,3))`.

```
Starting job 0
Starting job 1
Starting job 2
Starting job 3
Finished job 3
Finished job 0
Finished job 1
Finished job 2
Results: [0, 1, 2, 3]
```

In the next example, I’m putting two coroutines directly into `gather` and are setting `return_exceptions` to `True`, which gracefully returns the exceptions in the same result list:

```python
import asyncio

async def task1():
    raise ValueError()

async def task2():
    raise KeyError()

async def main():
    results = await asyncio.gather(task1(), task2(), return_exceptions=True)
    print(results)  # Will print [ValueError(), KeyError()]

asyncio.run(main())
```

One last feature of `asyncio.gather` is that just like how you can cancel an individual task with `Task.cancel()`, the object that `gather` returns (to then be awaited) has its own `cancel()` method which will loop through all of the tasks that it’s managing and cancel all of them.

## asyncio.as\_completed

The next one is a bit different from the above two; Instead of returning a set or list of the results all at once, `as_completed` returns an iterable object that lets you handle results as they finish! It accepts all types of awaitables (generally either coroutines, tasks, and futures) and like many of the other methods, also has a   `timeout` keyword argument, which will raise a `TimeoutError` if the tasks haven’t finished by the specified time.

```
asyncio.as_completed(aws, *, timeout=None)
```

The following is an example of how `as_completed` works:

```python
import asyncio

async def my_task(id):
    return f’I am number {id}’

async def main():
    tasks = [my_task(id) for id in range(5)]
    
    for coro in asyncio.as_completed(tasks):
        result = await coro
        print(result)

asyncio.run(main())
```

We can see that the output is random, as it just prints out whichever finishes first:

```
I am number 3
I am number 0
I am number 4
I am number 2
I am number 1
```

## Wait for a Group of Tasks

The newest addition to the Asyncio world in Python 3.11 was `asyncio.TaskGroup`, which simplified the process of managing a group of tasks in the form of a context manager. It ensures that if one task within the group fails, all other tasks are canceled, helping to maintain robust error handling within async code.

Consider a scenario where you have two coroutines, each responsible for calling a different API. Once you get the API responses from both coroutines, you want to enter all the data into a database, but if one API fails, you don’t want to insert anything. Well, this would be a perfect use-case for a `TaskGroup` since you want both coroutines to finish, but if one fails, you might as well cancel the other one right away.

You can use the `tg.create_task()` method to add tasks to a task group. The first time any of the task group tasks fail, all of the other tasks in the group will be canceled. An exception will then bubble up to the coroutine with the task group as an `ExceptionGroup` or `BaseExceptionGroup`.

Here's an example of how to use a task group:

```python
import asyncio

async def do_something():
    return 1

async def do_something_else():
    return 2

async def main():
    async with asyncio.TaskGroup() as tg:
        task1 = tg.create_task(do_something())
        task2 = tg.create_task(do_something_else())

    print(f’Everything done: {task1.result()}, {task2.result()}’)

asyncio.run(main())
```

Output:

```
Everything done: 1, 2
```

## Summary

That’s a lot of ways to handle awaitables, so here’s a summary of what we covered:

- `await` is the most basic form of waiting. You can put this keyword in front of any awaitable object and it will run the code inside of said awaitable; however, `await` doesn’t let you directly handle multiple tasks at a time.
- `asyncio.wait_for` handles a single awaitable object like `await`, but also lets you set a timeout to handle long-running tasks.
- `asyncio.wait` Is like `asyncio.wait_for` but accepts a collection of either task or future objects. You can specify a timeout and also when you want to return, whether that’s when they are all completed, the first one is completed, or on the first exception.
- `asyncio.gather` takes any number of awaitable objects in the form of positional arguments. The nice part of `gather` is that it returns a list in the same order as the positional arguments that were passed in and can also return tasks that encountered exceptions.
- `asyncio.as_completed` is an iterable that takes in any awaitable object and lets you handle tasks as they finish instead of all at once. It also has a timeout argument.
- `asyncio.TaskGroup` is the newest addition to Python 3.11; It lets you handle a group of tasks and will either return all or none of them depending on whether any of the tasks raise an exception.

Phew – that was a lot of ways to handle tasks. It took me a while to get comfortable with when exactly to use each of these, but if you’ve read this far, you’re one step closer to mastering Python’s Async features!