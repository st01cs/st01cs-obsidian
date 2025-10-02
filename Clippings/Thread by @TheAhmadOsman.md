---
title: "Thread by @TheAhmadOsman"
source: "https://x.com/TheAhmadOsman/status/1966780033206264100"
author:
  - "[[@TheAhmadOsman]]"
published: 2025-09-13
created: 2025-10-01
description:
tags:
  - "clippings"
---
**Ahmad** @TheAhmadOsman [2025-09-13](https://x.com/TheAhmadOsman/status/1966780033206264100)

\> be you

\> want to actually learn how LLMs work

\> sick of “just start with linear algebra and come back in 5 years”

\> decide to build my own roadmap

\> no fluff. no detours. no 200-hour generic ML playlists

\> just the stuff that actually gets you from “what’s a token?” to “I trained a mini-GPT with LoRA adapters and FlashAttention”  
  
\> goal: build, fine-tune, and ship LLMs

\> not vibe with them. not "learn the theory" forever

\> build them  
  
\> you will:  
  
\> > build an autograd engine from scratch

\> > write a mini-GPT from scratch

\> > implement LoRA and fine-tune a model on real data

\> > hate CUDA at least once

\> > cry

\> > keep going  
  
\> 5 phases

\> if you already know something? skip

\> if you're lost? rewatch

\> if you’re stuck? use DeepResearch

\> this is a roadmap, not a leash

\> by the end: you either built the thing or you didn’t  
\> 5 个阶段

\> 如果你已经知道某些内容？跳过

\> 如果迷路了？重新观看

\> 如果卡住了？使用 DeepResearch

\> 这是一条路线图，不是一条绳索

\> 最终：要么你建成了，要么你没有  
  
\> phase 0: foundations  
  
\> > if matrix multiplication is scary, you’re not ready yet

\> > watch 3Blue1Brown’s linear algebra series

\> > MIT 18.06 with Strang, yes, he’s still the GOAT

\> > code Micrograd from scratch (Karpathy)

\> > train a mini-MLP on MNIST

\> > no frameworks, no shortcuts, no mercy  
  
\> phase 1: transformers  
  
\> > the name is scary

\> > it’s just stacked matrix multiplies and attention blocks

\> > Jay Alammar + 3Blue1Brown for the “aha”

\> > Stanford CS224N for the theory

\> > read "Attention Is All You Need" only AFTER building mental models

\> > Karpathy's "Let's Build GPT" will break your brain in a good way

\> > project: build a decoder-only GPT from scratch

\> > bonus: swap tokenizers, try BPE/SentencePiece  
  
\> phase 2: scaling  
\> 第 2 阶段：扩展  
  
\> > LLMs got good by scaling, not magic

\> > Kaplan paper -> Chinchilla paper

\> > learn Data, Tensor, Pipeline parallelism

\> > spin up multi-GPU jobs using HuggingFace Accelerate

\> > run into VRAM issues

\> > fix them

\> > welcome to real training hell  
  
\> phase 3: alignment & fine-tuning  
\> 第 3 阶段：对齐与微调  
  
\> > RLHF: OpenAI blog -> Ouyang paper

\> > SFT -> reward model -> PPO (don’t get lost here)

\> > Anthropic's Constitutional AI = smart constraints

\> > LoRA/QLoRA: read, implement, inject into HuggingFace models

\> > fine-tune on real data

\> > project: fine-tune gpt2 or distilbert with your own adapters

\> > not toy examples. real use cases or bust  
  
\> phase 4: production  
  
\> this is the part people skip to, but you earned it

\> inference optimization: FlashAttention, quantization, sub-second latency

\> read the paper, test with quantized models  
  
\> resources:  
资源：  
  
\> math/coding:

\> > 3Blue1Brown, MIT 18.06, Goodfellow’s book  
数学/编程：

\> 3Blue1Brown, MIT 18.06, Goodfellow 的书  
  
\> PyTorch:

\> > Karpathy, Zero to Mastery

\> > transformers:

\> > Alammar, Karpathy, CS224N, Vaswani et al

\> > scaling:

\> > Kaplan, Chinchilla, HuggingFace Accelerate

\> > alignment:

\> > OpenAI, Anthropic, LoRA, QLoRA

\> > inference:

\> > FlashAttention  
  
\> the endgame:  
  
\> > understand how these models actually work

\> > see through hype

\> > ignore LinkedIn noise

\> > build tooling

\> > train real stuff

\> > ship your own stack

\> > look at a paper and think “yeah I get it”

\> > build your own AI assistant, infra, whatever  
  
\> make it all the way through?

\> ship something real?

\> DM me.

\> I wanna see what you built.  
\> 能做到底吗？

\> 真正发布点东西？

\> DM 我。

\> 我想看看你建的东西。  
  
\> happy hacking.  
\> 祝你编程愉快。