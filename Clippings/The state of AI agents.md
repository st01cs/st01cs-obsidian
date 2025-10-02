---
title: "The state of AI agents"
source: "https://rlancemartin.github.io/2025/06/10/aie/"
author:
published:
created: 2025-10-01
description: "Reflections on the AI Engineering World's fair."
tags:
  - "clippings"
---
[@rlancemartin](https://x.com/RLanceMartin)

The [AI Engineering World’s fair](https://www.ai.engineer/) took place last week in San Francisco. After seeing a few talks live and [watching a few of the recordings](https://www.youtube.com/@aiDotEngineer/streams), I had a few takeaways about the current state of AI agents.

## The Rise of Ambient Agents

[“Ambient”](https://blog.langchain.dev/introducing-ambient-agents/) agents are becoming more common. They perform tasks autonomously and asynchronously “in the background”, often without a chat interface.[Scott Wu](https://x.com/ScottWu46) of Cognition showed a key driver for this: the length of tasks that AI can perform autonomously is doubling every ~7 months.

![](https://rlancemartin.github.io/assets/scott_wu.png)

Scott outlined the history of Devin, Cognition’s coding agent. Since last summer, Devin has been able to fix bugs or implement features based on user requests via Slack or other surfaces. [Kevin Hou](https://x.com/kevinhou22) from Windsurf also discussed the transition from human-in-the-loop synchronous workflows that are ~80:20 agent:human to “ambient” asynchronous workflows that are autonomous and only ask the human for final approval.

![](https://rlancemartin.github.io/assets/kevin_hou_async.png)

Recent podcasts with Michael Truell (Cursor) [have touched on this theme](https://www.lennysnewsletter.com/p/the-rise-of-cursor-michael-truell). OpenAI also [launched their Codex agent](https://openai.com/index/introducing-codex/), which can connect to GitHub and manage asynchronous coding tasks.

[Solomon Hykes](https://x.com/solomonstre) summarized the environment he wants for ambient agents: do background work for me, with ability to easily add constraints (e.g., tools to define the action space, secrets, etc.), with “multiplayer” mode (human in the loop) so that I can get alerts if the agents needs my attention, and with discoverability so that I can choose different agents to work with easily.

![](https://rlancemartin.github.io/assets/solomon_hykes.png)

## The Bitter Lesson + Agent UX

The right agent UX is a big question right now. [Boris Cherny](https://x.com/bcherny) of Anthropic gave a talk on Claude Code. His view on agent UX is influenced by [the bitter lesson](http://www.incompleteideas.net/IncIdeas/BitterLesson.html): general methods that scale with computation and data outperform more specialized approaches that rely on hand-crafted inductive biases. Boris mentioned a corollary to this: general things *around* the model also tend to win.

With models improving quickly, Claude Code is general, minimalistic, and unopinionated. It runs in terminal without a UI. At Anthropic demo day, Boris mentioned that that people [may not be using IDEs](https://www.youtube.com/watch?v=6eBSHbLKuN0) by the end of this year.

![](https://rlancemartin.github.io/assets/boris_cherny.png)

[Kevin Hou](https://x.com/kevinhou22) from Windsurf gave an alternative view: build an opinionated UI (IDE, in the case of coding) tailored to the workflow of today and use it to collect data. The data can be used to train models for that specific task, as shown in the data flywheel underpinning Windsurf’s SWE-1 model.

![](https://rlancemartin.github.io/assets/kevin_hou.png)

## Agent Training

Agents are being trained with task-specific reinforcement learning (RL). [Nathan Lambert](https://x.com/natolambert) gave an overview of Reinforcement Learning with Verifiable Rewards (RLVR) and made the point that we are early on this scaling curve: OpenAI increased the RL compute by ~10x [from o1 to o3](https://openai.com/index/introducing-o3-and-o4-mini/). The compute that has been historically used in RL “post-training” is much less than pre-training.

![](https://rlancemartin.github.io/assets/nathan_lambert.png)

A central question is whether RLVR will work on “non-verifiable tasks” (beyond code and math). [Will Brown](https://x.com/willccbb) mentioned that a well-curated LLM-as-judge reward function is a promising approach.

[Kyle Corbitt](https://x.com/corbtt) from Open Pipe discussed Art-E, which is a nice example of this. They built an agent for e-mail QA using RLVR (see the blog [here](https://openpipe.ai/blog/art-e-mail-agent)). It used [the Enron email dataset](https://www.cs.cmu.edu/~enron/), synthetically generated QA pairs from ~100k emails, and used LLM-as-judge for answer correctness as the reward function.

They trained Art-E to answer questions about e-mails using Qwen-2.5-14b as the base model with e-mail tools. Training used GRPO, the project took ~1 wk of work, and it cost $80 of compute. The central point is that Art-E can outperform frontier models with prompting on this narrow task.

![](https://rlancemartin.github.io/assets/kyle_corbitt.png)

## Agent Tools

Agents need the right tools to be effective. It’s not hard to define tools and bind them to an LLM using the various model SDKs. So, why is a protocol like [MCP](https://modelcontextprotocol.io/introduction) useful? [John Walsch](https://x.com/johnw188) gave a talk on the practical origins of MCP within Anthropic.

LLMs got good at tool calling. Everyone started writing tools without coordination, resulting in duplication and many custom endpoints for each use-case. Inconsistent interfaces confused developers. Duplicated functionality created maintenance challenges.

![](https://rlancemartin.github.io/assets/standardization.png)

MCP provides a standard protocol to address these problems. But, an interesting lesson from the talk was the need to build internal tooling around the MCP protocol: Anthropic built an internal MCP Gateway to handle MCP connections and made it the easiest way to connect Claude to context or tools. It abstracts all transport and auth, and provides observability. This gives a central point of ingress / egress for all model context, allowing for auditing / policy enforcement and visibility into what models are trying to do.

![](https://rlancemartin.github.io/assets/pit.png)

## Agent Memory

[Scott Wu](https://x.com/ScottWu46) made an important point: if you tell an agent how to do something, you want it to *remember* that for next time! Devin, [Windsurf](https://docs.windsurf.com/windsurf/cascade/memories) and [Cursor](https://docs.cursor.com/guides/working-with-context) all have memory. In his talk on Claude Code, Boris Cherny gave some useful examples of saving memories to various `CLAUDE.md` files.

The UX for memory is tricky, though. When should the agent fetch memories? [Simon Willison](https://x.com/simonw?lang=en) gave an example of the challenge: memory can mean loss of control for the user. He highlighted a case where GPT-4o injected location into an image based upon his memories, which was not desired.

Also, memory systems today are external to the model. [Nathan Lambert](https://x.com/natolambert) brought up the topic of continual learning, which has been mentioned [elsewhere](https://www.dwarkesh.com/p/timelines-june-2025) recently. Human feedback may be incorporated directly into the model in the future rather than using external memory systems.

## Conclusion

At least three themes emerged:

**Autonomy is accelerating.** Agents can now work on tasks for hours or days, doubling their capability every 7 months. This is pushing us toward “ambient” agents that work behind the scenes.

**The tooling ecosystem is maturing.** Standards like MCP solve coordination problems, while memory systems are becoming essential for agents to learn from past interactions.

**Training methods are evolving.** Reinforcement learning with verifiable rewards is showing promise beyond just code and math, potentially transforming how we build agents in non-verifiable domains.

The future of AI agents looks less like improved chatbots and more like assistants that handle complex work autonomously.