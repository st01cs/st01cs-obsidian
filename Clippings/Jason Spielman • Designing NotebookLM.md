---
title: "Jason Spielman • Designing NotebookLM"
source: "https://jasonspielman.com/notebooklm"
author:
published:
created: 2025-10-01
description: "Designer, builder, and visual storyteller. Now building Huxe. Previously led design on NotebookLM and contributed to Google AI projects like Gemini and Search. Also shoot photo/video for brands like Coachella, GoPro, and Rivian."
tags:
  - "clippings"
---
Home

[

Next

](https://jasonspielman.com/gemini)

Design Lead

UX + Identity

2024

## NotebookLM

I led design for NotebookLM, shaping the product’s core user experience, brand identity, and visual system from experiment to launch.

This remains one of my proudest projects, and I’m incredibly grateful for the opportunity to design something entirely new from the ground up. It was a chance to explore fresh paradigms, invent new patterns, and bring a product to life that hadn’t existed before. None of it would’ve been possible without the tight-knit, cross-functional team I was fortunate to collaborate with.


Podcast • Seqouia Training Data

Raiza and I discuss the journey building NotebookLM.

![](https://jasonspielman.com/_assets/v11/7d7b4ac2fa329465dccb8f8d7bded50df32e911d.png)

NotebookLM • Winner!

Recognized as one of TIME’s Best Inventions of 2024.

|

Architecture

|

3 Panel

|

Brand Identity

|

Visual Assets

|

Takeaways

Architecture

![](https://jasonspielman.com/_assets/v11/e7fc1fc695b1d67fd8f6690482d11239c9608628.png)

Design Evolution

![](https://jasonspielman.com/_assets/v11/b319c31e96dd9ecb9090c45f089292baf5680c44.png)

Early Prototype

This is what the UI looked like when I first joined the early project.

![](https://jasonspielman.com/_assets/v11/be1835cd54b62fa455f03f647a4b96d238ddd00c.png)

Notes driven UI

Exploratory chat UI introduced as an overlay on the note canvas.

![](https://jasonspielman.com/_assets/v11/c714c561bba823793a69be95e70d79e2fde08ab6.png)

3-Panel Structure

Synthesizes learnings into a scalable and adaptive layout.

## Problem + Requirements

One of the core problems we set out to solve with NotebookLM was “tab overwhelm” the scattered, fractured experience of jumping between tools while trying to synthesize ideas. We wanted to create a space where every part of the creation journey could happen in one place.

→ Inputs

- Source list, Open Source (wide)

Outputs →

- Notes list, Open Note (wide)

Chat

• Citations

Creation

• Multiple entry points

This visual shows how the core building blocks came together.

![](https://jasonspielman.com/_assets/v11/31fc511ae32e54f29fbb56667a0e1b1d2558b835.png) ![](https://jasonspielman.com/_assets/v11/d8209b7fae3b4708fcfeea9fd198a8a67e462ec0.png) ![](https://jasonspielman.com/_assets/v11/2e43530ee2a861f2b2c2b697d604c39ebf9646f5.png)

## Early Sketches

The structure you see now may look obvious but it took what felt like a thousand iterations to get there. I was trying to arrange these blocks in a way that supported a clear mental model and a UI that felt intuitive and digestible.

These sketches were done on a plane. I ran out of paper and ended up sketching the final solution across a few napkins.

## Mental Model

The mental model of NotebookLM was built around the creation journey: starting with inputs, moving through conversation, and ending with outputs. Users bring in their sources (documents, notes, references), then interact with them through chat by asking questions, clarifying, and synthesizing before transforming those insights into structured outputs like notes, study guides, and Audio Overviews.

By grounding the design in this linear but flexible flow (Inputs → Chat → Outputs) we gave users a clear sense of place within the product while keeping the complexity of new AI interactions digestible and intuitive.

![](https://jasonspielman.com/_assets/v11/e5191da518df72c5874ef2600ff2705b0ae21403.png)

## Solution • 3 Panel Structure

It’s rare to find a product that brings reading, writing, and creation together in a truly integrated way largely because juggling all three can be overwhelming. But with AI reducing friction, the opportunity emerged to design a space where every part of the creative process could coexist.

To make that possible, I designed a responsive panel system that adapts to the user’s needs, scaling fluidly while preserving quick access to key elements like sources and notes, even at the smallest sizes.

![](https://jasonspielman.com/_assets/v11/31fc511ae32e54f29fbb56667a0e1b1d2558b835.png) ![](https://jasonspielman.com/_assets/v11/bae8c27809204a5c02635ccd1388e65af3921b1b.png) ![](https://jasonspielman.com/_assets/v11/3972590b20186fc31ac682edc760bbf09e9fd568.png)

Standard

The default layout, offering a balanced view of sources, chat, and notes.

![](https://jasonspielman.com/_assets/v11/b1906403314a12e7039e7f2b6da290d72129ffa9.png)

Reading + Writing

Ideal for composing while keeping source material in view.

## Panel States

To optimize spatial utility, I created a set of responsive panels that scale based on user needs, retaining essential icons for sources and notes even at minimal widths.

Scalability was a core principle. While the content within these panels can shift and evolve, the underlying system is built to support growth, accommodating new tools, modes, and workflows without breaking the structure.

![](https://jasonspielman.com/_assets/v11/f729e7ef4c94e5fb9400c22ca906ccd673d1fc52.png)

Source Panel

## This is where all user-provided sources or “inputs” live. It’s the starting point of the user’s journey.

![](https://jasonspielman.com/_assets/v11/f7a5b9910c519ea7e454954c75b4745d4c22dd47.png) ![](https://jasonspielman.com/_assets/v11/e463d8886dffd220df8227de008a8a1f3a197dce.png) ![](https://jasonspielman.com/_assets/v11/18f126daf66d9851faf6dfa4b37303f4220d5302.png)

Studio Panel

## Where inputs turn into outputs. This is the space for creating, shaping, and capturing work

![](https://jasonspielman.com/_assets/v11/5dcd5886f31b03e081ff6a25c85254f150e1783f.png) ![](https://jasonspielman.com/_assets/v11/0069dc14717465640b441e7557436c8c7bd23121.png) ![](https://jasonspielman.com/_assets/v11/8d39b5a6bbfffc04713ad929926a822789dbcf15.png)[New! NotebookLM Announces flashcards, quizzes, professional reports](https://blog.google/technology/google-labs/notebooklm-student-features/)

See how the team has continued to scale this system with the newest launch of flashcards, quizzes, professional reports.

![](https://jasonspielman.com/_assets/v11/42ad768a95d183a5a1b4c64847936c9f80617f3b.png)

Chat Panel

## The chat panel stays

## at the core of the experience, dynamically adjusting its size to accommodate other tools as needed.

![](https://jasonspielman.com/_assets/v11/149c4c710e3df61aec4294bb945f479313d695a9.png) ![](https://jasonspielman.com/_assets/v11/38dd2fdc62ab355ae50652978feb3dd75b1f57b5.png)

Here’s what that looks like:

## Panels dynamically adjust based on the user’s focus and current task.

![](https://jasonspielman.com/_assets/v11/44fc5ae5582e14e21d94665859dc19b7d1a5d923.png)

## User Journey • Annotated Overview

![](https://jasonspielman.com/_assets/v11/7ffdcea1cf1f158ac87a5424956d5b348f998556.png)

## Audio Overviews

## I led design on Audio Overviews, shaping the experience from prototype to launch and introducing new paradigms such as “interrupt.” I worked closely with the team to craft the end-to-end experience — and fun fact: I unintentionally coined the name Audio Overview.

## Shout out to a few of the amazing x-fn team: Stephen Hughes, Oliver King, Biao (Frank) Wang, Corbin Cunningham, PhD, Yi Yao, Usama Bin Shafqat, Simon Tokumine, Michael Chen (+ more)

[

Read the full story

](https://www.linkedin.com/posts/jason-spielman-creative_we-built-and-launched-a-viral-ai-product-activity-7247661593268756480-AZUf?utm_source=li_share&utm_content=feedcontent&utm_medium=g_dt_web&utm_campaign=copy)

![](https://jasonspielman.com/_assets/v11/31fc511ae32e54f29fbb56667a0e1b1d2558b835.png) ![](https://jasonspielman.com/_assets/v11/db9e3d9b3a5aa3acc7e78cc3ce2e401846b85487.png)

## Brand Identity

Defining the brand identity was a fast-paced effort, made possible by close collaboration with Google Labs and the central brand team. Shoutout [Feel Hwang](https://www.linkedin.com/in/feelwonderland/), [Nick Mcginnis](https://www.linkedin.com/in/nick-mcginnis-6178301b/), [Jennifer Leartanasan](https://www.linkedin.com/in/jenleart/) and team.

![](https://jasonspielman.com/_assets/v11/af3c29800bf2db7e09e3e2a6d40cf016c0aa09c3.png) ![](https://jasonspielman.com/_assets/v11/c25bfd7390974b0b1105851eeb3d0366468f69c7.png) ![](https://jasonspielman.com/_assets/v11/a6da7f795470d5cf562a89615559a4520071022e.png) ![](https://jasonspielman.com/_assets/v11/7bf57082896ab34dfb509d3da0ae48416d05f97e.png) ![](https://jasonspielman.com/_assets/v11/4e58691b2490f4836923ca958464ad82a0d5fc9d.png) ![](https://jasonspielman.com/_assets/v11/1ea2d458d7c082ef01fe1932ae44ebadd565701a.png) ![](https://jasonspielman.com/_assets/v11/10b788f2feba68b4a3eff642bbeaa6b38c2fa5e3.png)

## Visual Assets

## From press kits to launch visuals, I crafted the full suite of assets. Here are some of my favorites.

![](https://jasonspielman.com/_assets/v11/db9e3d9b3a5aa3acc7e78cc3ce2e401846b85487.png) ![](https://jasonspielman.com/_assets/v11/3924f22155c39ab98dff17b3264ae11b5a877547.png)[Keyword blog](https://blog.google/technology/ai/notebooklm-update-october-2024/)

![My project hero](https://jasonspielman.com/_assets/v11/f3db0b7e451ee98fe639b1ef628552c925534a95.png) ![My project hero](https://jasonspielman.com/_assets/v11/6c13cbc3b134441632e60fac973e6b989596ab55.png) ![](https://jasonspielman.com/_assets/v11/e2bcafc3fbbd7e938b533f5cfe2c6ccb5a4ad5a6.png)[Keyword blog](https://blog.google/technology/ai/notebooklm-goes-global-support-for-websites-slides-fact-check/)

![My project hero](https://jasonspielman.com/_assets/v11/15daa0acc944fba566d14154fa187ae79ac22bdf.png)

Early animation for Website

## Key Takeaways from the Journey

1. Building Audio Overviews

We built and launched a viral AI product in 2 months (at Google!). Here's how:Our little NotebookLM team has had a crazy few months and is proving that small, nimble teams not only exist within Google, but can move fast and have significant impact.Our newest feature “Audio Overviews” has taken over the internet the past few days. The team has been sprinting - we went from idea to prototype in weeks, then launched publicly in under 2 months. It’s not perfect (yet!), but that’s the point. Here are a few takeaways: 1. It's about building products \*with\* our users, not just \*for\* them. We’re not waiting to launch, we’re shipping early and iterating. Tech is evolving faster than users can possibly know what they want. We're often anticipating needs for V1 then working alongside them to improve. Example: Very quickly we saw a massive user desire for in-line citations so our team quickly pivoted to build and launch. (Join our discord!)2. Built-in not bolted-on: We’re building net-new, AI native products. This isn’t just AI for the sake of “AI”, we’re working to bridge the gap between state-of-the-art research and human problems. Audio Overviews are great because they sound amazingly real, yes -- but useful because they are (1) source grounded and (2) an easy one-click way to study and digest your own information. 3. Meetings are spent \*building\*, not just talking about building. We’re collaborating, deeply. I am the only UX designer on the team so we have to make every moment count. Raiza and I are constantly strategizing and iterating together. NotebookLM represents a new era of product development within Labs at Google. We're putting user feedback and community engagement at the heart of everything we do. We’re building quickly and have a lot more coming soon...The audio below is made with the NotebookLM Audio Overview feature simply by feeding it the text above^! If you haven’t tried it, I highly recommend it. We want to make it better for you! Try it: notebooklm.googleShout out to a few of the amazing people on the team who've been hustling to make this all happen: Stephen Hughes, Oliver King, Biao (Frank) Wang, Corbin Cunningham, PhD, Yi Yao, Usama Bin Shafqat, Simon Tokumine (+ more)See post by Andrej Karpathy: https://lnkd.in/ghTdbyXN

![](https://jasonspielman.com/_assets/v11/0e1cae07ca0e9de49ca20e35fe8466d7ab9d52a7.png)

Jason Spielman

Linkedin →

[View original](https://www.linkedin.com/posts/jason-spielman-creative_we-built-and-launched-a-viral-ai-product-activity-7247661593268756480-AZUf?utm_source=share&utm_medium=member_desktop&rcm=ACoAABSWZB4B7dwJtHun5sKkOp4PdtLi9NOm7Dg)

1. Here’s what I learned designing a novel, AI-first experience:

[![](https://jasonspielman.com/_assets/v11/0e1cae07ca0e9de49ca20e35fe8466d7ab9d52a7.png)

Jason Spielman

Linkedin →

](https://www.linkedin.com/feed/update/urn:li:activity:7273366318202896384/)