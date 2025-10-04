---
title: "ai4trade/XtQuant: 迅投QMT接口"
source: "https://github.com/ai4trade/XtQuant"
author:
  - "[[ai4trade]]"
published:
created: 2025-09-30
description: "迅投QMT接口. Contribute to ai4trade/XtQuant development by creating an account on GitHub."
tags:
  - "clippings"
---
[Skip to content](https://github.com/ai4trade/#start-of-content)

**[XtQuant](https://github.com/ai4trade/XtQuant)** Public

- [Fork 101 Fork your own copy of ai4trade/XtQuant](https://github.com/ai4trade/XtQuant/fork)

迅投QMT接口

### License

[MIT license](https://github.com/ai4trade/XtQuant/blob/main/LICENSE)

[Open in github.dev](https://github.dev/) [Open in a new github.dev tab](https://github.dev/) [Open in codespace](https://github.com/codespaces/new/ai4trade/XtQuant?resume=1)

## ai4trade/XtQuant

## Add file

## XtQuant

迅投QMT接口相关介绍和常用功能封装，详细文章介绍请移步公众号

## 目录

- [XtQuant](https://github.com/ai4trade/#xtquant)
	- [目录](https://github.com/ai4trade/#%E7%9B%AE%E5%BD%95)
	- [初探迅投QMT极简策略系统](https://github.com/ai4trade/#%E5%88%9D%E6%8E%A2%E8%BF%85%E6%8A%95qmt%E6%9E%81%E7%AE%80%E7%AD%96%E7%95%A5%E7%B3%BB%E7%BB%9F)
	- [行情接口分析](https://github.com/ai4trade/#%E8%A1%8C%E6%83%85%E6%8E%A5%E5%8F%A3%E5%88%86%E6%9E%90)
		- [行情接口以及历史行情数据下载](https://github.com/ai4trade/#%E8%A1%8C%E6%83%85%E6%8E%A5%E5%8F%A3%E4%BB%A5%E5%8F%8A%E5%8E%86%E5%8F%B2%E8%A1%8C%E6%83%85%E6%95%B0%E6%8D%AE%E4%B8%8B%E8%BD%BD)
		- [历史行情批量缓存](https://github.com/ai4trade/#%E5%8E%86%E5%8F%B2%E8%A1%8C%E6%83%85%E6%89%B9%E9%87%8F%E7%BC%93%E5%AD%98)
		- [历史行情转存数据库](https://github.com/ai4trade/#%E5%8E%86%E5%8F%B2%E8%A1%8C%E6%83%85%E8%BD%AC%E5%AD%98%E6%95%B0%E6%8D%AE%E5%BA%93)
		- [实时行情接口接入](https://github.com/ai4trade/#%E5%AE%9E%E6%97%B6%E8%A1%8C%E6%83%85%E6%8E%A5%E5%8F%A3%E6%8E%A5%E5%85%A5)
	- [量化策略研究](https://github.com/ai4trade/#%E9%87%8F%E5%8C%96%E7%AD%96%E7%95%A5%E7%A0%94%E7%A9%B6)
		- [新闻事件量化](https://github.com/ai4trade/#%E6%96%B0%E9%97%BB%E4%BA%8B%E4%BB%B6%E9%87%8F%E5%8C%96)
		- [技术面特征提取](https://github.com/ai4trade/#%E6%8A%80%E6%9C%AF%E9%9D%A2%E7%89%B9%E5%BE%81%E6%8F%90%E5%8F%96)
		- [跨市场联动](https://github.com/ai4trade/#%E8%B7%A8%E5%B8%82%E5%9C%BA%E8%81%94%E5%8A%A8)

---

## 初探迅投QMT极简策略系统

[初探迅投QMT极简策略系统](https://mp.weixin.qq.com/s/5XI09nyStjmD0faYs9UIlw) 迅投QMT是一个门槛相对较低、功能强大的量化策略交易系统。本文首先介绍一些背景知识，并主要分析极简策略交易系统的一些功能，后续将陆续分享行情、交易、策略等相关实战教程。

## 行情接口分析

### 行情接口以及历史行情数据下载

[行情接口以及历史行情数据下载](https://mp.weixin.qq.com/s/R2WquJUD4Mu6wuoFjoC3AQ):本文主要介绍QMT行情接口概况和一个历史行情数据下载案例

### 历史行情批量缓存

[历史行情批量缓存](https://mp.weixin.qq.com/s/l-pFVnqsWjLP1iBM63dD9Q):本文进一步介绍如何获取批量股票代码并缓存对应的tick、分钟、日级别的历史数据。

### 历史行情转存数据库

[迅投QMT历史行情转存Clickhouse数据库](https://mp.weixin.qq.com/s/5337pliFLRlpQoEkQA31Og): 本节介绍如何将读取本地的缓存数据并写入到clickhouse数据库中。历史行情数据从格式上看分为tick数据和K线数据两大类，针对这两类的数据我们分别处理。

### 实时行情接口接入

[迅投QMT实时行情接口接入](https://mp.weixin.qq.com/s/cWYXulT-daBgrDtr36CHAA): 迅投QMT量化平台的xtquant库提供了python操作API，我们利用其提供的全推行情能力封装成独立的实时行情服务，实现tick、1Min等粒度的行情加工，为后续实时因子和交易信号生成提供基础保障。

## 量化策略研究

### 新闻事件量化

[基于新闻事件Bert序列建模的行业涨跌预测](https://mp.weixin.qq.com/s/CJxhVB6m2-DINp1mGNL4Bw): 利用先进的深度学习技术单独分析新闻事件序列对行业指数的短期影响，和读者一起探讨利用AI做行业选股的可行性。

### 技术面特征提取

[利用pandas\_ta自动提取技术面特征](https://mp.weixin.qq.com/s/PPduk4xPcix9USW9HmUpHw): TA-Lib是一个技术分析库，涵盖了150多种股票、期货交易软件中常用的技术分析指标，如MACD、RSI、KDJ、动量指标、布林带等等，而pandas-ta则是一个基于pandas和ta-lib的高级技术分析工具，具有130多个指标和实用功能以及60多个TA-Lib中包含的蜡烛模式。本章节记录如何利用pandas-ta快速提取技术面特征。

### 跨市场联动

[跨市场联动: 基于美股隔日行情预测A股行业涨跌](https://mp.weixin.qq.com/s/4d6ihxZ7V73iSWUfyaz7tg): 随着A股北上资金的不断涌入，跨市场联动性也愈发显著，在内循环的同时也时刻受着外部重要市场行情波动的影响，美股作为全球市场，一丝风吹草动都对全球金融造成剧烈波动。本文将探索美股行情中的技术面因子对当天A股市场的行业影响，使用机器学习技术预测行业涨跌情况，并同基准沪深300指数作对比以说明实际效果。

---

欢迎关注我的公众号“ **量化实战** ”，原创技术文章第一时间推送。

[![公众号](https://github.com/ai4trade/XtQuant/raw/main/misc/qrcode.jpg)](https://github.com/ai4trade/XtQuant/blob/main/misc/qrcode.jpg)

## Releases

No releases published

## Packages

No packages published  

## Languages

- [Python 100.0%](https://github.com/ai4trade/XtQuant/search?l=python)