---
title: DeepSearch/DeepResearch中最优文本段选择和URL重排
source: https://mp.weixin.qq.com/s/apnorBj4TZs3-Mo23xUReQ
author:
  - "[[Jina AI]]"
published:
created: 2025-10-01
description: 被忽略的两个工程细节，直接决定了深度搜索的质量
tags:
  - clippings
  - deepresearch
---
原创 Jina AI *2025年03月13日 15:39*

![图片](https://mmbiz.qpic.cn/sz_mmbiz_png/3EjVEqjYF3I1Du00fibf7PQaZiaIFX8xSY1UZP1kw8R2iclGPic8fwSURcUqU1XFtG0ibqjkS4TDEBj0NYOichVdxP6g/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1#imgIndex=0)

如果你已经读过我们上一篇经典长文《 [DeepSearch/DeepResearch 的设计与实现](https://mp.weixin.qq.com/s?__biz=MzkyODIxMjczMA==&mid=2247502169&idx=1&sn=1f566cd34d96a5e5dfe810eba2441ed5&scene=21#wechat_redirect) 》，那么不妨再深挖一些能大幅提升回答质量的细节。这次，我们将重点关注两个细节：

1. **从长网页提取最优文本段** ：如何利用迟分(late-chunking)算法，从长网页内容中选取最相关的信息小片段。
2. **对收集到的URL进行重排** ：如何利用重排器(Reranker) 让 LLM Agent 在几百个URL中 聪明地 选择爬取哪一个 URL？

可能有人还记得我们上一篇里的结论：“在 DeepSearch 中，Embeddings 模型仅适用于诸如 STS（语义文本相似度）任务之类的查询去重，而 Reranker 甚至不在我们最初的 DeepSearch 编程实现中。”

现在看来，这两类召回模型还是有其价值的，只是用法和我们常规的认知不太一样。我们做搜索一直遵循“80-20”原则，不会为了照顾情绪价值，或为证明自己作为 Embeddings 和 Reranker 提供商的市场存在感 而硬上什么模型 。我们非常 80-20，非常务实， **务实到我们只关心搜索系统的最最本质的需求。**

所以，经过数周的反复试验和迭代，我们发现了 Embeddings 和 Reranker 在 DeepSearch/DeepResearch 系统中的一些非常规但非常有效的应用。用了这些方法后，我们显著提高了 Jina DeepSearch 的质量（欢迎大家来体验）。我们也想把这些经验分享给在这个领域一起摸爬滚打的同行们。

![图片](https://mmbiz.qpic.cn/sz_mmbiz_png/3EjVEqjYF3JTKz9S0TK5cnicM6SiboVibq9cfEnned4DpeRNlcvjJ1o0a8XvP2yjNQeiaWRR1Pd1099Xt8Yh4UeUzg/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1#imgIndex=1)

🔗 https://search.jina.ai

## 从长文本中选取最优文本段

问题是这样的： 用 Jina Reader 读取网页内容后，我们需要把它作为一条知识，放到 Agent 的上下文里，供它推理。虽然把全部内容一股脑塞进 LLM 的上下文是最省事的办法，但考虑到 Token 成本和生成速度，这肯定不是最好的选择。在实际应用里，我们需要找出内容中与问题最相关的部分，只把这些部分作为知识添加到 Agent 的上下文里。

💡 这里说的是，即使用 Jina Reader 清理成干净 Markdown 后，内容仍然太长的情况。比如 GitHub Issues、Reddit 帖子、论坛讨论和博客文章等长页面中。

基于 LLM 的筛选方法也有同样的成本和延迟问题，所以我们得找找有没有小模型的解决方案： **我们需要更小、更便宜，但仍然支持多种语言的模型。** 这是个关键因素，因为我们没法保证问题或文档永远都是中文的。

我们一边是问题（原始查询或“信息差”问题），另一边是大量的 Markdown 内容，其中大部分内容都是无关紧要的。我们需要选出与问题最相关的片段。这就很像 RAG 社区自 2023 年以来一直在努力解决的分块问题——使用检索器模型只检索相关块，并放到上下文窗口中进行总结。

不过，我们的情况有两个关键区别：

1. **有限数量文档中的有限数量的文本块。**

假设每个块大约有 500 个 Token，那么一个典型的长网页文档大约有 20 万 Token（中位数）到 100 万 Token（99 分位）。我们每一步用 Jina Reader 抓取 4-5 个 URL，这样大概会产生几百个文本块。也就是说，几百个向量和几百个余弦相似度。用 JavaScript 在内存里就能轻松处理，根本不需要向量数据库。

1. **我们需要连续的文本块来形成有效的知识摘要。**

我们不能接受像 \[1-2, 6-7, 9, 14, 17,...\] 这样由分散的句子组成的摘要。更有用的知识摘要应该是像 \[3-15, 17-24,...\] 这样的，更能保持文本的连贯性。这样 LLM 更容易从知识源中复制和引用，也能减少“幻觉”。

剩下的都是开发者们抱怨的那些注意事项：每个文本块不能太长，因为向量模型处理不了太长的上下文；分块会导致上下文丢失，并使得每个文本块的向量都是独立同分布的；以及，到底怎么找到既保持可读性又保持语义的最佳边界？如果你知道我们在说什么，那你很可能在你的 RAG 实现中也被这些问题困扰过。

不过长话短说——使用 `jina-embeddings-v3` 的 [**迟分（Late Chunking）**](https://mp.weixin.qq.com/s?__biz=MzkyODIxMjczMA==&mid=2247501187&idx=1&sn=94fd0b8f53b39bd0adbaab86834996cd&scene=21#wechat_redirect) 完美地解决了这三个问题。“迟分”保留了每个块的上下文信息，对边界不敏感，而且 `jina-embeddings-v3` 本身在非对称多语言检索任务中也是最先进的。感兴趣的读者可以关注我们的博客文章或论文了解详情，总体的实现是这样的。

☞ [长文本 Embedding 模型中的“迟分”策略](https://mp.weixin.qq.com/s?__biz=MzkyODIxMjczMA==&mid=2247501187&idx=1&sn=94fd0b8f53b39bd0adbaab86834996cd&scene=21#wechat_redirect)

🔗 https://arxiv.org/pdf/2409.04701

![使用迟分的片段选择的流程图](https://mmbiz.qpic.cn/sz_mmbiz_png/3EjVEqjYF3I1Du00fibf7PQaZiaIFX8xSYGibdia1L5AI0b9WICW6AAibxCJh6NfUBcr1Fcs7OZcWldWryClFLribe5g/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1#imgIndex=2)

使用迟分的片段选择的流程图

这张图展示了摘要选择算法，它的工作原理类似于一维卷积（Conv1D）。这个过程首先把一个长文档分割成固定长度的块，然后用开启了迟分的 `jina-embeddings-v3` 向量化这些文本块。计算完每个块和问题之间的相似度分数后，一个滑动窗口会在这些相似度分数上移动，以找到平均值最高的窗口。

以下是示意代码：用迟分和类似“一维卷积”的平均池化，挑出跟问题最相关的段落。

```
function cherryPick(question, longContext, options) {
  if (longContext.length < options.snippetLength * options.numSnippets)
    return longContext;

  const chunks = splitIntoChunks(longContext, options.chunkSize);

  const chunkEmbeddings = getEmbeddings(chunks, "retrieval.passage");
  const questionEmbedding = getEmbeddings([question], "retrieval.query")[0];

  const similarities = chunkEmbeddings.map(embed =>
    cosineSimilarity(questionEmbedding, embed));

  const chunksPerSnippet = Math.ceil(options.snippetLength / options.chunkSize);
  const snippets = [];
  const similaritiesCopy = [...similarities];

  for (let i = 0; i < options.numSnippets; i++) {
    let bestStartIndex = 0;
    let bestScore = -Infinity;

    for (let j = 0; j <= similarities.length - chunksPerSnippet; j++) {
      const windowScores = similaritiesCopy.slice(j, j + chunksPerSnippet);
      const windowScore = average(windowScores);

      if (windowScore > bestScore) {
        bestScore = windowScore;
        bestStartIndex = j;
      }
    }

    const startIndex = bestStartIndex * options.chunkSize;
    const endIndex = Math.min(startIndex + options.snippetLength, longContext.length);
    snippets.push(longContext.substring(startIndex, endIndex));

    for (let k = bestStartIndex; k < bestStartIndex + chunksPerSnippet; k++)
      similaritiesCopy[k] = -Infinity;
  }

  return snippets.join("\n\n");
}
```

调用 Jina Embeddings API 的时候，记得把 `task` 设置成 retrieval，打开 `late_chunking` ， `truncate` 也要像下面这样设置：

```
await axios.post(
  'https://api.jina.ai/v1/embeddings',
  {
    model: "jina-embeddings-v3",
    task: "retrieval.passage",
    late_chunking: true,
    input: chunks,
    truncate: true
  },
  { headers });
```

如果是要向量化问题，记得把 `task` 换成 `retrieval.query` ，然后关掉 `late_chunking` 。

完整的实现代码可以在 GitHub 上找到： *https://github.com/jina-ai/node-DeepResearch/blob/main/src/tools/jina-latechunk.ts*

## 为“下一步阅读”进行 URL 排序

问题如下： 在每一次 DeepSearch 漫长过程中，你可能会从搜索引擎结果页（SERP）里收集一堆 URL，每打开一个网页，又能顺藤摸瓜找出不少新链接，就算是去重后，也是轻轻松松几百个网址。同样的，一股脑儿全塞给 LLM 肯定不行，浪费宝贵的上下文长度不说，更要命的是，我们发现 LLM 基本上就是瞎选。所以，得想办法引导 LLM 去挑出那些最有可能包含答案的 URL。

```
curl https://r.jina.ai/https://example.com \
  -H "Accept: application/json" \
  -H "Content-Type: application/json" \
  -H "X-Retain-Images: none" \
  -H "X-Md-Link-Style: discarded" \
  -H "X-Timeout: 20" \
  -H "X-With-Links-Summary: all"
```

这行命令，是在 DeepSearch 里让 Jina Reader 抓取网页的最佳配置。它会把页面上所有链接都单拎出来，放到 links 字段里，同时从 content 字段里把它们删干净。

**你可以把这个问题看作“上下文内的 PageRank”，只不过，我们是在一次会话中对数百个 URL 打分。**  

我们会综合考虑多个因素：最后更新时间、域名出现的频率、网页路径结构，以及最重要的与问题的语义相关性，算出一个综合评分。不过，我们只能使用那些还没点开 URL 就能拿到的信息。

![图片](https://mmbiz.qpic.cn/mmbiz_svg/I1YzhXxW8YAOTWmHRH4bQa8q9OibktrYBLjkLDOvHiaiccpfwjLImbP9D6b41E0FrL7RN0Iiafc3c6SuJ4TeCODzQxtszQNXJqbM/640?wx_fmt=svg&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1#imgIndex=3)

**1\. 频率信号** ：如果某个 URL 在不同的信息源中多次出现，它的权重就会更高。另外，如果某个域名在搜索结果中经常出现，来自这个域名的 URL 也会被加分。因为一般来说，热门域名往往包含更权威的内容。

**2\. 路径结构** ：我们会分析 URL 的路径结构，来判断哪些内容是聚集在一起的。如果多个网址都属于同一个路径层级，它们的分数会更高；但路径越深，分数加成会逐渐减少。

**3\. 语义相关性** ：我们用 `jina-reranker-v2-base-multilingual` 来评估问题和每个 URL 的文本信息（例如标题和摘要）的语义相关性，这是一个典型的重排序问题。每个 URL 的文本信息来自以下几个地方：

- 搜索引擎结果页（SERP）API 返回的标题和摘要（https://s.jina.ai/ 这个接口，加上 'X-Respond-With': 'no-content'，就可以只返回标题和摘要，不返回具体内容）。
- 页面上 URL 的锚文本（用 https://r.jina.ai 接口，设置 'X-With-Links-Summary': 'all'，可以返回页面内所有链接的摘要信息，也就是锚文本)。

**4\. 最后更新时间** ：DeepSearch 的有些查询对时效性要求很高，所以一般来说，越新的 URL 价值越高。但是在不具备像 Google 这样的大规模索引能力的前提下，很难准确判断网页的最后更新时间。我们这里用的是一套组合拳，综合考虑以下信号，最终给出一个带有置信度评分的时间戳，以便在需要时优先展示最新的内容：

- SERP API 提供的筛选功能（比如 s.jina.ai 的 tbs 参数，可以按时间过滤）。
- 元数据提取（比如 meta 标签和 Schema.org 时间戳）。
- 内容模式识别（识别 HTML 里可见的日期）。
- 针对特定 CMS 平台的指标 (比如 WordPress, Drupal, Ghost 这些平台)

**5\. 受限内容** ：某些社交媒体平台的内容是受限的，或者需要付费才能访问。不登录的话，没办法合法地获取这些内容。因此，我们会积极维护一份黑名单，把这些有问题的 URL 和域名都记录下来，降低它们的排名，避免在这些无法访问的内容上浪费计算资源。

**6\. 域名多样性** ：有时候，权重最高的几个网址都来自同一个域名，这会让 DeepSearch 陷入“局部最优”，影响最终结果的质量。就像前面提到的，排名靠前的 URL 全都来自 StackOverflow。为了提高结果的多样性，我们可以用一种“探索-利用”的策略：从每个域名下选择排名 Top K 的 URL。

URL 排序的完整代码实现，可以在我们的 Github 上找到： https://github.com/jina-ai/node-DeepResearch/blob/main/src/utils/url-tools.ts#L192

```
<action-visit>
- Crawl and read full content from URLs, you can get the fulltext, last updated datetime etc of any URL.
- Must check URLs mentioned in <question> if any
- Choose and visit relevant URLs below for more knowledge. higher weight suggests more relevant:
<url-list>
  + weight: 0.20 "https://huggingface.co/docs/datasets/en/loading": "Load - Hugging FaceThis saves time because instead of waiting for the Dataset builder download to time out, Datasets will look directly in the cache. Set the environment ...Some datasets may have more than one version based on Git tags, branches, or commits. Use the revision parameter to specify the dataset version you want to load ..."
  + weight: 0.20 "https://huggingface.co/docs/datasets/en/index": "Datasets - Hugging Face🤗 Datasets is a library for easily accessing and sharing datasets for Audio, Computer Vision, and Natural Language Processing (NLP) tasks. Load a dataset in a ..."
  + weight: 0.17 "https://github.com/huggingface/datasets/issues/7175": "[FSTimeoutError] load_dataset · Issue #7175 · huggingface/datasetsWhen using load_dataset to load HuggingFaceM4/VQAv2, I am getting FSTimeoutError. Error TimeoutError: The above exception was the direct cause of the following ..."
  + weight: 0.15 "https://github.com/huggingface/datasets/issues/6465": "\`load_dataset\` uses out-of-date cache instead of re-downloading a ...When a dataset is updated on the hub, using load_dataset will load the locally cached dataset instead of re-downloading the updated dataset."
  + weight: 0.12 "https://stackoverflow.com/questions/76923802/hugging-face-http-request-on-data-from-parquet-format-when-the-only-way-to-get-i": "Hugging face HTTP request on data from parquet format when the ...I've had to get the data from their data viewer using the parquet option. But when I try to run it, there is some sort of HTTP error. I've tried downloading ..."
</url-list>
</action-visit>
```

## 总结

自 2025 年 2 月 2 日我们的 DeepSearch 开源以来，我们发现了两个能大幅提高质量的工程细节。 **有意思的是，这两个细节都以一种“上下文窗口内”的方式利用了多语言 Embedding 和 Reranker 模型。** 跟这些模型通常需要的大规模预计算索引相比，简直是小巫见大巫。

这可能预示着，未来的搜索技术会朝着两极分化的方向发展。我们可以借用卡尼曼（Kahneman）的双过程理论来理解这个趋势：

- **快思考** **Fast-think** (grep、BM25、SQL)：快速、基于规则的模式匹配，计算量很小。
- **慢思考** **Slow-think** (LLM)：全面推理，具有深层次的上下文理解能力，但计算量很大。
- **中间地** **带** **Mid-think** (Embedding，Reranker 等召回模型): 具备一定的语义理解能力，优于简单的模式匹配，但推理能力远不及 LLM。

有一种可能就是： **两级分化的搜索架构变得越来越流行** ：轻量级、高效的 SQL/BM25 负责检索的输入，然后直接把结果喂给 LLM 进行检索输出。那么，中间层模型的剩余价值就转移到了特定的上下文窗口内的任务上：比如过滤、去重、排序等等。在这些场景下，如果用 LLM 做完整推理反而效率不高。

但无论如何， **挑选关键片段** 和 **URL 排序** 仍然是仍然是直接影响 DeepSearch/DeepResearch 系统质量的根本环节。希望我们的发现能帮助你改进自己的系统。

**查询扩展（Query expansion）是另一个决定质量的关键因** **素。** 我们正在积极评估各种方法，从简单的基于 Prompt 的重写，到小模型，再到基于推理的方法。请期待我们后续在这个方向上的研究成果！

  

**活动报名开启**

![图片](https://mmbiz.qpic.cn/sz_mmbiz_png/3EjVEqjYF3I1Du00fibf7PQaZiaIFX8xSYQWOJ4zqIkf5uhyI5GYLZr23ssWRPxDywhZd7rtmEux9QEKiaxLXHFJQ/640?wx_fmt=png&from=appmsg&tp=webp&wxfrom=5&wx_lazy=1#imgIndex=4)

  

继续滑动看下一个

Jina AI

向上滑动看下一个