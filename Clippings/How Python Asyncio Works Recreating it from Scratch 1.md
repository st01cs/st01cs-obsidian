---
title: "How Python Asyncio Works: Recreating it from Scratch"
source: "https://jacobpadilla.com/articles/recreating-asyncio"
author:
  - "[[Jacob Padilla]]"
published: 2024-05-07
created: 2025-10-01
description: "Learn how asyncio works by recreating it from scratch with Python generators and using the __await__ dunder method for the async/await keywords."
tags:
  - "clippings"
---
Right now, asyncio is one of the trendier topics in Python, and rightfully so – It’s a great way to handle I/O-bound programs! When I was learning about asyncio, It took me a while to understand how it actually worked. But later, I came to find out that it’s basically just a really nice layer on top of Python Generators. In this article, I’m going to create a simplified version of asyncio using just Python generators. Then, I’m going to refactor the example to use the `async` and `await` keywords with the help of the `__await__` dunder method before coming full circle and swapping out my version for the real asyncio. By building a simple version of asyncio, hopefully, by the end of this article, you’ll be able to get a better grasp of how it does its magic!

## Generators Review

If you're already familiar with generators skip this part, but if you aren't, it's what asyncio is built off of, so it's very important to understand how they work.

First of all, the reason why generators are a thing is because they allow you to make your code more memory efficient. Imagine if you had the following loop:

```python
for i in range(100_000_000):
    print(i)
```

If `range` wasn't a generator, but rather was a function that returned a list for you to then loop over, code like the example above would be very memory inefficient since you would be creating a list with 100 million elements… However, because `range` is a generator, at least in Python 3+, you only generate the numbers as they are needed, one by one, without ever storing the entire sequence in memory.

There are a few ways to create generators, but we're going to focus on generator functions. These generators are defined like any other function but use the `yield` statement to return data. This statement turns a regular function into a generator that, instead of executing all at once, can pause and resume its state when calling `next(iterator)`.

Take the following generator function, for example:

```python
def generator():
   yield 'hello'
   yield 'world'

iterator = generator()
```

When you call the generator, instead of running the code inside of the function like Python normally would, it sees the `yield` keyword and, therefore, returns a generator object. Once we have the generator object, we can then call `next(iterator)`, which will run the function’s code up until the first/next `yield` statement:

```python
print(next(iterator))  # Output: hello
print(next(iterator))  # Output: world
```

If we try calling `next(iterator)` again, the generator will raise a `StopIteration` exception because there are no more yield statements in the generator function.

Another cool feature of Python generators is `yield from`, which lets a generator call a sub-generator or an iterable object, enabling you to create a chain of generators!

```python
def generator():
   yield 'hello'

def another_generator():
   yield from generator()

iterable = another_generator()
print(next(iterable))  # Output: hello
```

There’s a bit more to generators than I’m talking about, such as generator comprehensions, which are like list comprehensions but created with parentheses instead of brackets, and the ability to send data to generators with `iterator.send(value)`. However, for this article, the important thing to remember about generators is that they allow a function to be started and stopped while maintaining its state!

## The Event Loop

The event loop, which is in charge of running and managing all of the current tasks, is the core of asyncio and is the first thing we’ll recreate with generators. While the asyncio event loop is written in C, an easy way to think about it is as a list that holds all of the current tasks. For now, think of these tasks as just generator objects. The event loop manager will loop through each task in the list and use the `next(task)` function to run each of them. That task will then run, and when it's doing I/O-bound work like sleeping, it’ll use the `yield` keyword to pause its execution and give control back to this event loop, which will then go on to the next task in the loop.

Here’s an example of that — we have two tasks that both print their task number and then yield, which stops their execution. Since the event loop manager is the one that calls `next()`, after the task yields, it gets back control and then goes to run the next task in the loop.

```python
def task1():
   while True:
       print('Task 1')
       yield

def task2():
   while True:
       print('Task 2')
       yield

event_loop = [task1(), task2()]

while True:
   for task in event_loop:
       next(task)
```

Subsequently, the output of this code is going to look like the following and will go on forever since both of the generator functions never finish due to the `while True` loops.

```
Task 1
Task 2
Task 1
Task 2
…
```

## Sleeping

If we take the same code from above, we can add sub-generators to our tasks via the use of `yield from`. Below, I added a sleeping generator which will pause the execution of the tasks until the specified time is up. This works because `sleep` will keep yielding until a certain amount of seconds has passed, at which point it will leave the `while` loop. Since there are no more `yield` statements in `sleep`, a `StopIteration` exception is raised which signals to the `yield from` in the task functions to continue to the next line of code.

```python
import time

def sleep(seconds):
   start_time = time.time()
   while time.time() - start_time < seconds:
       yield

def task1():
   while True:
       print('Task 1')
       yield from sleep(1)

def task2():
   while True:
       print('Task 2')
       yield from sleep(5)

event_loop = [task1(), task2()]

while True:
   for task in event_loop:
       next(task)
```

Output:

```
Task 1
Task 2
Task 1
Task 1
Task 1
Task 1
Task 2
Task 1
…
```

## Yield to Await

We can now take the above code, and transition from using `yield` to `await` by using the `__await__` dunder method and the `async` keyword. When a class has the `__await__` method, we can use the `await` keyword in front of an instance of the class to call it. In asyncio, you are generally working with `Task` objects via a function like `asyncio.create_task`. These `Task` objects inherit from the asyncio `Future` object, which has the `__await__` method. We can also use `await` in front of a coroutine, which is an object created when calling a function with the `async` keyword in front of it. Coroutines are similar to generator functions in the sense that a coroutine’s execution can also be paused and resumed.

You can think of the `await` keyword as just a synonym for `yield from` with some extra validation rules. So, when writing the code `await object`, you are basically saying to either yield from the `__await__` method in the “object” class instance OR “object” could be another coroutine (like a sub-generator).

You can actually look in the Asyncio [source code](https://github.com/python/cpython/blob/main/Lib/asyncio/futures.py) and see that the `__await__` method inside of the `Future` object basically just calls `yield` if the future (or task) is not done completing:

  
![Asyncio source code. The __await__ method in the Future object](https://jacobpadilla.com/articles/blog_posts/recreating-asyncio/static/images/yield-to-await-193740693.png)

To move the code that we wrote in the above section to using `async` and `await`, we first need to make our own `Task` class since a function can’t have the `__await__` dunder method. Below is a simple version that I came up with:

```python
from queue import Queue

event_loop = Queue()

class Task():
    def __init__(self, generator):
        self.iter = generator
        self.finished = False

    def done(self):
        return self.finished

    def __await__(self):
        while not self.finished:
            yield self

def create_task(generator):
    task = Task(generator)
    event_loop.put(task)

    return task
```

This time, instead of using a Python list to create the event loop, we’re using a queue, which makes a bit more sense since we want to be able to add and delete tasks from the loop in constant time.

For our `Task` class, we store the generator object in `self.iter` and also set `self.finished` to `False`, which will keep track of if the generator is done running (It’s done running when it raises `StopIteration`). Our `Task` object also has an `__await__` dunder method, which will just keep yielding control back to the event loop until the task is finished. Lastly, after creating the `Task` object with the `create_task` helper function, we add it to the event loop, which schedules it to be run.

Now, let’s build the event loop manager, which will run the tasks:

```python
def run(main):
    event_loop.put(Task(main))

    while not event_loop.empty():
        task = event_loop.get()
        try:
            task.iter.send(None)
        except StopIteration:
            task.finished = True
        else:
            event_loop.put(task)
```

You may notice that this is starting to mimic the actual asyncio API since to start the event loop, we need to call `run` with an initial function. The function first wraps the main function in a `Task` object and adds it to the event loop. The `while` loop will then run, and for each cycle, will get the next task to run via the queue. Instead of using `next(task.iter)`, we now need to use `task.iter.send(None)`, which is just a weird quirk of working with the async/await keywords, but it does the same thing. We also want to wrap this call in a try-except block since if a `StopIteration` exception is thrown, we can set `task.finished` to `True`, but if no exceptions are raised, the code will go to the `else` statement which adds the task back to the event loop to be run again.

Next, we need to make the sleep function async-compliant. Before, we were using a generator function with a while-loop and one `yield` to handle the sleeping. I like this approach, but you can’t use the `await` keyword in combination with a generator function - it needs to be an object with the `__await__` dunder method or a coroutine function. So, to solve this, I moved the code to another function, and now the actual `sleep` function creates a task object and then awaits it. This `await` will call the `__await__` method inside of the Task object, which will then yield, letting the event loop move to another task. When the event loop gets to the new `_sleep` task, it will check the time, and if not enough has passed, will also call `yield` to give control back to the event loop. If the task that is sleeping is called via the event loop again, like how a generator stores its state, the coroutine would still be waiting for `sleep` to return, and since `sleep` would still be awaiting the `_sleep` task to finish, the `__await__` dunder method of the task will be called again and since the task isn't finished, the yield in the dunder method will be called.

```python
import time

def _sleep(seconds):
    start_time = time.time()
    while time.time() - start_time < seconds:
        yield

async def sleep(seconds):
    task = create_task(_sleep(seconds))
    return await task
```

Here’s all of the code put together:

```python
from queue import Queue
import time

event_loop = Queue()

def _sleep(seconds):
    start_time = time.time()
    while time.time() - start_time < seconds:
        yield

async def sleep(seconds):
    task = create_task(_sleep(seconds))
    return await task

class Task():
    def __init__(self, generator):
        self.iter = generator
        self.finished = False

    def done(self):
        return self.finished

    def __await__(self):
        while not self.finished:
            yield self

def create_task(generator):
    task = Task(generator)
    event_loop.put(task)

    return task

def run(main):
    event_loop.put(Task(main))

    while not event_loop.empty():
        task = event_loop.get()
        try:
            task.iter.send(None)
        except StopIteration:
            task.finished = True
        else:
            event_loop.put(task)
```

Now that we’ve built the event loop, a way to create tasks, and a sleep function, we can import the file (called “jacobio.py”) and take the code from back when we were using yields and replace all of the `yield from` statements with `await`, add `async` to the functions with the `await` keyword to signify that those functions can be awaited, and then create a main function, like you would in asyncio, to add the tasks to the event loop:

```python
import jacobio

async def task1():
    for _ in range(2):
        print('Task 1')
        await jacobio.sleep(1)

async def task2():
    for _ in range(3):
        print('Task 2')
        await jacobio.sleep(0)

async def main():
    one = jacobio.create_task(task1())
    two = jacobio.create_task(task2())

    await one
    await two
    
    print('done')

if __name__ == '__main__':
    jacobio.run(main())
```

Output:

```
Task 1
Task 2
Task 2
Task 2
Task 1
done
```

## Await with AsyncIO

We can now take our code from above and replace all occurrences of “jacobio” with “asyncio” and we’re now fully using the asyncio package!

```python
import asyncio

async def task1():
    for _ in range(2):
        print('Task 1')
        await asyncio.sleep(1)

async def task2():
    for _ in range(3):
        print('Task 2')
        await asyncio.sleep(0)

async def main():
    one = asyncio.create_task(task1())
    two = asyncio.create_task(task2())

    await one
    await two
    
    print('done')

if __name__ == '__main__':
    asyncio.run(main())
```

Asyncio does a lot more behind the scenes, but we were able to go from basic generators to recreating the core parts of asyncio from scratch! I tried to make the event loop manager as simple as possible, and while this is the basic idea behind asyncio, given the scale and complexity of the actual package, my implementation is slightly different from the flow of the actual source code. Also, now that we have the full power of the real asyncio package, we don’t need to create two tasks just to await both; instead, we can use a function such as `asyncio.gather()` to handle multiple tasks. If you’re curious about all of the ways to manage tasks in asyncio, check out my article on [handling asyncio tasks like a pro](https://jacobpadilla.com/articles/handling-asyncio-tasks)!