---
title: "Learnings from two years of using AI tools for software engineering"
source: "https://newsletter.pragmaticengineer.com/p/two-years-of-using-ai"
author:
  - "[[Gergely Orosz]]"
published: 2025-06-24
created: 2025-10-02
description: "How to think about today’s AI tools, approaches that work well, and concerns about using them for development. Guest post by Birgitta Böckeler, Distinguished Engineer at Thoughtworks"
tags:
  - "clippings"
---
### How to think about today’s AI tools, approaches that work well, and concerns about using them for development. Guest post by Birgitta Böckeler, Distinguished Engineer at Thoughtworks

It feels like GenAI is changing software engineering fast: first, it was smarter autocomplete, and now there’s ever more agentic tools that many engineers utilize. But what are some practical approaches for using these tools?

To find out more, I turned to [Birgitta Böckeler](https://birgitta.info/), Distinguished Engineer at Thoughtworks, who has been tackling this question full time for the past two years. She still writes production code at Thoughtworks, but her main focus is developing expertise in AI-assisted software delivery.

To stay on top of the latest developments, Birgitta talks to Thoughtworks colleagues, clients, and fellow industry practitioners, and uses the tools. She tries out tools, and figures out how they fit into her workflow. Today, Birgitta walks us through what she’s learned the last two years of working with AI tools:

1. **Evolution from “autocomplete on steroids” to AI agents**. From the early days of autocompete, through AI chats and IDE integration, to the agentic step change.
2. **Working with AI**:a practical mental model of your “AI teammate,” beware of cognitive biases where GenAI can “manipulate” you, and emerging workflows with AI
3. **Impact on team effectiveness.** AI coding assistants increase the speed of software delivery – though it’s complicated to measure by *exactly* how much. Without close supervision, the impact on quality could be negative. Team dynamics will most likely be impacted when rolling out these tools quickly.
4. **The future.** LLMs are *not* the next compilers: they are something different, the future of AI coding is unevenly distributed, and we will take on tech debt while figuring out how to use these AI tools the right way.

To learn more, check out additional thoughts by Birgitta in the [Exploring Generative AI](https://martinfowler.com/articles/exploring-gen-ai.html) collection on her colleague Martin Fowler's website.

*Programming note: this week, I’m in Mongolia for the launch of The Software Engineer’s Guidebook translated into Mongolian, so there will be no podcast episode or The Pulse this week: see you for the next issue, next Tuesday!*

*With that, it’s over to Birgitta. Note, the terms AI, Generative AI, and LLM are used interchangeably throughout this article.*

---

Almost precisely 2 years ago in July 2023, Thoughtworks decided to introduce a full-time, subject-matter expert role for "AI-assisted software delivery". It was when the immense impact that Generative AI can have on software delivery was becoming ever more apparent, and I was fortunate enough to be in the right place at the right time, with the right qualifications to take on the position. And I’ve been drinking from the firehose ever since.

**I see myself as a domain expert for effective software delivery who applies Generative AI to that domain.** As part of the role, I talk to Thoughtworks colleagues, clients, and fellow industry practitioners. I use the tools myself and try to stay on top of the latest developments, and regularly [write](https://martinfowler.com/articles/exploring-gen-ai.html) and [talk](https://birgitta.info/) about my findings and experiences.

This article is a round-up of my findings, experiences, and content, from the past 2 years.

## 1\. Evolution from “autocomplete on steroids” to AI agents

AI coding tools have been developing at breakneck speed, making it very hard to stay on top of the latest developments. Therefore, developers not only face the challenge of adapting to generative AI's nature, they also face an additional hurdle: once they've formed opinions about tools or established workflows, they must adjust constantly to accommodate new developments. Some thrive in this environment, while others find it frustrating.

So, let’s start with a recap of that race so far, of how AI coding assistants have evolved in two years. It all started with enhanced autocomplete, and has led to a swarm of coding agents to choose from today.

![](https://substackcdn.com/image/fetch/$s_!Mmxx!,w_424,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F94587a2c-3dc9-45e6-92ef-5705eaa64638_1600x1326.png)

How AI assistants evolved, 2021-2025

### Early days: autocomplete on steroids

The first step of AI coding assistance felt like an enhanced version of the autocomplete we already knew, but on a new level. As far as I know, Tabnine was the first prominent product to offer this, in around 2019. GitHub Copilot was first released in preview in 2021. It was a move from predictions based on abstract syntax trees and known refactoring and implementation patterns, to a suggestion engine that is much more adaptive to our current context and logic, but also less deterministic, and more hit and miss. Developer reactions ranged from awe, to a dismissive “I’ll stick with my reliable IDE functions and shortcuts, thank you very much.”

Back then, I already found it a useful productivity booster, and soon didn’t want to work without it, especially for languages I was less familiar with. However, like many others, I soon discovered the reality of “review fatigue” which leads some developers to switch off the assistant and focus fully on code creation, instead of code review.

### AI chats in the IDE

It seems unimaginable today, but there was a time when assistants did not have chat functionality. I recall announcing in the company chat in July 2023 that our GitHub Copilot licenses finally had the chat feature: 24 minutes later somebody posted that they’d asked Copilot to explain a shell script in Star Wars metaphors. From a developer experience point of view, it was a big deal to be able to ask questions directly in the IDE, without having to go to the browser and sift through lots of content to find the relevant nugget for my situation.

And it was not just about asking straightforward questions, like whether there are static functions in Python; we also started using them for code explanation and simple debugging. I remember fighting with a piece of logic for a while before the assistant explained that two of my variables were named the wrong way around, which is why I had been misunderstanding the code the whole time.

At that point, hallucinations started to become an even bigger topic of discourse, along with comparisons to StackOverflow, which was starting to observe its first decline in traffic.

### Enhanced IDE integrations

Over time, AI tooling also got more advanced integration into existing IDE functionality: AI started showing up in “quick fix” menus, and integration with the IDE terminal got better. In late 2023, I finally stopped prompting through code comments; instead, I started popping up the little inline editor chat to give quick prompting instructions right where my code was.

![](https://substackcdn.com/image/fetch/$s_!Y3Rm!,w_424,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F209f1cfc-1939-41b0-a952-538ece90f1c0_1600x365.png)

Inline editor chat in VS Code

IDE integration is one reason I prefer using IDE coding assistants over terminal-based ones. IDEs are built to understand, navigate, and change code, and pairing them with token-based LLMs is really powerful. I believe there is much more potential integration still untapped, and look forward to having my agent access the debugger or refactoring functionalities.

### Chatting with the Codebase

The key to AI assistants is the context of what’s being worked on, so their integration with the codebase as a whole was the next big step, which started happening in around autumn 2023. Being able to ask questions about the codebase is especially useful when working with an unfamiliar one, and I found it very useful to be able to ask questions like “where is validation of X implemented”, or “how are we filtering?”. Even in the early days of these features, I found they more often than not pointed me in the right direction, and offered added value over text search. Since then, codebase awareness has significantly improved.

How effectively this codebase search is implemented is still a differentiating factor between coding assistants. The approaches range from vector-based indices like Cursor and Windsurf, to abstract syntax and file tree based text search such as Cline, and sophisticated code search engines like Sourcegraph Cody.

**Context Providers**

The codebase is not all the context there is, though; there are lots of other data sources that can provide helpful context for an AI assistant. More context providers were integrated into the assistants to give developers greater control over what information the AI assistant sees. Developers could point at the local change set, terminal output, website URLs, reference documentation, and even the first instances of JIRA ticket integration.

There were also the first indications of the need for an ecosystem when GitHub announced [GitHub Copilot Extensions](https://github.blog/news-insights/product-news/introducing-github-copilot-extensions/) in May 2024; a way for providers to integrate context providers. Fast forward to today, [MCP](https://newsletter.pragmaticengineer.com/p/mcp) (Model Context Protocol) has sent the context provider ecosystem into overdrive and taken over the space.

**Model evolution**

In parallel to all these tool features, the models have evolved, too. This space is particularly tricky to keep up with, as it's hard to get objective measures of how well a model performs for coding. A “TL/DR” summary of where model evolution is at this point, is that while there are multiple good candidates out there, Anthropic's Claude Sonnet series has clearly emerged as a consistent favorite for coding tasks. It’s my "sensible default" recommendation, as of today. The model used is definitely important, but I think it’s still widely underestimated what a big role the features and integrated tools play, especially when models are paired up with tools that understand code, and can therefore complement the large language model’s (LLM) purely tokenised understanding of things.

### The agentic step change

The current frontier – and arguably the biggest step change so far – is the emergence of agentic coding. I currently divide the coding agents into two buckets:

**Supervised coding agents:** Interactive chat agents driven and steered by a developer. Create code locally, in the IDE.

***Tools:*** The very first tool in this style I saw was Aider, and its git history starts as early as May 2023. Cline has been around since July 2024, the agentic modes in Cursor and Windsurf started around November 2024, and GitHub Copilot Coding Agent was a late arrival [in May 2025](https://github.com/newsroom/press-releases/coding-agent-for-github-copilot). Claude Code and various Cline forks have also gained a lot of traction in the first half of 2025.

**Autonomous background coding agents:** Headless agents which are sent off to work autonomously through a whole task. Code gets created in a remote environment spun up exclusively for that agent, and usually results in a pull request. Some are also runnable locally.

***Tools:*** The very first one of these that got a lot of attention was Devin, with big announcements in March 2024, soon followed by online controversy. They released a generally available version in December 2024. While there were a few similar attempts here and there, including an open source project called “OpenDevin” that quickly had to rename itself to “OpenHands”, background agents have recently seen new momentum with the releases of OpenAI Codex, Google Jules, and Cursor background agents.

Coding agents expand the size of the task that can be collaborated on with AI into a larger problem-solving loop. This is mainly fuelled by increased automation and integration with tools like terminal command execution or web search. Just imagine any tool used by developers in their coding workflow, and how it could enhance a coding agent's capabilities if it were integrated. MCP is the catalyst of that ecosystem of integrations, at the moment.

Here’s an example of a problem-solving loop:

- "I'm getting this error message, help me debug: …"
- Agent does web research, finds something in the library's documentation, and some issue discussions on GitHub
- Adds patch library dependency to the project
- Runs npm install to install the new dependency
- Adds necessary code to the project
- Restarts application
- Sees error message
- Tries to fix the code based on the error message
- Restarts application again
- ...

With a **supervised agent**, a human is looking over the agent's shoulder and intervenes when necessary. This over-the-shoulder look can range from skimming the agent's reasoning to see if it's going in a good direction, code review, interrupting and rolling back, answering questions from the agent, or approving the execution of terminal commands.

Many people were introduced to the supervised agentic modes via the “vibe coding” meme in early February 2025. Even though vibe coding by definition is a mode where a person does not review the code, I still see it in this supervised category, as a human constantly looks at the resulting application and gives the agent feedback.

**Autonomous background agents** are assigned to work on a task autonomously, and a person only looks at the result once the agent is done. The result can be a local commit or a pull request. I haven’t yet seen them work for more than small, simple tasks, but they’ll probably have their place in our toolchain as they mature.

**We cover supervised agents in this article**. Autonomous background agents are [still in their early days](https://martinfowler.com/articles/exploring-gen-ai/autonomous-agents-codex-example.html), and have a lot of kinks to work out. Below, I use "coding agents" synonymously with "supervised agents."

## 2\. Working with AI

Generative AI is a fast-moving target, so practices constantly adapt to new developments. However, there are some “timeless” principles and ways of working that I apply today.

First of all, there’s a distinct shift in mindset required to work effectively with GenAI. [Ethan Mollick](https://www.linkedin.com/in/emollick), professor at Wharton, researcher on AI, made the observation early on that [“AI is terrible software”](https://www.oneusefulthing.org/p/ai-is-not-good-software-it-is-pretty). This really clicked for me: generative AI tooling is not like any other software. To use it effectively, it’s necessary to adapt to its nature and embrace it. This is a shift that’s especially hard for software engineers who are attached to building deterministic automation. It feels uncomfortable and hacky that these tools sometimes work and other times don’t.

Therefore, the first thing to navigate is the mindset change of becoming an effective human in the loop.

### Cognitive shift: mental model of the AI teammate

A helpful step for me was to give my coding assistant a persona, to anthropomorphize it just enough to calibrate my expectations (inspired by Ethan Mollick and his book, [Co-Intelligence](https://www.goodreads.com/book/show/198678736-co-intelligence)). There are mental models for each human teammate, which are used implicitly when deciding to trust their work and input. Someone who’s very experienced in backend and infrastructure work is likely to have their input and advice trusted, but it still might be wise to double check when they’re building their first React Hook.

Here’s [the persona](https://martinfowler.com/articles/exploring-gen-ai/08-how-to-tackle-unreliability.html) I settled on for AI assistants:

- Eager to help
- Stubborn, and sometimes with a short-term memory
- Very well-read, but inexperienced
- Overconfident

![](https://substackcdn.com/image/fetch/$s_!_N29!,w_424,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Ffe3f9b49-97ae-45f8-9a67-c73f5db75694_1600x751.png)

My mental model for an AI teammate

This mental model helped me develop an intuition of when to reach for GenAI, when to trust its results more, and when to trust it less. I expect enthusiasm and assistance, and even access to current information via web search. But I must still exercise judgment, context, and final authority.

### Beware biases

Working with Generative AI is fertile ground for several cognitive biases that can undermine judgment. I find this a fascinating part of GenAI: how manipulative this technology is.

Here are just a few examples of potential cognitive biases:

**[Automation bias](https://en.wikipedia.org/wiki/Automation_bias)** represents our tendency to favor suggestions from automated systems while ignoring contradictory information, even when that information is correct. Once you've experienced success with AI-generated code, it's natural to start over-trusting the system. The confident tone and polished output can make us less likely to question its recommendations, even when experience suggests a different approach.

**The [framing effect](https://en.wikipedia.org/wiki/Framing_effect_\(psychology\))** reinforces the impact of the positive, confident phrasing of LLM responses. For instance, if an AI suggests that a particular approach is "best practice," we are more likely to take that at face value and adopt it, without considering context-specific factors.

**The [anchoring effect](https://en.wikipedia.org/wiki/Anchoring_effect)** can kick in when AI presents a solution before we thought about it. After viewing AI's suggestions, we can find it harder to think creatively about alternative solutions. The AI's approach becomes our mental starting point, potentially limiting our exploration of better alternatives. On the flip side, AI can also help us mitigate anchoring bias, for example when assisting with modernising a pre-existing solution we're already anchored to.

And finally, there is also a version of **[sunk cost fallacy](https://en.wikipedia.org/wiki/Sunk_cost#Fallacy_effect)** at work when coding with AI. Investing less human labour into writing code, should make it easier to discard code that’s not working. However, I've caught myself becoming over-attached to large pieces of AI-generated code which I’d rather try to fix instead of revert. Perceived time savings create a psychological investment that can make one reluctant to abandon AI-generated solutions, even when they're sub-optimal.

### General ways of working principles

Once you’re mentally prepared and have steeled yourself against the biases, the following are some general principles I’ve found practical for utilizing AI assistants efficiently.

**Reflect on feedback loops**. How do you know the AI did as instructed, and can this be learned quickly, and review fatigue reduced? If it's a small change, do you write a unit test, or let AI generate one and use that as the main point of review? If it's a larger change, which available tests are trustworthy: an integration test, an end-to-end test, or an easy manual test? Beyond functionality, what is in place to quickly assess code quality: a static code analysis plugin in the IDE, a pre-commit hook, a human pairing partner? It’s sensible to be aware of all options and to reflect on the feedback loop when working on a task with AI.

**Know when to quit**. When I feel like I'm losing control of a solution and don't really understand what's happening, I revert; either the whole set of local changes, or to a previous checkpoint – which is a feature supported by most coding assistants. I then reflect on how to take a better approach, like ways to improve my prompts, or breaking down a task into smaller steps, or resorting to "artisanal coding" like writing the code from scratch, myself.

**Know your context providers and integrated tools**. Does a tool have web access, or does it solely rely on its training data, how much access does it have to your codebase, does it search it automatically, or do you have to provide explicit references, what other context providers and MCP servers are available and useful? Having knowledge of the capabilities and access of the tool is important for picking the right one for the job, and for adjusting expectations and trust level. You should also know which data an agent has access to and where it's sent, in order to understand [risks to the software supply chain](https://martinfowler.com/articles/exploring-gen-ai/software-supply-chain-attack-surface.html), and wield this powerful tool responsibly.

### Emerging workflows with agents

Before coding agents, the coding workflow with AI assistants was relatively close to how engineers usually work, 1-50 lines of code at a time. AI was along for the ride and boosting us step by step. This has changed with coding agents, which not only increase the size of tasks to work on, but also the size of the code review and the context information needed.

Below are the main recommendations I currently give for working with agentic assistants. I should say, all of these are ways to increase the likelihood of success, but as always with Generative AI, there are no guarantees, and its effectiveness depends on the task and the context.

**Use custom instructions**. Custom instructions – or “custom rules” as some tools call them – are a great way to maintain common instructions for the AI. They are like a natural language configuration of the coding assistant, and can contain instructions about coding style and conventions, tech stack, domain, or just mitigations for common pitfalls the AI falls into.

**Plan (with AI) first**. As appealing as it sounds to just throw one sentence at the agent and then have it magically translate that into multiple code changes across a larger codebase, that's usually not how it works well. Breaking down the work first into smaller tasks not only makes it easier for the agent to execute the right changes in small steps, but also gives a person the chance to review the direction the AI is going in and to correct it early, if needed.

**Keep tasks small**. The planning stage should break the work down into small tasks. Even though models technically have larger and larger context windows, that doesn't necessarily mean they can handle all the context in a long coding conversation well, or that they can maintain focus on the most important things in that long context. It’s much more effective to start new conversations frequently, and not let the context grow too large because the performance usually degrades.

**Be concrete**. "Make it so I can toggle the visibility of the edit button", is an example of a more high level task description that an agent could translate into multiple different interpretations and solutions. A concrete description which will lead to more success is something like, "add a new boolean field 'editable' to the DB, expose it through /api/xxx and toggle visibility based on that".

**Use some form of memory**. Working in small tasks is all well and good, but when working on a larger task in multiple smaller sessions, it’s not ideal to repeat the task, the context, and what has already been done, every time a new subtask is started. A common solution to this is to have the AI create and maintain a set of files in the workspace that represent the current task and its context, and then point at them whenever a new session starts. The trick then becomes to have a good idea of how to best structure those files, and what information to include. [Cline's memory bank](https://docs.cline.bot/prompting/cline-memory-bank) is one example of a definition of such a memory structure.

## 3\. AI’s impact on team effectiveness

The introduction of AI tooling to software delivery teams has led to a resurgence of the perennial question of how to measure software team productivity. *Note from Gergely: we dig into this topic with Kent Beck in [Measuring developer productivity? A response to McKinsey](https://newsletter.pragmaticengineer.com/p/measuring-developer-productivity).*

My short answer to how to measure developer productivity is that the problem does not change just because there’s something new in the toolbox. We still have the same challenge, which is that software delivery is not an assembly line that produces a stream of comparable pieces to count and measure. Productivity is a multi-dimensional concept that can’t be summed up in a single number.

Having said that, of course it’s possible to look at the many indicators that make up the holistic picture of productivity, and see how AI impacts them. I focus on speed and quality first, and then touch on team flow and process.

### Impact on speed

AI coding assistants can definitely increase the speed of software delivery, and there’s lots of evidence of a decrease in cycle time and an increase in coding throughput, number of commits, pull requests, and the size of pull requests. I have seen this first hand, and heard credible reports and examples from teams. This speed increase doesn’t only stem from engineers typing faster; it’s fed by the potential for faster onboarding, faster learning, and faster debugging with GenAI’s help.

At the same time, there are many organisations which say they don't really see a *measurable* impact from AI, and wonder if they’re doing something wrong, or fell for the hype.

From my observations, disappointments are rooted in the following things:

- **Mileage varies**: How effective coding assistants are can vary widely, depending on the situation, such as the complexity of a project or domain, tech stack, quality of existing code and documentation, the seniority of the team, and whether they use the latest AI features effectively.
- **AI tooling is a moving target**: Tooling and possibilities constantly evolve, which further skews any measurements made in this transition period, as teams who are all-in on AI are more likely to constantly experiment with new developments.
- **Hard to get distinct, visible measures**: Not only is it hard to attribute changes in speed to AI tooling, but a lower impact like 10% might also not even be visible, given the high variance in cycle time that’s the reality for many teams.
- **Overblown expectations**: Organisations which expect a visible 50% team speed improvement are likely to be disappointed when it's 5-10% in practice, even though that's not bad at all, considering the cost of the tools.

So, as always in software, it's complicated, and it depends. But what's the ballpark?

I’ve found it useful to think in scenarios and to identify relevant parameters when assessing a particular team or organisation’s situation. It’s a helpful tool to get an idea of what to expect when it comes to impact on speed.

One of the better proxy variables for delivery speed is story cycle time, i.e. the time from when a developer picks up a user story, to the point it’s deployed to production. So, let's look at the parameters of a coding assistant's impact on cycle time:

- How much of the cycle time does a team spend on coding? Let's say **40%**.
- How much of that time is a coding assistant useful? Let's say **60%**. ([GitHub claimed in early January 2023 already that ~60% of code in Java codebases was written by Copilot](https://github.blog/ai-and-ml/github-copilot/github-copilot-now-has-a-better-ai-model-and-new-capabilities/))
- How much faster are they when they use the coding assistant? Let's say **55%** (the number for faster task completion that was [published by GitHub in 2023](https://github.blog/news-insights/research/research-quantifying-github-copilots-impact-on-developer-productivity-and-happiness/)).

For this scenario, the potential ballpark impact on a team's cycle time would be 0.4x0.6x0.55 = 13.2%.

Look at the numbers in this scenario and consider how that applies to your teams. Do they spend more or less than 40% of their cycle time on coding, and how useful is the coding assistant for their type of problem and tech stack? How much faster are they when they use it: do they have an agentic assistant, and have they figured out effective ways to use it? In that case, 55% faster task completion might be conservative. Or are they already a very high performing team with experienced coders, in which case 55% speed boost might be too optimistic.

I know of one case where teams were expected to improve a “rework” metric after the introduction of AI coding assistants. This was much harder for the teams already performing really well at this (at 2% rework rate) than those which weren’t (at 10%).

![](https://substackcdn.com/image/fetch/$s_!CwVd!,w_424,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F94cd4256-46a9-4af5-9045-6397edf56032_1486x992.png)

Estimating potential time saved with coding assistants.

I'm using this heuristic to help you gauge the ballpark impact that can be expected in cycle time measures, and also to show how difficult it is to pin down speed impact with relative percentages. And I haven't even touched on the fact that to get good percentages, there’s only a small window of time until teams start including the coding assistant’s impact in estimations, which will mess up comparisons even more.

### Impact on quality

Let's say a team does indeed increase speed and throughput, like the number of PRs, or number of features released to production in a month. That in itself is not necessarily a good thing, as they might just be building more bad, unnecessary software, faster. Speed measurements always have to be looked at in conjunction with quality.

Software quality is of course even harder to define and measure than speed. For the sake of this article, let's define quality as "long-term maintainability and extensibility". The vast majority of the software which matters has that as a goal, and let's assume it stays this way. On one hand, I’ve heard reports of increased test coverage, new incentives to create more readable and expressive code because it makes AI results better, or usage of AI to assist with code reviews.

Unfortunately, there are also indications that AI coding assistants might be creating more quality problems than they solve. The most interesting study I have seen is [GitClear's data about how the nature of code changes has evolved over the past two years](https://www.gitclear.com/ai_assistant_code_quality_2025_research), since the rise of coding assistants.

GitClear analyzed millions of code changes from a mix of open-source projects mostly maintained by Google, Facebook, and Microsoft, and also private corporate codebases. These are the patterns they found:

![](https://substackcdn.com/image/fetch/$s_!uOV7!,w_424,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F07a4e0dd-3248-43eb-bc7f-fabfdbd601c9_1600x959.png)

With AI, adding code is easier than changing it. Will this become a problem? Source: GitClear

- **Code churn is rising**: Code churn is defined as changes that are revised or reverted within 2 weeks of the original change.
- **Refactoring is declining**: GitClear sees moved lines of code as a good proxy metric for refactoring, and that number has been in decline.
- **More code additions**: While this might be expected with the availability of coding assistants, it's a good idea to monitor if the increase in codebase size is proportionate. With AI, it's easier to add new code than to change existing code, so if a codebase is growing at an accelerated rate, it could be a [code smell](https://en.wikipedia.org/wiki/Code_smell) because GitClear also found an increase in code duplication. Unintentional code duplication can become a serious maintainability issue over time.

**My personal experience: AI agents need close supervision.** I use AI for coding all the time, and don't want to work without it any more. Even in successful sessions with coding agents, I intervene, correct, and steer *all* the time.

Here are some examples of interventions:

- Too much upfront work: AI frequently does too much, too early. Or it even does too much, period, and builds things I didn't plan for
- Brute force fixes instead of root cause analysis
- Test quality: Verbose or redundant tests, not enough tests, too much mocking, tests in the wrong places, fixing the test instead of the code – or the other way around
- Lack of reuse of existing code. My experience aligns with GitClear's findings here, and I also see a risk of more code duplication
- Overly complex implementations

This is particularly insidious when it comes to things that impact longer-term maintainability of the codebase. It might not even be noticeable at the time of a change that it will have a negative impact, or this might be noticed a few months later, when that code needs to be touched again. And no, just because "AI will also maintain the code in the future", this type of internal quality still matters. It turns out, AI agents – like humans – perform better with well-factored codebases than messy ones.

![](https://substackcdn.com/image/fetch/$s_!HIY7!,w_424,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F3559c2ad-7cd6-40ec-bfc7-7f368411ddcb_1600x901.png)

Typical AI missteps and their impact radius. Source: my article, The role of developer skills in agentic coding

Due to these risks to quality, it’s dangerous for organisations to put too much pressure on teams about speed when they roll out AI tools. In their attempt to fulfill those expectations, people will start cutting corners. I believe everyone should waste less energy on measuring ever more seemingly exact numbers about *speed* impact, and instead focus more on monitoring risks and impact on quality. To quote "Cat's Law", recently shared by [Dr. Cat Hicks](https://www.drcathicks.com/) at the Craft conference: "The more a software team fixates on demonstrating short-term performance in their environment, the less they are able to protect the foundation on which long-term performance depends."

### Impact on team flow

The more I use AI in a team context, and the more stories I hear from teams who have been using AI for longer and at a larger scale, the more I wonder about the following questions of AI's impact on teams overall.

**Build more, faster! A promise or a threat?**

In terms of adoption, many organisations mainly adopt AI for coding, but don’t yet do much for the other software delivery tasks. This is probably due to the fact AI can most obviously have an impact on coding, and producing code is a big part of the software creation process. However, what happens if throughput is increased in one part of the process, but the rest is kept mostly the same?

![](https://substackcdn.com/image/fetch/$s_!iEJN!,w_424,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fc6b4131d-dbee-4538-a31a-f4b2fc8cb521_1600x815.png)

Coding faster means you need to review/test/ship faster to speed up.

Can the backlog be filled faster, the code reviewed, tested, and deployed faster, and bugs likewise fixed faster?

One response would be that using AI to speed up other parts of the process is the solution; and yes, it can be part of it. But it’s also sensible to be careful to not use GenAI as a band-aid to cover up cracks in the path to production. In [this post](https://varoa.net/2025/04/07/ai-generated-code.html), Galo Navarro, a principal engineer at Midokura, reminds us of learnings from organisations which increased their throughput pre-AI:

> "After all, the software industry was already competent at increasing supply well before AI. The real struggle happened on the systems downstream."

A sudden increase in volume risks overwhelming existing delivery pipelines, testing, integration, deployment, so organisations should be careful what they wish for when rolling out coding assistants, and invest in being prepared for higher throughput.

**More options: blessing or curse?**

One of the most interesting new things Generative AI brings to the table is ideation. It can bring us more ideas and find gaps in thinking across the board, from product improvements and design, to coding solution options, to more comprehensive testing scenarios. [Gene Kim calls out the "option value" of AI](https://itrevolution.com/articles/genai-metrics-of-value-for-developers-option-value-dora/), and draws parallels to other technologies that made it easier to explore options, which had a profound impact on how software is delivered. I agree, and have personally seen the option value that AI unlocks in action.

However, I'm also starting to hear stories about the downside of that; of teams getting stuck in divergence too long, overwhelmed by all the ideas that AI provides, and spending too much time reviewing and revisiting decisions every time a new idea comes up. Or of developers starting to build things just because it's easier now, not because they’re actually needed.

So these options are a double-edged sword, and it’s important to mitigate the risk of option overload with strong team alignment, and very clear definitions of focus and priorities.

**Waterfall allure: temptation to fall back into old, bad habits?**

GenAI is infamous for generating very plausible-sounding responses that often start breaking down on a second or third look. This leads to tendencies that could tempt engineers back into more waterfall-like ways of working.

- **More upfront design**: When I can generate beautiful user stories with lots of acceptance criteria and details early on, will that lead to more up-front design? On one hand, I have heard stories from teams which improved their quality by discovering more comprehensive scenarios and edge cases early on, and therefore had less back and forth and bugs later during cycle time. But I also see a need to time that well because when generating lots of details too early with AI, editing those details weeks later when a developer picks up the story and the world has changed, creates friction and rework. Therefore, I recommend thinking about when to use AI to create a level of detail.
- **Human quality control is shifted more [to the right](https://martinfowler.com/articles/rise-test-impact-analysis.html#ShiftLeftAndRight)**: With AI generating all those nice, plausible solutions, we are more tempted to push them on to the next step in our team flow without proper scrutiny and review. I hear stories of PR reviewers getting annoyed at reviewing code that the human author cannot explain when asked. And when I hear of tools that let AI do code review on pull requests, I always wonder why the developer didn't run that AI tool before they even committed the code. So, we have to be careful to not shift the human quality control too far to the right.

## 4\. The future

Thanks to my role, I naturally get asked about the future of GenAI's impact on software delivery. I have started to wonder if we’re fixating too much on the future, and not having enough discourse and curiosity about what it actually means on the ground today for a software team. That's why I address so many practical concerns and open questions in this article, even though I wouldn't call myself a GenAI skeptic.

With that said, here are three of my thoughts about the future of Generative AI and LLMs in software delivery.

### LLMs are not the new compilers

Some common takes are: "LLMs will be the new compilers", "natural language will be the newest bump in the abstraction level, the new programming language", "remember, we used to know Assembly, and now we don't anymore, it will be the same with Java".

But I don't see it that way.

Abstraction means the "drawing away" of details, and it is indeed the key concept that has made programming more accessible and effective over time. The abstraction level is raised by removing a bunch of details from human responsibility, and delegating those details to a translator that can reliably and repeatedly add them, such as a compiler or a framework.

![](https://substackcdn.com/image/fetch/$s_!-ZnJ!,w_424,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fd9b9982e-e864-463b-8f63-ac370aeffbfa_1600x887.png)

The abstraction level was raised by delegating details to a deterministic “translator” level. Until now, that is!

The argument today is that natural language is the next level up, and LLMs are the translators that fill in the details left out of prompts. However, LLMs cannot reliably and repeatedly add those details because of their inherent non-determinism. And *if* it was somehow possible to put them in a straight jacket that made them fill in the same details again and again in a way that made their output repeatable, then why bother? Energy would be spent on taking away the thing that is powerful and special about LLMs.

Instead, a good approach is to embrace the fact that GenAI is a lateral move and an opportunity for something new, not a continuation of how abstraction and automation used to be done. There is now this new tool that allows us to specify things in an unstructured way, and use it on *any* abstraction level. It’s possible to create low code applications with it, and framework code – even Assembly. I find this lateral move much more exciting than thinking of natural language as "yet another abstraction level". LLMs open up a totally new way in from the “side of the stack” (as illustrated in the image below) which offers many new opportunities.

![](https://substackcdn.com/image/fetch/$s_!nVOe!,w_424,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F09c833f6-0716-438d-9802-53fa4595ba70_1600x970.png)

LLMs do raise the abstraction level, but in a new lateral way

As Martin Fowler told me:

> *"I think the appearance of LLMs will change software development to a similar degree as the change from Assembly to the first high-level programming languages. The further development of languages and frameworks increased our abstraction level and productivity, but didn't have that kind of impact on the nature of programming. LLMs are making that degree of impact, but with the distinction that it isn't just raising the level of abstraction, but also forcing us to consider what it means to program with non-deterministic tools."*

*Martin Fowler expands his thoughts on this topic further in the article [LLMs bring a new nature of abstraction](https://martinfowler.com/articles/2025-nature-abstraction.html).*

### It’s not all or nothing, it’s unevenly distributed

The question of whether GenAI will replace software engineers is too absolute for me; I don't think it leads to the right type of thinking about how to employ it. I try to ask myself what types of *tasks* Generative AI will enhance, change or replace, or how it will change how software engineers work. As Tim O'Reilly says, [AI is "the end of programming as we know it"](https://www.oreilly.com/radar/the-end-of-programming-as-we-know-it/), but not the end of programming.

Also, the future of AI coding is unevenly distributed. Some small, simple tasks can already be done autonomously by GenAI, others will in the near future, but some we will never be able to delegate to AI. From all that I have experienced so far, I don't think that LLMs will be the thing that helps us write all software autonomously.

### How much debt is being taken on while this is figured out?

I'll end with a gloomy scenario I think is quite likely, unfortunately. At this point, there’s a massive pile of software that societies increasingly depend upon, which has grown organically over decades. And let's be honest, it's not pretty. Technical debt dominates discussions at almost every software company that has been around for more than a year, often because they find themselves ever less responsive to change. And it's not just technical debt either, but also product debt. As a consumer, my perception is that many services have gotten worse, not better, over the past decade.

Generative AI increases speed, but amplifies indiscriminately when unchecked. Yes, there's still significant potential to improve usage, and mitigate the quality risks and challenges I outline above. But meanwhile, the foot is already hard on the accelerator. Over the next 5-10 years, the size of this software pile might well double. Even *if* I'm wrong, and a way is found for AI to replace programmers, will it replace only the programming of entirely new software, or will it also tackle the existing pile, with all its flaws and variations?

![](https://substackcdn.com/image/fetch/$s_!8lEm!,w_424,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F2eef2174-ab4a-46b6-85fe-967f609494c7_1079x1099.jpeg)

The future? Image by Forrest Brazeal

As the current transition phase accelerates, and the software profession figures out how to use GenAI sustainably, it’s important to have discourse about the present *and* the future. We should value skeptics and pragmatists as much as enthusiasts, and dismiss neither. And the key question will be who can use GenAI to reduce debt, rather than increase it.

## Takeaways

*Gergely, again.* Thanks, Birgitta for sharing what you’ve seen work, and for tackling the several open questions which exist about AI tools. You can read more from Birgitta on AI-assisted coding in her [series of articles on this topic](https://martinfowler.com/articles/exploring-gen-ai.html).

**How we write software is changing, and everyone is figuring out how.** LLMs are not a similar abstraction change as introducing compiled languages was, or like how opinionated frameworks offered ways to create programs faster with more constraints. GenAI is a new paradigm, of working with non-deterministic tools that are surprisingly good at some things like turning natural language into code that usually works, and bad at others such as how much generated code is harder to maintain.

The best way to find out what works for you and your team is to try these tools. Patterns are starting to emerge, which Birgitta has covered:

- Hard to measure *exactly* how much time and effort these tools save.
- Quality is dubious. Without engineers monitoring output, it tends to become sloppy
- Teams can easily get overwhelmed by AI, and often don’t become faster, since faster code generation doesn’t automatically mean shipping more high-quality features!

Understanding the tradeoffs of these tools is important for engineers, and the better we map these out, the more confidently we can decide when to use them, and when to set them aside.