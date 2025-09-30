---
title: langchain-ai/deep_research_from_scratch
source: https://github.com/langchain-ai/deep_research_from_scratch
author:
  - "[[rlancemartin]]"
published:
created: 2025-09-30
description: Contribute to langchain-ai/deep_research_from_scratch development by creating an account on GitHub.
tags:
  - clippings
  - langgraph
  - deepresearch
---
**[deep\_research\_from\_scratch](https://github.com/langchain-ai/deep_research_from_scratch)** Public

[Open in github.dev](https://github.dev/) [Open in a new github.dev tab](https://github.dev/) [Open in codespace](https://github.com/codespaces/new/langchain-ai/deep_research_from_scratch?resume=1)

Deep research has broken out as one of the most popular agent applications. [OpenAI](https://openai.com/index/introducing-deep-research/), [Anthropic](https://www.anthropic.com/engineering/built-multi-agent-research-system), [Perplexity](https://www.perplexity.ai/hub/blog/introducing-perplexity-deep-research), and [Google](https://gemini.google/overview/deep-research/?hl=en) all have deep research products that produce comprehensive reports using [various sources](https://www.anthropic.com/news/research) of context. There are also many [open](https://huggingface.co/blog/open-deep-research) [source](https://github.com/google-gemini/gemini-fullstack-langgraph-quickstart) implementations. We built an [open deep researcher](https://github.com/langchain-ai/open_deep_research) that is simple and configurable, allowing users to bring their own models, search tools, and MCP servers. In this repo, we'll build a deep researcher from scratch! Here is a map of the major pieces that we will build:

[![overview](https://private-user-images.githubusercontent.com/122662504/465415610-b71727bd-0094-40c4-af5e-87cdb02123b4.png?jwt=eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3NTkyMTYzMDgsIm5iZiI6MTc1OTIxNjAwOCwicGF0aCI6Ii8xMjI2NjI1MDQvNDY1NDE1NjEwLWI3MTcyN2JkLTAwOTQtNDBjNC1hZjVlLTg3Y2RiMDIxMjNiNC5wbmc_WC1BbXotQWxnb3JpdGhtPUFXUzQtSE1BQy1TSEEyNTYmWC1BbXotQ3JlZGVudGlhbD1BS0lBVkNPRFlMU0E1M1BRSzRaQSUyRjIwMjUwOTMwJTJGdXMtZWFzdC0xJTJGczMlMkZhd3M0X3JlcXVlc3QmWC1BbXotRGF0ZT0yMDI1MDkzMFQwNzA2NDhaJlgtQW16LUV4cGlyZXM9MzAwJlgtQW16LVNpZ25hdHVyZT01ZTdjZmNmY2E4YWNlOGU2ZmE5ODQ3MmRjMjE3NTBmNzNlZTQzZGQ1OWNkOGRhMjMxNmIzNzc0MzRiNmY4ZmUwJlgtQW16LVNpZ25lZEhlYWRlcnM9aG9zdCJ9.Fi4Bw13pl3zfGBQpCz2sFD5upTjvHZ9V-PH2axeddkg)](https://private-user-images.githubusercontent.com/122662504/465415610-b71727bd-0094-40c4-af5e-87cdb02123b4.png?jwt=eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3NTkyMTYzMDgsIm5iZiI6MTc1OTIxNjAwOCwicGF0aCI6Ii8xMjI2NjI1MDQvNDY1NDE1NjEwLWI3MTcyN2JkLTAwOTQtNDBjNC1hZjVlLTg3Y2RiMDIxMjNiNC5wbmc_WC1BbXotQWxnb3JpdGhtPUFXUzQtSE1BQy1TSEEyNTYmWC1BbXotQ3JlZGVudGlhbD1BS0lBVkNPRFlMU0E1M1BRSzRaQSUyRjIwMjUwOTMwJTJGdXMtZWFzdC0xJTJGczMlMkZhd3M0X3JlcXVlc3QmWC1BbXotRGF0ZT0yMDI1MDkzMFQwNzA2NDhaJlgtQW16LUV4cGlyZXM9MzAwJlgtQW16LVNpZ25hdHVyZT01ZTdjZmNmY2E4YWNlOGU2ZmE5ODQ3MmRjMjE3NTBmNzNlZTQzZGQ1OWNkOGRhMjMxNmIzNzc0MzRiNmY4ZmUwJlgtQW16LVNpZ25lZEhlYWRlcnM9aG9zdCJ9.Fi4Bw13pl3zfGBQpCz2sFD5upTjvHZ9V-PH2axeddkg)

## 🚀 Quickstart

### Prerequisites

- **Node.js and npx** (required for MCP server in notebook 3):
```
# Install Node.js (includes npx)
# On macOS with Homebrew:
brew install node

# On Ubuntu/Debian:
curl -fsSL https://deb.nodesource.com/setup_lts.x | sudo -E bash -
sudo apt-get install -y nodejs

# Verify installation:
node --version
npx --version
```
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
git clone https://github.com/langchain-ai/deep_research_from_scratch
cd deep_research_from_scratch
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
OPENAI_API_KEY=your_openai_api_key_here
ANTHROPIC_API_KEY=your_anthropic_api_key_here

# Optional: For evaluation and tracing
LANGSMITH_API_KEY=your_langsmith_api_key_here
LANGSMITH_TRACING=true
LANGSMITH_PROJECT=deep_research_from_scratch
```
1. Run notebooks or code using uv:
```
# Run Jupyter notebooks directly
uv run jupyter notebook

# Or activate the virtual environment if preferred
source .venv/bin/activate  # On Windows: .venv\Scripts\activate
jupyter notebook
```

## Background

Research is an open‑ended task; the best strategy to answer a user request can’t be easily known in advance. Requests can require different research strategies and varying levels of search depth. Consider this request.

[Agents](https://langchain-ai.github.io/langgraph/tutorials/workflows/#agent) are well suited to research because they can flexibly apply different strategies, using intermediate results to guide their exploration. Open deep research uses an agent to conduct research as part of a three step process:

1. **Scope** – clarify research scope
2. **Research** – perform research
3. **Write** – produce the final report

## 📝 Organization

This repo contains 5 tutorial notebooks that build a deep research system from scratch:

**Purpose**: Clarify research scope and transform user input into structured research briefs

**Key Concepts**:

- **User Clarification**: Determines if additional context is needed from the user using structured output
- **Brief Generation**: Transforms conversations into detailed research questions
- **LangGraph Commands**: Using Command system for flow control and state updates
- **Structured Output**: Pydantic schemas for reliable decision making

**Implementation Highlights**:

- Two-step workflow: clarification → brief generation
- Structured output models (`ClarifyWithUser`, `ResearchQuestion`) to prevent hallucination
- Conditional routing based on clarification needs
- Date-aware prompts for context-sensitive research

**What You'll Learn**: State management, structured output patterns, conditional routing

---

**Purpose**: Build an iterative research agent using external search tools

**Key Concepts**:

- **Agent Architecture**: LLM decision node + tool execution node pattern
- **Sequential Tool Execution**: Reliable synchronous tool execution
- **Search Integration**: Tavily search with content summarization
- **Tool Execution**: ReAct-style agent loop with tool calling

**Implementation Highlights**:

- Synchronous tool execution for reliability and simplicity
- Content summarization to compress search results
- Iterative research loop with conditional routing
- Rich prompt engineering for comprehensive research

**What You'll Learn**: Agent patterns, tool integration, search optimization, research workflow design

---

**Purpose**: Integrate Model Context Protocol (MCP) servers as research tools

**Key Concepts**:

- **Model Context Protocol**: Standardized protocol for AI tool access
- **MCP Architecture**: Client-server communication via stdio/HTTP
- **LangChain MCP Adapters**: Seamless integration of MCP servers as LangChain tools
- **Local vs Remote MCP**: Understanding transport mechanisms

**Implementation Highlights**:

- `MultiServerMCPClient` for managing MCP servers
- Configuration-driven server setup (filesystem example)
- Rich formatting for tool output display
- Async tool execution required by MCP protocol (no nested event loops needed)

**What You'll Learn**: MCP integration, client-server architecture, protocol-based tool access

---

**Purpose**: Multi-agent coordination for complex research tasks

**Key Concepts**:

- **Supervisor Pattern**: Coordination agent + worker agents
- **Parallel Research**: Concurrent research agents for independent topics using parallel tool calls
- **Research Delegation**: Structured tools for task assignment
- **Context Isolation**: Separate context windows for different research topics

**Implementation Highlights**:

- Two-node supervisor pattern (`supervisor` + `supervisor_tools`)
- Parallel research execution using `asyncio.gather()` for true concurrency
- Structured tools (`ConductResearch`, `ResearchComplete`) for delegation
- Enhanced prompts with parallel research instructions
- Comprehensive documentation of research aggregation patterns

**What You'll Learn**: Multi-agent patterns, parallel processing, research coordination, async orchestration

---

**Purpose**: Complete end-to-end research system integrating all components

**Key Concepts**:

- **Three-Phase Architecture**: Scope → Research → Write
- **System Integration**: Combining scoping, multi-agent research, and report generation
- **State Management**: Complex state flow across subgraphs
- **End-to-End Workflow**: From user input to final research report

**Implementation Highlights**:

- Complete workflow integration with proper state transitions
- Supervisor and researcher subgraphs with output schemas
- Final report generation with research synthesis
- Thread-based conversation management for clarification

**What You'll Learn**: System architecture, subgraph composition, end-to-end workflows

---

- **Structured Output**: Using Pydantic schemas for reliable AI decision making
- **Async Orchestration**: Strategic use of async patterns for parallel coordination vs synchronous simplicity
- **Agent Patterns**: ReAct loops, supervisor patterns, multi-agent coordination
- **Search Integration**: External APIs, MCP servers, content processing
- **Workflow Design**: LangGraph patterns for complex multi-step processes
- **State Management**: Complex state flows across subgraphs and nodes
- **Protocol Integration**: MCP servers and tool ecosystems

Each notebook builds on the previous concepts, culminating in a production-ready deep research system that can handle complex, multi-faceted research queries with intelligent scoping and coordinated execution.

## Releases

No releases published

## Packages

No packages published  

## Languages

- [Jupyter Notebook 96.7%](https://github.com/langchain-ai/deep_research_from_scratch/search?l=jupyter-notebook)
- [Python 3.3%](https://github.com/langchain-ai/deep_research_from_scratch/search?l=python)