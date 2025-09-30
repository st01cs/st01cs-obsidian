---
title: "knownsec/aipyapp: AI-Powered Python & Python-Powered AI (Python-Use)"
author:
  - "[[Github]]"
description: "AI-Powered Python & Python-Powered AI (Python-Use) - knownsec/aipyapp"
source: "https://github.com/knownsec/aipyapp"
language:
license:
created:
lastUpdated:
tags:
  - "github"
  - "repository"
categories:
  - "[[Repositories]]"
---
[![logo](https://private-user-images.githubusercontent.com/858592/475162574-3af4e228-79b2-4fa0-a45c-c38276c6db91.svg?jwt=eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3NTkxOTg3NjcsIm5iZiI6MTc1OTE5ODQ2NywicGF0aCI6Ii84NTg1OTIvNDc1MTYyNTc0LTNhZjRlMjI4LTc5YjItNGZhMC1hNDVjLWMzODI3NmM2ZGI5MS5zdmc_WC1BbXotQWxnb3JpdGhtPUFXUzQtSE1BQy1TSEEyNTYmWC1BbXotQ3JlZGVudGlhbD1BS0lBVkNPRFlMU0E1M1BRSzRaQSUyRjIwMjUwOTMwJTJGdXMtZWFzdC0xJTJGczMlMkZhd3M0X3JlcXVlc3QmWC1BbXotRGF0ZT0yMDI1MDkzMFQwMjE0MjdaJlgtQW16LUV4cGlyZXM9MzAwJlgtQW16LVNpZ25hdHVyZT0wN2M5N2M4NzdlN2QxNDYwZTMyYWMwYmM4OGQ5NTM3ZjRiZWMzNmRmYWZjMzY3MmY0NmJlZjM5NTAyZWZjYjkwJlgtQW16LVNpZ25lZEhlYWRlcnM9aG9zdCJ9.8FTmbmza-uCguS3opc9hRRoQRsvRR0_4DHcnLE7wX9A)](https://private-user-images.githubusercontent.com/858592/475162574-3af4e228-79b2-4fa0-a45c-c38276c6db91.svg?jwt=eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3NTkxOTg3NjcsIm5iZiI6MTc1OTE5ODQ2NywicGF0aCI6Ii84NTg1OTIvNDc1MTYyNTc0LTNhZjRlMjI4LTc5YjItNGZhMC1hNDVjLWMzODI3NmM2ZGI5MS5zdmc_WC1BbXotQWxnb3JpdGhtPUFXUzQtSE1BQy1TSEEyNTYmWC1BbXotQ3JlZGVudGlhbD1BS0lBVkNPRFlMU0E1M1BRSzRaQSUyRjIwMjUwOTMwJTJGdXMtZWFzdC0xJTJGczMlMkZhd3M0X3JlcXVlc3QmWC1BbXotRGF0ZT0yMDI1MDkzMFQwMjE0MjdaJlgtQW16LUV4cGlyZXM9MzAwJlgtQW16LVNpZ25hdHVyZT0wN2M5N2M4NzdlN2QxNDYwZTMyYWMwYmM4OGQ5NTM3ZjRiZWMzNmRmYWZjMzY3MmY0NmJlZjM5NTAyZWZjYjkwJlgtQW16LVNpZ25lZEhlYWRlcnM9aG9zdCJ9.8FTmbmza-uCguS3opc9hRRoQRsvRR0_4DHcnLE7wX9A)

## Python use

AIPy is an implementation of the Python-use concept, demonstrating its practical value and potential.

- **Mission**: unleash the full potential of large language models.
- **Vision**: a future where LLMs can think independently and proactively leverage AIPy to solve complex problems.

## What

Python use provides the entire Python execution environment to LLM. Imagine LLM sitting in front of a computer, typing various commands into the Python command-line interpreter, pressing Enter to execute, observing the results, and then typing and executing more code.

Unlike Agents, Python use does not define any tools interface. LLM can freely use all the features provided by the Python runtime environment.

## Why

If you are a data engineer, you are likely familiar with the following scenarios:

- Handling various data file formats: csv/excel, json, html, sqlite, parquet, etc.
- Performing operations like data cleaning, transformation, computation, aggregation, sorting, grouping, filtering, analysis, and visualization.

This process often requires:

- Starting Python, importing pandas as pd, and typing a bunch of commands to process data.
- Generating a bunch of intermediate temporary files.
- Describing your needs to ChatGPT/Claude, copying the generated data processing code, and running it manually.

So, why not start the Python command-line interpreter, directly describe your data processing needs, and let it be done automatically? The benefits are:

- No need to manually input a bunch of Python commands temporarily.
- No need to describe your needs to GPT, copy the program, and run it manually.

This is the problem Python use aims to solve!

## How

Python use (aipython) is a Python command-line interpreter integrated with LLM. You can:

- Enter and execute Python commands as usual.
- Describe your needs in natural language, and aipython will automatically generate Python commands and execute them.

Moreover, the two modes can access data interchangeably. For example, after aipython processes your natural language commands, you can use standard Python commands to view various data.

## Usage

AIPython has two running modes:

- Task mode: Very simple and easy to use, just input your task, suitable for users unfamiliar with Python.
- Python mode: Suitable for users familiar with Python, allowing both task input and Python commands, ideal for advanced users.

The default running mode is task mode, which can be switched to Python mode using the `--python` parameter.

### Basic Config

~/.aipyapp/aipyapp.toml:

```
[llm.deepseek]
type = "deepseek"
api_key = "Your DeepSeek API Key"
```

### Task Mode

`uv run aipy`

```
>>> Get the latest posts from Reddit r/LocalLLaMA
......
......
>>> /done
```

`pip install aipyapp` and run with `aipy`

```
-> % aipy
🚀 Python use - AIPython (0.1.22) [https://aipy.app]
>> Get the latest posts from Reddit r/LocalLLaMA
......
>>
```

### Python Mode

#### Basic Usage

Automatic task processing:

```
>>> ai("Get the title of Google's homepage")
```

#### Automatically Request to Install Third-Party Libraries

```
Python use - AIPython (Quit with 'exit()')
>>> ai("Use psutil to list all processes on MacOS")

📦 LLM requests to install third-party packages: ['psutil']
If you agree and have installed, please enter 'y [y/n] (n): y
```

## Thanks

- Hei Ge: Product manager/senior user/chief tester
- Sonnet 3.7: Generated the first version of the code, which was almost ready to use without modification.
- ChatGPT: Provided many suggestions and code snippets, especially for the command-line interface.
- Codeium: Intelligent code completion
- Copilot: Code improvement suggestions and README translation