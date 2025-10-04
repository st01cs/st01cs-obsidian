---
title: "Project: Ambient Agents with LangGraph - LangChain Academy"
source: https://academy.langchain.com/courses/take/ambient-agents/texts/66147173-getting-set-up
author:
published:
created: 2025-09-30
description: "Project: Ambient Agents with LangGraph - LangChain Academy"
tags:
  - clippings
  - langgraph
---
### Getting Set Up

![](https://files.cdn.thinkific.com/file_uploads/967498/images/3b3/5eb/78b/buildingambientagents.png)

  

**Introduction**

Welcome to LangChain Academy’s Ambient Agents with LangGraph course! This course is divided into five modules that walk you through understanding LangGraph, building your email agent, evaluating its performance, and deploying it.

Each module includes a video lesson to walk you through key concepts, along with corresponding notebooks.

---

  

**Setup**

Here’s our recommended setup to get started with the course. We'll be using the set of notebooks located [here](https://github.com/langchain-ai/agents-from-scratch/tree/main). If you prefer to download the notebooks manually, you can access a ZIP file [here](https://github.com/langchain-ai/agents-from-scratch/archive/refs/heads/main.zip). Each module will also include links to the corresponding notebooks.

**Python version**

Ensure you're using Python 3.11 or later. This version is required for optimal compatibility with LangGraph.

```
python3 --version
```

**Clone repo**

```
git clone https://github.com/langchain-ai/agents-from-scratch.git
$ cd agents-from-scratch
```

**Running notebooks**

If you don't have Jupyter set up, follow installation instructions [here](https://jupyter.org/install).

```
$ jupyter notebook
```

**Sign up for LangSmith**

Sign up [here](https://smith.langchain.com/). You can reference LangSmith docs [here](https://docs.smith.langchain.com/).

Navigate to the Settings page, and generate an API key in LangSmith.

Create a.env file that mimics the provided.env.example. Set

```
LANGCHAIN_API_KEY
```

in the.env file.

**Set up OpenAI API key**

If you don’t have an OpenAI API key, you can sign up [here](https://openai.com/index/openai-api/).

Then, set

```
OPENAI_API_KEY
```

in the.env file.

**Set environment variables**

**Create a.env file in the root directory:**

```
# Copy the .env.example file to .env
cp .env.example .env
```

Edit the.env file with the following:

```
LANGSMITH_API_KEY=your_langsmith_api_key
LANGSMITH_TRACING=true
LANGSMITH_PROJECT="interrupt-workshop"
OPENAI_API_KEY=your_openai_api_key
```

You can also set the environment variables in your terminal:

```
export LANGSMITH_API_KEY=your_langsmith_api_key
export LANGSMITH_TRACING=true
export OPENAI_API_KEY=your_openai_api_key
```

**Package Installation**

Recommended: Using uv (faster and more reliable)

```
# Install uv if you haven't already
pip install uv
# Install the package with development dependencies
uv sync --extra dev
# Activate the virtual environment
source .venv/bin/activate
```

Alternative: Using pip

```
$ python3 -m venv .venv
$ source .venv/bin/activate
# Ensure you have a recent version of pip (required for editable installs with pyproject.toml)
$ python3 -m pip install --upgrade pip
# Install the package in editable mode
$ pip install -e .
```

⚠️ IMPORTANT: Do not skip the package installation step! This editable install is required for the notebooks to work correctly. The package is installed as interrupt\_workshop with import name email\_assistant, allowing you to import from anywhere with from from email\_assistant import...

---

  

**Slack Community**

If you're interested in connecting with other learners, you can join our Slack Community [here](https://www.langchain.com/join-community). If you have any questions, we encourage you to ask and explore in our community-run [Forum](https://forum.langchain.com/). We encourage you to [pay it forward](https://www.langchain.com/community-code) within the community and help other learners.

Please note that our Slack Community is not an official support channel. If you are a customer and need product support, reach out to support@langchain.dev.