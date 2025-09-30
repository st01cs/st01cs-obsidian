---
title: "GeeeekExplorer/nano-vllm: Nano vLLM"
source: "https://github.com/GeeeekExplorer/nano-vllm"
author:
  - "[[GeeeekExplorer]]"
published:
created: 2025-09-30
description: "Nano vLLM. Contribute to GeeeekExplorer/nano-vllm development by creating an account on GitHub."
tags:
  - "clippings"
---
[Skip to content](https://github.com/GeeeekExplorer/#start-of-content)

**[nano-vllm](https://github.com/GeeeekExplorer/nano-vllm)** Public

- [Fork 867 Fork your own copy of GeeeekExplorer/nano-vllm](https://github.com/GeeeekExplorer/nano-vllm/fork)

Nano vLLM

### License

[MIT license](https://github.com/GeeeekExplorer/nano-vllm/blob/main/LICENSE)

[Open in github.dev](https://github.dev/) [Open in a new github.dev tab](https://github.dev/) [Open in codespace](https://github.com/codespaces/new/GeeeekExplorer/nano-vllm?resume=1)

## GeeeekExplorer/nano-vllm

## Add file

## Nano-vLLM

A lightweight vLLM implementation built from scratch.

## Key Features

- 🚀 **Fast offline inference** - Comparable inference speeds to vLLM
- 📖 **Readable codebase** - Clean implementation in ~ 1,200 lines of Python code
- ⚡ **Optimization Suite** - Prefix caching, Tensor Parallelism, Torch compilation, CUDA graph, etc.

## Installation

```
pip install git+https://github.com/GeeeekExplorer/nano-vllm.git
```

## Manual Download

If you prefer to download the model weights manually, use the following command:

```
huggingface-cli download --resume-download Qwen/Qwen3-0.6B \
  --local-dir ~/huggingface/Qwen3-0.6B/ \
  --local-dir-use-symlinks False
```

## Quick Start

See `example.py` for usage. The API mirrors vLLM's interface with minor differences in the `LLM.generate` method:

```
from nanovllm import LLM, SamplingParams
llm = LLM("/YOUR/MODEL/PATH", enforce_eager=True, tensor_parallel_size=1)
sampling_params = SamplingParams(temperature=0.6, max_tokens=256)
prompts = ["Hello, Nano-vLLM."]
outputs = llm.generate(prompts, sampling_params)
outputs[0]["text"]
```

## Benchmark

See `bench.py` for benchmark.

**Test Configuration:**

- Hardware: RTX 4070 Laptop (8GB)
- Model: Qwen3-0.6B
- Total Requests: 256 sequences
- Input Length: Randomly sampled between 100–1024 tokens
- Output Length: Randomly sampled between 100–1024 tokens

**Performance Results:**

| Inference Engine | Output Tokens | Time (s) | Throughput (tokens/s) |
| --- | --- | --- | --- |
| vLLM | 133,966 | 98.37 | 1361.84 |
| Nano-vLLM | 133,966 | 93.41 | 1434.13 |

## Star History

[![Star History Chart](https://camo.githubusercontent.com/9d77943eb142ab5773e78a27135fb2d3df2e3b3718b57943b7abd006ae6034a8/68747470733a2f2f6170692e737461722d686973746f72792e636f6d2f7376673f7265706f733d47656565656b4578706c6f7265722f6e616e6f2d766c6c6d26747970653d44617465)](https://www.star-history.com/#GeeeekExplorer/nano-vllm&Date)

## Releases

No releases published

## Packages

No packages published  

## Languages

- [Python 100.0%](https://github.com/GeeeekExplorer/nano-vllm/search?l=python)