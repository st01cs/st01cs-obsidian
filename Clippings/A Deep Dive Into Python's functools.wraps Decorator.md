---
title: "A Deep Dive Into Python's functools.wraps Decorator"
source: "https://jacobpadilla.com/articles/Functools-Deep-Dive"
author:
  - "[[Jacob Padilla]]"
published: 2024-01-04
created: 2025-10-01
description: "Take a deep dive into Python's functools.wraps decorator to learn how it maintains metadata in your code. A concise guide to effective decorator use."
tags:
  - "clippings"
---
Decorators in Python are great! So far, my favorite use case for them is using decorators to store first-class functions, which is what Flask's `app.route` decorator does. However, due to the language's underlying mechanics, wrapping one object over another can result in the loss of valuable metadata from the encapsulated object. This is why it's crucial to use the wraps decorator from the Python Standard Library's functools (function tools) module when developing your own Python decorators.

## What Does functools.wraps Do?

`functools.wraps`, an easy-to-use interface for `functools.update_wrapper`, is a decorator that automatically transfers the key metadata from a callable (generally a function or class) to its wrapper. Typically, this wrapper is another function, but it can be any callable object such as a class.

Besides the `wrapped` parameter, which accepts the callable that gets enclosed by the wrapper, there are two more arguments that we can play around with:

```
@functools.wraps(wrapped, assigned=WRAPPER_ASSIGNMENTS, updated=WRAPPER_UPDATES)
```

The `assigned` parameter tells `functools.wraps` which attributes should be taken from the object being wrapped and transferred over to the wrapper. The parameter has a default tuple `WRAPPER_ASSIGNMENTS`, which has the following dunder attributes:

1. `__module__`**:** The name of the module in which the object is declared.
2. `__name__`: The object name.
3. `__qualname__`: A more detailed version of the `__name__`.
4. `__doc__`: The doc string at the top of an object.

The `updated` parameter also has a default tuple value of `(‘__dict__’,)`. The `updated` parameter tells the wraps decorator which attributes of the wrapper callable need to be updated with the values from the original object. By default, the wrapping object's `__dict__` attribute gets updated with the key-value pairs of the `__dict__` from the wrapped object.

The wraps decorator also adds a new attribute to the wrapping object called `__wrapped__`, which holds a pointer to the enclosed function or class. This is very useful as it allows you to peek into the actual object being wrapped to see more metadata about the object that `functools.wraps` doesn't automatically include, such as `__defaults__`.

## Decorators Without functools.wraps

First, let's see what a function that has a decorator looks like when there is no metadata transfer. Below is the decorator that I'll be using in the example; this decorator isn't actually doing anything, but note that it has its own docstring (“““wrapper function”“”) and the `__name__` of the wrapping function is called “wrapper.“

```python
def example_decorator(func):
    def wrapper(*args, **kwargs):
        """Wrapper function"""
        return func(*args, **kwargs)

    return wrapper
```

Now, let's use the decorator on the following function and look at some of it’s metadata:

```python
@example_decorator
def hello_world(planet: str = 'earth'):
    """Say hello to a world"""
    print(f"Hello, {planet}!")

# Checking metadata of the decorated function
print(f'{hello_world.__name__        =  }')
print(f'{hello_world.__doc__         =  }')
print(f'{hello_world.__annotations__ =  }')
print(f'{hello_world.__dict__        =  }')
```

Output:

```
hello_world.__name__        =  'wrapper'
hello_world.__doc__         =  'Wrapper function'
hello_world.__annotations__ =  {}
hello_world.__dict__        =  {}
```

From the output, we can see that none of the metadata was transferred to the wrapping function.

Furthermore, if we print the function object:

```python
print(hello_world)
```

We get the following output, which gives us no information about the `hello_world` function.

```
<function example_decorator.<locals>.wrapper at 0x7a122c8a9090>
```

## Decorators With functools.wraps

Now let's make the same decorator, but add the `functools.wraps` decorator. To use `functools.wraps`, you just need to add it to the wrapping object like such:

```python
from functools import wraps

def example_decorator(func):
    @wraps(func)
    def wrapper(*args, **kwargs):
        """Wrapper function"""
        return func(*args, **kwargs)

    return wrapper
```

And if we now look at the same metadata as before:

```python
@example_decorator
def hello_world(planet: str='earth'):
   """Say hello to a world"""
   print(f"Hello, {planet}!")

# Checking metadata of the decorated function
print(f'{hello_world.__name__         =  }')
print(f'{hello_world.__doc__          =  }')
print(f'{hello_world.__annotations__  =  }')
print(f'{hello_world.__dict__         =  }')
```

We get the following output:

```
hello_world.__name__         =  'hello_world'
hello_world.__doc__          =  'Say hello to a world'
hello_world.__annotations__  =  {'planet': <class 'str'>}
hello_world.__dict__         =  {'__wrapped__': <function hello_world at 0x7b49d5fccc10>}
```

We can see that the `__name__` attribute has been updated to match the name of the function that the decorator is wrapping. The docstring of the wrapped function also gets updated, as well as the static typing annotations. The `__dict__` attribute also contains all of the attributes from `hello_world` (which is nothing since it's a function) and also has the `__wrapped__` attribute, which holds a direct link to the original function.

As mentioned above, the `__wrapped__` attribute holds a pointer to the original object. This can be very useful if another program or developer wants to introspect/get more information on the encapsulated object. There is another Python Standard Library module for this called “inspect.“ In that module, there's a function called `inspect.signature` which actually looks for a `__wrapped__` attribute in `__dict__` and if one is found, it follows the `__wrapped__` value to be able to inspect the actual object!

However, you can also manually use the `__wrapped__` attribute to get extra information on the encapsulated object. For example, `functools.wraps` doesn't automatically transfer over default values to the wrapping object (because classes don’t have a `__defaults__` attribute and a class can be a wrapper), but with `__wrapped__`, we can see the default values which are stored in the `__defaults__` attribute:

```python
print(f'{hello_world.__dict__["__wrapped__"].__defaults__ =  }')
```

And we can see that the output is as expected; the `planet` argument from the function above has a default value of “earth.”

```
hello_world.__dict__["__wrapped__"].__defaults__ =  ('earth',)
```

Lastly, we can also print the function object; it shows the correct function:

```python
print(hello_world)
```

Output:

```
<function hello_world at 0x7a122d7295a0>
```

Using the predefined values from the wraps decorator is usually enough, but if you want to transfer more (or less) metadata over to the wrapper function, you can pass in your own arguments. Let's say that we want to save the default values of your function's arguments; we can add more dunder attributes to the `assigned` argument:

```python
MORE_WRAPPER_ASSIGNMENTS = (
   '__module__', '__name__',
   '__qualname__', '__annotations__',
   '__doc__', '__defaults__',
   '__kwdefaults__'
)

def example_decorator(func):
    @wraps(func, assigned=MORE_WRAPPER_ASSIGNMENTS)
    def wrapper(*args, **kwargs):
        """Wrapper function"""
        return func(*args, **kwargs)

    return wrapper

@example_decorator
def hello_world(planet: str='earth'):
    """Say hello to a world"""
    print(f"Hello, {planet}!")
```

Now if we try to print out the `__defaults__` dunder attribute, we will see `(‘earth’,)` because the `planet` parameter in the `hello_world` function has a default value of “earth”:

```python
print(f'{hello_world.__defaults__ =  }')
```

And the output:

```
hello_world.__defaults__ =  ('earth',)
```

## Final Thoughts

Saving the metadata of objects that use decorators is extremely important as it leads to code that's easier to debug and ensures that your objects still work with other parts of the language, such as introspection. Adding `functools.wraps` to your decorators allows you to easily carry over the most important attributes to the wrapper object. That being said, just be mindful that `functools.wraps` doesn't automatically move every attribute over, and you shouldn't have any problems!

Thanks for reading - I hope you learned something new!