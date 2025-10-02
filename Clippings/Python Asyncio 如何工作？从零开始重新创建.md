---
title: "Python Asyncio 如何工作？从零开始重新创建"
source: "https://juejin.cn/post/7366945260792447014"
author:
  - "[[宇宙之一粟]]"
published: 2024-05-10
created: 2025-10-01
description: "当下 asyncio 是 Python 中最流行的话题之一，这是理所当然的：它是处理 I/O 密集型程序最好的方法之一。当我学习 asyncio 时，我花了很长一段时间去理解它的实现原理。"
tags:
  - "clippings"
---
![横幅](https://p9-piu.byteimg.com/tos-cn-i-8jisjyls3a/8c759ddb57d0440986f4768fc644f879~tplv-8jisjyls3a-2:0:0:q75.image)

> 原文标题： [How Python Asyncio Works: Recreating it from Scratch](https://link.juejin.cn/?target=https%3A%2F%2Fjacobpadilla.com%2Farticles%2Frecreating-asyncio "https://jacobpadilla.com/articles/recreating-asyncio")
> 
> 作者： [Jacob Padilla](https://link.juejin.cn/?target=https%3A%2F%2Fjacobpadilla.com%2F "https://jacobpadilla.com/")

当下 `asyncio` 是 Python 中最流行的话题之一，这是理所当然的：它是处理 I/O 密集型程序最好的方法之一。当我学习 `asyncio` 时，我花了很长一段时间去理解它的实现原理。但后来，我发现它基本只是 Python 生成器之上的一个非常好的层。

在这篇文章中，我将仅仅使用 Python 生成器创建 `asyncio` 的简化版。然后，我将在 `__await__` dunder 方法的帮助下重构该示例，以使用 `async` 和 `await` 关键字，最后再把我的版本换成真正的 `asyncio` 。

通过构建一个简单的 `asyncio` 版本，希望在本文结束时，您将能够更好地掌握它是如何发挥作用的！

## 回顾生成器

如果您已经熟悉生成器，请跳过这一部分，但如果您不熟悉，那么 `asyncio` 就是基于它构建的，因此了解它们的工作原理非常重要。

首先，生成器之所以存在，是因为它能让你的代码更有效地利用内存。想象一下，如果你有如下循环：

```python
for i in range(100_000_000):
    print(i)
```

如果 `range` 不是一个生成器，而是一个返回列表供你循环的函数，则像上面示例这样的代码将非常低效的，因为你将创建一个包含 1 亿个元素的列表...然而，因为 `range` 是一个生成器，至少在 Python 3+ 中是这样的，所以你只需要一个接一个生成数字，而无需在内存中存储整个序列。

有几个方法可以创建生成器，但我们将重点讨论生成器函数。这些生成器的定义与任何其他函数类似，但是使用 `yield` 语句返回数据。该语句将普通函数转换为生成器，该生成器不是一次性执行所有函数，而是可以暂停，并在调用 `next(iterator)` 时恢复状态。

以下面的生成器函数为例：

```python
def generator():
    yield 'hello'
    yield 'world'

iterator = generator()
```

当你调用生成器时，它不会像 Python 通常那样运行函数内部的代码，而是会看到 `yield` 关键字，因此返回一个生成器对象。一旦我们有了生成器对象，我们就可以调用 `next(iterator)` ，它将运行函数的代码，直到第一个/下一个 `yield` 语句：

```python
print(next(iterator))  # Output: hello
print(next(iterator))  # Output: world
```

如果我们尝试再次调用 `next(iterator)` ，生成器将引发 `StopIteration` 异常，因为生成器函数中不再有 `yield` 语句。

Python 生成器的另一个很酷的特性是 `yield from` ，它可以让生成器调用子生成器或可迭代对象，从而创建生成器链！

```python
def generator():
   yield 'hello'

def another_generator():
   yield from generator()

iterable = another_generator()
print(next(iterable))  # Output: hello
```

生成器的功能远不止这些，例如生成器推导式（类似于列表推导式，但使用圆括号而不是方括号创建），以及使用 `iterator.send(value)` 向生成器推送数据的功能。不过，就本文而言，关于生成器需要记住的重要一点是，它们允许在保持函数状态的情况下启动和停止函数！

## 事件循环

事件循环负责运行和管理所有当前任务，是 `asyncio` 的核心，也是我们首先要使用生成器重新创建的。虽然 `asyncio` 事件循环是用 C 语言编写的，但我们可以简单地将其理解为一个保存所有当前任务的列表。现在，我们将这些任务看作是生成器对象。事件循环管理器将循环处理列表中的每个任务，并使用 `next(task)` 函数运行每个任务。然后，该任务将开始运行，在执行睡眠等 I/O 绑定工作时，它将使用 `yield` 关键字暂停执行，并将控制权交还给事件循环，事件循环将继续执行循环中的下一个任务。

下面是一个例子--我们有两个任务，它们都会打印任务编号，然后 yield，停止执行。由于事件循环管理器调用了 `next()` ，因此在任务让出后，它会重新获得控制权，然后继续运行循环中的下一个任务。

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

随后，这段代码的输出结果将如下所示，而且由于两个生成器函数都使用了 `while True` 循环，因此将一直持续下去。

```arduino
Task 1
Task 2
Task 1
Task 2
…
```

## Sleep

如果我们使用上面的代码，就可以通过 `yield from` 为任务添加子生成器。下面，我添加了一个睡眠生成器，它会暂停任务的执行，直到指定时间结束。这样做的原因是， `sleep` 会一直让出，直到特定的秒数过去，然后退出 `while` 循环。由于 `sleep` 中不再有 `yield` 语句，因此会引发 `StopIteration` 异常，该异常向任务函数中的 `yield from` 发出继续执行下一行代码的信号。

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

输出：

```arduino
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

现在，我们可以使用 `__await__` dunder 方法和 `async` 关键字，将上述代码从 `yield` 过渡到 `await` 。当一个类有 `__await__` 方法时，我们可以在类的实例前面使用 `await` 关键字来调用它。在 `asyncio` 中，你通常通过 `asyncio.create_task` 这样的函数来处理 `Task` 对象。这些 `Task` 对象继承自 asyncio `Future` 对象，该对象具有 `__await__` 方法。我们还可以在 coroutine(协程） 前面使用 `await` ，协程是调用带有 `async` 关键字的函数时创建的对象。协程类似于生成器函数，因为协程的执行也可以暂停和恢复。

你可以将 `await` 关键字视为 `yield from` 的同义词，只是多了一些验证规则。因此，在编写代码 `await object` 时，您基本上是在说：要么从“object”类实例中的 `__await__` 方法中 yield，要么“object”可以是另一个协程（如子生成器）。

您实际上可以查看 Asyncio [源代码](https://link.juejin.cn/?target=https%3A%2F%2Fgithub.com%2Fpython%2Fcpython%2Fblob%2Fmain%2FLib%2Fasyncio%2Ffutures.py "https://github.com/python/cpython/blob/main/Lib/asyncio/futures.py") ，在 Asyncio 源代码中可以看到，Future 对象内部的 `__await__` 方法基本上只是在 future（或任务）未完成时调用 yield：

![yield-to-await-193740693.png](https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/5e035e42391c4755b13efa4626d66fd7~tplv-k3u1fbpfcp-jj-mark:3024:0:0:0:q75.awebp#?w=1999&h=639&s=507518&e=png&b=ffffff)

要将我们在上一节中编写的代码移动到使用 `async` 和 `await` ，我们首先需要创建自己的 `Task` 类，因为函数不能有 `__await__` dunder 方法。下面是我想出的一个简单版本：

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

这一次，我们没有使用 Python 列表来创建事件循环，而是使用了队列，这更合理一些，因为我们希望能够在恒定时间内从循环中添加和删除任务。

对于我们的 `Task` 类，我们将生成器对象存储在 `self.iter` 中，并将 `self.finished` 设为 `False` ，这样就可以跟踪生成器是否已运行完毕（当它引发 `StopIteration` 时，它就运行完毕了）。我们的任务对象也有一个 `__await__ dunder` 方法，它将继续把控制权交还给事件循环，直到任务完成。最后，在使用 `create_task` 辅助函数创建 `Task` 对象后，我们将其添加到事件循环中，该循环将调度任务的运行。

现在，让我们构建事件循环管理器，它将运行任务：

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

您可能会注意到，这已经开始模仿实际的 asyncio API，因为要启动事件循环，我们需要调用带有初始函数的 `run` 。该函数首先将 main 函数封装在一个任务对象中，然后将其添加到事件循环中。然后， `while` 循环将运行，每个循环将通过队列获取下一个要运行的任务。我们现在需要使用 `task.iter.send(None)` ，而不是使用 `next(task.iter)` ，这只是使用 async/await 关键字时的一个奇怪的怪癖，但它的作用是一样的。我们还想用一个 try-except 块来封装这个调用，因为如果抛出 StopIteration 异常，我们可以将 `task.finished` 设为 `True` ，但如果没有异常，代码将转到 `else` 语句，将任务添加回事件循环中再次运行。

接下来，我们需要使睡眠函数符合异步标准。之前，我们使用一个带有 while 循环和一个 `yield` 的生成器函数来处理睡眠。我喜欢这种方法，但你不能将 `await` 关键字与生成器函数结合使用--它需要是一个带有 `__await__` dunder 方法的对象或一个 coroutine 函数。因此，为了解决这个问题，我把代码移到了另一个函数中，现在实际的 `sleep` 函数创建了一个任务对象，然后等待它。这个 `await` 将调用任务对象内部的 `__await__` 方法，然后任务对象将 `yield` ，让事件循环转移到另一个任务。当事件循环到达新的 `_sleep` 任务时，它会检查时间，如果时间不够，还会调用 `yield` 将控制权交还给事件循环。如果正在休眠的任务再次被事件循环调用，就像生成器存储其状态一样，那么 coroutine 仍在等待 `sleep` 返回，由于 `sleep` 仍在等待 `_sleep` 任务完成，任务的 `__await__` dunder 方法将再次被调用，由于任务尚未完成，dunder 方法中的 yield 将被调用。

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

以下是所有代码的汇总：

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

现在我们已经构建了事件循环、创建任务的方法和睡眠函数，我们可以导入文件（称为“jacobio.py”）并从我们使用 yields 时获取后面的代码并替换所有 `yield from` 语句与 `await` ，将 `async` 添加到带有 `await` 关键字的函数中，以表示可以等待这些函数，然后创建一个 main 函数，就像在 asyncio 中一样，用于将任务添加到事件循环中：

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

输出：

```arduino
Task 1
Task 2
Task 2
Task 2
Task 1
done
```

## Await with AsyncIO

现在，我们可以从上面获取代码，并将所有出现的“jacobio”替换为“asyncio”，我们现在完全使用 asyncio 包！

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

Asyncio 背后原理做了很多事情，但我们能够从基本的生成器到从头开始重新创建 asyncio 的核心部分！虽然这是 asyncio 背后的基本思想，但考虑到实际软件包的规模和复杂性，我的实现与实际源代码的流程略有不同。另外，既然我们已经拥有了真正的 asyncio 软件包的全部功能，我们就不需要为了等待两个任务而创建两个任务了；相反，我们可以使用 `asyncio.gather()` 这样的函数来处理多个任务。如果你对 asyncio 中管理任务的所有方法感到好奇，请查看我的文章《 [像专家一样处理 asyncio 任务](https://link.juejin.cn/?target=https%3A%2F%2Fjacobpadilla.com%2Farticles%2Fhandling-asyncio-tasks "https://jacobpadilla.com/articles/handling-asyncio-tasks") 》！

本文收录于以下专栏

![cover](https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/4d5e28ad31ad4a1088c7acd057b56d72~tplv-k3u1fbpfcp-jj:160:120:0:0:q75.avis)

Python语言的点点滴滴

专栏目录

Python从入门到实战

126 订阅

·

81 篇文章

评论 2

![](https://lf-web-assets.juejin.cn/obj/juejin-web/xitu_juejin_web/c12d6646efb2245fa4e88f0e1a9565b7.svg) 14

![](https://lf-web-assets.juejin.cn/obj/juejin-web/xitu_juejin_web/336af4d1fafabcca3b770c8ad7a50781.svg) 2

![](https://lf-web-assets.juejin.cn/obj/juejin-web/xitu_juejin_web/3d482c7a948bac826e155953b2a28a9e.svg) 收藏

APP内打开

![yoyo](https://lf-web-assets.juejin.cn/obj/juejin-web/xitu_juejin_web/img/yoyo.3df25da.png)

## 登录掘金领取礼包

更多登录后权益等你解锁