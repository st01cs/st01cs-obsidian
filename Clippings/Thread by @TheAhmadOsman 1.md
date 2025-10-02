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
\> 你是

\> 想要真正了解 LLMs 的工作原理

\> 厌倦了“先从线性代数开始，五年后再回来”

\> 决定自己构建一条路线

\> 没有冗余。没有绕路。没有 200 小时的通用 ML 播放列表

\> 只有真正能让你从“什么是标记？”到“我训练了一个带有 LoRA 适配器和 FlashAttention 的小型 GPT”所需的内容  
  
\> goal: build, fine-tune, and ship LLMs

\> not vibe with them. not "learn the theory" forever

\> build them  
\> 目标: 构建、微调并发布 LLMs

\> 不感冒。不只是“学习理论”一辈子

\> 构建它们  
  
\> you will:  
\> 你将:  
  
\> > build an autograd engine from scratch

\> > write a mini-GPT from scratch

\> > implement LoRA and fine-tune a model on real data

\> > hate CUDA at least once

\> > cry

\> > keep going  
\> > 从头构建一个自动求导引擎

\> > 从头编写一个迷你 GPT

\> > 实现 LoRA 并在真实数据上微调模型

\> > 至少一次讨厌 CUDA

\> > 哭

\> > 继续  
  
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
\> 阶段 0：基础知识  
  
\> > if matrix multiplication is scary, you’re not ready yet

\> > watch 3Blue1Brown’s linear algebra series

\> > MIT 18.06 with Strang, yes, he’s still the GOAT

\> > code Micrograd from scratch (Karpathy)

\> > train a mini-MLP on MNIST

\> > no frameworks, no shortcuts, no mercy  
\> > 如果矩阵乘法让你感到害怕，那你还没有准备好

\> > 看看 3Blue1Brown 的线性代数系列

\> > 去 MIT 18.06，是的，他仍然是最强的（GOAT）

\> > 从零开始编写 Micrograd (Karpathy)

\> > 在 MNIST 上训练一个小型 MLP

\> > 不用框架，不走捷径，不留情面  
  
\> phase 1: transformers  
\> 第一阶段：变压器  
  
\> > the name is scary

\> > it’s just stacked matrix multiplies and attention blocks

\> > Jay Alammar + 3Blue1Brown for the “aha”

\> > Stanford CS224N for the theory

\> > read "Attention Is All You Need" only AFTER building mental models

\> > Karpathy's "Let's Build GPT" will break your brain in a good way

\> > project: build a decoder-only GPT from scratch

\> > bonus: swap tokenizers, try BPE/SentencePiece  
\> > 名字听着吓人

\> > 就是堆叠的矩阵乘法和注意力块

\> > Jay Alammar + 3Blue1Brown 才是“恍然大悟”

\> > Stanford CS224N 提供理论

\> > 请在构建完心智模型后再阅读“Attention Is All You Need”

\> > Karpathy 的“让我们一起构建 GPT”会以一种有益的方式让你的大脑受到挑战

\> > 项目：从零构建一个解码器版本的 GPT

\> > 奖励：更换分词器，尝试使用 BPE/SentencePiece  
  
\> phase 2: scaling  
\> 第 2 阶段：扩展  
  
\> > LLMs got good by scaling, not magic

\> > Kaplan paper -> Chinchilla paper

\> > learn Data, Tensor, Pipeline parallelism

\> > spin up multi-GPU jobs using HuggingFace Accelerate

\> > run into VRAM issues

\> > fix them

\> > welcome to real training hell  
\> > LLMs 是通过扩展而不是魔法变得优秀的

\> > Kaplan 论文 -> Chinchilla 论文

\> > 学习数据、张量、管道并行 ism

\> > 使用 HuggingFace Accelerate 启动多 GPU 任务

\> > 遇到 VRAM 问题

\> > 解决它们

\> > 欢迎来到真正的训练地狱  
  
\> phase 3: alignment & fine-tuning  
\> 第 3 阶段：对齐与微调  
  
\> > RLHF: OpenAI blog -> Ouyang paper

\> > SFT -> reward model -> PPO (don’t get lost here)

\> > Anthropic's Constitutional AI = smart constraints

\> > LoRA/QLoRA: read, implement, inject into HuggingFace models

\> > fine-tune on real data

\> > project: fine-tune gpt2 or distilbert with your own adapters

\> > not toy examples. real use cases or bust  
\> > RLHF：OpenAI 博客 -> 欧阳论文

\> > SFT -> 奖励模型 -> PPO（不要在这里迷失）

\> > Anthropic 的宪法 AI = 智能约束

\> > LoRA/QLoRA: 阅读，实现，并将其注入到 HuggingFace 模型中

\> > 在真实数据上进行微调

\> > 项目：使用你自己的适配器微调 gpt2 或 distilbert

\> > 不是玩具示例。要么实际应用，要么不搞  
  
\> phase 4: production  
\> 第 4 阶段：生产  
  
\> this is the part people skip to, but you earned it

\> inference optimization: FlashAttention, quantization, sub-second latency

\> read the paper, test with quantized models  
\> 这是人们跳过的部分，但你值得拥有

\> 推理优化：FlashAttention，量化，亚秒级延迟

\> 阅读论文，使用量化模型测试  
  
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
PyTorch：

\> > Karpathy，从零开始掌握

\> > transformers：

\> > Alammar, Karpathy, CS224N, Vaswani et al

\> > 规模化：

\> > Kaplan, Chinchilla, HuggingFace Accelerate

\> > 对齐：

\> > OpenAI, Anthropic, LoRA, QLoRA

\> > 推理：

\> > FlashAttention  
  
\> the endgame:  
\> 最终目标：  
  
\> > understand how these models actually work

\> > see through hype

\> > ignore LinkedIn noise

\> > build tooling

\> > train real stuff

\> > ship your own stack

\> > look at a paper and think “yeah I get it”

\> > build your own AI assistant, infra, whatever  
\> > 理解这些模型实际上是如何工作的

\> > 看穿 hype

\> > 忽略领英上的噪音

\> > 构建工具

\> > 训练实际的东西

\> > 发布你自己的栈

\> > 看了一篇论文就觉得自己懂了

\> > 自己动手搭建一个 AI 助手，基础设施什么的  
  
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