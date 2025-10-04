---
title: "OpenDerisk/README.zh.md at main · derisk-ai/OpenDerisk"
source: "https://github.com/derisk-ai/OpenDerisk/blob/main/README.zh.md"
author:
  - "[[yhjun1026]]"
published:
created: 2025-10-01
description:
tags:
  - "clippings"
---
[Skip to content](https://github.com/derisk-ai/OpenDerisk/blob/main/#start-of-content)

[Open in github.dev](https://github.dev/) [Open in a new github.dev tab](https://github.dev/) [Open in codespace](https://github.com/codespaces/new/derisk-ai/OpenDerisk/tree/main?resume=1)

### OpenDeRisk

OpenDeRisk AI 原生风险智能系统 —— 7\*24H 应用系统AI数字运维助手(AI-SRE), 我们的愿景是, 为每个应用系统提供一个7\*24H的AI系统数字管家，并能与真人进行协同，7\*24H处理业务问题，形成7\*24H得深度护航与防护网。

### 特性

[![](https://github.com/derisk-ai/OpenDerisk/raw/main/assets/feature_zh.png)](https://github.com/derisk-ai/OpenDerisk/blob/main/assets/feature_zh.png)

1. DeepResearch RCA: 通过深度分析日志、Trace、代码进行问题根因的快速定位。
2. 可视化证据链：定位诊断过程与证据链全部可视化展示，诊断过程一目了然，可以快速判断定位的准确性。
3. 多智能体协同: SRE-Agent、Code-Agent、ReportAgent、Vis-Agent、Data-Agent协同工作。
4. 架构开源开放: OpenDerisk采用完全开源、开放的方式构建，相关框架、代码在开源项目也能实现开箱即用。

### 架构方案

[![](https://github.com/derisk-ai/OpenDerisk/raw/main/assets/arch_zh.png)](https://github.com/derisk-ai/OpenDerisk/blob/main/assets/arch_zh.png)

#### 介绍文档

- [OpenDerisk DeepWiki文档](https://deepwiki.com/derisk-ai/OpenDerisk)

采用多Agent架构，目前代码中主要实现了绿色部分部分，告警感知采用的是微软开源的 [OpenRCA数据集](https://github.com/microsoft/OpenRCA), 数据集的大小解压后在26G左右，我们实现在26G的数据集合上，通过多Agent协同，Code-Agent动态写代码来进行最终根因的分析诊断。

#### 技术实现

1. 数据层: 拉取Github OpenRCA的大规模数据集(20G), 解压本地处理分析。
2. 逻辑层：Multi-Agent架构, 通过SRE-Agent、Code-Agent、ReportAgent、VisAgent、Data-Agent协同合作，进行深度的DeepResearch RCA(Root Cause Analyze)
3. 可视化层: 采用Vis协议、动态渲染整个处理流程与证据链, 以及多角色协同切换的过程。
4. OpenDeRisk中的数字员工(Agent)

[![](https://github.com/derisk-ai/OpenDerisk/raw/main/assets/ai-agent.png)](https://github.com/derisk-ai/OpenDerisk/blob/main/assets/ai-agent.png)

#### 快速启动

##### 1.open-derisk服务启动

- Install uv
	```
	curl -LsSf https://astral.sh/uv/install.sh | sh
	```
- 依赖安装
	```
	uv sync --all-packages  --frozen \
	--extra "base" \
	--extra "proxy_openai" \
	--extra "rag" \
	--extra "storage_chromadb" \
	--extra "derisks" \
	--extra "storage_oss2" \
	--extra "client"  \
	--extra "ext_base"    \
	--extra "proxy_tongyi"
	```
- 配置启动参数
	```
	> 配置\`derisk-proxy-aliyun.toml\`文件中相关的API_KEY, 然后运行下面的命令启动。
	> 也可参考 \`derisk-proxy-aliyun.toml\` 文件中的配置使用全阿里云模型和oss方案
	> ** 注意 ** 最好在全新的环境下启动0.2版本，不然可能被0.1旧数据影响导致启动失败.
	```
- 启动服务
	```
	uv run python packages/derisk-app/src/derisk_app/derisk_server.py --config configs/derisk-proxy-aliyun.toml
	```
- 服务访问
	> 打开浏览器访问 [`http://localhost:7777`](http://localhost:7777/)

##### 2.内置场景快速使用

- AI-SRE(OpenRca根因定位)
	- !注意, 我们默认使用OpenRCA数据集中的 [Telecom数据集](https://drive.usercontent.google.com/download?id=1cyOKpqyAP4fy-QiJ6a_cKuwR7D46zyVe&export=download&confirm=t&uuid=42621058-41af-45bf-88a6-64c00bfd2f2e),
	- 你可以通过链接, 或者下述命令进行下载：
	```
	gdown https://drive.google.com/uc?id=1cyOKpqyAP4fy-QiJ6a_cKuwR7D46zyVe
	```
	- 下载完成后, 将数据解压到 ${derisk项目}/pilot/datasets。
- 火焰图助手
	- 使用你本地应用服务进程的火焰图(java/python)上传给助手提问分析
- DataExpert
	- 上传你的指标、日志、trace等各种Excel表格数据进行对话分析

##### 3.快速开发

- Agent开发 参考derisk-ext.agent.agents下的实现逻辑
- 工具开发
	- local tool
	- mcp
- 其他开发 文档准备中....

#### 运行效果

如下图所示, 为多智能体协同运行处理一个复杂的运维诊断任务的场景。

[![](https://github.com/derisk-ai/OpenDerisk/raw/main/assets/scene_demo.png)](https://github.com/derisk-ai/OpenDerisk/blob/main/assets/scene_demo.png)

### RoadMap

- 0530 V0.1版本，基于领域知识与MCP服务，实现从异动感知 -> 自主决策 -> 自适应执行与问题处理。
	- 技术风险领域知识引擎
	- 基于大模型推理驱动的异动感知 -> 决策 -> 执行推理引擎
	- 自动TroubleShooting与Fix
- 0830 V0.2版本
	- 技术风险领域MCP服务与管理
	- 支持自定义绑定知识与MCP工具
	- 支持3+ DevOps领域MCP服务
- 0930 V0.3
	- 支持对接生产环境
	- 提供完整的生产环境部署解决方案，支持生产问题诊断。
- 1230 V0.4
	- 端到端AIOps在线Agentic RL
	- 端到端评测能力

### 致谢

- [DB-GPT](https://github.com/eosphoros-ai/DB-GPT)
- [GPT-Vis](https://github.com/antvis/GPT-Vis)
- [MetaGPT](https://github.com/FoundationAgents/MetaGPT)
- [OpenRCA](https://github.com/microsoft/OpenRCA)

OpenDeRisk-AI 社区致力于构建 AI 原生的风险智能系统。🛡️ 我们希望我们的社区能够为您提供更好的服务，同时也希望您能加入我们，共同创造更美好的未来。🤝

[![Star History Chart](https://camo.githubusercontent.com/f9bd7afc15f5f4abbc22ef622954a29296f4218c71c11ecc05d4651850c18735/68747470733a2f2f6170692e737461722d686973746f72792e636f6d2f7376673f7265706f733d64657269736b2d61692f4f70656e44657269736b26747970653d44617465)](https://star-history.com/#derisk-ai/OpenDerisk)

### 社区

加入钉钉群, 与我们一起交流讨论。

[![OpenDeRisk-AI 交流群](https://github.com/derisk-ai/OpenDerisk/raw/main/assets/derisk-ai.jpg)](https://github.com/derisk-ai/OpenDerisk/blob/main/assets/derisk-ai.jpg)