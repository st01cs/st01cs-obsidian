---
title: "langgptai/LangGPT: LangGPT: Empowering everyone to become a prompt expert! 🚀  📌 结构化提示词（Structured Prompt）提出者 📌 元提示词（Meta-Prompt）发起者   📌 最流行的提示词落地范式 | Language of GPT  The pioneering framework for structured & meta-prompt design 10,000+ ⭐ | Battle-tested by thousands of users worldwide  Created by 云中江树"
source: "https://github.com/langgptai/LangGPT?tab=readme-ov-file"
author:
  - "[[yzfly]]"
published:
created: 2025-11-19
description: "LangGPT: Empowering everyone to become a prompt expert! 🚀  📌 结构化提示词（Structured Prompt）提出者 📌 元提示词（Meta-Prompt）发起者   📌 最流行的提示词落地范式 | Language of GPT  The pioneering framework for structured & meta-prompt design 10,000+ ⭐ | Battle-tested by thousands of users worldwide  Created by 云中江树 - langgptai/LangGPT"
tags:
  - "clippings"
---
**[LangGPT](https://github.com/langgptai/LangGPT)** Public

LangGPT: Empowering everyone to become a prompt expert! 🚀 📌 结构化提示词（Structured Prompt）提出者 📌 元提示词（Meta-Prompt）发起者 📌 最流行的提示词落地范式 | Language of GPT The pioneering framework for structured & meta-prompt design 10,000+ ⭐ | Battle-tested by thousands of users worldwide Created by 云中江树

[github.com/langgptai](https://github.com/langgptai "https://github.com/langgptai")

[Apache-2.0 license](https://github.com/langgptai/LangGPT/blob/main/LICENSE)

[Open in github.dev](https://github.dev/) [Open in a new github.dev tab](https://github.dev/) [Open in codespace](https://github.com/codespaces/new/langgptai/LangGPT?resume=1)

---

**LangGPT is a structured, reusable prompt design framework** that enables anyone to create high-quality prompts for Large Language Models. Think of it as a **"programming language for prompts"** — systematic, template-based, and infinitely scalable.

### Why LangGPT?

Traditional prompt engineering relies on scattered tips and trial-and-error. LangGPT transforms this chaos into a structured methodology:

- 🎯 **Structured Templates** — Hierarchical organization inspired by programming paradigms
- 🔄 **Reusability** — Create once, adapt infinitely like code modules
- 📦 **Modularity** — Variables, commands, and conditional logic at your fingertips
- ⚡ **Efficiency** — Go from idea to working prompt in minutes
- 🌍 **Community-Driven** — 11,000+ stars, battle-tested by thousands of users

> **Academic Foundation**: Published research at [arXiv:2402.16929](https://arxiv.org/abs/2402.16929) | [中文版](https://github.com/langgptai/LangGPT/blob/main/Papers/LangGPT_paper_cn.md)

---

Let AI create prompts for you:

- **[LangGPT GPTs](https://chat.openai.com/g/g-Apzuylaqk-langgpt)** — Full-featured generator (GPT-4)
- **[Kimi+ LangGPT](https://kimi.moonshot.cn/kimiplus/conpg00t7lagbbsfqkq0)** — For Moonshot Kimi users
- **[PromptGPT](https://chat.openai.com/g/g-YKe3gmydD-promptgpt)** — Lite version (GPT-3.5)

Basic LangGPT structure:

```
# Role: Your_Role_Name

## Profile
- Author: YourName
- Version: 1.0
- Language: English
- Description: Clear role description and core capabilities

## Goal
- Outcome: What concrete result/outcome should be delivered for the user/session
- Done Criteria: Clear acceptance criteria (how we know it’s finished and good)
- Non-Goals: What is explicitly out of scope to avoid scope creep

### Skill-1
1. Specific skill description
2. Expected behavior and output

## Rules
1. Don't break character under any circumstance
2. Don't make up facts or hallucinate

## Workflow
1. Analyze user input and identify intent
2. Apply relevant skills systematically
3. Deliver structured, actionable output

## Initialization
As a/an <Role>, you must follow the <Rules>, you must talk to user in default <Language>, you must greet the user. Then introduce yourself and introduce the <Workflow>.
```

**Prerequisites**: Basic Markdown knowledge ([Quick Guide](https://docs.github.com/en/get-started/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax)) | GPT-4 or Claude recommended

Explore our [example library](https://langgptai.feishu.cn/wiki/RXdbwRyASiShtDky381ciwFEnpe) and adapt proven templates to your needs.

---

Before diving into tactics, understand the principles. These essays explore the philosophy behind effective prompting:

- **[对话动力学](https://github.com/langgptai/LangGPT/blob/main/Docs/%E5%AF%B9%E8%AF%9D%E5%8A%A8%E5%8A%9B%E5%AD%A6.md)** — The dynamics of human-AI dialogue
- **[五种理性](https://github.com/langgptai/LangGPT/blob/main/Docs/%E4%BA%94%E7%A7%8D%E7%90%86%E6%80%A7.md)** — Five types of rationality in prompt design
- **[镜像性倾向](https://github.com/langgptai/LangGPT/blob/main/Docs/%E9%95%9C%E5%83%8F%E6%80%A7%E5%80%BE%E5%90%91.md)** — Mirror tendencies in LLM behavior
- **[统计重力井和边缘表达](https://github.com/langgptai/LangGPT/blob/main/Docs/%E7%BB%9F%E8%AE%A1%E9%87%8D%E5%8A%9B%E4%BA%95%E5%92%8C%E8%BE%B9%E7%BC%98%E8%A1%A8%E8%BE%BE.md)** — Statistical gravity well and edge expression
- **[关系表达](https://github.com/langgptai/LangGPT/blob/main/Docs/%E5%85%B3%E7%B3%BB%E8%A1%A8%E8%BE%BE.md)** — Expressing relationships in prompts
- **[看见与言说](https://github.com/langgptai/LangGPT/blob/main/Docs/%E7%9C%8B%E8%A7%81%E4%B8%8E%E8%A8%80%E8%AF%B4.md)** — Seeing and articulation in AI interaction
- **[Prompt 的本质](https://github.com/langgptai/LangGPT/blob/main/Docs/Prompt%E7%9A%84%E6%9C%AC%E8%B4%A8.md)** — The essence and nature of prompts
- **[面向结果的提示词写作方法](https://github.com/langgptai/LangGPT/blob/main/Docs/%E9%9D%A2%E5%90%91%E7%BB%93%E6%9E%9C%E7%9A%84%E6%8F%90%E7%A4%BA%E8%AF%8D%E5%86%99%E4%BD%9C%E6%96%B9%E6%B3%95.md)** — Writing prompts that focus on achieving desired outcomes
- **[AI意识](https://github.com/langgptai/LangGPT/blob/main/Docs/AI%E6%84%8F%E8%AF%86.md)** — Understanding the role of AI in human-AI interaction
- **[AI时代的新管理：机器负责优化，人类定义应该](https://github.com/langgptai/LangGPT/blob/main/Docs/AI%E6%97%B6%E4%BB%A3%E7%9A%84%E6%96%B0%E7%AE%A1%E7%90%86%EF%BC%9A%E6%9C%BA%E5%99%A8%E8%B4%9F%E8%B4%A3%E4%BC%98%E5%8C%96%EF%BC%8C%E4%BA%BA%E7%B1%BB%E5%AE%9A%E4%B9%89%E5%BA%94%E8%AF%A5.md)** — The new management in the AI era: machines optimize, humans define the criteria

*These foundational insights will transform how you think about prompts.*

---

Define AI personas through clear, modular sections:

| Section | Purpose | Example |
| --- | --- | --- |
| **Role** | Role name/title | "逻辑学家" / "Expert Analyst" / "FitnessGPT" |
| **Profile** | Identity and capabilities | "Expert Python developer with 10 years experience" |
| **Goal** | Desired outcome, done criteria, and non-goals for this session/task | “Refactor a prompt into a reusable template; acceptance criteria: pass three structured checks; non-goal: rewriting the business logic.” |
| **Skills** | Specific abilities | "Debug complex code, optimize performance" |
| **Rules** | Boundaries and constraints | "Never execute destructive commands" |
| **Workflow** | Interaction logic | "1. Analyze → 2. Plan → 3. Execute" |
| **Initialization** | Opening message and setup | "As a, I will greet you and introduce the " |

Use `<Variable>` syntax for dynamic content:

```
As a <Role>, you must follow <Rules> and communicate in <Language>
```

This creates self-referential prompts that maintain consistency across complex instructions.

### 3\. Commands

Define reusable actions for better UX:

```
## Commands
- Prefix: "/"
- Commands:
    - help: Display all available commands
    - continue: Resume interrupted output
    - improve: Enhance current response with deeper analysis
```

Add intelligence to your prompts:

```
If user provides [code], then analyze and suggest improvements
Else if user asks [question], then provide detailed explanation
Else, prompt for clarification
```

**Reminders** — Combat context loss in long conversations:

```
## Reminder
1. Always check role settings before responding
2. Current language: <Language>, Active rules: <Rules>
```

**Alternative Formats** — Use JSON/YAML when markdown isn't ideal:

```
role: DataAnalyst
profile:
  version: "2.0"
  language: "Python"
skills:
  - statistical_analysis
  - data_visualization
```

---

| Prompt | Description | Link |
| --- | --- | --- |
| 🎯 **FitnessGPT** | Personalized diet and workout planner | [View](https://github.com/langgptai/LangGPT/blob/main/examples/FitnessGPT.md) |
| 💻 **Code Master CAN** | Advanced coding assistant with debugging expertise | [View](https://github.com/langgptai/LangGPT/blob/main/examples/code_anything_now/ChatGPT-Code_Anything_Now_en.md) |
| ✍️ **Xiaohongshu Writer** | Viral social media content generator | [View](https://github.com/langgptai/LangGPT/blob/main/examples/chinese_xiaohongshu_writer) |
| 🎨 **Chinese Poet** | Classical poetry composer in traditional styles | [View](https://github.com/langgptai/LangGPT/blob/main/examples/chinese_poet) |

[Browse 100+ more examples →](https://langgptai.feishu.cn/wiki/RXdbwRyASiShtDky381ciwFEnpe)

---

### Essential Guides

| Resource | Description | Date |
| --- | --- | --- |
| [Academic Paper](https://arxiv.org/abs/2402.16929) | LangGPT: Rethinking Structured Reusable Prompt Design ([中文](https://github.com/langgptai/LangGPT/blob/main/Papers/LangGPT_paper_cn.md)) | Feb 2024 |
| [Structured Prompts Guide](https://github.com/langgptai/LangGPT/blob/main/Docs/HowToWritestructuredPrompts.md) | Comprehensive tutorial on building high-performance prompts | Jul 2023 |
| [Prompt Chains](https://github.com/langgptai/LangGPT/blob/main/Docs/PromptChain.md) | Multi-prompt collaboration and task decomposition strategies | Aug 2023 |
| [Video Tutorial](https://www.bilibili.com/video/BV1rj411q78a) | BiliBili walkthrough (by AIGCLINK) | Sep 2023 |

### Advanced Topics

- **[推理模型提示方法变革](https://mp.weixin.qq.com/s/FLY0sy1jYv6eT9151Yz_jw)** — Paradigm shift from procedural to goal-oriented prompting
- **[提示词的道和术](https://langgptai.feishu.cn/wiki/AYMWwBPaSih46WkAo9jcfKkfntg)** — Philosophy and practice of prompt engineering by 李继刚
- **[企业级提示词工程](https://langgptai.feishu.cn/wiki/UTyswvusTiRw0TkZLI5cIG0Tnhc)** — Building production-ready prompt systems (百川智能)
- **[多模态提示词](https://mp.weixin.qq.com/s/Aan9NXO_vEZ9h0YrugpoGQ)** — GPT-4V and multi-modal prompting techniques
- **[提示词攻击与防护](https://mp.weixin.qq.com/s/aaABXnxRqDF716qRk79wYQ)** — Security: prompt injection, jailbreaks, and defenses
- **[大模型绘画指南](https://mp.weixin.qq.com/s/bJbZ9bwPXxlpyREqLKhDvA)** — AI image generation with structured prompts

### Community Hub

**[Feishu Knowledge Base](http://feishu.langgpt.ai/)** — Curated resources, templates, and community contributions

---

| Project | Description | Stars |
| --- | --- | --- |
| **[LangGPT](https://github.com/langgptai/LangGPT)** | Core framework and methodology |  |
| **[PromptVer](https://github.com/langgptai/PromptVer)** | Semantic versioning for prompts — version control like Git | [![](https://camo.githubusercontent.com/2dfe7e28cb09ab93bf27087f6b879fb7dee2c4925a4b177971586e3ca3163f3c/68747470733a2f2f62616467656e2e6e65742f6769746875622f73746172732f6c616e6767707461692f50726f6d7074566572)](https://camo.githubusercontent.com/2dfe7e28cb09ab93bf27087f6b879fb7dee2c4925a4b177971586e3ca3163f3c/68747470733a2f2f62616467656e2e6e65742f6769746875622f73746172732f6c616e6767707461692f50726f6d7074566572) |
| **[PromptShow](https://github.com/langgptai/PromptShow)** | Create beautiful prompt images ([Try it](https://show.langgpt.ai/)) | [![](https://camo.githubusercontent.com/3cbc6af757cf35940fea436e8a4d4172c7906c4a6793735732aa72209f02cc47/68747470733a2f2f62616467656e2e6e65742f6769746875622f73746172732f6c616e6767707461692f50726f6d707453686f77)](https://camo.githubusercontent.com/3cbc6af757cf35940fea436e8a4d4172c7906c4a6793735732aa72209f02cc47/68747470733a2f2f62616467656e2e6e65742f6769746875622f73746172732f6c616e6767707461692f50726f6d707453686f77) |
| **[Minstrel](https://github.com/langgptai/Minstrel)** | Multi-agent system for auto-generating prompts | [![](https://camo.githubusercontent.com/dfab518ce1c269b8691303e2369cb73e4fa9878e05c9b85bc6b9974c9395061f/68747470733a2f2f62616467656e2e6e65742f6769746875622f73746172732f6c616e6767707461692f4d696e737472656c)](https://camo.githubusercontent.com/dfab518ce1c269b8691303e2369cb73e4fa9878e05c9b85bc6b9974c9395061f/68747470733a2f2f62616467656e2e6e65742f6769746875622f73746172732f6c616e6767707461692f4d696e737472656c) |

Rather than writing prompts as procedures, write the persona. Writing prompts as procedures gives the model steps and tools. Writing prompts as a persona gives the model a worldview, motivations, a value system, and a preference profile. Below are prompts that Yunzhong Jiangshu wrote while studying some well-known figures.

- [巴菲特AI分身](https://github.com/langgptai/LangGPT/blob/main/Prompts/%E5%B7%B4%E8%8F%B2%E7%89%B9AI%E5%88%86%E8%BA%AB.md)
- [梵高AI分身](https://github.com/langgptai/LangGPT/blob/main/Prompts/%E6%A2%B5%E9%AB%98AI%E5%88%86%E8%BA%AB.md)
- [马斯克AI分身](https://github.com/langgptai/LangGPT/blob/main/Prompts/%E9%A9%AC%E6%96%AF%E5%85%8BAI%E5%88%86%E8%BA%AB.md)
- [段永平AI分身](https://github.com/langgptai/LangGPT/blob/main/Prompts/%E6%AE%B5%E6%B0%B8%E5%B9%B3AI%E5%88%86%E8%BA%AB.md)

Curated, optimized prompts for different AI models:

| Collection | Target Model | Stars |
| --- | --- | --- |
| [wonderful-prompts](https://github.com/langgptai/wonderful-prompts) | ChatGPT (Chinese) | [![](https://camo.githubusercontent.com/0db4b86a6e3f6817737c9b002f6e88cd0f317a85df723358fc7747e0fa19c518/68747470733a2f2f62616467656e2e6e65742f6769746875622f73746172732f6c616e6767707461692f776f6e64657266756c2d70726f6d707473)](https://camo.githubusercontent.com/0db4b86a6e3f6817737c9b002f6e88cd0f317a85df723358fc7747e0fa19c518/68747470733a2f2f62616467656e2e6e65742f6769746875622f73746172732f6c616e6767707461692f776f6e64657266756c2d70726f6d707473) |
| [awesome-claude-prompts](https://github.com/langgptai/awesome-claude-prompts) | Anthropic Claude | [![](https://camo.githubusercontent.com/9db8dac561f7fbf2844cc9d735dd579ccaf9b3680ab8b3d4d9ace919d017de30/68747470733a2f2f62616467656e2e6e65742f6769746875622f73746172732f6c616e6767707461692f617765736f6d652d636c617564652d70726f6d707473)](https://camo.githubusercontent.com/9db8dac561f7fbf2844cc9d735dd579ccaf9b3680ab8b3d4d9ace919d017de30/68747470733a2f2f62616467656e2e6e65742f6769746875622f73746172732f6c616e6767707461692f617765736f6d652d636c617564652d70726f6d707473) |
| [awesome-deepseek-prompts](https://github.com/langgptai/awesome-deepseek-prompts) | DeepSeek & R1 | [![](https://camo.githubusercontent.com/11d2f4f69e68dcd99cad65e119d08e5885e76cb89516fd30fc164cfcbd9448c1/68747470733a2f2f62616467656e2e6e65742f6769746875622f73746172732f6c616e6767707461692f617765736f6d652d646565707365656b2d70726f6d707473)](https://camo.githubusercontent.com/11d2f4f69e68dcd99cad65e119d08e5885e76cb89516fd30fc164cfcbd9448c1/68747470733a2f2f62616467656e2e6e65742f6769746875622f73746172732f6c616e6767707461692f617765736f6d652d646565707365656b2d70726f6d707473) |
| [awesome-gemini-prompts](https://github.com/langgptai/awesome-gemini-prompts) | Google Gemini | [![](https://camo.githubusercontent.com/bb06d7d1e2eac4008f047b9129cd963716134e7e6149392e563e3ac7600ae639/68747470733a2f2f62616467656e2e6e65742f6769746875622f73746172732f6c616e6767707461692f617765736f6d652d67656d696e692d70726f6d707473)](https://camo.githubusercontent.com/bb06d7d1e2eac4008f047b9129cd963716134e7e6149392e563e3ac7600ae639/68747470733a2f2f62616467656e2e6e65742f6769746875622f73746172732f6c616e6767707461692f617765736f6d652d67656d696e692d70726f6d707473) |
| [awesome-grok-prompts](https://github.com/langgptai/awesome-grok-prompts) | xAI Grok | [![](https://camo.githubusercontent.com/91e6a7281445295a355cd90000ea8aa327a8d35f453880dc7aef6dce56f85f8c/68747470733a2f2f62616467656e2e6e65742f6769746875622f73746172732f6c616e6767707461692f617765736f6d652d67726f6b2d70726f6d707473)](https://camo.githubusercontent.com/91e6a7281445295a355cd90000ea8aa327a8d35f453880dc7aef6dce56f85f8c/68747470733a2f2f62616467656e2e6e65742f6769746875622f73746172732f6c616e6767707461692f617765736f6d652d67726f6b2d70726f6d707473) |
| [qwen-prompts](https://github.com/langgptai/qwen-prompts) | Alibaba Qwen | [![](https://camo.githubusercontent.com/c9f433e6e51605d3f11923dab42bc216d69442b66579ee7dab53eb0ec9ae8e7d/68747470733a2f2f62616467656e2e6e65742f6769746875622f73746172732f6c616e6767707461692f7177656e2d70726f6d707473)](https://camo.githubusercontent.com/c9f433e6e51605d3f11923dab42bc216d69442b66579ee7dab53eb0ec9ae8e7d/68747470733a2f2f62616467656e2e6e65742f6769746875622f73746172732f6c616e6767707461692f7177656e2d70726f6d707473) |
| [awesome-llama-prompts](https://github.com/langgptai/awesome-llama-prompts) | Meta Llama 2/3 | [![](https://camo.githubusercontent.com/c733751336f6de60db940c4f098b6c93aee4459545cf308ec7e4b31cb40d1c22/68747470733a2f2f62616467656e2e6e65742f6769746875622f73746172732f6c616e6767707461692f617765736f6d652d6c6c616d612d70726f6d707473)](https://camo.githubusercontent.com/c733751336f6de60db940c4f098b6c93aee4459545cf308ec7e4b31cb40d1c22/68747470733a2f2f62616467656e2e6e65742f6769746875622f73746172732f6c616e6767707461692f617765736f6d652d6c6c616d612d70726f6d707473) |
| [awesome-doubao-prompts](https://github.com/langgptai/awesome-doubao-prompts) | ByteDance Doubao | [![](https://camo.githubusercontent.com/789390a80e331e29001125a1c76befc3f9a05b767f68b3a8ac7c6d606383f460/68747470733a2f2f62616467656e2e6e65742f6769746875622f73746172732f6c616e6767707461692f617765736f6d652d646f7562616f2d70726f6d707473)](https://camo.githubusercontent.com/789390a80e331e29001125a1c76befc3f9a05b767f68b3a8ac7c6d606383f460/68747470733a2f2f62616467656e2e6e65742f6769746875622f73746172732f6c616e6767707461692f617765736f6d652d646f7562616f2d70726f6d707473) |
| [awesome-system-prompts](https://github.com/langgptai/awesome-system-prompts) | System prompts from AI tools | [![](https://camo.githubusercontent.com/a573c27884af115dd6ba786e93cd5c877b2374d3c5a07ceeac4048c13220ecdb/68747470733a2f2f62616467656e2e6e65742f6769746875622f73746172732f6c616e6767707461692f617765736f6d652d73797374656d2d70726f6d707473)](https://camo.githubusercontent.com/a573c27884af115dd6ba786e93cd5c877b2374d3c5a07ceeac4048c13220ecdb/68747470733a2f2f62616467656e2e6e65742f6769746875622f73746172732f6c616e6767707461692f617765736f6d652d73797374656d2d70726f6d707473) |

### Specialized Domains

| Repository | Focus Area | Stars |
| --- | --- | --- |
| [Awesome-Multimodal-Prompts](https://github.com/langgptai/Awesome-Multimodal-Prompts) | GPT-4V, DALL-E 3, image/video prompts | [![](https://camo.githubusercontent.com/61ec4223a6d79fc7d8850cea38970b49dd232d7549e5606ad2946f3675e68d99/68747470733a2f2f62616467656e2e6e65742f6769746875622f73746172732f6c616e6767707461692f417765736f6d652d4d756c74696d6f64616c2d50726f6d707473)](https://camo.githubusercontent.com/61ec4223a6d79fc7d8850cea38970b49dd232d7549e5606ad2946f3675e68d99/68747470733a2f2f62616467656e2e6e65742f6769746875622f73746172732f6c616e6767707461692f417765736f6d652d4d756c74696d6f64616c2d50726f6d707473) |
| [deep-research-prompts](https://github.com/langgptai/deep-research-prompts) | Deep research across models | [![](https://camo.githubusercontent.com/7e9c81b8e97f0bdac2fb551e87bd4690a9f1c4c0b5b4d331c128bec1de3705b3/68747470733a2f2f62616467656e2e6e65742f6769746875622f73746172732f6c616e6767707461692f646565702d72657365617263682d70726f6d707473)](https://camo.githubusercontent.com/7e9c81b8e97f0bdac2fb551e87bd4690a9f1c4c0b5b4d331c128bec1de3705b3/68747470733a2f2f62616467656e2e6e65742f6769746875622f73746172732f6c616e6767707461692f646565702d72657365617263682d70726f6d707473) |
| [awesome-voice-prompts](https://github.com/langgptai/awesome-voice-prompts) | Voice AI and conversational agents | [![](https://camo.githubusercontent.com/b788e31a859f663391bb795a95b169f3e4688fee3ec5c957c85c0a0ccecbdec1/68747470733a2f2f62616467656e2e6e65742f6769746875622f73746172732f6c616e6767707461692f617765736f6d652d766f6963652d70726f6d707473)](https://camo.githubusercontent.com/b788e31a859f663391bb795a95b169f3e4688fee3ec5c957c85c0a0ccecbdec1/68747470733a2f2f62616467656e2e6e65742f6769746875622f73746172732f6c616e6767707461692f617765736f6d652d766f6963652d70726f6d707473) |
| [GraphRAG-Prompts](https://github.com/langgptai/GraphRAG-Prompts) | Graph-based retrieval prompts | [![](https://camo.githubusercontent.com/85e3d675504506899c4461f79e1ae68ee5cca42deb862952a92cd1718975cfbf/68747470733a2f2f62616467656e2e6e65742f6769746875622f73746172732f6c616e6767707461692f47726170685241472d50726f6d707473)](https://camo.githubusercontent.com/85e3d675504506899c4461f79e1ae68ee5cca42deb862952a92cd1718975cfbf/68747470733a2f2f62616467656e2e6e65742f6769746875622f73746172732f6c616e6767707461692f47726170685241472d50726f6d707473) |
| [LLM-Jailbreaks](https://github.com/langgptai/LLM-Jailbreaks) | Security research and defenses | [![](https://camo.githubusercontent.com/1cfffcc935fb2ba5f7461d8828337c251d722bf74b4668c3f8ee2c80f25846a9/68747470733a2f2f62616467656e2e6e65742f6769746875622f73746172732f6c616e6767707461692f4c4c4d2d4a61696c627265616b73)](https://camo.githubusercontent.com/1cfffcc935fb2ba5f7461d8828337c251d722bf74b4668c3f8ee2c80f25846a9/68747470733a2f2f62616467656e2e6e65742f6769746875622f73746172732f6c616e6767707461692f4c4c4d2d4a61696c627265616b73) |

### Applications

| Project | Description | Stars |
| --- | --- | --- |
| [BookAI](https://github.com/langgptai/BookAI) | AI-powered book generation | [![](https://camo.githubusercontent.com/16b24948963dd07bd3307e5cd366157d9708d636e04601b3f63f339477699aec/68747470733a2f2f62616467656e2e6e65742f6769746875622f73746172732f6c616e6767707461692f426f6f6b4149)](https://camo.githubusercontent.com/16b24948963dd07bd3307e5cd366157d9708d636e04601b3f63f339477699aec/68747470733a2f2f62616467656e2e6e65742f6769746875622f73746172732f6c616e6767707461692f426f6f6b4149) |
| [AI-Resume](https://github.com/langgptai/AI-Resume) | Beautiful resumes with Claude Artifacts | [![](https://camo.githubusercontent.com/71f634482af6b02a2c2981151ff6332935710684f68a8747313eef0c18c134d1/68747470733a2f2f62616467656e2e6e65742f6769746875622f73746172732f6c616e6767707461692f41492d526573756d65)](https://camo.githubusercontent.com/71f634482af6b02a2c2981151ff6332935710684f68a8747313eef0c18c134d1/68747470733a2f2f62616467656e2e6e65742f6769746875622f73746172732f6c616e6767707461692f41492d526573756d65) |

---

Transform ChatGPT with these specialized assistants:

| GPT | Purpose | Link |
| --- | --- | --- |
| 🎯 **LangGPT Expert** | Auto-generate structured prompts | [Launch](https://chat.openai.com/g/g-Apzuylaqk-langgpt) |
| ✍️ **PromptGPT** | Professional prompt engineer | [Launch](https://chat.openai.com/g/g-YKe3gmydD-promptgpt) |
| 🧠 **SmartGPT-5** | Never lazy, always diligent assistant | [Launch](https://chat.openai.com/g/g-sRQtxpN4C-smartgpt-5) |
| 💻 **Coding Expert** | Comprehensive programming assistant | [Launch](https://chat.openai.com/g/g-ky06YjwaP-coding-expert) |
| 📊 **Data Table GPT** | Transform messy data into clean tables | [Launch](https://chat.openai.com/g/g-nb6RjxHsb-data-table-gpt) |
| 🔥 **PytorchGPT** | PyTorch code specialist | [Launch](https://chat.openai.com/g/g-kyj3zKyHK-pytorchgpt) |
| 🎨 **LogoGPT** | Professional logo designer | [Launch](https://chat.openai.com/g/g-wdz2JlUBv-logogpt) |
| 📄 **PDF Reader** | Deep document analysis and extraction | [Launch](https://chat.openai.com/g/g-YaMjCVW0t-pdf-reader) |
| 🏅 **MathGPT** | Precise mathematical problem solver | [Launch](https://chat.openai.com/g/g-UIOlPhTjK-mathgpt) |
| 📝 **WriteGPT** | Professional writing across industries | [Launch](https://chat.openai.com/g/g-jwTMtRiL8-writegpt) |
| 🎙️ **时事热评员** | Current events commentator | [Launch](https://chat.openai.com/g/g-gbfs6fy7c-shi-shi-re-ping-yuan) |
| 🎀 **翻译大小姐** | Elegant Chinese translations | [Launch](https://chat.openai.com/g/g-2V90YGvVD-fan-yi-da-xiao-jie) |

[Discover 20+ more GPTs →](https://github.com/langgptai/LangGPT#langgpt-gpts)

---

## 🤝 Contributing

We welcome all contributions to make LangGPT better!

1. ⭐ **Star and share** — Increase visibility and help others discover LangGPT
2. 📝 **Submit examples** — Share your successful prompts built with LangGPT
3. 🆕 **Propose templates** — Create new templates beyond the Role structure
4. 📖 **Improve docs** — Fix typos, clarify instructions, add translations
5. 💡 **Suggest features** — Open issues with ideas for new capabilities
6. 🔧 **Code contributions** — Help build tools, utilities, and integrations

### Getting Started

New to GitHub contributions? Check out this [GitHub Minimal Contribution Guide](https://github.com/datawhalechina/DOPMC/blob/main/GITHUB.md)

---

[![Star History Chart](https://camo.githubusercontent.com/88f1dfb0e4197fba407487983453f26e55e7594dd67192134ab9d9cd8f66c3d9/68747470733a2f2f6170692e737461722d686973746f72792e636f6d2f7376673f7265706f733d6c616e6767707461692f4c616e6747505426747970653d44617465)](https://star-history.com/#langgptai/LangGPT&Date)

---

## 📄 Citation

If you use LangGPT in research or projects, please cite:

```
@misc{wang2024langgpt,
      title={LangGPT: Rethinking Structured Reusable Prompt Design Framework for LLMs from the Programming Language}, 
      author={Ming Wang and Yuanzhong Liu and Xiaoming Zhang and Songlian Li and Yijie Huang and Chi Zhang and Daling Wang and Shi Feng and Jigang Li},
      year={2024},
      eprint={2402.16929},
      archivePrefix={arXiv},
      primaryClass={cs.SE}
}
```

---

## 🙏 Acknowledgments

LangGPT was inspired by excellent projects:

- [Mr.-Ranedeer-AI-Tutor](https://github.com/JushBJJ/Mr.-Ranedeer-AI-Tutor) — Structured tutoring prompts
- [Auto-GPT](https://github.com/Significant-Gravitas/Auto-GPT) — Autonomous AI agents
- [SoM](https://github.com/SkalskiP/SoM) — Set of Mark prompting
- [yolov10](https://github.com/THU-MIG/yolov10) — Computer vision innovations

We're proud to see LangGPT principles applied in the wild:

- **[Prompt Optimizer](https://github.com/linshenkx/prompt-optimizer)** — Intelligent prompt optimization tool leveraging LangGPT methodology
- **[securityGPT](https://github.com/rryuliu/securityGPT)** — Secure prompt protection against leaks
- **[AIPainting-Structured-Prompts](https://github.com/zhutyler21/AIPainting-Structured-Prompts)** — Structured prompts for AI art generation

---

### Author

**云中江树 (Yun Zhong Jiang Shu)**

- 📱 WeChat Official Account: **「云中江树」**
- 💼 Creator of LangGPT Framework
- 🎓 Prompt Engineering Researcher

### Community

- 📚 [Knowledge Base](http://feishu.langgpt.ai/) — Comprehensive documentation
- 🐦 [Twitter/X](https://twitter.com/langgptai) — Latest updates
- 💬 [GitHub Discussions](https://github.com/langgptai) — Community forum
- 📧 Email: [contact@langgpt.ai](https://github.com/langgptai/)

---

**[⬆ Back to Top](https://github.com/langgptai/?tab=readme-ov-file#-langgpt--empowering-everyone-to-create-high-quality-prompts)**

Made with ❤️ by the [langgptai Community](https://github.com/langgptai)

*Empowering everyone to become a prompt expert* 🚀

## Releases

No releases published

## Packages

No packages published  

## Languages

- [Jupyter Notebook 83.2%](https://github.com/langgptai/LangGPT/search?l=jupyter-notebook)
- [JavaScript 16.7%](https://github.com/langgptai/LangGPT/search?l=javascript)
- Other 0.1%