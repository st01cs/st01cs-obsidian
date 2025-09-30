---
title: Open-source DeepResearch – Freeing our search agents
source: https://huggingface.co/blog/open-deep-research
author:
published: 2025-02-04
created: 2025-09-30
description: We’re on a journey to advance and democratize artificial intelligence through open source and open science.
tags:
  - clippings
  - deepresearch
---
[Back to Articles](https://huggingface.co/blog)

Published February 4, 2025

[Update on GitHub](https://github.com/huggingface/blog/blob/main/open-deep-research.md)

[Aymeric Roucher](https://huggingface.co/m-ric)

[m-ric](https://huggingface.co/m-ric)



Albert Villanova del Moral's avatar

[Albert Villanova del Moral](https://huggingface.co/albertvillanova)

[albertvillanova](https://huggingface.co/albertvillanova)



merve's avatar

[merve](https://huggingface.co/merve)

[merve](https://huggingface.co/merve)

[Thomas Wolf](https://huggingface.co/thomwolf)

[thomwolf](https://huggingface.co/thomwolf)

![Clémentine Fourrier's avatar](https://cdn-avatars.huggingface.co/v1/production/uploads/1644340617257-noauth.png)

Clémentine Fourrier's avatar

[Clémentine Fourrier](https://huggingface.co/clefourrier)

[clefourrier](https://huggingface.co/clefourrier)

## TLDR

Yesterday, OpenAI released [Deep Research](https://openai.com/index/introducing-deep-research/), a system that browses the web to summarize content and answer questions based on the summary. The system is impressive and blew our minds when we tried it for the first time.

One of the main results in the blog post is a strong improvement of performances on the [General AI Assistants benchmark (GAIA)](https://huggingface.co/gaia-benchmark), a benchmark we’ve been playing with recently as well, where they successfully reached near 67% correct answers on 1-shot on average, and 47.6% on especially challenging “level 3” questions that involve multiple steps of reasoning and tool usage (see below for a presentation of GAIA).

DeepResearch is composed of an LLM (which can be selected from the current list of LLMs provided by OpenAI, 4o, o1, o3, etc) and an internal “agentic framework” which guide the LLM to use tools like web search and organize its actions in steps.

While powerful LLMs are now freely available in open-source (see e.g. [the recent DeepSeek R1 model](https://huggingface.co/deepseek-ai/DeepSeek-R1)), OpenAI didn’t disclose much about the agentic framework underlying Deep Research…

So we decided to embark on a 24-hour mission to reproduce their results and open-source the needed framework along the way!

The clock is ticking, let’s go! ⏱️

## Table of Contents

- [Open-source DeepResearch – Freeing our search agents](https://huggingface.co/blog/#open-source-deepresearch--freeing-our-search-agents)
	- [TLDR](https://huggingface.co/blog/#tldr)
	- [Table of Contents](https://huggingface.co/blog/#table-of-contents)
	- [What are Agent frameworks and why they matter?](https://huggingface.co/blog/#what-are-agent-frameworks-and-why-they-matter)
	- [The GAIA benchmark](https://huggingface.co/blog/#the-gaia-benchmark)
	- [Building an open Deep Research](https://huggingface.co/blog/#building-an-open-deep-research)
		- [Using a CodeAgent](https://huggingface.co/blog/#using-a-codeagent)
		- [Making the right tools 🛠️](https://huggingface.co/blog/#making-the-right-tools-%EF%B8%8F)
	- [Results 🏅](https://huggingface.co/blog/#results-)
	- [Community Reproductions](https://huggingface.co/blog/#community-reproductions)
	- [Most important next steps](https://huggingface.co/blog/#most-important-next-steps)

## What are Agent frameworks and why they matter?

> An Agent framework is a layer on top of an LLM to make said LLM execute actions (like browse the web or read PDF documents), and organize its operations in a series of steps. For a quick intro to agents, check [this great interview by Andrew Ng](https://youtu.be/sal78ACtGTc?feature=shared&t=52) and our [introduction blog post](https://huggingface.co/blog/smolagents) to the smolagents library. For a more detailed dive in agents you can subscribe to our agents course that starts in just a few days: [link here](https://huggingface.us17.list-manage.com/subscribe?u=7f57e683fa28b51bfc493d048&id=9ed45a3ef6).

Almost everyone has already experienced how powerful LLMs can be simply by playing with chatbots.. However, what not everyone is aware of yet is that integrating these LLMs into agentic systems can give them real superpowers!

Here is a recent example comparing the performance of a few frontier LLMs with and without an agentic framework (in this case the simple [smolagents](https://github.com/huggingface/smolagents) library) - using an agentic framework bumps performance by up to 60 points!

[![Benchmarks](https://huggingface.co/datasets/huggingface/documentation-images/resolve/6c7ed2035810565043c92b472d5564c3f1fa4d7e/blog/open-deep-research/benchmarks.png)](https://huggingface.co/datasets/huggingface/documentation-images/resolve/6c7ed2035810565043c92b472d5564c3f1fa4d7e/blog/open-deep-research/benchmarks.png)

In fact, OpenAI also highlighted in [its release blogpost](https://openai.com/index/introducing-deep-research/) how Deep Research performed dramatically better than standalone LLMs on the knowledge-intensive " [Humanity’s Last Exam](https://huggingface.co/datasets/cais/hle) " benchmark.

So, what happens when we integrate our current top LLM in an agentic framework, to work toward an `open-DeepResearch`?

**A quick note:** We’ll benchmark our results on the same GAIA challenge but keep in mind that this is a work in progress. DeepResearch is a massive achievement and its open reproduction will take time. In particular, full parity will require improved browser use and interaction like OpenAI Operator is providing, i.e. beyond the current text-only web interaction we explore in this first step.

Let’s first understand the scope of the challenge: GAIA.

## The GAIA benchmark

[GAIA](https://huggingface.co/datasets/gaia-benchmark/GAIA) is arguably the most comprehensive benchmark for agents. Its questions are very difficult and hit on many challenges of LLM-based systems. Here is an example of a hard question:

> Which of the fruits shown in the 2008 painting "Embroidery from Uzbekistan" were served as part of the October 1949 breakfast menu for the ocean liner that was later used as a floating prop for the film "The Last Voyage"? Give the items as a comma-separated list, ordering them in clockwise order based on their arrangement in the painting starting from the 12 o'clock position. Use the plural form of each fruit.

You can see this question involves several challenges:

- Answering in a constrained format,
- Using multimodal capabilities (to extract the fruits from the image),
- Gathering several pieces of information, some depending on others:
	- Identifying the fruits on the picture
	- Finding which ocean liner was used as a floating prop for “The Last Voyage”
	- Finding the October 1949 breakfast menu for the above ocean liner
- Chaining together a problem-solving trajectory in the correct order.

Solving this requires both high-level planning abilities and rigorous execution, which are two areas where LLMs struggle when used alone.

So it’s an excellent test set for agent systems!

On GAIA’s [public leaderboard](https://huggingface.co/spaces/gaia-benchmark/leaderboard), GPT-4 does not even reach 7% on the validation set when used without any agentic setup. On the other side of the spectrum, with Deep Research, OpenAI reached 67.36% score on the validation set, so an order of magnitude better! (Though we don’t know how they would actually fare on the private test set.)

Let’s see if we can do better with open source tools!

## Building an open Deep Research

### Using a CodeAgent

The first improvement over traditional AI agent systems we’ll tackle is to use a so-called “code agent”. As shown by [Wang et al. (2024)](https://huggingface.co/papers/2402.01030), letting the agent express its actions in code has several advantages, but most notably that **code is specifically designed to express complex sequences of actions**.

Consider this example given by Wang et al.:

[![Code Agent](https://huggingface.co/datasets/huggingface/documentation-images/resolve/6c7ed2035810565043c92b472d5564c3f1fa4d7e/blog/open-deep-research/code_agent.png)](https://huggingface.co/datasets/huggingface/documentation-images/resolve/6c7ed2035810565043c92b472d5564c3f1fa4d7e/blog/open-deep-research/code_agent.png)

This highlights several advantages of using code:

- Code actions are **much more concise** than JSON.
	- Need to run 4 parallel streams of 5 consecutive actions? In JSON, you would need to generate 20 JSON blobs, each in their separate step; in Code it’s only 1 step.
	- On average, the paper shows that Code actions require 30% fewer steps than JSON, which amounts to an equivalent reduction in the tokens generated. Since LLM calls are often the dimensioning cost of agent systems, it means your agent system runs are ~30% cheaper.
- Code enables to re-use tools from common libraries
- Better performance in benchmarks, due to two reasons:
	- More intuitive way to express actions
	- Extensive exposure of LLMs to code in training

The advantages above were confirmed by our experiments on the [agent\_reasoning\_benchmark](https://github.com/aymeric-roucher/agent_reasoning_benchmark).

From building `smolagents` we can also cite a notable additional advantage, which is a better handling of state: this is very useful for multimodal tasks in particular. Need to store this image/audio/other for later use? No problem, just assign it as a variable in your state and you can re-use it 4 steps later if needed. In JSON you would have to let the LLM name it in a dictionary key and trust the LLM will later understand that it can still use it.

### Making the right tools 🛠️

Now we need to provide the agent with the right set of tools.

**1.** A web browser. While a fully fledged web browser interaction like [Operator](https://openai.com/index/introducing-operator/) will be needed to reach full performance, we started with an extremely simple text-based web browser for now for our first proof-of-concept. You can find the code [here](https://github.com/huggingface/smolagents/tree/main/examples/open_deep_research/scripts/text_web_browser.py)

**2.** A simple text inspector, to be able to **read a bunch of text file format**, find it [here](https://github.com/huggingface/smolagents/tree/main/examples/open_deep_research/scripts/text_inspector_tool.py).

These tools were taken from the excellent [Magentic-One](https://www.microsoft.com/en-us/research/articles/magentic-one-a-generalist-multi-agent-system-for-solving-complex-tasks/) agent by Microsoft Research, kudos to them! We didn’t change them much, as our goal was to get as high a performance as we can with the lowest complexity possible.

Here is a short roadmap of improvements which we feel would really improve these tools’ performance (feel free to open a PR and contribute!):

- extending the number of file formats which can be read.
- proposing a more fine-grained handling of files.
- replacing the web browser with a vision-based one, which we’ve started doing [here](https://github.com/huggingface/smolagents/tree/main/src/smolagents/vision_web_browser.py).

## Results 🏅

In our 24h+ reproduction sprint, we’ve already seen steady improvements in the performance of our agent on GAIA!

We’ve quickly gone up from the previous SoTA with an open framework, around 46% for Magentic-One, to our [current performance of 55.15% on the validation set](https://huggingface.co/spaces/gaia-benchmark/leaderboard).

This bump in performance is due mostly to letting our agents write their actions in code! Indeed, when switching to a standard agent that writes actions in JSON instead of code, performance of the same setup is instantly degraded to 33% average on the validation set.

[Here is the final agentic system.](https://github.com/huggingface/smolagents/tree/main/examples/open_deep_research)

We’ve set up [a live demo here](https://m-ric-open-deep-research.hf.space/) for you to try it out!

However, this is only the beginning, and there are a lot of things to improve! Our open tools can be made better, the smolagents framework can also be tuned, and we’d love to explore the performance of better open models to support the agent.

We welcome the community to come join us in this endeavour, so we can leverage the power of open research together to build a great open-source agentic framework! It would allow anyone to run a DeepResearch-like agent at home, with their favorite models, using a completely local and customized approach!

## Community Reproductions

While we were working on this and focusing on GAIA, other great open implementations of Deep Research emerged from the community, specifically from

- [dzhng](https://x.com/dzhng/status/1886603396578484630),
- [assafelovic](https://github.com/assafelovic/gpt-researcher),
- [nickscamara](https://github.com/nickscamara/open-deep-research),
- [jina-ai](https://github.com/jina-ai/node-DeepResearch) and
- [mshumer](https://x.com/mattshumer_/status/1886558939434664404).

Each of these implementations use different libraries for indexing data, browsing the web and querying LLMs. In this project, we would like to **reproduce the benchmarks presented by OpenAI (pass@1 average score), benchmark and document our findings with switching to open LLMs (like DeepSeek R1), using vision LMs, benchmark traditional tool calling against code-native agents.**

## Most important next steps

OpenAI’s Deep Research is probably boosted by the excellent web browser that they introduced with [Operator](https://openai.com/index/introducing-operator/).

So we’re tackling that next! In a more general problem: we’re going to build GUI agents, i.e. “agents that view your screen and can act directly with mouse & keyboard”. If you’re excited about this project, and want to help everyone get access to such cool capabilities through open source, we’d love to get your contribution!

We’re also [hiring a full time engineer](https://apply.workable.com/huggingface/j/AF1D4E3FEB/) to help us work on this and more, apply if you’re interested 🙂

- To get started with Open Deep Research, try the examples [here](https://github.com/huggingface/smolagents/tree/main/examples/open_deep_research).
- Check the [smolagents](https://github.com/huggingface/smolagents) repo.
- Read more about smolagents [docs](https://huggingface.co/docs/smolagents/index), [introduction blog post](https://huggingface.co/blog/smolagents).

More Articles from our Blog

[![](https://huggingface.co/blog/assets/beating-gaia/thumbnail.jpeg)](https://huggingface.co/blog/beating-gaia)

## [Our Transformers Code Agent beats the GAIA benchmark!](https://huggingface.co/blog/beating-gaia)

[By [m-ric](https://huggingface.co/m-ric) July 1, 2024 • 98](https://huggingface.co/blog/beating-gaia)

[![](https://huggingface.co/blog/assets/jupyter-agent-2/thumbnail.png)](https://huggingface.co/blog/jupyter-agent-2)

## [Jupyter Agents: training LLMs to reason with notebooks](https://huggingface.co/blog/jupyter-agent-2)

[

By [baptistecolle](https://huggingface.co/baptistecolle) September 10, 2025 • 45

](https://huggingface.co/blog/jupyter-agent-2)

### Community

[sfield](https://huggingface.co/sfield)

DeepSeek's reasoning skills are probably particularly useful for something like this. But in my mind, particularly for academic research type tasks, the propaganda baked into the model is a non-starter. I tested out the new  
DeepSeek-R1-Distill-Llama-70B-Uncensored-v2-Unbiased model yesterday. It was a very crude test, but I was quite impressed. I'm a newb over here, so take this as a light suggestion, just in case its helpful, nothing more.

·

[TGAI87](https://huggingface.co/TGAI87)

Yep I'm very impressed with it too. Follows direction exceptionally well, and corrects (intentional) mistakes. Going to try to get it working nicely on my RTX 4090 with offloading.

[ElanInPhilly](https://huggingface.co/ElanInPhilly)

This sounds pretty interesting, so I up voted based on description. However, the demo implementation definitely needs attention and work. Now, on several occasions, after long waits in 100+ user queues, I repeatedly get "Error in generating model output:  
litellm.ContextWindowExceededError: litellm.BadRequestError: ContextWindowExceededError: OpenAIException - Error code: 400 - {'error': {'message': "This model's maximum context length is 128000 tokens. However, your messages resulted in 419624 tokens. Please reduce the length of the messages.", 'type': 'invalid\_request\_error', 'param': 'messages', 'code': 'context\_length\_exceeded'}}". So this seems pretty basic, \*. \* the demo definitely to be crafted so the model can handle the correct token limits at the right time and place. Absent that....

[jonwondo](https://huggingface.co/jonwondo)

I'm getting the same errors as the person above on the demo site. Must be a bug as I tried different prompts and had to wait ~1hr for each one due to the queue:  
Error in generating model output:  
litellm.ContextWindowExceededError: litellm.BadRequestError: ContextWindowExceededError: OpenAIException - Error code: 400 - {'error': {'message': "This model's maximum context length is 128000 tokens. However, your messages resulted in 709582 tokens. Please reduce the length of the messages.", 'type': 'invalid\_request\_error', 'param': 'messages', 'code': 'context\_length\_exceeded'}}

[raidhon](https://huggingface.co/raidhon)

Very cool thanks! I think OpenAI already hate Open Source:)))))  
Products that are trying so hard to monetize are created in one day.

[shtefcs](https://huggingface.co/shtefcs)

•

[edited Feb 5](https://huggingface.co/blog/#67a3773e52adaa72db8a9736 "Edited 3 times by shtefcs")

This is a big step toward more capable AI agents. At [Automatio.ai](https://automatio.ai/), we're working on integrating similar autonomous web agents to streamline data extraction and web automation, letting users build powerful scrapers without coding. The challenge is making sure these agents can navigate complex websites reliably. How do you see open-source AI helping bridge the gap between research prototypes and real-world automation?

[MS100](https://huggingface.co/MS100)

Amazing. I am so interested in participating.

[Kumala3](https://huggingface.co/Kumala3)

I am currently exploring Open-Source alternatives to OpenAI DeepResearch as it's a really great product, one of the most useful since ChatGPT was launched in 2022 for me, as the results of research are incredible high-quality not just simple research with "search" function.  
I've decided to try out this Open Deep Research via Hugging face space and ran into issue with the returned output exceeded 128K token limit:  
[![image.png](https://cdn-uploads.huggingface.co/production/uploads/66bdf5cee61ccd71d7a8e345/pZVkSW0z3vT0lRVgfPU67.png)](https://cdn-uploads.huggingface.co/production/uploads/66bdf5cee61ccd71d7a8e345/pZVkSW0z3vT0lRVgfPU67.png)

[Kumala3](https://huggingface.co/Kumala3)

[@ albertvillanova](https://huggingface.co/albertvillanova) [@ clefourrier](https://huggingface.co/clefourrier) Is there any way to resolve this issue or maybe set the instruction to set the output token limit to ensure it doesn't throw errors and works appropriately even with certain limitations?  
PS. Working with limits is MUCH better than not working at all.

[mrsmirf](https://huggingface.co/mrsmirf)

Can we get a readme with instructions

[derekalia](https://huggingface.co/derekalia)

I tried running this locally but got a couple of errors with the run.py command after installing the requirements. Maybe you guys should add a readme to get this setup. [https://github.com/huggingface/smolagents/blob/gaia-submission-r1/examples/open\_deep\_research/run.py](https://github.com/huggingface/smolagents/blob/gaia-submission-r1/examples/open_deep_research/run.py)

[mrsmirf](https://huggingface.co/mrsmirf)

Yeah I got errors too. Not sure if I need to install the entire repo, what to install, etc. But, I tried and have not gotten it to run.

[Dikeshwar](https://huggingface.co/Dikeshwar)

how to see future

[TGAI87](https://huggingface.co/TGAI87)

Cursor is able to set this up nicely (and expand on it); just ensure you add the smolagents docs and direct it to the specific open deep research docs within the git repo under src.

·

[Agenciarc360](https://huggingface.co/Agenciarc360)

fale mais meu amigo....

[RocketNinja](https://huggingface.co/RocketNinja)

Hey guys! The demo is down:/

[Scrign29](https://huggingface.co/Scrign29)

impossible d’accéder à la démo.

[griged](https://huggingface.co/griged)

•

[edited Feb 8](https://huggingface.co/blog/#67a643f0f76404e1c1427422 "Edited by griged")

I attempted a side by side comparison between your tool and the for pay Gemini Advanced 1.5 Pro with Deep Research for a particularly interesting and challenging task, but it is difficult to benchmark the results. Gemini did an overall poor - average job, but only after many manual additional prompts.

Initial prompt:  
"what are the highest judgements received by tenants for claims relating to either negligent or intentional infliction of emotional distress in the last 10 years, against landlords in Massachusetts?"  
result - it couldn't find anything  
I further revised the workflow with prompts such as  
"Please note it may also be in landlord lawsuits against tenants, where tenants win in counter claim"

"There may be some useful results there, but. regenerate following my two stated criteria of "in the last 10 years" and "In Massachusetts" and afterwards try to assess why your process missed this obvious mistake in its final output, and share with me your self analysis"

"please consider a few ways that your filtering can be expanded while still satisfying my criteria. 1. There are various statutory frameworks within which "negligent infliction of emotional distress" or "intentional infliction of emotional distress" can be brought. It could be in the context of Chapter 93A consumer protection, it could be in the context of M.G.L. c. 186, §14, in particular when in counter claim in an eviction matter. 2. Those landmark older cases can be very helpful if you search cases that cite them, in particular simon vs. solomon and Haddad v. Gonzalez. 3. It is more diffiult to find regular cases than binding case law, a few suggestions, certain trial courts like the Western Division of the Massachusetts Housing court publishes it's 'court reporter' which is basically a data dump of almost all of their case rulings. 3. You were wise to scrape masscases.com as it has unpublished as well as published decisions which are of interest to me, and they use a scrape friendly URL scheme. judyrecords.com, trellis.law, docketalarm all chose to allow being crawled by google for purposes of appearing in google search results. The information I seek can almost always be inferred purely from the information made available to google, for example {massachusetts emotional distress tenant site:trellis.law} without the {} braces returns many cases. Please try again"

"Rader v Odermatt is an excellent example of a case matching my criteria. The tenant prevailed in counter claim, and was even awarded duplicative damages, normally discouraged and rare. Try to assess how you missed this case, output a revised list but also output your self analysis in your work flow"

I have omitted the self-analysis provided by Google, it was generally correct but as it recognized on its own, it failed to apply weights properly to my revisions. The other major hurdle of course is that for quazi-legal, sometimes technical, and due to outright politcal bias, most lower court, which in a way means "real cases", are very hard to find and even harder to scrape. I tried prompting with scraping strategies but in the end hardly any meaningful results were found. I had a certain results ready to assess its effectiveness. Unfortunetly your tool gave me the same error as stated by others upon just the first prompt

[pulkitmehtawork](https://huggingface.co/pulkitmehtawork)

I was able to run run.py locally.. please check solution at [https://github.com/huggingface/smolagents/issues/501](https://github.com/huggingface/smolagents/issues/501).. i have mentioned steps there.

[onedayatime](https://huggingface.co/onedayatime)

I read everything from A-Z. Thanks for this

[serkan90](https://huggingface.co/serkan90)

buffer

[inbuss](https://huggingface.co/inbuss)

I'd love to read a good README.md of this open\_deep\_research folder, how to use and tweak that example:)

[CodePhyt](https://huggingface.co/CodePhyt)

amazing

[ngxson](https://huggingface.co/ngxson)

📻 🎙️ Hey, I made a podcast about this blog post, check it out!

<audio src="https://huggingface.co/ngxson/hf-blog-podcast/resolve/main/open-deep-research.mp3" controls=""></audio>

*This podcast is generated via [ngxson/kokoro-podcast-generator](https://huggingface.co/spaces/ngxson/kokoro-podcast-generator), using DeepSeek-R1 and Kokoro-TTS*

·

[shtefcs](https://huggingface.co/shtefcs)

This is cool.

[Tamar](https://huggingface.co/Tamar)

Hey Great blog post! I noticed you published the models tested for the Gaia/Math benchmarking—thanks for sharing that.

I was wondering if you could let me know which server you used to run the models? I’m currently using vLLM, but it seems like it doesn’t yet support tool\_choice="required". To make it work, I had to tweak the model code to force it to return a tool for execution.

Thanks in advance for any insights!

[prabhu130986](https://huggingface.co/prabhu130986)

i've tried to run the agent in my local setup and i would say, its pretty impressive. i tried the same questions from Openai's deep research page ([https://openai.com/index/introducing-deep-research/](https://openai.com/index/introducing-deep-research/)), just to compare the workflow and output.

The plan of action it created was neat and executed all the workflow steps one by one, though there were some errors in between, but that didnt break the progress. Finally it gave the final recommendation based on all the gathered data.

Attached is the result of using gpt-4o model. using o1 model will definitely give a better inference.  
[![plan.jpg](https://cdn-uploads.huggingface.co/production/uploads/660c3c5c8eec126bfc7aa326/MvwT9enRT7gOESHA_tpRj.jpeg)](https://cdn-uploads.huggingface.co/production/uploads/660c3c5c8eec126bfc7aa326/MvwT9enRT7gOESHA_tpRj.jpeg)  
[![final-answer.jpg](https://cdn-uploads.huggingface.co/production/uploads/660c3c5c8eec126bfc7aa326/JNs_DrpFbr6ok_pSRUK4j.jpeg)](https://cdn-uploads.huggingface.co/production/uploads/660c3c5c8eec126bfc7aa326/JNs_DrpFbr6ok_pSRUK4j.jpeg)

[vinayp27](https://huggingface.co/vinayp27)

Can we add something that searches arxiv and pubmed articles and then presents the research. I think it would be a great start

·

[shtefcs](https://huggingface.co/shtefcs)

Like a scraper that will gather data from resesrch articles and feed into DeepSeek?

[Moza05](https://huggingface.co/Moza05)

This comment has been hidden

[milyiyo](https://huggingface.co/milyiyo)

The demo is not working:(

[https://m-ric-open-deep-research.hf.space/](https://m-ric-open-deep-research.hf.space/)

[CodePhyt](https://huggingface.co/CodePhyt)

•

[edited Mar 20](https://huggingface.co/blog/#67dc0b30c6c20c5dc796f616 "Edited by CodePhyt")

i will find a way to make every tech out there opensource and bring opensource humaniy into this world

[OMAP3530](https://huggingface.co/OMAP3530)

[@ m-ric](https://huggingface.co/m-ric) Hi, I am trying to leverage the `VisitTool` that is based on `SimpleTextBrowser` to fetch page content from URL. But I find it may returns `error 403 Enable JavaScript and cookies to continue` for some URLs like [https://www.businessresearchinsights.com/market-reports/software-resellers-market-117159](https://www.businessresearchinsights.com/market-reports/software-resellers-market-117159). So I am wondering how does Open DR handle such issues when generating final report or doing the analysis. just skip it or any other to fetch content snippet from the page via `GoogleSearchTool`?