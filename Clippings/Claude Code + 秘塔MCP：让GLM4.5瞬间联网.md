---
title: "Claude Code + 秘塔MCP：让GLM4.5瞬间联网"
source: "https://zhuanlan.zhihu.com/p/1948035709362508516"
author:
  - "[[猫哥AI量化用 AI 重构投资（公众号同名）]]"
published:
created: 2025-10-01
description: "文/猫哥AI量化 ps：1300字 朋友们，上次文章，猫哥提到了使用 Claude Code+秘塔MCP，搜索全天候策略的有关知识，然后进行量化策略开发： Claude Code 开发100个量化策略：全天候策略 今天就给大家讲一下，为什么我…"
tags:
  - "clippings"
---
![Claude Code + 秘塔MCP：让GLM4.5瞬间联网](https://picx.zhimg.com/70/v2-ab2140d3bdffa1b4983dfc125012e550_1440w.avis?source=172ae18b&biz_tag=Post)

Claude Code + 秘塔MCP：让GLM4.5瞬间联网

![](https://picx.zhimg.com/v2-f3ac351159ed33555f6082c484edd447_1440w.jpg)

文/猫哥AI量化 ps：1300字 朋友们，上次文章，猫哥提到了使用 Claude Code+ 秘塔MCP ，搜索全天候策略的有关知识，然后进行量化策略开发： Claude Code 开发100个量化策略：全天候策略 今天就给大家讲一下，为什么我们需要安装秘塔MCP，以及如何安装。 特别是使用智谱GLM4.5模型或者 魔搭 等第三方平台的API来接入Claude Code的，猫哥强烈建议安装秘塔MCP。 问题：GLM4.5无法联网 使用GLM4.5时，你是否遇到这些困扰： 想查最新API文档？不行！ 想找最新AI新闻？不行！ 甚至查询最近上映的热门电影，也不行！ 原因： GLM4.5等通过第三方平台接入， 无法使用 Anthropic 官方的 Web Search 功能 ， AI 被限制在"信息孤岛"中。 解决方案：秘塔MCP 秘塔MCP是可以调用秘塔API的插件，通过独立搜索服务让GLM4.5具备联网能力： 实时搜索网络信息 获取最新数据 打破知识截止限制 提升开发效率 安装步骤（三步搞定） 第一步：获取API密钥 访问 metaso.cn 注册并登录 进入API控制台： metaso.cn/search-api/ap 复制API密钥（格式：mk-xxxxxxxxxx） 第二步：运行安装命令 第三步：验证安装 claude mcp list 看到 metaso: https://metaso.cn/api/mcp (HTTP) - ✓ Connected 即表示成功。 核心功能 秘塔MCP提供： 多模态搜索 ：网页、图片、视频、文库 智能问答 ：AI总结而非简单链接罗列 网页抓取 ：提取正文内容，支持Markdown/JSON 无广告干扰 ：纯净搜索体验 实际应用场景 接下来实际演示一下，最近AI算力概念比较火，比如我让CC搜索一下光模块产业链，然后写个研究报告，提示词： 使用 metaso mcp 搜索 光模块产业链，写一份行业研究报告，保存为word文件 可以看到CC已经开始执行任务了，它以"光模块产业链 上下游 市场规模 发展趋势 2024"作为检索词进行搜索（实际上不太准确，最好是检索2025，后面可以让它重新搜索，这里不展示了）： CC检索了充足的信息，开始报告撰写工作： 最终整理完毕了，可以看到报告的逻辑非常清晰，然后是以html和markdown两种格式来呈现的（看来AI还是更擅长这俩格式） 现在看一下成果吧，虽然不是word，但这种网页形式反而更加美观，而且点击目录还可以自动跳转，真是令人惊喜： 这里仅作演示，此外还有更多CC结合秘塔MCP的场景，例如： 为什么选择秘塔MCP？ 一条命令安装 - 无需复杂配置 稳定可靠 - 千万级日调用验证 多语言支持 - cURL、Python、Node.js等 价格便宜 - 秘塔搜索API的定价为每次调用0.03元（即3分钱）。这个价格在目前的搜索API市场中是比较有竞争力的。 总结 秘塔MCP让GLM4.5从"信息孤岛"变为"实时在线"的AI助手，彻底解决国产模型的联网限制。对于需要实时信息的开发者来说，这是刚需工具。 推荐阅读： 8张图片带你通俗易懂的看懂"人工智能+"，十年一遇的大机遇 Claude Code的100种用法你能掌握几种？ Claude Code 开发100个量化策略：海龟交易策略 从零开始掌握 Claude Code 的Sub Agent机制，如何让AI工作效率翻倍（建议收藏） 一个 Claude Code 斜杠命令，让AI仿写万物

[所属专栏 · 2025-09-26 22:10 更新](https://zhuanlan.zhihu.com/c_1927019426173134807)



[猫哥AI量化](https://zhuanlan.zhihu.com/c_1927019426173134807)

[

猫哥AI量化

29 篇内容 · 294 赞同

](https://zhuanlan.zhihu.com/c_1927019426173134807)

[

最热内容 ·

Claude Code 开发100个量化策略：全天候策略

](https://zhuanlan.zhihu.com/c_1927019426173134807)

编辑于 2025-09-07 14:54・山东[AI](https://www.zhihu.com/topic/19588023)[Agent](https://www.zhihu.com/topic/28352669)[AI编程](https://www.zhihu.com/topic/28322950)



发首评

还没有评论，发表第一个评论吧