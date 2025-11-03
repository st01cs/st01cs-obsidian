---
title: "langchain-ai/deep-agents-from-scratch"
source: "https://github.com/langchain-ai/deep-agents-from-scratch"
author:
  - "[[gladwig2]]"
published:
created: 2025-11-03
description: "Contribute to langchain-ai/deep-agents-from-scratch development by creating an account on GitHub."
tags:
  - "clippings"
---
**[deep-agents-from-scratch](https://github.com/langchain-ai/deep-agents-from-scratch)** Public

[MIT license](https://github.com/langchain-ai/deep-agents-from-scratch/blob/main/LICENSE)

[Open in github.dev](https://github.dev/) [Open in a new github.dev tab](https://github.dev/) [Open in codespace](https://github.com/codespaces/new/langchain-ai/deep-agents-from-scratch?resume=1)

[![Screenshot 2025-08-12 at 2 13 54 PM](https://private-user-images.githubusercontent.com/122662504/477273449-90e5a7a3-7e88-4cbe-98f6-5b2581c94036.png?jwt=eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3NjIxNzMxODUsIm5iZiI6MTc2MjE3Mjg4NSwicGF0aCI6Ii8xMjI2NjI1MDQvNDc3MjczNDQ5LTkwZTVhN2EzLTdlODgtNGNiZS05OGY2LTViMjU4MWM5NDAzNi5wbmc_WC1BbXotQWxnb3JpdGhtPUFXUzQtSE1BQy1TSEEyNTYmWC1BbXotQ3JlZGVudGlhbD1BS0lBVkNPRFlMU0E1M1BRSzRaQSUyRjIwMjUxMTAzJTJGdXMtZWFzdC0xJTJGczMlMkZhd3M0X3JlcXVlc3QmWC1BbXotRGF0ZT0yMDI1MTEwM1QxMjI4MDVaJlgtQW16LUV4cGlyZXM9MzAwJlgtQW16LVNpZ25hdHVyZT0zYmFiZTUzYmVlNmFjMjAwYTU4NWYxZThkYTZiZWExYjQzN2Y0NGI1MTJmMzBmNjE1MGJhODU3MjIwMmIxYmNjJlgtQW16LVNpZ25lZEhlYWRlcnM9aG9zdCJ9.B0SEBfkb-bhKVssJuPOyCNasLNn2i5-96wUBFTBtGk0)](https://private-user-images.githubusercontent.com/122662504/477273449-90e5a7a3-7e88-4cbe-98f6-5b2581c94036.png?jwt=eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3NjIxNzMxODUsIm5iZiI6MTc2MjE3Mjg4NSwicGF0aCI6Ii8xMjI2NjI1MDQvNDc3MjczNDQ5LTkwZTVhN2EzLTdlODgtNGNiZS05OGY2LTViMjU4MWM5NDAzNi5wbmc_WC1BbXotQWxnb3JpdGhtPUFXUzQtSE1BQy1TSEEyNTYmWC1BbXotQ3JlZGVudGlhbD1BS0lBVkNPRFlMU0E1M1BRSzRaQSUyRjIwMjUxMTAzJTJGdXMtZWFzdC0xJTJGczMlMkZhd3M0X3JlcXVlc3QmWC1BbXotRGF0ZT0yMDI1MTEwM1QxMjI4MDVaJlgtQW16LUV4cGlyZXM9MzAwJlgtQW16LVNpZ25hdHVyZT0zYmFiZTUzYmVlNmFjMjAwYTU4NWYxZThkYTZiZWExYjQzN2Y0NGI1MTJmMzBmNjE1MGJhODU3MjIwMmIxYmNjJlgtQW16LVNpZ25lZEhlYWRlcnM9aG9zdCJ9.B0SEBfkb-bhKVssJuPOyCNasLNn2i5-96wUBFTBtGk0)

[Deep Research](https://academy.langchain.com/courses/deep-research-with-langgraph) broke out as one of the first major agent use-cases along with coding. Now, we've seeing an emergence of general purpose agents that can be used for a wide range of tasks. For example, [Manus](https://manus.im/blog/Context-Engineering-for-AI-Agents-Lessons-from-Building-Manus) has gained significant attention and popularity for long-horizon tasks; the average Manus task uses ~50 tool calls!. As a second example, Claude Code is being used generally for tasks beyond coding. Careful review of the [context engineering patterns](https://docs.google.com/presentation/d/16aaXLu40GugY-kOpqDU4e-S0hD1FmHcNyF0rRRnb1OU/edit?slide=id.p#slide=id.p) across these popular "deep" agents shows some common approaches:

- **Task planning (e.g., TODO), often with recitation**
- **Context offloading to file systems**
- **Context isolation through sub-agent delegation**

This course will show how to implement these patterns from scratch using LangGraph!

## 🚀 Quickstart

### Prerequisites

- Ensure you're using Python 3.11 or later.
- This version is required for optimal compatibility with LangGraph.
```
python3 --version
```
- [uv](https://docs.astral.sh/uv/) package manager
```
curl -LsSf https://astral.sh/uv/install.sh | sh
# Update PATH to use the new uv version
export PATH="/Users/$USER/.local/bin:$PATH"
```

### Installation

1. Clone the repository:
```
git clone https://github.com/langchain-ai/deep_agents_from_scratch
cd deep_agents_from_scratch
```
1. Install the package and dependencies (this automatically creates and manages the virtual environment):
```
uv sync
```
1. Create a `.env` file in the project root with your API keys:
```
# Create .env file
touch .env
```

Add your API keys to the `.env` file:

```
# Required for research agents with external search
TAVILY_API_KEY=your_tavily_api_key_here

# Required for model usage
ANTHROPIC_API_KEY=your_anthropic_api_key_here

# Optional: For evaluation and tracing
LANGSMITH_API_KEY=your_langsmith_api_key_here
LANGSMITH_TRACING=true
LANGSMITH_PROJECT=deep-agents-from-scratch
```
1. Run notebooks or code using uv:
```
# Run Jupyter notebooks directly
uv run jupyter notebook

# Or activate the virtual environment if preferred
source .venv/bin/activate  # On Windows: .venv\Scripts\activate
jupyter notebook
```

This repository contains five progressive notebooks that teach you to build advanced AI agents:

### 0\_create\_agent.ipynb -

Learn how to use the create\_agent component. This component,

- implements a ReAct (Reason - Act) loop that forms the foundation for many agents.
- is easy to use and quick to set up.
- serves as the

Learn to implement structured task planning using TODO lists. This notebook introduces:

- Task tracking with status management (pending/in\_progress/completed)
- Progress monitoring and context management
- The `write_todos()` tool for organizing complex multi-step workflows
- Best practices for maintaining focus and preventing task drift

Implement a virtual file system stored in agent state for context offloading:

- File operations: `ls()`, `read_file()`, `write_file()`, `edit_file()`
- Context management through information persistence
- Enabling agent "memory" across conversation turns
- Reducing token usage by storing detailed information in files

Master sub-agent delegation for handling complex workflows:

- Creating specialized sub-agents with focused tool sets
- Context isolation to prevent confusion and task interference
- The `task()` delegation tool and agent registry patterns
- Parallel execution capabilities for independent research streams

Combine all techniques into a production-ready research agent:

- Integration of TODOs, files, and sub-agents
- Real web search with intelligent context offloading
- Content summarization and strategic thinking tools
- Complete workflow for complex research tasks with LangGraph Studio integration

Each notebook builds on the previous concepts, culminating in a sophisticated agent architecture capable of handling real-world research and analysis tasks.

## Releases

[1 tags](https://github.com/langchain-ai/deep-agents-from-scratch/tags)

## Packages

No packages published  

## Languages

- [Jupyter Notebook 97.5%](https://github.com/langchain-ai/deep-agents-from-scratch/search?l=jupyter-notebook)
- [Python 2.5%](https://github.com/langchain-ai/deep-agents-from-scratch/search?l=python)