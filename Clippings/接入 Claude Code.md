---
title: "接入 Claude Code"
source: "https://docs.bigmodel.cn/cn/guide/develop/claude"
author:
  - "[[智谱AI开放文档]]"
published:
created: 2025-09-30
description: "将智谱最新 GLM-4.5 系列模型集成到 Claude Code 的方法"
tags:
  - "clippings"
---
智谱模型 GLM-4.5 可以通过一个兼容 Anthropic API 的端点与 Claude Code 集成。这意味着可以让 Claude Code 与 GLM-4.5 通信，而不需要修改 Claude Code 的任何代码。

Claude Code 玩转新体验：20 元起解锁 GLM Coding 包月，3倍用量，1/7价格，独家升级支持联网搜索&多模态理解，响应更快，调用更稳。限时羊毛价， [立即订阅](https://bigmodel.cn/claude-code?utm_source=bigmodel&utm_medium=link&utm_term=cc&utm_campaign=Platform_Ops&_channel_track_key=i8kwCaos) ！ PRO 及以上等级套餐专属 [视觉理解 MCP Server](https://docs.bigmodel.cn/cn/coding-plan/mcp/vision-mcp-server) 、 [网络搜索 MCP Server](https://docs.bigmodel.cn/cn/coding-plan/mcp/search-mcp-server) 让您的 Code Agent 拥有搜索与视觉。

## 1\. 前往获取智谱 API key

前往智谱 Bigmodel 开放平台，获取你的 [API key](https://open.bigmodel.cn/usercenter/proj-mgmt/apikeys)

## 2\. 配置环境变量

完成 Claude code 安装后，有以下 2 种方式设置环境变量 **方式一：使用脚本（首次使用推荐）** 在你的终端或 IDE 中运行以下命令，下载一个帮你自动配置环境变量的 shell 脚本，运行即可

```
curl -O "http://bigmodel-us3-prod-marketplace.cn-wlcb.ufileos.com/1753683727739-0b3a4f6e84284f1b9afa951ab7873c29.sh?ufileattname=claude_code_prod.sh"
```

**方式二：手动配置** 若之前有配置过 Claude code 的环境变量，可按以下方式手动配置

```
export ANTHROPIC_BASE_URL=https://open.bigmodel.cn/api/anthropic

export ANTHROPIC_AUTH_TOKEN=YOUR_API_KEY
```

## 3\. 快速开始使用 Claude Code

> 如果遇到「Do you want to use this API key」选择 Yes 即可

启动后选择信任 Claude Code 访问文件夹里的文件，如下：![Description](https://cdn.bigmodel.cn/markdown/1753631613096claude-2.png?attname=claude-2.png)

Description

现在就已经正常使用 Claude Code 进行开发了！

> 对话/规划/代码编写/复杂推理等主场景时默认使用模型均为 GLM-4.5，Claude code 会在部分轻量任务时自动路由到 GLM-4.5-Air，这也是我们推荐的使用方式，兼顾性能、速度与价格，暂不支持其它模型（如 GLM-4.5-X/AirX/Flash 等）。

以下为简单示例： **Case 1：根据提示信息创建网页**![Description](https://cdn.bigmodel.cn/static/platform/images/usage-guide/scenario-examples/claude-code-case1-1.jpg)

Description

![Description](https://cdn.bigmodel.cn/static/platform/images/usage-guide/scenario-examples/claude-code-case1-2.jpg)

Description

- 生成文件： [megatron\_lm\_detailed\_architecture\_analysis.html](https://cdn.bigmodel.cn/static/platform/images/usage-guide/scenario-examples/megatron_lm_detailed_architecture_analysis.html)
**Case 2：生成一个打地鼠游戏**![Description](https://cdn.bigmodel.cn/markdown/1753631619635claude-3.png?attname=claude-3.png)

Description

![Description](https://cdn.bigmodel.cn/markdown/1753631624521claude-4.png?attname=claude-4.png)

Description

![Description](https://cdn.bigmodel.cn/markdown/1753631630147claude-5.png?attname=claude-5.png)

Description

**Case 3：生成一个日蚀动效** Prompt：帮我生成日蚀过程的动态特效，尽量采用苹果手机的风格![Description](https://cdn.bigmodel.cn/markdown/1753631640389claude-6.png?attname=claude-6.png)

Description

![Description](https://cdn.bigmodel.cn/markdown/1753631646074claude-7.png?attname=claude-7.png)

Description

## 补充说明：如何切换使用的模型

> Claude code 内部有 2 个模型环境变量，其中 ANTHROPIC\_MODEL 主模型使用 GLM-4.5（对应对话/规划/代码编写/复杂推理等场景），ANTHROPIC\_SMALL\_FAST\_MODEL 使用 GLM-4.5-Air（对应文件搜索/语法检查等辅助场景），这也是我们推荐的使用方式，兼顾性能、速度与价格，暂不支持其它模型（如 GLM-4.5-X/AirX/Flash 等）。

```
{

  "env": {

      "ANTHROPIC_MODEL": "glm-4.5-air",

        "ANTHROPIC_SMALL_FAST_MODEL": "glm-4.5-air"

  }

}
```

1. 启动一个新的命令行窗口，运行 `claude` 启动 Claude Code
2. 在 Claude Code 中输入 `/status` 确认模型状态：
![claudecode](https://cdn.bigmodel.cn/markdown/1756439367494claudecode.png)

claudecode

1. 如需切换回 GLM-4.5 模型，将~/.claude/settings.json 改为：

```
{

  "env": {

      "ANTHROPIC_MODEL": "glm-4.5",

        "ANTHROPIC_SMALL_FAST_MODEL": "glm-4.5-air"

  }

}
```

[接入 Cline](https://docs.bigmodel.cn/cn/guide/develop/cline)