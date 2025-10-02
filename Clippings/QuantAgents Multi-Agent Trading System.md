---
title: "QuantAgents: Multi-Agent Trading System"
source: "https://y-research-sbu.github.io/QuantAgent/"
author:
  - "[[Fei Xiong]]"
  - "[[Xiang Zhang]]"
  - "[[Aosong Feng]]"
  - "[[Siqi Sun]]"
  - "[[Chenyu You]]"
published:
created: 2025-10-01
description:
tags:
  - "clippings"
---
## QuantAgent: Price-Driven Multi-Agent LLMs for High-Frequency Trading

## Abstract

Recent advances in Large Language Models (LLMs) have demonstrated impressive capabilities in financial reasoning and market understanding. However, existing LLM frameworks for High-Frequency Trading (HFT) face significant limitations in terms of latency, interpretability, and the ability to handle real-time market dynamics. We introduce QuantAgent, the first multi-agent LLM framework specifically designed for HFT, which decomposes trading into four specialized agents: Indicator, Pattern, Trend, and Risk.

Our framework leverages structured financial priors and language-native reasoning to achieve superior performance in zero-shot evaluations across ten financial instruments, including Bitcoin and Nasdaq futures, in terms of predictive accuracy and cumulative return over 4-hour trading intervals. The results suggest that combining structured financial priors with language-native reasoning unlocks new potential for traceable, real-time decision systems in high-frequency financial markets.

## Multi-Agent Interaction

**Indicator Agent**: Comprehensive technical analysis using multiple indicators including RSI, MACD, and Bollinger Bands to generate robust trading signals with high accuracy.

![Indicator Agent](https://y-research-sbu.github.io/QuantAgent/assets/indicator.png) 

## Evaluation Metrics

![Benchmark Asset Properties](https://y-research-sbu.github.io/QuantAgent/assets/benchmark_4h.png)

Overview of 4-hour benchmark asset properties. Each asset is characterized by its name, market type, the start and end dates of the data collection window, and the total number of bars sampled.

![Benchmark Asset Properties](https://y-research-sbu.github.io/QuantAgent/assets/benchmark_1h.png)

Overview of 1-hour benchmark asset properties. Each asset is characterized by its name, market type, the start and end dates of the data collection window, and the total number of bars sampled.

## Main Results

![Performance Comparison Table](https://y-research-sbu.github.io/QuantAgent/assets/table1.png)

4-hour Performance comparison across assets between a random baseline, Linear Regression (LR), XGBoost and our method (highlighted in green). Upward arrows indicate improvements on metrics where higher is better. Bold values indicate the highest (best) results for each metric.

![Performance Comparison Line Chart](https://y-research-sbu.github.io/QuantAgent/assets/1hour.png)

Line chart of 1-hour performance comparison across assets between a random baseline, Linear Regression, XGBoost, and our method (shown in red).

### Detailed Analysis

**Rolling Performance**: Sample-based directional accuracy on SPX. Of 10 LLM-generated signals, correct predictions are shown in green/red, errors in grey, yielding 80% accuracy during the highlighted period.

![Rolling Performance](https://y-research-sbu.github.io/QuantAgent/assets/rolling.png)

## BibTeX

```
@article{xiong2025quantagent,
  title={QuantAgent: Price-Driven Multi-Agent LLMs for High-Frequency Trading},
  author={Fei Xiong and Xiang Zhang and Aosong Feng and Siqi Sun and Chenyu You},
  journal={arXiv preprint arXiv:2509.09995},
  year={2025}
}
```