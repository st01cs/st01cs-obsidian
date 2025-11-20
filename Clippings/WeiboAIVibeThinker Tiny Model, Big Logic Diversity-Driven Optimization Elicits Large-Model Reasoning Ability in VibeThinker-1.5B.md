---
title: "WeiboAI/VibeThinker: Tiny Model, Big Logic: Diversity-Driven Optimization Elicits Large-Model Reasoning Ability in VibeThinker-1.5B"
source: "https://github.com/WeiboAI/VibeThinker"
author:
  - "[[GitHub]]"
published:
created: 2025-11-14
description: "Tiny Model, Big Logic: Diversity-Driven Optimization Elicits Large-Model Reasoning Ability in VibeThinker-1.5B - WeiboAI/VibeThinker"
tags:
  - "clippings"
---
微博AI开源 VibeThinker-1.5B：小模型也可以有大智慧  
目前业界最强大模型参数量大都超过了1T，甚至出现了2T规模的模型，是否只有巨量参数模型才有高度的智能？是否只有少量科技巨头才有能力做大模型？  
  
VibeThinker-1.5B，正是微博AI对此问题给出的否定答案，它证明了小模型也可以有高智商。这意味着做最强大模型不再像传统观念以为的那样主要依赖推高参数量，也可以通过巧妙的算法设计来做到这一点。  
  
这款模型仅有1.5B(15亿)参数，经过微博AI研发人员提出的创新“频谱到信号原理”（SSP）方法训练后，其效果堪称颠覆：VibeThinker在AIME24、AIME25以及HMMT25三个高难度数学测试集上的表现，超越了参数量超其400倍的模型DeepSeek-R1-0120版本（模型大小671B），与规模为456B的MiniMax-M1效果接近或相当；在LiveCodeBench v6（编程算法题测试集）中的成绩，成功追平参数量数超其数十倍的模型，比如欧洲领先AI企业Minstral.AI的深度思考模型Magistral-Medium-2506版本。  
  
VibeThinker能力强大不靠堆参数，而是源于微博研发人员提出的SSP训练理念，即在学习阶段先鼓励模型发散探索所有可能的解题路径，而非一味关注正确率；随后，通过强化学习进行高效策略优化，精准锁定正确路径，将模型性能提升至极致。  
  
模型的单次“后训练”（Post-Training）成本不足8000美元，与此对应，DeepSeek-R1和MiniMax-M1的后训练成本分别是29万及53万美元，降低了几十倍。  
  
VibeThinker-1.5B的开源，旨在为全球计算资源有限的中型企业及高校研究团队，提供一条高性价比的研发新路径，使得人人都可以训练最前沿的大模型，而不是像之前一样被排斥在外，这对于业界技术进步至关重要。

Tiny Model, Big Logic: Diversity-Driven Optimization Elicits Large-Model Reasoning Ability in VibeThinker-1.5B

[MIT license](https://github.com/WeiboAI/VibeThinker/blob/main/LICENSE)

[Open in github.dev](https://github.dev/) [Open in a new github.dev tab](https://github.dev/) [Open in codespace](https://github.com/codespaces/new/WeiboAI/VibeThinker?resume=1)

<table><thead><tr><th colspan="2"><span>Name</span></th><th colspan="1"><span>Name</span></th><th><p><span>Last commit message</span></p></th><th colspan="1"><p><span>Last commit date</span></p></th></tr></thead><tbody><tr><td colspan="3"><p><span><a href="https://github.com/WeiboAI/VibeThinker/commit/47bec8a977510d5abc26d8f45ad39af843425a01">Add.gitignore to ignore.DS_Store files</a></span></p><p><span><a href="https://github.com/WeiboAI/VibeThinker/commit/47bec8a977510d5abc26d8f45ad39af843425a01">47bec8a</a> ·</span></p><p><a href="https://github.com/WeiboAI/VibeThinker/commits/main/"><span><span><span>50 Commits</span></span></span></a></p></td></tr><tr><td colspan="2"><p><a href="https://github.com/WeiboAI/VibeThinker/tree/main/eval">eval</a></p></td><td colspan="1"><p><a href="https://github.com/WeiboAI/VibeThinker/tree/main/eval">eval</a></p></td><td><p><a href="https://github.com/WeiboAI/VibeThinker/commit/54a599be0834b3a02d7cf8c6af4009eb4cb4ac2a">Remove existing.DS_Store files from tracking</a></p></td><td></td></tr><tr><td colspan="2"><p><a href="https://github.com/WeiboAI/VibeThinker/tree/main/figures">figures</a></p></td><td colspan="1"><p><a href="https://github.com/WeiboAI/VibeThinker/tree/main/figures">figures</a></p></td><td><p><a href="https://github.com/WeiboAI/VibeThinker/commit/86435589e866835166bb3b4cd7ec85929c926c89">update figure</a></p></td><td></td></tr><tr><td colspan="2"><p><a href="https://github.com/WeiboAI/VibeThinker/blob/main/.gitignore">.gitignore</a></p></td><td colspan="1"><p><a href="https://github.com/WeiboAI/VibeThinker/blob/main/.gitignore">.gitignore</a></p></td><td><p><a href="https://github.com/WeiboAI/VibeThinker/commit/47bec8a977510d5abc26d8f45ad39af843425a01">Add.gitignore to ignore.DS_Store files</a></p></td><td></td></tr><tr><td colspan="2"><p><a href="https://github.com/WeiboAI/VibeThinker/blob/main/LICENSE">LICENSE</a></p></td><td colspan="1"><p><a href="https://github.com/WeiboAI/VibeThinker/blob/main/LICENSE">LICENSE</a></p></td><td><p><a href="https://github.com/WeiboAI/VibeThinker/commit/7c4b892f6e9fc99854d26ae748cbc8732de89bfd">Initial commit</a></p></td><td></td></tr><tr><td colspan="2"><p><a href="https://github.com/WeiboAI/VibeThinker/blob/main/README.md">README.md</a></p></td><td colspan="1"><p><a href="https://github.com/WeiboAI/VibeThinker/blob/main/README.md">README.md</a></p></td><td><p><a href="https://github.com/WeiboAI/VibeThinker/commit/eba5715b2933a626793408634034374ece61fef7">add news</a></p></td><td></td></tr><tr><td colspan="2"><p><a href="https://github.com/WeiboAI/VibeThinker/blob/main/VibeThinker-1.5B.pdf">VibeThinker-1.5B.pdf</a></p></td><td colspan="1"><p><a href="https://github.com/WeiboAI/VibeThinker/blob/main/VibeThinker-1.5B.pdf">VibeThinker-1.5B.pdf</a></p></td><td><p><a href="https://github.com/WeiboAI/VibeThinker/commit/34ac7a3f0034379da3ca93fde9a678c7b3e83afd">251107</a></p></td><td></td></tr><tr><td colspan="3"></td></tr></tbody></table>

## VibeThinker

[![](https://github.com/WeiboAI/VibeThinker/raw/main/figures/logo.png)](https://github.com/WeiboAI/VibeThinker/blob/main/figures/logo.png)

🤗 [Hugging Face](https://huggingface.co/WeiboAI) | 🤖 [Model Scope](https://modelscope.cn/organization/WeiboAI)   | 📄 [Techical Report](https://huggingface.co/papers/2511.06221) | 🏆 [arxiv paper](https://arxiv.org/abs/2511.06221)

## Introduction

VibeThinker-1.5B is a 1.5B-parameter dense model that challenges the prevailing notion that small models inherently lack robust reasoning capabilities. Developed with an innovative post-training methodology centered on the **"Spectrum-to-Signal Principle (SSP)"**, VibeThinker-1.5B demonstrates superior reasoning capabilities compared to closed-source models Magistral Medium and Claude Opus 4, while achieving performance on par with open-source models like GPT OSS-20B Medium.

Most remarkably, VibeThinker-1.5B surpasses the initial DeepSeek R1 model—which is over 400 times larger—across three challenging mathematical benchmarks: AIME24 (80.3 vs. 79.8), AIME25 (74.4 vs. 70.0), and HMMT25 (50.4 vs. 41.7).

[![](https://github.com/WeiboAI/VibeThinker/raw/main/figures/vibethinker_eval2.png)](https://github.com/WeiboAI/VibeThinker/blob/main/figures/vibethinker_eval2.png)

## News

\[2025.11.11\] 🎉🎉🎉 VibeThinker-1.5B is now open source! The model weights and technical report can be accessed via the links at the top.

\[2025.11.05\] 📢📢📢 VibeThinker-1.5B will be open-sourced soon. Stay tuned!

## Key Features

- **Ultra-Efficient**: VibeThinker-1.5B redefines the efficiency frontier for reasoning models, achieving state-of-the-art performance in mathematical and coding tasks with only 1.5B parameters—100× to 600× smaller than giants like Kimi K2 (1000B+) and DeepSeek R1(671B).

[![](https://github.com/WeiboAI/VibeThinker/raw/main/figures/am25_1.5B.png)](https://github.com/WeiboAI/VibeThinker/blob/main/figures/am25_1.5B.png)

- **Innovative Methodology**: We propose an innovative post-training technique centered on the “Spectrum-to-Signal Principle (SSP)”. This framework systematically enhances output diversity by first employing a “Two-Stage Diversity-Exploring Distillation” in the SFT phase to generate a broad spectrum of solutions, followed by the “MaxEnt-Guided Policy Optimization (MGPO)” framework in the RL phase to amplify the correct signal.

[![](https://github.com/WeiboAI/VibeThinker/raw/main/figures/technicalArchitecture1.png)](https://github.com/WeiboAI/VibeThinker/blob/main/figures/technicalArchitecture1.png)

- **Outstanding Capabilities**: Despite a substantial parameter gap—competing with models 10 to hundreds of times larger—our 1.5B model demonstrates remarkable performance. On the AIME24, AIME25, and HMMT25 benchmarks, it surpasses open-source contenders like DeepSeek R1-0120 and GPT-OSS-20B-Medium, while achieving results comparable to MiniMax-M1.

[![](https://github.com/WeiboAI/VibeThinker/raw/main/figures/Performence1.png)](https://github.com/WeiboAI/VibeThinker/blob/main/figures/Performence1.png)

- **Cost-Effective**: While state-of-the-art models like DeepSeek R1 and MiniMax-M1 incur post-training costs of $294K and $535K respectively, our approach achieves this for just $7,800. This represents a reduction by a factor of “30 to 60”, fundamentally changing the economics of developing high-performance reasoning models.

[![](https://github.com/WeiboAI/VibeThinker/raw/main/figures/Cost.png)](https://github.com/WeiboAI/VibeThinker/blob/main/figures/Cost.png)

## Model Downloads

The model checkpoint is available at: [Hugging Face](https://huggingface.co/WeiboAI/VibeThinker-1.5B) and [ModelScope](https://modelscope.cn/models/WeiboAI/VibeThinker-1.5B).

## Eval

If you wish to reproduce the results reported in our technical report, the evaluation program and usage guide have been prepared and are available at the following links.: [Math Eval](https://github.com/WeiboAI/VibeThinker/blob/main/eval/math/README.md) and [Code Eval](https://github.com/WeiboAI/VibeThinker/blob/main/eval/code/README.md).

Sample responses from some benchmarks:[here](https://drive.google.com/drive/folders/1qom754QSjujDI98Wv8LIKTaTszPkAN6q?usp=drive_link).

## Usage Guidelines

**We recommend using this model for competitive-style math and coding problems.**

To facilitate quick verification by the community, we recommend the following parameter settings: **temperature: 0.6 or 1.0, max token length: 40960, top\_p: 0.95, top\_k: -1.**

## Quick Start

Required: **transformers>=4.54.0**

Recommended for better inference performance: **vLLM==0.10.1 or SGLang>=0.4.9.post6**

Here is a code snippet to show you how to use the chat model with transformers:

```
from transformers import AutoModelForCausalLM, AutoTokenizer, GenerationConfig

class VibeThinker:
    def __init__(self, model_path):
        self.model_path = model_path
        self.model = AutoModelForCausalLM.from_pretrained(
            self.model_path,
            low_cpu_mem_usage=True,
            torch_dtype="bfloat16",
            device_map="auto"
        )
        self.tokenizer = AutoTokenizer.from_pretrained(self.model_path, trust_remote_code=True)

    def infer_text(self, prompt):
        messages = [
            {"role": "user", "content": prompt}
        ]
        text = self.tokenizer.apply_chat_template(messages, tokenize=False, add_generation_prompt=True)
        model_inputs = self.tokenizer([text], return_tensors="pt").to(self.model.device)

        text = self.tokenizer.apply_chat_template(
            messages,
            tokenize=False,
            add_generation_prompt=True
        )
        model_inputs = self.tokenizer([text], return_tensors="pt").to(self.model.device)

        generation_config = dict(
            max_new_tokens=40960,
            do_sample=True,
            temperature=0.6, # 0.6 or 1.0, you can set it according to your needs
            top_p=0.95,
            top_k=None # in vLLM or SGlang, please set top_k to -1, it means skip top_k for sampling
        )
        generated_ids = self.model.generate(
            **model_inputs,
            generation_config=GenerationConfig(**generation_config)
        )
        generated_ids = [
            output_ids[len(input_ids):] for input_ids, output_ids in zip(model_inputs.input_ids, generated_ids)
        ]

        response = self.tokenizer.batch_decode(generated_ids, skip_special_tokens=True)[0]

        return response

if __name__ == '__main__':
    model = VibeThinker('Your model path')
    prompt = 'Your Prompt'
    print(model.infer_text(prompt))
```

## License

This code repository is licensed under [the MIT License](https://github.com/WeiboAI/VibeThinker/blob/main/LICENSE).

## Citations

If you use VibeThinker in your research or product, please cite:

```
@misc{xu2025tinymodelbiglogic,
      title={Tiny Model, Big Logic: Diversity-Driven Optimization Elicits Large-Model Reasoning Ability in VibeThinker-1.5B}, 
      author={Sen Xu and Yi Zhou and Wei Wang and Jixin Min and Zhibin Yin and Yingwei Dai and Shixi Liu and Lianyu Pang and Yirong Chen and Junlin Zhang},
      year={2025},
      eprint={2511.06221},
      archivePrefix={arXiv},
      primaryClass={cs.AI},
      url={https://arxiv.org/abs/2511.06221}, 
}
```

## Releases

No releases published

## Packages

No packages published  

## Languages

- [Python 91.9%](https://github.com/WeiboAI/VibeThinker/search?l=python)
- [Shell 8.1%](https://github.com/WeiboAI/VibeThinker/search?l=shell)