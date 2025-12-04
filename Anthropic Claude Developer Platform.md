Anthropic最新发布的Claude Developer Platform功能，开启了AI代理工具使用的新纪元。未来的AI代理将无缝调用数百甚至数千种工具，像IDE助手整合Git操作、文件管理、测试框架，或运维协调连接Slack、GitHub、Jira等多个系统。  
  
他们面临的最大挑战是：如何避免因预加载海量工具定义而导致的上下文爆炸？传统方式可能消耗十万以上tokens，严重影响模型性能。Anthropic提出“工具按需发现”策略——Tool Search Tool，让Claude只加载当前任务真正需要的工具，节省85%上下文空间，大幅提升准确率和响应速度。  
  
另一方面，传统自然语言调用工具方式带来的上下文污染和多次推理开销，也被Programmatic Tool Calling（编程式工具调用）彻底革新。Claude通过生成Python代码来批量调用、处理工具数据，只把最终结果放入上下文，极大节省token消耗（约降37%），降低延迟，并提高了复杂流程的执行准确度。  
  
此外，JSON Schema虽能定义参数结构，却难以表达正确用法和参数间的关联。Anthropic引入Tool Use Examples，允许开发者通过示例明确工具调用规范，显著提升复杂参数场景下的调用准确率（测试中从72%提升到90%）。  
  
这三项功能——工具搜索、编程调用、用例示范——协同解决了大规模多工具场景下的发现效率、执行效率和调用准确度问题。它们不仅适合构建跨多个服务的大型系统，也为开发者提供了灵活、高效的工具管理和调用新范式。  
  
开发者可根据应用场景分层使用，先从最大瓶颈入手：  
- 上下文爆炸优先用Tool Search Tool  
- 中间数据过多用Programmatic Tool Calling  
- 参数复杂易错用Tool Use Examples  
  
Anthropic的实践证明，这样的设计大幅提升了AI代理的实用性和稳定性，推动智能代理从简单调用迈向智能编排。期待更多创新应用在Claude平台上诞生。  
  
原文详见 anthopic.com/engineering/advanced-tool-use  
  
——  
这项技术展示了AI工具集成的未来方向：动态发现、代码驱动执行和示范引导，三者合力打造高效、精准、可扩展的智能代理生态。对希望打造复杂多工具AI系统的开发者来说，Anthropic的方案无疑提供了宝贵的参考和实践路径。

![](https://tvax1.sinaimg.cn/large/5396ee05ly8i7vc9vq7zpj21hb0u0whn.jpg)

![](https://tvax1.sinaimg.cn/large/5396ee05ly8i7vc9y0xamj21480u0gnz.jpg)

![](https://tvax2.sinaimg.cn/large/5396ee05ly8i7vccvh038j21hp0u0tgj.jpg)