---
title: "sagar-n/deepagents"
source: "https://github.com/sagar-n/deepagents"
author:
  - "[[sagar-n]]"
published:
created: 2025-11-03
description: "Contribute to sagar-n/deepagents development by creating an account on GitHub."
tags:
  - "clippings"
---
**[deepagents](https://github.com/sagar-n/deepagents)** Public

[Open in github.dev](https://github.dev/) [Open in a new github.dev tab](https://github.dev/) [Open in codespace](https://github.com/codespaces/new/sagar-n/deepagents?resume=1)

<table><thead><tr><th colspan="2"><span>Name</span></th><th colspan="1"><span>Name</span></th><th><p><span>Last commit message</span></p></th><th colspan="1"><p><span>Last commit date</span></p></th></tr></thead><tbody><tr><td colspan="3"><p><span><a href="https://github.com/sagar-n/deepagents/commit/ba56f38cb410a35d54e4b9c9b1168ee1a62d1b69">Revise README for Stock Research Agent Version 3</a></span></p><p><span><a href="https://github.com/sagar-n/deepagents/commit/ba56f38cb410a35d54e4b9c9b1168ee1a62d1b69">ba56f38</a> ·</span></p><p><a href="https://github.com/sagar-n/deepagents/commits/main/"><span><span><span>27 Commits</span></span></span></a></p></td></tr><tr><td colspan="2"><p><a href="https://github.com/sagar-n/deepagents/tree/main/deep-research-agents-v1">deep-research-agents-v1</a></p></td><td colspan="1"><p><a href="https://github.com/sagar-n/deepagents/tree/main/deep-research-agents-v1">deep-research-agents-v1</a></p></td><td><p><a href="https://github.com/sagar-n/deepagents/commit/211d0a8a315cfd6bba350735287e6db8729a6b34">merge conflict resolved</a></p></td><td></td></tr><tr><td colspan="2"><p><a href="https://github.com/sagar-n/deepagents/tree/main/deep-research-agents-v2">deep-research-agents-v2</a></p></td><td colspan="1"><p><a href="https://github.com/sagar-n/deepagents/tree/main/deep-research-agents-v2">deep-research-agents-v2</a></p></td><td><p><a href="https://github.com/sagar-n/deepagents/commit/26f998a295cde25146c631e5b1298bf91f94f2c9">Delete deep-research-agents-v2/__pycache__ directory</a></p></td><td></td></tr><tr><td colspan="2"><p><a href="https://github.com/sagar-n/deepagents/tree/main/deep-research-agents-v3">deep-research-agents-v3</a></p></td><td colspan="1"><p><a href="https://github.com/sagar-n/deepagents/tree/main/deep-research-agents-v3">deep-research-agents-v3</a></p></td><td><p><a href="https://github.com/sagar-n/deepagents/commit/30d4cbf821486bbf807b94be21f3bd95c89d2c01">Update readme.md</a></p></td><td></td></tr><tr><td colspan="2"><p><a href="https://github.com/sagar-n/deepagents/blob/main/.gitignore">.gitignore</a></p></td><td colspan="1"><p><a href="https://github.com/sagar-n/deepagents/blob/main/.gitignore">.gitignore</a></p></td><td><p><a href="https://github.com/sagar-n/deepagents/commit/87804adef7489fd020fe224ee4dc05e30ce35c19">git igonre</a></p></td><td></td></tr><tr><td colspan="2"><p><a href="https://github.com/sagar-n/deepagents/blob/main/readme.md">readme.md</a></p></td><td colspan="1"><p><a href="https://github.com/sagar-n/deepagents/blob/main/readme.md">readme.md</a></p></td><td><p><a href="https://github.com/sagar-n/deepagents/commit/ba56f38cb410a35d54e4b9c9b1168ee1a62d1b69">Revise README for Stock Research Agent Version 3</a></p></td><td></td></tr><tr><td colspan="3"></td></tr></tbody></table>

- [Version 2](https://github.com/sagar-n/deepagents/blob/main/deep-research-agents-v2)
- [Version 3](https://github.com/sagar-n/deepagents/blob/main/deep-research-agents-v3)

## 🚀 Overview

This is the **third version (V3)** of the Stock Research Agent, built on top of the LangGraph + LangSmith ecosystem.  
Version 3 brings a production-grade architecture with a modular backend and an interactive frontend powered by **Deep Agents UI**.

It extends Version 2 by introducing real-time observability, agent collaboration, and a complete local deployment workflow.

---

| Feature | Version 1 (Old) | Version 2 (Improved) | **Version 3 (New)** |
| --- | --- | --- | --- |
| **Configuration** | Hardcoded in `.py` | `.env`, `.json`, `.md` external configs | Same as V2 |
| **Search Provider** | Fixed to Brave | Optional Brave / Tavily (auto-selected) | Same as V2 |
| **Sub-agents** | Defined inline in code | Externalized in `subagents.json` | Same as V2 |
| **Core Instructions** | Inline (long) | Moved to `instructions.md` | Same as V2 |
| **Token Usage per Query** | ~13 000 | ~3 500 | Same as V2 |
| **Response Time** | Slow (bloated context) | 60–70 % faster (context engineered) | Same as V2 |
| **UI** | Basic textbox | Markdown + Chat UI (Gradio) | **Integrated with Deep Agents UI via LangSmith Server** |
| **Error Handling** | Minimal | Graceful fallbacks, provider status banners | Same as V2 |
| **Backend Runtime** | Local Python | Gradio app | **LangGraph / LangSmith Server** |
| **Deployment** | Manual | Scripted | Same as V2 + UI integration |
| **Monitoring** | None | Console logs | **UI-based interaction through Deep Agents UI** |

---

- **Before (v1):** ~13,000 tokens per research query (bloated instructions + redundant context).
- **Now (v2):** ~3,500 tokens per query.
- Achieved through:
	- Externalizing prompts (`.md` + `.json` files).
	- Removing redundant instructions.
	- Adding clear tool descriptions.
	- Context-aware selective tool usage.

💰 **Impact:** Reducing from 13k → 3.5k tokens saves ~73% in API costs and improves response latency by 60–70%.

---

- When deep agents or tools recurse too much, Python may throw a `RecursionError`.
- **Avoid simply increasing the recursion limit** — it may hide design flaws or cause infinite loops.
- Instead:
	- Set clear stopping conditions in agents.
	- Limit maximum depth of reasoning/tool calls.
	- Use guardrails in prompts to discourage looping.
- Keep prompts **precise** and **minimal**.
- Avoid duplicate phrases across instructions and sub-agent definitions (they bloat token count).
- Provide **short, structured tool descriptions** instead of verbose text.
- Define workflows clearly so the model doesn’t need extra clarification cycles.

**Before (v1, verbose):**

**After (v2, concise):**

```
@tool
def get_stock_price(symbol: str) -> str:
    """Fetch stock price, company name, market cap, P/E ratio, 52-week range."""
```

➡️ The shorter description conveys the same meaning but reduces tokens and avoids repetition.

**Token Comparison:**

- v1: ~60 tokens
- v2: ~20 tokens
- **Reduction:** ~67%

**Before (v1, verbose):**

```
fundamental_analyst = {
    "name": "fundamental-analyst",
    "description": "Performs deep fundamental analysis of companies including financial ratios, growth metrics, and valuation",
    "prompt": """You are an expert fundamental analyst with 15+ years of experience. 
    Focus on:
    - Financial statement analysis
    - Ratio analysis (P/E, P/B, ROE, ROA, Debt-to-Equity)
    - Growth metrics and trends
    - Industry comparisons
    - Intrinsic value calculations
    Always provide specific numbers and cite your sources.""",
}
```

**After (v2, concise):**

```
fundamental_analyst = {
    "name": "fundamental-analyst",
    "description": "Performs company fundamental analysis",
    "prompt": "You are a fundamental analyst. Focus only on:\n- Financial statements (Revenue, Net Income, Assets, Debt)\n- Ratios: P/E, P/B, ROE, ROA, Debt/Equity\n- Growth trends vs peers\n- Valuation (intrinsic value)"
}
```

➡️ Context was streamlined by removing persona fluff ("expert with 15+ years") and redundant phrasing. The new version conveys the same scope but with fewer tokens.

**Token Comparison:**

- v1: ~120 tokens
- v2: ~55 tokens
- **Reduction:** ~55%
- Tool descriptions are always loaded into the agent’s context.
- Long, verbose descriptions add up quickly because they are **repeated on every query**.
- Short, clear descriptions save tokens while still giving the model enough guidance.
- Example: If you have 5 tools and each has a 100-token description, that’s **500 tokens added to every query** — even if only 1 tool is used.
- Externalize large prompts and configs into `.md` and `.json` files.
- Pass only the **needed tools** and **subagents** for each run.
- Remove unnecessary background text or repetition.
- Result: faster responses, fewer tokens, and no information loss.

---

- Keep tool descriptions under 1–2 lines.
- Avoid persona fluff in sub-agent prompts.
- Externalize long instructions to `.md` and `.json` files.
- Monitor token counts with `tiktoken` or similar utilities.
- Set guardrails to prevent recursion loops.

---

- Add multi-company comparative analysis.
- Add streaming responses for real-time progress display.
- Extend UI with charts (price trends, RSI graphs).
- Option to export reports as PDF.

---

## ✅ Summary

Version 2 of the Stock Research Agent delivers:

- Cleaner configuration (`.env`, `.json`, `.md`).
- Flexible and optional search provider setup.
- Optimized token usage with **context engineering**.
- Practical learnings on recursion, prompt design, and context control.
- Much faster and cheaper queries without sacrificing depth.

This sets the foundation for more advanced reporting, visualization, and deployment.

---

- [Screenshot 1](https://github.com/sagar-n/deepagents/blob/main/deep-research-agents-v2/screenshots/image1.png) – UI previews and analysis examples
- [Screenshot 2](https://github.com/sagar-n/deepagents/blob/main/deep-research-agents-v2/screenshots/image2.png) – Example stock research report
- [Demo Video](https://github.com/sagar-n/deepagents/blob/main/deep-research-agents-v2/deepagents-v2.mp4) – walkthrough of the stock research workflow

---

## 📖 Reference

- [Version 1 README](https://github.com/sagar-n/deepagents/blob/main/deep-research-agents-v1/readme.md) – for comparison with the original implementation

## 🚨 Disclaimer

This tool is for educational and research purposes only. It does not constitute financial advice. Always consult with qualified financial advisors before making investment decisions. Past performance does not guarantee future results.

---

## 🙏 Acknowledgments

- **LangChain** – for the DeepAgent framework
- **Yahoo Finance** – for free and reliable financial data APIs
- **Gradio** – for the intuitive and flexible UI framework
- **Ollama** – for enabling local LLM hosting
- **Tavily** – for providing fast browser search APIs
- **Brave** – for offering a robust web search API

---

If you find this project useful, please consider giving it a star ⭐️ on GitHub!

---

[![Star History Chart](https://camo.githubusercontent.com/3379c1784dd9a21b2b8eb22f16553d58611271be77facd7ce9660d745f103fd0/68747470733a2f2f6170692e737461722d686973746f72792e636f6d2f7376673f7265706f733d73616761722d6e2f646565706167656e747326747970653d44617465)](https://star-history.com/#sagar-n/deepagents&Date)

**Built with ❤️ using LangChain DeepAgents**

*Transform your investment research with the power of specialized AI agents.*

## Releases 2

[\+ 1 release](https://github.com/sagar-n/deepagents/releases)

## Packages

No packages published  

## Languages

- [Python 100.0%](https://github.com/sagar-n/deepagents/search?l=python)