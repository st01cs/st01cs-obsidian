---
created: 2025-09-19
tags:
  - note
  - journal
url: https://learn.deeplearning.ai/courses/ai-agents-in-langgraph/
---
# Build an Agent from Scratch

[AI Agents in LangGraph - DeepLearning.AI](https://learn.deeplearning.ai/courses/ai-agents-in-langgraph/lesson/c1l2c/build-an-agent-from-scratch)

手工执行一个ReACT Agent
- 调用LLM获取结果
- 手工执行Action
- 拼装Action结果为next_prompt
- 继续执行到得出结果

把手动执行过程自动化（循环）
- 正则判断有没有Action
	- 有Action则调用
	- 没有Action结束

# [LangGraphh Components ](https://learn.deeplearning.ai/courses/ai-agents-in-langgraph/lesson/l7rgk/langgraph-components)

LangGraph实现同一个Agent

# [ Agentic Search Tools](https://learn.deeplearning.ai/courses/ai-agents-in-langgraph/lesson/oj6p9/agentic-search-tools)

