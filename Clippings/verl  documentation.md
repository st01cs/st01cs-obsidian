---
title: "Welcome to verl’s documentation! — verl  documentation"
source: "https://verl.readthedocs.io/en/latest/index.html"
author:
published:
created: 2025-11-20
description:
tags:
  - "clippings"
---
## Welcome to verl’s documentation!

verl is a flexible, efficient and production-ready RL training framework designed for large language models (LLMs) post-training. It is an open source implementation of the [HybridFlow](https://arxiv.org/pdf/2409.19256) paper.

verl is flexible and easy to use with:

- **Easy extension of diverse RL algorithms**: The hybrid programming model combines the strengths of single-controller and multi-controller paradigms to enable flexible representation and efficient execution of complex Post-Training dataflows. Allowing users to build RL dataflows in a few lines of code.
- **Seamless integration of existing LLM infra with modular APIs**: Decouples computation and data dependencies, enabling seamless integration with existing LLM frameworks, such as PyTorch FSDP, Megatron-LM, vLLM and SGLang. Moreover, users can easily extend to other LLM training and inference frameworks.
- **Flexible device mapping and parallelism**: Supports various placement of models onto different sets of GPUs for efficient resource utilization and scalability across different cluster sizes.
- Ready integration with popular HuggingFace models

verl is fast with:

- **State-of-the-art throughput**: By seamlessly integrating existing SOTA LLM training and inference frameworks, verl achieves high generation and training throughput.
- **Efficient actor model resharding with 3D-HybridEngine**: Eliminates memory redundancy and significantly reduces communication overhead during transitions between training and generation phases.

---

Quickstart

- [Installation](https://verl.readthedocs.io/en/latest/start/install.html)
	- [Requirements](https://verl.readthedocs.io/en/latest/start/install.html#requirements)
	- [Choices of Backend Engines](https://verl.readthedocs.io/en/latest/start/install.html#choices-of-backend-engines)
	- [Install from docker image](https://verl.readthedocs.io/en/latest/start/install.html#install-from-docker-image)
	- [Install from custom environment](https://verl.readthedocs.io/en/latest/start/install.html#install-from-custom-environment)
	- [Install with AMD GPUs - ROCM kernel support](https://verl.readthedocs.io/en/latest/start/install.html#install-with-amd-gpus-rocm-kernel-support)
- [Quickstart: PPO training on GSM8K dataset](https://verl.readthedocs.io/en/latest/start/quickstart.html)
	- [Introduction](https://verl.readthedocs.io/en/latest/start/quickstart.html#introduction)
	- [Dataset Introduction](https://verl.readthedocs.io/en/latest/start/quickstart.html#dataset-introduction)
	- [Step 1: Prepare the dataset](https://verl.readthedocs.io/en/latest/start/quickstart.html#step-1-prepare-the-dataset)
	- [Step 2: Download a model for post-training](https://verl.readthedocs.io/en/latest/start/quickstart.html#step-2-download-a-model-for-post-training)
	- [Step 3: Perform PPO training with the instruct model](https://verl.readthedocs.io/en/latest/start/quickstart.html#step-3-perform-ppo-training-with-the-instruct-model)
- [Multinode Training](https://verl.readthedocs.io/en/latest/start/multinode.html)
	- [Option 1: Launch Manually](https://verl.readthedocs.io/en/latest/start/multinode.html#option-1-launch-manually)
	- [Option 2: Launch via SkyPilot on Kubernetes or clouds](https://verl.readthedocs.io/en/latest/start/multinode.html#option-2-launch-via-skypilot-on-kubernetes-or-clouds)
	- [Option 3: Launch via Slurm](https://verl.readthedocs.io/en/latest/start/multinode.html#option-3-launch-via-slurm)
	- [Option 4: Launch via dstack](https://verl.readthedocs.io/en/latest/start/multinode.html#option-4-launch-via-dstack)
	- [How to debug?](https://verl.readthedocs.io/en/latest/start/multinode.html#how-to-debug)
	- [Multi-node training on AMD clusters](https://verl.readthedocs.io/en/latest/start/multinode.html#multi-node-training-on-amd-clusters)
- [Ray Debug Tutorial](https://verl.readthedocs.io/en/latest/start/ray_debug_tutorial.html)
	- [How to debug?](https://verl.readthedocs.io/en/latest/start/ray_debug_tutorial.html#how-to-debug)
- [More Resources](https://verl.readthedocs.io/en/latest/start/more_resources.html)
- [Agentic RL Training](https://verl.readthedocs.io/en/latest/start/agentic_rl.html)
	- [Overview](https://verl.readthedocs.io/en/latest/start/agentic_rl.html#overview)
	- [Server-based Asynchronous Rollout](https://verl.readthedocs.io/en/latest/start/agentic_rl.html#server-based-asynchronous-rollout)
	- [Multi-turn Conversations and Tool Calls](https://verl.readthedocs.io/en/latest/start/agentic_rl.html#multi-turn-conversations-and-tool-calls)
	- [Agent Framework](https://verl.readthedocs.io/en/latest/start/agentic_rl.html#agent-framework)

Programming guide

- [HybridFlow Programming Guide](https://verl.readthedocs.io/en/latest/hybrid_flow.html)
	- [Motivation and Design](https://verl.readthedocs.io/en/latest/hybrid_flow.html#motivation-and-design)
	- [Codebase walkthrough (PPO)](https://verl.readthedocs.io/en/latest/hybrid_flow.html#codebase-walkthrough-ppo)
	- [Repository organization](https://verl.readthedocs.io/en/latest/hybrid_flow.html#repository-organization)
- [The Design of `verl.single_controller`](https://verl.readthedocs.io/en/latest/single_controller.html)
	- [Preface](https://verl.readthedocs.io/en/latest/single_controller.html#preface)
	- [Origin](https://verl.readthedocs.io/en/latest/single_controller.html#origin)
	- [A Running Example: `generate_sequences`](https://verl.readthedocs.io/en/latest/single_controller.html#a-running-example-generate-sequences)
	- [Beyond RL Post-Training: Generalizing `verl.single_controller`](https://verl.readthedocs.io/en/latest/single_controller.html#beyond-rl-post-training-generalizing-verl-single-controller)

Data Preparation

- [Prepare Data for Post-Training](https://verl.readthedocs.io/en/latest/preparation/prepare_data.html)
- [Implement Reward Function for Dataset](https://verl.readthedocs.io/en/latest/preparation/reward_function.html)

Configurations

- [Config Explanation](https://verl.readthedocs.io/en/latest/examples/config.html)
	- [ppo\_trainer.yaml for RL FSDP Backend](https://verl.readthedocs.io/en/latest/examples/config.html#ppo-trainer-yaml-for-rl-fsdp-backend)
	- [evaluation.yaml](https://verl.readthedocs.io/en/latest/examples/config.html#evaluation-yaml)
	- [sft\_trainer.yaml for SFT FSDP Backend](https://verl.readthedocs.io/en/latest/examples/config.html#sft-trainer-yaml-for-sft-fsdp-backend)

Algorithms

- [Proximal Policy Optimization (PPO)](https://verl.readthedocs.io/en/latest/algo/ppo.html)
- [Group Relative Policy Optimization (GRPO)](https://verl.readthedocs.io/en/latest/algo/grpo.html)
- [Recipe: CollabLLM](https://verl.readthedocs.io/en/latest/algo/collabllm.html)
- [Recipe: Decoupled Clip and Dynamic Sampling Policy Optimization (DAPO)](https://verl.readthedocs.io/en/latest/algo/dapo.html)
- [Recipe: Self-Play Fine-Tuning (SPIN)](https://verl.readthedocs.io/en/latest/algo/spin.html)
- [Recipe: Self-Play Preference Optimization (SPPO)](https://verl.readthedocs.io/en/latest/algo/sppo.html)
- [Recipe: Entropy Mechanism](https://verl.readthedocs.io/en/latest/algo/entropy.html)
- [On-Policy RL with Optimal Reward Baseline (OPO)](https://verl.readthedocs.io/en/latest/algo/opo.html)
- [Algorithm Baselines](https://verl.readthedocs.io/en/latest/algo/baseline.html)
- [GPG: Group Policy Gradient](https://verl.readthedocs.io/en/latest/algo/gpg.html)
- [Rollout Correction](https://verl.readthedocs.io/en/latest/algo/rollout_corr.html)
- [Mathematical Formulations of Rollout Correction Methods in `verl`](https://verl.readthedocs.io/en/latest/algo/rollout_corr_math.html)

Performance Tuning Guide

- [Training DeepSeek 671b](https://verl.readthedocs.io/en/latest/perf/dpsk.html)
- [Verl LLM Best Practices (DAPO + Qwen3-235B)](https://verl.readthedocs.io/en/latest/perf/best_practices.html)
- [Performance Tuning Guide](https://verl.readthedocs.io/en/latest/perf/perf_tuning.html)
- [Upgrading to vLLM >= 0.8](https://verl.readthedocs.io/en/latest/README_vllm0.8.html)
- [Hardware Resource Needed for RL](https://verl.readthedocs.io/en/latest/perf/device_tuning.html)
- [verl Profiler System](https://verl.readthedocs.io/en/latest/perf/verl_profiler_system.html)
- [NVIDIA Nsight Systems profiling in verl](https://verl.readthedocs.io/en/latest/perf/nsight_profiling.html)

Adding new models

- [Add models with the FSDP backend](https://verl.readthedocs.io/en/latest/advance/fsdp_extension.html)
- [Add models with the Megatron-LM backend](https://verl.readthedocs.io/en/latest/advance/megatron_extension.html)

Advanced Features

- [Using Checkpoints to Support Fault Tolerance Training](https://verl.readthedocs.io/en/latest/advance/checkpoint.html)
- [RoPE Scaling override](https://verl.readthedocs.io/en/latest/advance/rope.html)
- [Attention Implementation Override](https://verl.readthedocs.io/en/latest/advance/attention_implementation.html)
- [RL(HF) algorithms with LoRA Support](https://verl.readthedocs.io/en/latest/advance/ppo_lora.html)
- [Multi-turn Rollout Support](https://verl.readthedocs.io/en/latest/sglang_multiturn/multiturn.html)
- [Interaction System for Multi-turn RL Training](https://verl.readthedocs.io/en/latest/sglang_multiturn/interaction_system.html)
- [Ray API Design Tutorial](https://verl.readthedocs.io/en/latest/advance/placement.html)
- [Extend to other RL(HF) algorithms](https://verl.readthedocs.io/en/latest/advance/dpo_extension.html)
- [Sandbox Fusion Example](https://verl.readthedocs.io/en/latest/examples/sandbox_fusion_example.html)
- [Trace Function Usage Instructions](https://verl.readthedocs.io/en/latest/advance/rollout_trace.html)
- [RolloutSkip Function Usage Documentation](https://verl.readthedocs.io/en/latest/advance/rollout_skip.html)
- [Recipe: One Step Off Policy Async Trainer](https://verl.readthedocs.io/en/latest/advance/one_step_off.html)
- [Agent Loop](https://verl.readthedocs.io/en/latest/advance/agent_loop.html)
- [Reward Loop](https://verl.readthedocs.io/en/latest/advance/reward_loop.html)
- [Recipe: Fully Async Policy Trainer](https://verl.readthedocs.io/en/latest/advance/fully_async.html)
- [TransferQueue Data System](https://verl.readthedocs.io/en/latest/data/transfer_queue.html)
- [Use Prometheus and Grafana to Monitor Rollout](https://verl.readthedocs.io/en/latest/advance/grafana_prometheus.html)

Hardware Support

- [Getting started with AMD (ROCM Kernel)](https://verl.readthedocs.io/en/latest/amd_tutorial/amd_build_dockerfile_page.html)
- [verl performance tuning for AMD (ROCm Kernel)](https://verl.readthedocs.io/en/latest/amd_tutorial/amd_vllm_page.html)
- [Ascend Quickstart](https://verl.readthedocs.io/en/latest/ascend_tutorial/ascend_quick_start.html)
- [Data collection based on FSDP backend on Ascend devices(zh)](https://verl.readthedocs.io/en/latest/ascend_tutorial/ascend_profiling_zh.html)
- [Data collection based on FSDP backend on Ascend devices(en)](https://verl.readthedocs.io/en/latest/ascend_tutorial/ascend_profiling_en.html)
- [Ascend Dockerfile Build Guidance](https://verl.readthedocs.io/en/latest/ascend_tutorial/dockerfile_build_guidance.html)
- [Ascend Quickstart with SGLang Backend](https://verl.readthedocs.io/en/latest/ascend_tutorial/ascend_sglang_quick_start.html)

FAQ

- [Frequently Asked Questions](https://verl.readthedocs.io/en/latest/faq/faq.html)
	- [Ray related](https://verl.readthedocs.io/en/latest/faq/faq.html#ray-related)
	- [Distributed training](https://verl.readthedocs.io/en/latest/faq/faq.html#distributed-training)
	- [Install related](https://verl.readthedocs.io/en/latest/faq/faq.html#install-related)
	- [Illegal memory access](https://verl.readthedocs.io/en/latest/faq/faq.html#illegal-memory-access)
	- [Checkpoints](https://verl.readthedocs.io/en/latest/faq/faq.html#checkpoints)
	- [Triton `compile_module_from_src` error](https://verl.readthedocs.io/en/latest/faq/faq.html#triton-compile-module-from-src-error)
	- [What is the meaning of train batch size, mini batch size, and micro batch size?](https://verl.readthedocs.io/en/latest/faq/faq.html#what-is-the-meaning-of-train-batch-size-mini-batch-size-and-micro-batch-size)
	- [How to generate ray timeline to analyse performance of a training job?](https://verl.readthedocs.io/en/latest/faq/faq.html#how-to-generate-ray-timeline-to-analyse-performance-of-a-training-job)
	- [How to set proxy only for wandb?](https://verl.readthedocs.io/en/latest/faq/faq.html#how-to-set-proxy-only-for-wandb)
	- [Missmatch between inference and training sequence (high actor/grad\_norm)](https://verl.readthedocs.io/en/latest/faq/faq.html#missmatch-between-inference-and-training-sequence-high-actor-grad-norm)

Development Notes

- [Sandbox Fusion Tool Integration](https://verl.readthedocs.io/en/latest/sglang_multiturn/sandbox_fusion.html)

## Contribution

verl is free software; you can redistribute it and/or modify it under the terms of the Apache License 2.0. We welcome contributions. Join us on [GitHub](https://github.com/volcengine/verl), [Slack](https://join.slack.com/t/verlgroup/shared_invite/zt-2w5p9o4c3-yy0x2Q56s_VlGLsJ93A6vA) and [Wechat](https://raw.githubusercontent.com/eric-haibin-lin/verl-community/refs/heads/main/WeChat.JPG) for discussions.

Contributions from the community are welcome! Please check out our [project roadmap](https://github.com/volcengine/verl/issues/710) and [good first issues](https://github.com/volcengine/verl/issues?q=is%3Aissue%20state%3Aopen%20label%3A%22good%20first%20issue%22) to see where you can contribute.

### Code Linting and Formatting

We use pre-commit to help improve code quality. To initialize pre-commit, run:

```bash
pip install pre-commit
pre-commit install
```

To resolve CI errors locally, you can also manually run pre-commit by:

```bash
pre-commit run
```

### Adding CI tests

If possible, please add CI test(s) for your new feature:

1. Find the most relevant workflow yml file, which usually corresponds to a `hydra` default config (e.g. `ppo_trainer`, `ppo_megatron_trainer`, `sft_trainer`, etc).
2. Add related path patterns to the `paths` section if not already included.
3. Minimize the workload of the test script(s) (see existing scripts for examples).

We are HIRING! Send us an [email](https://verl.readthedocs.io/en/latest/) if you are interested in internship/FTE opportunities in MLSys/LLM reasoning/multimodal alignment.