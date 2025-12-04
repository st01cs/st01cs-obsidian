---
title: "Hypothesis 6.147.0 documentation"
source: "https://hypothesis.readthedocs.io/en/latest/"
author:
published:
created: 2025-12-04
description:
tags:
  - "clippings"
---
## Welcome to Hypothesis!

Hypothesis is the property-based testing library for Python. With Hypothesis, you write tests which should pass for all inputs in whatever range you describe, and let Hypothesis randomly choose which of those inputs to check - including edge cases you might not have thought about. For example:

```python
from hypothesis import given, strategies as st

@given(st.lists(st.integers() | st.floats()))
def test_sort_correct(lst):
    # hypothesis generates random lists of numbers to test
    assert my_sort(lst) == sorted(lst)

test_sort_correct()
```

You should start with the [tutorial](https://hypothesis.readthedocs.io/en/latest/tutorial/index.html), or alternatively the more condensed [quickstart](https://hypothesis.readthedocs.io/en/latest/quickstart.html).

## Tutorial

An introduction to Hypothesis.

New users should start here, or with the more condensed [quickstart](https://hypothesis.readthedocs.io/en/latest/quickstart.html).

## How-to guides

Practical guides for applying Hypothesis in specific scenarios.

## Explanations

Commentary oriented towards deepening your understanding of Hypothesis.

## API Reference

Technical API reference.