---
title: "langchain-ai/deep-agents-ui: Custom UI for Deep Agents"
source: "https://github.com/langchain-ai/deep-agents-ui"
author:
  - "[[nhuang-lc]]"
published:
created: 2025-11-03
description: "Custom UI for Deep Agents. Contribute to langchain-ai/deep-agents-ui development by creating an account on GitHub."
tags:
  - "clippings"
---
[Skip to content](https://github.com/langchain-ai/#start-of-content)

**[deep-agents-ui](https://github.com/langchain-ai/deep-agents-ui)** Public

- [Fork 171 Fork your own copy of langchain-ai/deep-agents-ui](https://github.com/langchain-ai/deep-agents-ui/fork)

Custom UI for Deep Agents

### License

[MIT license](https://github.com/langchain-ai/deep-agents-ui/blob/main/LICENSE)

[Open in github.dev](https://github.dev/) [Open in a new github.dev tab](https://github.dev/) [Open in codespace](https://github.com/codespaces/new/langchain-ai/deep-agents-ui?resume=1)

## langchain-ai/deep-agents-ui

## Add file

Deep Agents are generic AI agents that are capable of handling tasks of varying complexity. This is a UI intended to be used alongside the [`deep-agents`](https://github.com/hwchase17/deepagents?ref=blog.langchain.com) package from LangChain.

If the term "Deep Agents" is new to you, check out these videos![What are Deep Agents?](https://www.youtube.com/watch?v=433SmtTc0TA)[Implementing Deep Agents](https://www.youtube.com/watch?v=TTMYJAw5tiA&t=701s)

And check out this [video](https://youtu.be/0CE_BhdnZZI) for a walkthrough of this UI.

Create a `.env.local` file and set two variables

```
NEXT_PUBLIC_DEPLOYMENT_URL="http://127.0.0.1:2024" # Or your server URL
NEXT_PUBLIC_AGENT_ID=<your agent ID from langgraph.json>
```

Create a `.env.local` file and set three variables

```
NEXT_PUBLIC_DEPLOYMENT_URL="your agent server URL"
NEXT_PUBLIC_AGENT_ID=<your agent ID from langgraph.json>
NEXT_PUBLIC_LANGSMITH_API_KEY=<langsmith-api-key>
```

Once you have your environment variables set, install all dependencies and run your app.

```
npm install
npm run dev
```

Open [http://localhost:3000](http://localhost:3000/) to test out your deep agent!

## Releases

No releases published

## Packages

No packages published