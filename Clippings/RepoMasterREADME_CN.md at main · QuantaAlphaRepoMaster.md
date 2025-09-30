---
title: "RepoMaster/README_CN.md at main · QuantaAlpha/RepoMaster"
source: "https://github.com/QuantaAlpha/RepoMaster/blob/main/README_CN.md"
author:
  - "[[Nicole-Yi]]"
published:
created: 2025-09-30
description:
tags:
  - "clippings"
---
[Open in github.dev](https://github.dev/) [Open in a new github.dev tab](https://github.dev/) [Open in codespace](https://github.com/codespaces/new/QuantaAlpha/RepoMaster/tree/main?resume=1)

## 📰 News

- **2025.09.19** 🎉 Excited to announce that our papers have been accepted to **NeurIPS 2025** — [**RepoMaster**](https://arxiv.org/abs/2505.21577) as a ***Spotlight*** (≈3.2%) and [**SE-Agent**](https://arxiv.org/abs/2508.02085) as a ***Poster*** (≈24.52%)!
- **2025.08.28** 🎉 We open-sourced [**RepoMaster**](https://github.com/QuantaAlpha/RepoMaster) — an AI agent that leverages GitHub repos to solve complex real-world tasks.
- **2025.08.26** 🎉 We open-sourced [**GitTaskBench**](https://github.com/QuantaAlpha/GitTaskBench) — a repo-level benchmark & tooling suite for real-world tasks.
- **2025.08.10** 🎉 We open-sourced [**SE-Agent**](https://github.com/JARVIS-Xs/SE-Agent) — a self-evolution trajectory framework for multi-step reasoning.

> 🔗 **Ecosystem**: [RepoMaster](https://github.com/QuantaAlpha/RepoMaster) · [GitTaskBench](https://github.com/QuantaAlpha/GitTaskBench) · [SE-Agent](https://github.com/JARVIS-Xs/SE-Agent) · [Team Homepage](https://quantaalpha.github.io/)

---

---

## 🚀 概述

RepoMaster 通过 **自动找到合适的GitHub工具** 并让它们无缝协作，彻底改变了您解决编程任务的方式。只需描述您的需求，看着开源仓库成为您的智能助手。

💬 描述任务 → 🧠 AI分析 → 🔍 自动发现 → ⚡ 智能执行 → ✅ 完美结果

  

[![RepoMaster performance](https://github.com/QuantaAlpha/RepoMaster/raw/main/docs/assets/images/performance_01.jpg)](https://github.com/QuantaAlpha/RepoMaster/blob/main/docs/assets/images/performance_01.jpg)

---

## 快速开始

### 安装

```
git clone https://github.com/QuantaAlpha/RepoMaster.git
cd RepoMaster
pip install -r requirements.txt
```

### 配置

复制示例配置文件并使用您的API密钥进行自定义：

```
cp configs/env.example configs/.env
# 使用您喜欢的编辑器编辑配置文件
nano configs/.env  # 或使用 vim, code 等
```

**必需的API密钥：**

```
# 主要AI提供商配置（必需）
OPENAI_API_KEY=your_openai_api_key_here
OPENAI_MODEL=gpt-5

# 外部服务API（深度搜索功能必需）
SERPER_API_KEY=your_serper_key          # Google搜索集成
JINA_API_KEY=your_jina_key              # 网页内容提取

# 可选：其他AI提供商
# ANTHROPIC_API_KEY=your_claude_key     # Anthropic Claude支持
# DEEPSEEK_API_KEY=your_deepseek_key    # DeepSeek集成
# GEMINI_API_KEY=your_gemini_key        # Google Gemini支持
```

💡 **提示**: `configs/env.example` 文件包含所有可用的配置选项和详细注释。

### 启动

**Web界面（推荐初学者使用）：**

```
python launcher.py --mode frontend
# 访问Web仪表板：http://localhost:8501
```

**命令行界面（推荐高级用户使用）：**

```
python launcher.py --mode backend --backend-mode unified
# 通过终端提供智能多代理编排
```

**专用代理访问：**

```
python launcher.py --mode backend --backend-mode deepsearch      # 深度搜索代理
python launcher.py --mode backend --backend-mode general_assistant  # 编程助手
python launcher.py --mode backend --backend-mode repository_agent   # 仓库代理
```

> 📘 **需要帮助？** 查看我们的综合 [用户指南](https://github.com/QuantaAlpha/RepoMaster/blob/main/USAGE.md) 获取高级配置、故障排除和详细使用示例。

---

## 🎯 快速演示

只需用自然语言描述您的任务。RepoMaster的AI会自动分析您的请求，智能路由到最优解决方案路径，并编排完美的GitHub工具来实现您的想法。

| 任务描述 | RepoMaster操作 | 结果 |
| --- | --- | --- |
| *"帮我从这个网页上抓取产品价格"* | 🔍 找到抓取工具 → 🔧 自动配置 → ✅ 提取数据 | 结构化CSV输出 |
| *"将照片转换成梵高风格"* | 🔍 找到风格迁移仓库 → 🎨 处理图像 → ✅ 生成艺术 | 艺术杰作 |

从 **"从零开始编写代码"** → 到 **"让开源为我所用"**

### 🎨 神经风格迁移案例研究

repomaster.2.1.mp4<video src="https://private-user-images.githubusercontent.com/49181437/482483984-a21b2f2e-a31c-4afd-953d-d143beef781a.mp4?jwt=eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3NTkyMTUwNTAsIm5iZiI6MTc1OTIxNDc1MCwicGF0aCI6Ii80OTE4MTQzNy80ODI0ODM5ODQtYTIxYjJmMmUtYTMxYy00YWZkLTk1M2QtZDE0M2JlZWY3ODFhLm1wND9YLUFtei1BbGdvcml0aG09QVdTNC1ITUFDLVNIQTI1NiZYLUFtei1DcmVkZW50aWFsPUFLSUFWQ09EWUxTQTUzUFFLNFpBJTJGMjAyNTA5MzAlMkZ1cy1lYXN0LTElMkZzMyUyRmF3czRfcmVxdWVzdCZYLUFtei1EYXRlPTIwMjUwOTMwVDA2NDU1MFomWC1BbXotRXhwaXJlcz0zMDAmWC1BbXotU2lnbmF0dXJlPWE1YzAyMGMwY2M5ZDIzYTE4MWViOGI4NjJiYTM3MjhiOGQ4NmMwNTgzNTcxNWI0MTZlN2IxNzAxMGNiN2Y3MzkmWC1BbXotU2lnbmVkSGVhZGVycz1ob3N0In0.MUP6DWforUOGJTyUMr5QqvHnPYcjzgKMFP5ijS9wajo" controls="controls"></video>

*RepoMaster自主执行神经风格迁移任务的完整过程*

**更多高级用法、配置选项和故障排除，请参阅我们的 [用户指南](https://github.com/QuantaAlpha/RepoMaster/blob/main/USAGE.md).**

---

## 🤝 贡献

### 🌟 加入我们的使命，革命化代码智能

我们相信社区驱动创新的力量。您的贡献帮助让RepoMaster变得更智能、更快速、功能更强大。

### 🚀 贡献方式

- **🐛 问题报告**: 通过 [报告问题](https://github.com/QuantaAlpha/RepoMaster/issues) 帮助我们识别和修复问题。
- **💡 功能请求**: 有好想法？ [建议新功能](https://github.com/QuantaAlpha/RepoMaster/discussions) 。
- **📖 文档**: 通过贡献我们的 [文档](https://github.com/QuantaAlpha/RepoMaster/blob/main/docs) 来改进清晰度和示例。
- **💻 代码贡献**: 准备开始？查看我们的 [开发环境设置](https://github.com/QuantaAlpha/RepoMaster/blob/main/#development-setup) 开始贡献。

### 🛠️ 开发环境设置

**快速开发环境设置**
```
# Fork并克隆仓库
git clone https://github.com/your-username/RepoMaster.git
cd RepoMaster

# 安装开发依赖
pip install -e ".[dev]"

# 设置代码质量预提交钩子
pre-commit install

# 运行测试确保一切正常
pytest tests/

# 开始开发！🚀
```

> 📋 **初次接触开源？** 查看我们的 [贡献指南](https://github.com/QuantaAlpha/RepoMaster/blob/main/CONTRIBUTING.md) 获取详细说明和最佳实践。

---

## 📄 许可证

本项目采用 MIT 许可证 - 详见 [LICENSE](https://github.com/QuantaAlpha/RepoMaster/blob/main/LICENSE) 文件。

---

## 📞 支持

- 📧 **邮箱**: [quantaalpha.ai@gmail.com](https://github.com/QuantaAlpha/RepoMaster/blob/main/)
- 🐛 **问题**: [GitHub Issues](https://github.com/QuantaAlpha/RepoMaster/issues)
- 💬 **讨论**: [GitHub Discussions](https://github.com/QuantaAlpha/RepoMaster/discussions)
- 📖 **文档**: [完整文档](https://github.com/QuantaAlpha/RepoMaster/blob/main/docs)

---

## 🙏 致谢

特别感谢：

- [AutoGen](https://github.com/microsoft/autogen) - 多代理框架
- [OpenHands](https://github.com/All-Hands-AI/OpenHands) - 软件工程代理
- [SWE-Agent](https://github.com/princeton-nlp/SWE-agent) - GitHub问题解决代理
- [MLE-Bench](https://github.com/openai/mle-bench) - 机器学习工程基准

---

- QuantaAlpha 成立于 **2025 年 4 月** ，由来自 **清华、北大、中科院、CMU、港科大** 等高校的教授、博士后、博士与硕士组成。

🌟 我们的使命是探索智能的 **"量子"** ，引领智能体研究的 **"阿尔法"** 前沿 —— 从 **CodeAgent** 到 **自进化智能** ，再到 **金融与跨领域专用智能体** ，致力于重塑人工智能的边界。

✨ 在 **2025 年** ，我们将在以下方向持续产出高质量研究成果：

- **CodeAgent** ：真实世界任务的端到端自主执行
- **DeepResearch** ：深度推理与信息检索增强
- **Agentic Reasoning / Agentic RL** ：智能体推理与强化学习
- **自进化与协同学习** ：多智能体的自我进化与协作

📢 欢迎对我们方向感兴趣的同学加入！

🔗 团队主页： [QuantaAlpha](https://quantaalpha.github.io/)

---

## 📖 Citation

如果你觉得RepoMaster对你的研究有帮助，请引用我们的工作：

```
@article{wang2025repomaster,
  title={RepoMaster: Autonomous Exploration and Understanding of GitHub Repositories for Complex Task Solving},
  author={Huacan Wang and Ziyi Ni and Shuo Zhang and Lu, Shuo and Sen Hu and  Ziyang He and Chen Hu and Jiaye Lin and Yifu Guo and Ronghao Chen and Xin Li and Daxin Jiang and Yuntao Du and Pin Lyu},
  journal={arXiv preprint arXiv:2505.21577},
  year={2025},
  doi={10.48550/arXiv.2505.21577},
  url={https://arxiv.org/abs/2505.21577}
}
```

---

**⭐ 如果 RepoMaster 对您有帮助，请给我们一个星标！**

Made with ❤️ by the QuantaAlpha Team