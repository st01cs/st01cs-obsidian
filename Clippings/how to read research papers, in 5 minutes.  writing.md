---
title: "how to read research papers, in 5 minutes. | writing"
source: "https://masonjwang.com/writing/reading-research"
author:
published: 2025-09-13
created: 2025-10-20
description: "My top learnings aggregated into a short guide."
tags:
  - "clippings"
---
[m.w.](https://masonjwang.com/)

/

[Back to writing](https://masonjwang.com/writing)

![how to read research papers, in 5 minutes.](https://masonjwang.com/_next/image?url=%2Fassets%2Fimg%2Fpoly%2Fwriting%2Flumon.png&w=256&q=75)

## how to read research papers, in 5 minutes.

· 5 min read

From what I can tell, most people aren’t taught how to read research papers. Inside academia it’s treated as an assumed skill you’ll pick up on your own, and outside there’s this false barrier of being too technical or tedious to bother with.

I spent roughly three years treating paper-reading as a chore. Now it’s something I quite enjoy .

Looking back, here are the three most useful principles:

## 1\. Intuition → empirics → details. In that order.

What’s the most efficient way to digest a paper? Nothing has worked better for me than the framework of: (1) grasp the big picture, (2) check the evidence, and (3) dive into details only if it’s worth the time.

1. **INTUITION.** Can you summarize the paper in your own words in three sentences? If nothing else, you’ll want a rough sense of *what the paper is doing and why*.
2. **EMPIRICS.** (Empirics = the evidence and data). How well does the method work, *really*?
	Because almost all papers are trying to advertise themselves, getting to the truth isn’t easy.
	1. A great place to start is the charts. **How cleanly a paper tells its story through figures is a strong proxy for quality.** (If you can, think of the few foundational, long-lived ML papers; clarity like that is rarely found in incremental “+1% on another benchmark” work.)

![GPT-3 scaling law](https://masonjwang.com/_next/image?url=%2Fassets%2Fimg%2Fwriting%2Freading-research%2Fgpt3.jpg&w=640&q=75)

GPT-3 scaling law

*[GPT-3](https://arxiv.org/abs/2005.14165) scaling law. As models get bigger and use more compute, their loss ("error") steadily goes down. A clear, convincing pattern: more compute = better performance.*

![Grokking phenomenon](https://masonjwang.com/_next/image?url=%2Fassets%2Fimg%2Fwriting%2Freading-research%2Fgrokking.jpg&w=640&q=75)

Grokking phenomenon

*[Grokking](https://arxiv.org/abs/2201.02177). At first the model just memorizes the training examples (red line jumps up fast). Only much later does it figure out the underlying pattern and start getting new examples right (green line).*

![Chain-of-thought prompting](https://masonjwang.com/_next/image?url=%2Fassets%2Fimg%2Fwriting%2Freading-research%2Fcot.jpg&w=640&q=75)

Chain-of-thought prompting

*[Chain-of-thought prompting](https://arxiv.org/abs/2201.11903). Beyond result graphs, strong papers often have helpful explanatory visuals. This figure shows how adding step-by-step reasoning to the model's answers makes a huge difference.*

1. **DETAILS: Only if you decide it’s worth the time.** People differ most when it comes to this:
	- Coming from an engineering background, writing some code to follow along the paper made theory tangible, and in turn, much easier to understand. For example: [my Hopfield networks code](https://github.com/masonwang025/learning-associative-mem/blob/main/associative-mem/hopfield.ipynb).
	- A math PhD I worked with preferred diving straight into the definitions and methods, since “everything else was built on that.” This was always too slow for me.
	- In some cases going through the derivations yourself and confirming them can be incredibly useful not just for learning but also because they are not always right !

At any step, you can stop. Often you’ll get the intuition behind 20 papers and only decide to invest further into the 2 most promising ones, which is the point!

Taking a step back, why does speed matter? Because you’ll want to:

Read a lot and fast , while trying to optimize for these three dimensions:

1. **WHAT: Developing research taste.** ML research papers are especially vulnerable to [Sturgeon’s Law](https://en.wikipedia.org/wiki/Sturgeon%27s_law) (90% of everything is crap). If you take too long on each one, you’ll never see enough to build a sense for quality. There were many days I spent hours on a single paper, but the problem is that no paper exists in a vacuum, and each idea’s significance usually comes from how it fits into the larger web of ideas around it (the other approaches, the benchmarks, the inspiration).![image.png](https://masonjwang.com/_next/image?url=%2Fassets%2Fimg%2Fwriting%2Freading-research%2Fsturgeons.jpg&w=3840&q=75)
2. **HOW: Figure out your process for understanding.** I tried physical notepad, Jupyter notebooks, and ended up using a Notion database. Here’s my process:
	1. Paste the whole paper into a saved prompt that gives me three paragraphs: intuition, empirics, details. I find it’s a useful bird’s-eye view for layering questions on after.
	2. Once finished, add an entry to my Notion database (now [my bookshelf](https://masonjwang.com/bookshelf?f=medium:contains:research+paper&s=enjoyment:desc&s=importance:desc)):
		- 3 sentence "TLDR”
		- 2 sentence “Two Cents” (subjective comment)
		- Enjoyment and importance ratings (ranking papers is difficult but good practice)
		![Screenshot 2025-09-10 at 6.41.10 PM.png](https://masonjwang.com/_next/image?url=%2Fassets%2Fimg%2Fwriting%2Freading-research%2Fnotion.jpg&w=640&q=75)
		Screenshot 2025-09-10 at 6.41.10 PM.png
3. **WHERE: Know where to find papers****.** Some people curate their Twitter feeds, others use Deep Research surveys, others follow citations down rabbit holes. You should try to define your purpose for reading at all. Sometimes I wanted a survey of what’s been tried, other times I wanted to see old problems in entirely new framings ; this clarity helps you choose.

This is all to say: just try shit. The worst thing you can do is copy someone else’s recipe (so don’t take my advice beyond using it as a starting point!). I think this is also *why* people aren’t taught how to read papers, or why the advice is conflicting (do you read the abstract first or last? I’ve been told to do both).

## 3\. Use AI tools, but make thinking hard.

On one hand, there’s no better time to learn new things: ChatGPT and other AI tools can explain just about anything. On the other hand, I am very, very grateful I learned to code *before* those tools existed. When friction is stripped away, real learning gets harder. (Ironically, I’ve seen friends take so much longer to pick up programming with AI than they would have without it.)

> What happens when that \[tacit knowledge — things we know but cannot explain\] gets replaced by a second kind: *things we claim to know but never really did?* It looks the same on the outside — in both cases we sound confident, in both cases we feel informed — but only one of them survives challenge.
> 
> \- Joan Westenberg, [*Cognitive Hygiene: Why You Need to Make Thinking Hard Again*](https://www.youtube.com/watch?v=rHPOyS6mjwI)

As such, I use AI to help me understand (I even craft and save prompts to paste), but when it comes to writing the 3 sentence summary or brief personal comments, I never allow AI. It’s surprisingly difficult, and that’s the point. You can find other ways to build back friction into your learning.

Lastly, hone the skill of asking questions. AI can give you answers, but the burden of asking the right questions is still on you. I remind myself that I am always in one of two buckets:

- I understand this topic well enough to comment on it / judge it / use it, or
- I don’t.

The only thing separating the latter from the former is a series of questions. In particular, know that many papers can be really hard to grasp if you don’t understand the “prerequisite ideas” .

So if you’re confused, you should search for the precise next question you need answered, and fill the gaps one by one. Be unapologetically curious.

**Thank you** to [Dhruv Pai](https://x.com/dhruv31415) for teaching me most of the above , and to Dhruv, [Matthew Noto](https://x.com/matthewnoto73), [Tina Mai](https://tinabmai.com/), [Nathan Chen](https://nathanchen.me/), Krish Parikh, William Zhao, and [Vedant Khanna](https://www.vedant.space/) for their feedback across drafts.

In interest of keeping the post short, I moved many notes and examples here. I think they're worth reading through!

[Back to writing](https://masonjwang.com/writing)