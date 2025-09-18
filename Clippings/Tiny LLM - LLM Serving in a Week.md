---
title:
source: "https://skyzh.github.io/tiny-llm/"
author:
published:
created: 2025-09-15
description:
tags:
  - "clippings"
---
## Keyboard shortcuts

Press ← or → to navigate between chapters

Press S or / to search in the book

Press ? to show this help

Press Esc to hide this help

1. [Preface](https://skyzh.github.io/tiny-llm/preface.html)
2. [Setting Up the Environment](https://skyzh.github.io/tiny-llm/setup.html)

5. [**1.** Week 1: From Matmul to Text](https://skyzh.github.io/tiny-llm/week1-overview.html)
6. 1. [**1.1.** Attention and Multi-Head Attention](https://skyzh.github.io/tiny-llm/week1-01-attention.html)
2. [**1.2.** Positional Encodings and RoPE](https://skyzh.github.io/tiny-llm/week1-02-positional-encodings.html)
3. [**1.3.** Grouped/Multi Query Attention](https://skyzh.github.io/tiny-llm/week1-03-gqa.html)
4. [**1.4.** RMSNorm and MLP](https://skyzh.github.io/tiny-llm/week1-04-rmsnorm-and-mlp.html)
5. [**1.5.** The Qwen2 Model](https://skyzh.github.io/tiny-llm/week1-05-qwen2-model.html)
6. [**1.6.** Generating the Response](https://skyzh.github.io/tiny-llm/week1-06-generate-response.html)
7. [**1.7.** Sampling and Preparing for Week 2](https://skyzh.github.io/tiny-llm/week1-07-sampling-prepare.html)
7. [**2.** Week 2: Tiny vLLM](https://skyzh.github.io/tiny-llm/week2-overview.html)
8. 1. [**2.1.** Key-Value Cache](https://skyzh.github.io/tiny-llm/week2-01-kv-cache.html)
2. **2.2.** Quantized Matmul (2 Days)
3. **2.3.** Flash Attention (2 Days)
4. [**2.4.** Continuous Batching (2 Days)](https://skyzh.github.io/tiny-llm/week2-06-prefill-and-batch.html)

12. [Glossary Index](https://skyzh.github.io/tiny-llm/glossary.html)

## Tiny LLM - LLM Serving in a Week

## Preface

This course is designed for systems engineers who want to understand how LLMs work.

As a system engineer, I always wonder how things work internally and how to optimize them. I had a hard time figuring out the LLM stuff. Most of the open source projects that serve LLMs are highly optimized with CUDA kernels and other low-level optimizations. It is not easy to understand the whole picture by looking at a codebase of 100k lines of code. Therefore, I decided to implement an LLM serving project from scratch -- with only matrix manipulations APIs, so that I can understand what it takes to load those LLM model parameters and do the math magic to generate text.

You can think of this course as an LLM version of CMU Deep Learning Systems course's [needle](https://github.com/dlsyscourse/hw1/tree/main/python/needle) project.

## Prerequisites

You should have some experience with the basics of deep learning and have some idea of how PyTorch works. Some recommended resources are:

- CMU [Intro to Machine Learning](https://www.cs.cmu.edu/~mgormley/courses/10601/) -- this course teaches you the basics of machine learning
- CMU [Deep Learning Systems](https://dlsyscourse.org/) -- this course teaches you how to build PyTorch from scratch

## Environment Setup

This course uses [MLX](https://github.com/ml-explore/mlx), an array/machine learning library for Apple Silicon. Nowadays it's much easier to get an Apple Silicon device than NVIDIA GPUs. In theory you can also do this course with PyTorch or numpy, but we just don't have the test infra to support them. We test your implementation against PyTorch's CPU implementation and MLX's implementation to ensure correctness.

## Course Structure

This course is divided into 3 weeks. We will serve the Qwen2-7B-Instruct model and optimize it throughout the course.

- Week 1: serve Qwen2 with purely matrix manipulation APIs. Just Python.
- Week 2: optimizations, implement C++/Metal custom kernels to make the model run faster.
- Week 3: more optimizations, batch the requests to serve the model with high throughput.

## How to Use This Book

The thing you are reading right now is the tiny-llm book. It is designed more like a guidebook instead of a textbook that explains everything from scratch. In this course, we provide the materials that we find useful on the Internet when the author(s) implemented the tiny-llm project. The Internet does a better job of explaining the concepts and I do not think it is necessary to repeat everything here. Think of this as a guide (of a list of tasks) and some hints! We will also unify the language of the Internet materials so that it is easier to correspond them to the codebase. For example, we will have a unified dimension symbols for the tensors. You do not need to figure out what `H`, `L`, `E` stands for and what dimension of the matrixes are passed into the function.

## About the Authors

This course is created by [Chi](https://github.com/skyzh) and [Connor](https://github.com/Connor1996).

Chi is a systems software engineer at [Neon](https://neon.tech/) (now acquired by Databricks), focusing on storage systems. Fascinated by the vibe of large language models (LLMs), he created this course to explore how LLM inference works.

Connor is a software engineer at [PingCAP](https://pingcap.com/), developing the TiKV distributed key-value database. Curious about the internals of LLMs, he joined this course to practice how to build a high-performance LLM serving system from scratch, and contributed to building the course for the community.

## Community

You may join skyzh's Discord server and study with the tiny-llm community.

[![Join skyzh's Discord Server](https://skyzh.github.io/tiny-llm/discord-badge.svg)](https://skyzh.dev/join/discord)

## Get Started

Now, you can start to set up the environment following the instructions in [Setting Up the Environment](https://skyzh.github.io/tiny-llm/setup.html) and begin your journey to build tiny-llm!

Your feedback is greatly appreciated. Welcome to join our [Discord Community](https://skyzh.dev/join/discord).  
Found an issue? Create an issue / pull request on [github.com/skyzh/tiny-llm](https://github.com/skyzh/tiny-llm).  
tiny-llm-book © 2025 by Alex Chi Z is licensed under CC BY-NC-SA 4.0.