---
title: "TradingAgents: Multi-Agents LLM Financial Trading Framework"
source: "https://tradingagents-ai.github.io/"
author:
published:
created: 2025-10-01
description: "TradingAgents: Multi-Agents LLM Financial Trading Framework"
tags:
  - "clippings"
---
## Abstract

We introduce **TradingAgents**, a novel stock trading framework inspired by trading firms, utilizing multiple LLM-powered agents with specialized roles such as fundamental, sentiment, and technical analysts, as well as traders with diverse risk profiles. The system features Bull and Bear researchers evaluating market conditions, a risk management team overseeing exposure, and traders integrating insights from debates and historical data to make informed decisions. This collaborative, dynamic environment enhances trading performance, as demonstrated by our comprehensive experiments showing significant improvements in cumulative returns, Sharpe ratio, and maximum drawdown compared to baseline models. Our results highlight the effectiveness of multi-agent LLM frameworks in financial trading.

## TradingAgents: Overview

**TradingAgents** leverages a multi-agent framework to simulate a professional trading firm with distinct roles: fundamental, sentiment, and technical analysts; researchers; traders; and risk managers. These agents collaborate through structured communication and debates, enhancing decision-making and optimizing trading strategies.

![TradingAgents Overall Framework Organization](https://tradingagents-ai.github.io/static/images/schema.png)

Figure 1: TradingAgents Overall Framework Organization. I. Analysts Team: Four analysts concurrently gather relevant market information. II. Research Team: The team discusses and evaluates the collected data. III. Trader: Based on the researchers' analysis, the trader makes the trading decision. IV. Risk Management Team: Risk guardians assess the decision against current market conditions to mitigate risks. V. Fund Manager: The fund manager approves and executes the trade.

## TradingAgents: Role Specialization

Assigning specific roles to LLM agents allows complex trading objectives to be broken down into manageable tasks. Inspired by trading firms, **TradingAgents** features seven distinct roles: Fundamentals Analyst, Sentiment Analyst, News Analyst, Technical Analyst, Researcher, Trader, and Risk Manager. Each agent is equipped with specialized tools and constraints tailored to their function, ensuring comprehensive market analysis and informed decision-making.

### Analyst Team

The Analyst Team gathers and analyzes market data across various domains:

- **Fundamental Analysts:** Assess company fundamentals to identify undervalued or overvalued stocks.
- **Sentiment Analysts:** Analyze social media and public sentiment to gauge market mood.
- **News Analysts:** Evaluate news and macroeconomic indicators to predict market movements.
- **Technical Analysts:** Use technical indicators to forecast price trends and trading opportunities.

Combined, their insights provide a holistic market view, feeding into the Researcher Team for further evaluation.

![TradingAgents Analyst Team](https://tradingagents-ai.github.io/static/images/Analyst.png)

Figure 2: TradingAgents Analyst Team

### Researcher Team

The Researcher Team critically evaluates analyst data through a dialectical process involving bullish and bearish perspectives. This debate ensures balanced analysis, identifying both opportunities and risks to inform trading strategies.

![TradingAgents Researcher Team](https://tradingagents-ai.github.io/static/images/Researcher.png)

Figure 3: TradingAgents Researcher Team

![TradingAgents Trader Decision-Making Process](https://tradingagents-ai.github.io/static/images/Trader.png)

Figure 4: TradingAgents Trader Decision-Making Process

![TradingAgents Risk Management Team Workflow](https://tradingagents-ai.github.io/static/images/RiskMGMT.png)

Figure 5: TradingAgents Risk Management Workflow

- **Bullish Researchers:** Highlight positive market indicators and growth potential.
- **Bearish Researchers:** Focus on risks and negative market signals.

This process ensures a balanced understanding of market conditions, aiding Trader Agents in making informed decisions.

### Trader Agents

Trader Agents execute decisions based on comprehensive analyses. They evaluate insights from analysts and researchers to determine optimal trading actions, balancing returns and risks in a dynamic market environment.

- Assessing analyst and researcher recommendations.
- Determining trade timing and size.
- Executing buy/sell orders.
- Adjusting portfolios in response to market changes.

Precision and strategic thinking are essential for their role in maximizing performance.

### Risk Management Team

The Risk Management Team oversees the firm's exposure to market risks, ensuring trading activities stay within predefined limits.

- Assessing market volatility and liquidity.
- Implementing risk mitigation strategies.
- Advising Trader Agents on risk exposures.
- Aligning portfolio with risk tolerance.

They ensure financial stability and safeguard assets through effective risk control.

All agents utilize the ReAct prompting framework, facilitating a collaborative and dynamic decision-making process reflective of real-world trading systems.

## TradingAgents: Agent Workflow

### Communication Protocol

To enhance communication efficiency, **TradingAgents** employs a structured protocol that combines clear, structured outputs with natural language dialogue. This approach minimizes information loss and maintains context over long interactions, ensuring focused and effective communication among agents.

### Types of Agent Interactions

Unlike previous frameworks that rely heavily on unstructured dialogue, our agents communicate through structured reports and diagrams, preserving essential information and enabling direct queries from the global state.

- **Analyst Team:** Compiles research into concise analysis reports.
- **Traders:** Review analyst reports and produce decision signals with detailed rationales.

Natural language dialogue is reserved for specific interactions, such as debates within the Researcher and Risk Management teams, fostering deeper reasoning and balanced decision-making.

- **Researcher Team:** Engages in debates to form balanced perspectives.
- **Risk Management Team:** Deliberates on trading plans from multiple risk perspectives.
- **Fund Manager:** Reviews and approves risk-adjusted trading decisions.

### Backbone LLMs

We select LLMs based on task requirements, using quick-thinking models for data retrieval and deep-thinking models for in-depth analysis and decision-making. This strategic alignment ensures efficiency and robust reasoning, allowing **TradingAgents** to operate without the need for GPUs and enabling easy integration of alternative models in the future.

## Experiments

We evaluated **TradingAgents** using a comprehensive experimental setup to assess its performance against various baselines.

### Back Trading

Our simulation utilized a multi-asset, multi-modal financial dataset including historical stock prices, news articles, social media sentiments, insider transactions, financial reports, and technical indicators from January to March 2024.

### Simulation Setup

The trading environment spanned from June to November 2024. Agents operated on a daily basis, making decisions based on available data without future information, ensuring unbiased results.

### Baseline Models

We compared **TradingAgents** against the following strategies:

- **Buy and Hold:** Investing equally across selected stocks throughout the period.
- **MACD:** Momentum strategy based on MACD crossovers.
- **KDJ & RSI:** Combined momentum indicators for trading signals.
- **ZMR:** Mean reversion strategy based on price deviations.
- **SMA:** Trend-following strategy using moving average crossovers.

### Evaluation Metrics

![Cumulative Returns on AAPL](https://tradingagents-ai.github.io/static/images/CumulativeReturns_AAPL.png)

(a) Cumulative Returns on AAPL

![TradingAgents Transactions for AAPL](https://tradingagents-ai.github.io/static/images/TradingAgents_Transactions_AAPL.png)

(b) TradingAgents Transactions for AAPL. Green / Red Arrows for Long / Short Positions.

<table><thead><tr><th>Categories</th><th>Models</th><th colspan="4">AAPL</th><th></th><th colspan="4">GOOGL</th><th></th><th colspan="4">AMZN</th></tr><tr><th></th><th></th><th>CR%↑</th><th>ARR%↑</th><th>SR↑</th><th>MDD%↓</th><th></th><th>CR%↑</th><th>ARR%↑</th><th>SR↑</th><th>MDD%↓</th><th></th><th>CR%↑</th><th>ARR%↑</th><th>SR↑</th><th>MDD%↓</th></tr></thead><tbody><tr><td>Market</td><td>B&amp;H</td><td>-5.23</td><td>-5.09</td><td>-1.29</td><td>11.90</td><td></td><td>7.78</td><td>8.09</td><td>1.35</td><td>13.04</td><td></td><td>17.1</td><td>17.6</td><td>3.53</td><td>3.80</td></tr><tr><td rowspan="4">Rule-based</td><td>MACD</td><td>-1.49</td><td>-1.48</td><td>-0.81</td><td>4.53</td><td></td><td>6.20</td><td>6.26</td><td>2.31</td><td>1.22</td><td></td><td>-</td><td>-</td><td>-</td><td>-</td></tr><tr><td>KDJ&amp;RSI</td><td>2.05</td><td>2.07</td><td>1.64</td><td>1.09</td><td></td><td>0.4</td><td>0.4</td><td>0.02</td><td>1.58</td><td></td><td>-0.77</td><td>-0.76</td><td>-2.25</td><td>1.08</td></tr><tr><td>ZMR</td><td>0.57</td><td>0.57</td><td>0.17</td><td>0.86</td><td></td><td>-0.58</td><td>0.58</td><td>2.12</td><td>2.34</td><td></td><td>-0.77</td><td>-0.77</td><td>-2.45</td><td>0.82</td></tr><tr><td>SMA</td><td>-3.2</td><td>-2.97</td><td>-1.72</td><td>3.67</td><td></td><td>6.23</td><td>6.43</td><td>2.12</td><td>2.34</td><td></td><td>11.01</td><td>11.6</td><td>2.22</td><td>3.97</td></tr><tr><td rowspan="1">Ours</td><td><strong>TradingAgents</strong></td><td><strong>26.62</strong></td><td><strong>30.5</strong></td><td><strong>8.21</strong></td><td>0.91</td><td></td><td><strong>24.36</strong></td><td><strong>27.58</strong></td><td><strong>6.39</strong></td><td>1.69</td><td></td><td><strong>23.21</strong></td><td><strong>24.90</strong></td><td><strong>5.60</strong></td><td>2.11</td></tr><tr><td colspan="2">Improvement(%)</td><td>24.57</td><td>28.43</td><td>6.57</td><td>-</td><td></td><td>16.58</td><td>19.49</td><td>4.26</td><td>-</td><td></td><td>6.10</td><td>7.30</td><td>2.07</td><td>-</td></tr></tbody></table>

**Table 1:** TradingAgents: Performance Metrics Comparison across AAPL, GOOGL, and AMZN.

### Sharpe Ratio

**TradingAgents** achieves superior risk-adjusted returns, consistently outperforming all baselines across AAPL, GOOGL, and AMZN. The enhanced Sharpe Ratios demonstrate the framework's effectiveness in balancing returns with risk, highlighting its robustness in diverse market conditions.

### Maximum Drawdown

While rule-based strategies excel in controlling risk, **TradingAgents** maintains a low maximum drawdown without sacrificing high returns. This balance underscores the framework's ability to maximize profits while effectively managing risk.

### Explainability

Unlike traditional deep learning models, **TradingAgents** offers transparent decision-making through natural language explanations. Each agent's actions are accompanied by detailed reasoning and tool usage, making the system's operations easily interpretable and debuggable, which is crucial for real-world financial applications.

## Conclusion

We presented **TradingAgents**, a multi-agent LLM-driven stock trading framework that emulates a realistic trading firm with specialized agents collaborating through debates and structured communication. Our framework leverages diverse data sources and multi-agent interactions to enhance trading decisions, achieving superior performance in cumulative returns, Sharpe ratio, and risk management compared to traditional strategies. Future work includes live deployment, expanding agent roles, and integrating real-time data processing to further improve performance.

## BibTeX

```
@article{xiao2024tradingagents,
  title={TradingAgents: Multi-Agents LLM Financial Trading Framework},
  author={Xiao, Yijia and Sun, Edward and Luo, Di and Wang, Wei},
  journal={arXiv preprint arXiv:2412.20138},
  year={2024}
}
```