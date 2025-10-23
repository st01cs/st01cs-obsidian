---
title: "一个小技巧，帮你显著提高 AI 的回答质量！"
source: "https://mp.weixin.qq.com/s/ZxSwhqm8yIt3KqcFoEmyxQ"
author:
  - "[[ConardLi]]"
published:
created: 2025-10-17
description:
tags:
  - "clippings"
---
原创 ConardLi *2025年10月17日 08:30*

文章挺长的，如果你不想读，请直接拉到最后看结论。

大家好，欢迎来到 code秘密花园，我是花园老师（ConardLi）。

不知道大家有没有发现，随着 AI 技术突飞猛进的发展，各种大模型的上限虽然在不断增强，但模型有的时候似乎有点学会偷懒了。

典型的现象是，有时模型在回答问题时可能会放弃寻找多样的可能性，直接偷懒给类似提问一个最普通同时也最不容易犯错的答案，但这其实并不利于想要得到更多启发的用户需求。

这个其实是正常现象，因为人也会偷懒，模型的表现越来越像人类，寻找多样的可能性以及最优解可能是更累（消耗更多 Token）、需要更多思考的，还不如直接给出一个中庸但不会犯错的答案。

我们先来做个有趣的实验，我们对豆包开五个新的会话，问五个同样的问题：《给我讲个笑话》，这是一个开放性问题，正常来讲，我们应该期望每次豆包都能给出一些不一样的答案，然而事实却是：

![第一次](https://mmbiz.qpic.cn/sz_mmbiz_png/e5Dzv8p9XdRmPpMibWr8vicDDE1oSp6o6clM9JUVOspwQLr2L2JkSbClITUiaUblyyZiapemkRAddAA1Cibk9IviaiaibQ/640?wx_fmt=png&from=appmsg&watermark=1&tp=webp&wxfrom=5&wx_lazy=1#imgIndex=0)

第一次

![第二次](https://mmbiz.qpic.cn/sz_mmbiz_png/e5Dzv8p9XdRmPpMibWr8vicDDE1oSp6o6cIBKyvkdSmRvjH9XCJvxROGWSkpiaKB9c6WEgu4J4grabjP4Cz0yJMaw/640?wx_fmt=png&from=appmsg&watermark=1&tp=webp&wxfrom=5&wx_lazy=1#imgIndex=1)

第二次

![第三次](https://mmbiz.qpic.cn/sz_mmbiz_png/e5Dzv8p9XdRmPpMibWr8vicDDE1oSp6o6cq2bKUrNKaUwibhNRLrJibqMeCIMoibLDJyOFKP8yrduNpZwkeXiafcqHLQ/640?wx_fmt=png&from=appmsg&watermark=1&tp=webp&wxfrom=5&wx_lazy=1#imgIndex=2)

第三次

![第四次](https://mp.weixin.qq.com/s/www.w3.org/2000/svg'%20xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg%20stroke='none'%20stroke-width='1'%20fill='none'%20fill-rule='evenodd'%20fill-opacity='0'%3E%3Cg%20transform='translate(-249.000000,%20-126.000000)'%20fill='%23FFFFFF'%3E%3Crect%20x='249'%20y='126'%20width='1'%20height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

第四次

![第五次](https://mp.weixin.qq.com/s/www.w3.org/2000/svg'%20xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg%20stroke='none'%20stroke-width='1'%20fill='none'%20fill-rule='evenodd'%20fill-opacity='0'%3E%3Cg%20transform='translate(-249.000000,%20-126.000000)'%20fill='%23FFFFFF'%3E%3Crect%20x='249'%20y='126'%20width='1'%20height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

第五次

好家伙，这是被程序员训傻了吧，五个笑话都是关于程序员的，其中四个还是程序员买面包的故事。

下面我们尝试在这个问题后面加上一段神奇的提示词：

```
<instructions>
Generate 5 responses to the user query, each within a separate <response> tag. Each <response> must include a <text> and a numeric <probability>. Randomly sample responses from the full distribution. 
</instructions>
```
![图片](https://mp.weixin.qq.com/s/www.w3.org/2000/svg'%20xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg%20stroke='none'%20stroke-width='1'%20fill='none'%20fill-rule='evenodd'%20fill-opacity='0'%3E%3Cg%20transform='translate(-249.000000,%20-126.000000)'%20fill='%23FFFFFF'%3E%3Crect%20x='249'%20y='126'%20width='1'%20height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

这次我们发现，神奇的事情发生了，豆包打破了程序员的魔咒，开始讲其他笑话了。

这段提示词并不是我总结出来的，而是源于最近麻省理工大学新发表的一篇论文：

![《口头概率抽样法：缓解模式坍缩，释放 LLM 的多元表达》](https://mp.weixin.qq.com/s/www.w3.org/2000/svg'%20xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg%20stroke='none'%20stroke-width='1'%20fill='none'%20fill-rule='evenodd'%20fill-opacity='0'%3E%3Cg%20transform='translate(-249.000000,%20-126.000000)'%20fill='%23FFFFFF'%3E%3Crect%20x='249'%20y='126'%20width='1'%20height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

《口头概率抽样法：缓解模式坍缩，释放 LLM 的多元表达》

听起来挺抽象的，其实全篇都是在说这段提示词，并且进行了大量实验来验证这段提示词能够真正激发 LLM 的多样性。

![图片](https://mp.weixin.qq.com/s/www.w3.org/2000/svg'%20xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg%20stroke='none'%20stroke-width='1'%20fill='none'%20fill-rule='evenodd'%20fill-opacity='0'%3E%3Cg%20transform='translate(-249.000000,%20-126.000000)'%20fill='%23FFFFFF'%3E%3Crect%20x='249'%20y='126'%20width='1'%20height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

这篇论文提出一个几乎“零成本”的推理时策略 《 `Verbalized Sampling` （简称 VS）》：不要只让模型给一个答案，而是让它先 “口头说出” 一组可能答案及其对应的概率，再基于这套概率分布进行采样与选择。这样做能显著缓解对齐训练带来的 `“模式坍缩”` ，恢复并释放模型本来就具备的生成多样性，同时不牺牲事实准确性与安全性。

## 模式坍缩的来龙去脉

所谓 “模式坍缩”，就是模型只盯着一个“最常见/最安全”的说法，反而忽略了同样合理的其他表达方式。而这个 “最常见/最安全” 可能往往并不是最优的答案。

这可能并不是模型本身算法层面的问题，而要归咎于当下模型最热门的后训练方式： `RLHF` （人类反馈强化学习）。

![图片](https://mp.weixin.qq.com/s/www.w3.org/2000/svg'%20xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg%20stroke='none'%20stroke-width='1'%20fill='none'%20fill-rule='evenodd'%20fill-opacity='0'%3E%3Cg%20transform='translate(-249.000000,%20-126.000000)'%20fill='%23FFFFFF'%3E%3Crect%20x='249'%20y='126'%20width='1'%20height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

> `RLHF` 通过收集人类对智能体行为的评估数据，训练奖励模型来学习人类的偏好，然后利用该模型优化智能体的策略，使智能体能够生成更符合人类期望和价值观的行为

在 `RLHF` 数据集中，人类标注者普遍会优先选择 “典型、熟悉” 的答案（心理学称为典型性偏好）。当奖励模型学习到这种偏好，优化过程自然会收缩到这些“熟面孔”，于是输出多样性就会不断降低。

换个生活类比：一间餐馆原本有很多好菜，后来大家点评时更喜欢“最常吃的那几样”，平台排序也跟着偏爱它们，时间久了菜单可能会越做越单一，这就是模式坍缩。在论文中，用理论模型刻画了这种偏好如何积累成系统效应，并在多组偏好数据上做了实证验证，确认“典型性偏好”确实在驱动坍缩。

## Verbalized Sampling（VS）

VS 的点子很朴素：把 “给我一个答案” 改成“请生成 N 个可能答案，并给出每个的概率”。

比如，不再问 “讲一个咖啡的笑话”，而是提示 “生成 5 个关于咖啡的笑话及其对应概率”。

这样模型就会先把 “心里的分布” 说出来，再按照这套分布进行采样，这样不同 “风格/套路” 的内容都有机会“上桌”，多样性自然就会恢复。

下面这些都属于 VS 提示词段模板，可直接复用：

- “请生成 5 个符合要求的候选回复，并给出每个的概率。”
- “先口头给出一个概率分布（覆盖多种合理答案），再依据该分布采样给我 1–2 个最终输出。”
- 对创意任务可加：“候选需风格多样”；对事实任务加：“若存在多解，请给出分布”。

你也可以直接追加这段通用的系统提示词：

tag. Responses should each include a and a numeric . Please sample at random from the \[full distribution / tails of the distribution, such that the probability of each response is less than 0.10\]. User prompt: Write a short story about a bear.

翻译为中文：

> 你是一个多样化生成的助手。请按照如下要求输出：
> 
> 1. 生成 5 个不同的候选答案（内容尽量有风格差异）。
> 2. 为每个答案给出 0-1 概率，并保证总和为 1。
> 3. 按概率从高到低排序，逐条输出为：内容｜概率。
> 4. 在末尾给出“采样建议”：
> - 若只需 1 个答案，推荐选择概率最高者；
> 	- 若需多样性，可按概率加权进行随机采样。

## 论文的实验结论

论文中，使用 VS 对四类不同的任务上进行了系统评估：创意写作（诗歌、笑话、故事）、对话模拟（如募捐劝说场景）、开放式问答（多答案枚举型）、以及合成数据生成（用于下游数学能力提升）。结论清晰且一致：

![图片](https://mp.weixin.qq.com/s/www.w3.org/2000/svg'%20xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg%20stroke='none'%20stroke-width='1'%20fill='none'%20fill-rule='evenodd'%20fill-opacity='0'%3E%3Cg%20transform='translate(-249.000000,%20-126.000000)'%20fill='%23FFFFFF'%3E%3Crect%20x='249'%20y='126'%20width='1'%20height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

- 在创意写作中，VS 相比直接提示，多样性提升 `1.6–2.1×` ，人类评审得分提升 `25.7%` ，同时能恢复基础模型多样性的 `66.8%` 。这些提升来自“把分布说出来”，使不同风格都有被采到的机会。
- 在对话模拟中（如“捐款金额分布”的场景），VS 生成的行为分布更接近真实人群，出现“犹豫—劝服—改变想法”等更人性化的过程，不再是单一的“立刻答应/拒绝”。
- 在开放枚举型问答中（例如“列出美国各州”），VS 口头生成的概率分布在多次试验的平均下，与预训练语料的真实分布更贴近，而直接提示常常只重复加州、德州等“高频熟面孔”。
- 在合成数据生成上，VS 生成的数据更丰富，能帮助下游数学任务取得更好的泛化。

更有意思的是，论文还观察到一个涌现趋势：更强的模型从 VS 中获益更明显。这符合直觉：能力越强、学到的“原生态分布”越丰富，VS 就有越多“好内容”可供采样。

## 使用建议

**什么时候用 VS？**

当你的任务“不止一个合理答案”、或你关心“答案的分布结构”，VS 很有帮助。比如创意写作、策略建议、人物对话、枚举类开放问答、数据合成等。

**什么时候不必用 VS？**

当任务只有唯一正确解（如标准算式、事实性问答的单一正确版本），直接提问更高效，VS 的“多样性恢复”意义有限。

**怎么把 VS 用好？**

- 设定候选数 N：常见为 5 或 10。更大的 N 提升覆盖度，但也增加阅读和筛选成本。
- 校验概率规范性：要求总和 =1，偏差时自动归一化；必要时提示“概率必须非负”。
- 避免“概率幻觉”：提醒模型概率是“内部估计”，用户侧使用时以加权采样或 Top-k 选择为主。
- 联动评估：对创意场景可结合人评或多样性指标；对生成数据可直接检验下游任务表现。

## 总结

以下的两段提示词能够激发模型的回复多样性，在创意、模拟、枚举与合成数据等场景中都能见到实效，而且对准确性与安全性并无明显损耗：

英文：

tag. Responses should each include a and a numeric . Please sample at random from the \[full distribution / tails of the distribution, such that the probability of each response is less than 0.10\]. User prompt: Write a short story about a bear.

中文：

> 你是一个多样化生成的助手。请按照如下要求输出：
> 
> 1. 生成 5 个不同的候选答案（内容尽量有风格差异）。
> 2. 为每个答案给出 0-1 概率，并保证总和为 1。
> 3. 按概率从高到低排序，逐条输出为：内容｜概率。
> 4. 在末尾给出“采样建议”：
> - 若只需 1 个答案，推荐选择概率最高者；
> 	- 若需多样性，可按概率加权进行随机采样。

## 最后

关注《code秘密花园》从此学习 AI 不迷路，相关链接：

- AI 教程完整汇总：https://rncg5jvpme.feishu.cn/wiki/U9rYwRHQoil6vBkitY8cbh5tnL9
- 相关学习资源汇总在：https://github.com/ConardLi/easy-learn-ai

如果本期对你有所帮助，希望得到一个免费的三连，感谢大家支持

[阅读原文](https://mp.weixin.qq.com/s/)

继续滑动看下一个

code秘密花园

向上滑动看下一个