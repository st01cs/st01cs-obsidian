---
title: PandaAI-Tech/panda_factor
source: https://github.com/PandaAI-Tech/panda_factor?tab=readme-ov-file
author:
  - "[[PandaAI-Tech]]"
published:
created: 2025-09-30
description: Contribute to PandaAI-Tech/panda_factor development by creating an account on GitHub.
tags:
  - clippings
  - quant
---
**[panda\_factor](https://github.com/PandaAI-Tech/panda_factor)** Public

[AGPL-3.0 license](https://github.com/PandaAI-Tech/panda_factor/blob/main/LICENSE)

[Open in github.dev](https://github.dev/) [Open in a new github.dev tab](https://github.dev/) [Open in codespace](https://github.com/codespaces/new/PandaAI-Tech/panda_factor?resume=1)

[![预览](https://camo.githubusercontent.com/36c19059f3436921abe14a12a73ff7dd1326ba25482708b29e642598f24e2ca6/68747470733a2f2f7a796e662d746573742e6f73732d636e2d7368616e676861692e616c6979756e63732e636f6d2f6769746875622f657a6769662d38346463356134393936333234362e676966)](https://camo.githubusercontent.com/36c19059f3436921abe14a12a73ff7dd1326ba25482708b29e642598f24e2ca6/68747470733a2f2f7a796e662d746573742e6f73732d636e2d7368616e676861692e616c6979756e63732e636f6d2f6769746875622f657a6769662d38346463356134393936333234362e676966)

## PandaAI首届因子大赛已启动，你的Alpha值得被看见

“没有一个alpha，一开始就是alpha”

“开始量化，最好是十年前，其次是现在”

“如果没有天赋，那就一直重复”

“看似不起眼的数学，会在将来的某一天，突然让你看到坚持的意义”

“一切都很好，我听到自己，向上的声音”

“市场会惩罚，模糊的愿望，奖励清晰的请求”

“你正在寻找的因子，此刻也在寻找你”

[点击报名](https://www.pandaai.online/factorhub/factorcompetition)

## 概述

PandaFactor 提供了一系列高性能的量化算子，用于金融数据分析、技术指标计算和因子构建，并且提供了一系列的可视化图表。

## 因子编写方法

编写方法主要分为两种方式：

- Python方式（适合有一定编程基础的小伙伴）（易维护，推荐）
- 公式方式（适合无编程基础的小伙伴）

### Python模式

基本语法

```
class CustomFactor(Factor):
    def calculate(self, factors):
        return result
```

重点要求，必须继承Factor，必须实现calculate方法，calculate返回值必须是Series格式，列为value，索引列为\['symbol','date'\]构成的多级索引。

factors包含了基础的量价信息，例如:"close"、"open"、“volume”等，可通过factors\['close'\]方式获取。

#### 示例

```
class ComplexFactor(Factor):
    def calculate(self, factors):
        close = factors['close']
        volume = factors['volume']
        high = factors['high']
        low = factors['low']
        
        # 计算20日收益率
        returns = (close / DELAY(close, 20)) - 1
        # 计算20日波动率
        volatility = STDDEV((close / DELAY(close, 1)) - 1, 20)
        # 计算价格区间
        price_range = (high - low) / close
        # 计算成交量比率
        volume_ratio = volume / DELAY(volume, 1)
        # 计算20日成交量均值
        volume_ma = SUM(volume, 20) / 20
        # 计算动量信号
        momentum = RANK(returns)
        # 计算波动率信号
        vol_signal = IF(volatility > DELAY(volatility, 1), 1, -1)
        # 合成最终因子
        result = momentum * vol_signal * SCALE(volume_ratio / volume_ma)
        return result
```

### 公式方式

基本语法

```
"函数1(函数2(基础因子), 参数) 运算符 函数3(基础因子)"
```

若是公式比较复杂，可以考虑设置中间变量，分多行编写，系统将读取最后一行作为因子值。

```
# 计算20日收益率排名
RANK((CLOSE / DELAY(CLOSE, 20)) - 1)

# 计算价格和成交量的相关性
CORRELATION(CLOSE, VOLUME, 20)

# 复杂因子示例
RANK((CLOSE / DELAY(CLOSE, 20)) - 1) * 
STDDEV((CLOSE / DELAY(CLOSE, 1)) - 1, 20) * 
IF(CLOSE > DELAY(CLOSE, 1), 1, -1)
```

## 函数和算子支持情况

[点击查看](https://www.pandaai.online/community/article/72)

## 安装

- 若您为个人交易者，想要快速本地的使用该因子模块，我们准备了一份初始数据库，解压即可运行，因为文件较大，请联系小助理领取，下载解压后，直接执行bin/db\_start.bat即可启动数据库。
- 若您为团队或者机构使用者，可以下载系统源码，在本地部署供团队使用。需要提前准备MongoDB，并且修改panda\_common的config.yaml的文件与其对应。

## 关于数据更新

目前系统内置了近五年的基础数据，供用户使用。后续的数据更新将在每晚8点自动清洗执行（需要保证程序在期间正常运行），我们计划对接以下数据源：

| 数据源 | 支持情况 |
| --- | --- |
| Tushare | 已上线 |
| RiceQuant | 已上线 |
| 迅投 | 已上线 |
| Tqsdk | 测试中 |
| QMT | 测试中 |
| Wind | 对接中 |
| Choice | 对接中 |

若您有相关数据源需求，请务必联系我们，我们会尽快为您接入。

## 下载最新数据库

因表结构更新，请在网盘下载最新的数据库 网盘链接: [https://pan.baidu.com/s/15jip2SATiORuqaBNMDm4fw?pwd=uupm](https://pan.baidu.com/s/15jip2SATiORuqaBNMDm4fw?pwd=uupm) 提取码: uupm 近期更新因子持久化功能，让计算好的因子直接保存，自动更新，极速提取。

## 📁 项目结构

```
panda_factor/
├── panda_common/       # 公共函数&工具类
│   └── config.yaml     # 配置文件
├── panda_data          # 数据模块，提取数据与因子
├── panda_data_hub/     # 自动更新
│   └── __main__.py     # 自动更新任务启动入口
├── panda_factor        # 因子计算与分析
├── panda_llm           # 大模型接入，支持OpenAI协议，兼容Deepseek
├── panda_factor_server/       # 服务器接口
│   └── __main__.py     # 接口服务启动入口
├── panda_web/          # 服务器前端页面
├── requirements.txt    # 依赖列表
└── README.md           # 项目说明文
```

## 开发者工具指南

### PyCharm工具

请将panda\_common、panda\_data、panda\_data\_hub、panda\_factor、panda\_llm、panda\_factor\_server这几个文件夹右键标记为Mark Directiory as Sources root

请在含有Python解释器的终端中进入各个子模块目录下面，执行：

```
pip install -e .
```

### 如何在自己的系统或策略中引用因子

项目本身只是帮助大家生产和更新因子，避免大家在数据清洗、自动化构建上花太多时间。 可通过以下代码，将生产的因子整合到自己的系统或者策略中：

```
import panda_data

panda_data.init()
factor = panda_data.get_factor_by_name(factor_name="VH03cc651", start_date='20240320',end_date='20250325')
```

## 加群答疑（备注【开源】更快通过）

[![PandaAI 交流群](https://camo.githubusercontent.com/51f206f0e21bfeb4faca2835121ea64c9962ff8505db342d11db44f8ef4d179d/68747470733a2f2f7a796e662d746573742e6f73732d636e2d7368616e676861692e616c6979756e63732e636f6d2f6769746875622f7765636861745f323032352d30362d32375f3130323633335f3631352e706e67)](https://camo.githubusercontent.com/51f206f0e21bfeb4faca2835121ea64c9962ff8505db342d11db44f8ef4d179d/68747470733a2f2f7a796e662d746573742e6f73732d636e2d7368616e676861692e616c6979756e63732e636f6d2f6769746875622f7765636861745f323032352d30362d32375f3130323633335f3631352e706e67)

## 贡献

欢迎贡献代码、提出 Issue 或 PR：

Fork 本项目

新建功能分支 git checkout -b feature/AmazingFeature

提交更改 git commit -m 'Add some AmazingFeature'

推送分支 git push origin feature/AmazingFeature

发起 Pull Request

## 致谢

感谢量化李不白的粉丝们对我们的支持

感谢所有开源社区的贡献者

## 许可证

本项目采用 GPLV3 许可证

## Releases

No releases published

## Packages

No packages published  

## Languages

- [Python 98.4%](https://github.com/PandaAI-Tech/panda_factor/search?l=python)
- [JavaScript 1.2%](https://github.com/PandaAI-Tech/panda_factor/search?l=javascript)
- Other 0.4%