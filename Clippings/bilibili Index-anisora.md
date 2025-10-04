---
title: "Index-anisora/README_CN.md at main · bilibili/Index-anisora"
source: "https://github.com/bilibili/Index-anisora/blob/main/README_CN.md"
author:
published:
created: 2025-09-30
description:
tags:
  - "clippings"
---
[Open in github.dev](https://github.dev/) [Open in a new github.dev tab](https://github.dev/) [Open in codespace](https://github.com/codespaces/new/bilibili/Index-anisora/tree/main?resume=1)

[update Wan&AniSora evaluation results on AniSora-Benchmark](https://github.com/bilibili/Index-anisora/commit/0b2a6fec8d20918df4b1256bc29cf91ab2bb624a)

[0b2a6fe](https://github.com/bilibili/Index-anisora/commit/0b2a6fec8d20918df4b1256bc29cf91ab2bb624a) ·

[![](https://github.com/bilibili/Index-anisora/raw/main/assets/index_icon.png)](https://github.com/bilibili/Index-anisora/blob/main/assets/index_icon.png)

🖥️ [GitHub](https://github.com/bilibili/Index-anisora/tree/main) | 🤗 [Hugging Face](https://huggingface.co/IndexTeam/Index-anisora) | 🤖 [Model Scope](https://www.modelscope.cn/organization/bilibili-index) | 📑 ｜ 📑  

**中文简体** | [**English**](https://github.com/bilibili/Index-anisora/blob/main/README.md)

  

---

[**Index‑AniSora：终极开源动漫视频生成模型**](http://arxiv.org/abs/2412.10255)

本项目是哔哩哔哩献给二次元世界的礼物—— **Index‑AniSora** ，目前最强大的开源动漫视频生成模型。  
它支持一键生成多种动漫风格的视频镜头，包括番剧片段、国创动画、漫画改编、VTuber 内容、动画 PV、鬼畜（MAD）等！  
该项目基于我们已被 IJCAI ’25 录用的论文  
[*AniSora: Exploring the Frontiers of Animation Video Generation in the Sora Era*](http://arxiv.org/abs/2412.10255)

## 🎬 视频演示

anisora\_re2\_small.mp4<video src="https://private-user-images.githubusercontent.com/1173937/445397527-4351fc5e-f7fd-456b-807e-82fdcb321de2.mp4?jwt=eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3NTkyMDI4NzYsIm5iZiI6MTc1OTIwMjU3NiwicGF0aCI6Ii8xMTczOTM3LzQ0NTM5NzUyNy00MzUxZmM1ZS1mN2ZkLTQ1NmItODA3ZS04MmZkY2IzMjFkZTIubXA0P1gtQW16LUFsZ29yaXRobT1BV1M0LUhNQUMtU0hBMjU2JlgtQW16LUNyZWRlbnRpYWw9QUtJQVZDT0RZTFNBNTNQUUs0WkElMkYyMDI1MDkzMCUyRnVzLWVhc3QtMSUyRnMzJTJGYXdzNF9yZXF1ZXN0JlgtQW16LURhdGU9MjAyNTA5MzBUMDMyMjU2WiZYLUFtei1FeHBpcmVzPTMwMCZYLUFtei1TaWduYXR1cmU9MmY5MjVkMGM2MTRlOGZmODg2YzhkNjRhMzExNDE2ZTdjNGZjNDJmOGEyZTM3NmE3YjJkMmNjNmYxNzI3OTMzYSZYLUFtei1TaWduZWRIZWFkZXJzPWhvc3QifQ.almvge-Qk9TMcIp6kbvhw89ZOp7_A5Shpt4k1ExhoFY" controls="controls"></video>

## 📣 更新日志

- `2025/05/12` 🔥 **所有成果均已开源，欢迎查看！**
- `2025/05/10` 🔥 论文被 IJCAI ’25 接收，已更新定稿版本。
- `2024/12/19` 项目及评测基准首次在 arXiv 发布。

## 项目指南

### AniSora V1.0

位置：📁 `anisoraV1_infer`

- 基于 **CogVideoX‑5B** 基础模型训练，完整训练与推理代码开源
- 支持 **局部区域控制** 、 **时间控制** （首帧/尾帧/关键帧插帧、多帧引导）
- 在 📁 `anisoraV1_train_npu` 提供完整训练代码
- 可在 RTX 4090 上经济部署
- 覆盖 80 % 应用场景

### AniSora V2.0

位置：📁 `anisoraV2_gpu`, `anisoraV2_npu`

- 基于升级后的 **Wan2.1‑14B** 基础模型，稳定性更佳
- 蒸馏加速推理，无损画质，更快更省
- 原生支持华为 Ascend 910B NPU（全流程国产芯片训练）
- 高质量镜头生成，覆盖 90 % 应用场景

### 生态工具

位置：📁 `data_pipeline`

- 端到端数据集流水线，快速扩充训练数据
- 动画数据清洗管道

### 面向动漫的评测体系

位置：📁 `reward`

- 为动漫视频生成定制的评测模型与打分算法
- 适用于强化学习和基准测试的奖励模型
- 与 ACG 审美对齐的标准测试集
- 人工偏好对齐

该评测数据集包含 948 段动画视频片段，每个动作标签含 10–30 个视频。文本提示先由 Qwen‑VL2 自动生成，再由人工校对以确保文本‑视频对齐。  
填写表格后以 PDF 形式发送至 [yangsiqian@bilibili.com](https://github.com/bilibili/Index-anisora/blob/main/) 或 [xubaohan@bilibili.com](https://github.com/bilibili/Index-anisora/blob/main/) （链接在同意协议后提供）。

### AniSora V1.0\_RL

位置：📁 `anisora_rl`

- 首个面向动漫视频生成的 RLHF 框架
- RL 优化后的 AniSora V1.0，可生成更具动漫风格的作品
- 详见预印本： [*Aligning Anime Video Generation with Human Feedback*](http://arxiv.org/abs/2504.10044)

## 📑 待办列表

- **AniSora V2.0**
	- 支持 14B 版本，预计 5 月底前发布
- **AniSora 数据集**
	- **开放高质量训练集申请**
- **AniSora 基准**
	- 更新最新 SOTA 模型性能

---

## 💡 摘要

动画内容在当今影视行业中备受关注。  
尽管 Sora、Kling、CogVideoX 等先进模型在自然视频生成方面表现出色，但在动漫视频上仍捉襟见肘。  
此外，由于动漫独特的艺术风格、夸张的运动以及对物理规律的打破，也给评测带来了巨大挑战。

本文提出了完整的系统 **AniSora** ，涵盖：

1. **数据处理流水线** ：超过 1000 万高质量数据；
2. **可控生成模型** ：引入时空掩码模块，支持图生视频、帧插值、局部图像引导等关键动画制作功能；
3. **评测数据集** ：收集 948 段多样化动画视频，配套双盲人评实验及 VBench 测试，人物一致性与运动一致性均达到 SOTA。

## 🖥️ 方法

下图展示了 Index‑AniSora 的整体框架：

![](https://github.com/bilibili/Index-anisora/raw/main/assets/framework.png)

**主要特点：**

1. 搭建了完整的视频处理系统，显著提升生成前的数据预处理效率；
2. 提出统一的时空掩码框架，用于动漫视频生成，可同时处理图生视频、帧插值、局部引导等任务；
3. 发布面向动漫视频生成的专用基准数据集。

## 🎞️ 案例展示

**不同艺术风格的图生视频：**

| 提示词 | 图片 | 视频 |
| --- | --- | --- |
| 画面中，角色坐在前进的汽车里，朝后方挥手，长发在风中左右摆动。 | [![](https://github.com/bilibili/Index-anisora/raw/main/assets/000000(225).png)](https://github.com/bilibili/Index-anisora/blob/main/assets/000000\(225\).png) | [![Demo](https://github.com/bilibili/Index-anisora/raw/main/assets/000000(225).gif)](https://github.com/bilibili/Index-anisora/blob/main/assets/000000\(225\).gif) |
| 场景中，两位身着红色婚服的角色拉着红绳，携手远去。 | [![](https://github.com/bilibili/Index-anisora/raw/main/assets/000000(223).png)](https://github.com/bilibili/Index-anisora/blob/main/assets/000000\(223\).png) | [![Demo](https://github.com/bilibili/Index-anisora/raw/main/assets/000000(223).gif)](https://github.com/bilibili/Index-anisora/blob/main/assets/000000\(223\).gif) |
| 金发角色伸手轻触跪地之人的头顶，后者喘息起伏。 | [![](https://github.com/bilibili/Index-anisora/raw/main/assets/000000(232).png)](https://github.com/bilibili/Index-anisora/blob/main/assets/000000\(232\).png) | [![Demo](https://github.com/bilibili/Index-anisora/raw/main/assets/000000(232).gif)](https://github.com/bilibili/Index-anisora/blob/main/assets/000000\(232\).gif) |
| 画面中，一人高速冲刺向前，速度导致动作出现轻微拖影。 | [![](https://github.com/bilibili/Index-anisora/raw/main/assets/image_1.jpg)](https://github.com/bilibili/Index-anisora/blob/main/assets/image_1.jpg) | [![Demo](https://github.com/bilibili/Index-anisora/raw/main/assets/image_1_vid.gif)](https://github.com/bilibili/Index-anisora/blob/main/assets/image_1_vid.gif) |
| 画面中，角色抬起手臂，手臂表面有气流流动效果。 | [![](https://github.com/bilibili/Index-anisora/raw/main/assets/image_2.jpg)](https://github.com/bilibili/Index-anisora/blob/main/assets/image_2.jpg) | [![Demo](https://github.com/bilibili/Index-anisora/raw/main/assets/image_2_vid.gif)](https://github.com/bilibili/Index-anisora/blob/main/assets/image_2_vid.gif) |
| 老人目光锁定宝石，右手微调放大镜，似在揭示古老秘密。 | [![](https://github.com/bilibili/Index-anisora/raw/main/assets/image_3.jpg)](https://github.com/bilibili/Index-anisora/blob/main/assets/image_3.jpg) | [![Demo](https://github.com/bilibili/Index-anisora/raw/main/assets/image_3_vid.gif)](https://github.com/bilibili/Index-anisora/blob/main/assets/image_3_vid.gif) |
| 左侧男子紧抿双唇，面露愤怒与决然；右侧男子张口欲言。 | [![](https://github.com/bilibili/Index-anisora/raw/main/assets/image_4.jpg)](https://github.com/bilibili/Index-anisora/blob/main/assets/image_4.jpg) | [![Demo](https://github.com/bilibili/Index-anisora/raw/main/assets/image_4_vid.gif)](https://github.com/bilibili/Index-anisora/blob/main/assets/image_4_vid.gif) |
| 岩石爆炸，耀眼光芒四射，碎片向四周激射。 | [![](https://github.com/bilibili/Index-anisora/raw/main/assets/image_5.jpg)](https://github.com/bilibili/Index-anisora/blob/main/assets/image_5.jpg) | [![Demo](https://github.com/bilibili/Index-anisora/raw/main/assets/image_5_vid.gif)](https://github.com/bilibili/Index-anisora/blob/main/assets/image_5_vid.gif) |

**时间控制示例：**

| 提示词 | 首帧 | 中间帧 | 末帧 | 视频 |
| --- | --- | --- | --- | --- |
| 动画电影《美女与野兽》场景：贝儿身着紫色礼服，站在落地窗前对窗外说话，金发披肩。 | [![](https://github.com/bilibili/Index-anisora/raw/main/assets/cartoon_films_ren_wu_shuo_hua_34_firstmidlast_first.png)](https://github.com/bilibili/Index-anisora/blob/main/assets/cartoon_films_ren_wu_shuo_hua_34_firstmidlast_first.png) | [![](https://github.com/bilibili/Index-anisora/raw/main/assets/cartoon_films_ren_wu_shuo_hua_34_firstmidlast_mid.png)](https://github.com/bilibili/Index-anisora/blob/main/assets/cartoon_films_ren_wu_shuo_hua_34_firstmidlast_mid.png) | [![](https://github.com/bilibili/Index-anisora/raw/main/assets/cartoon_films_ren_wu_shuo_hua_34_firstmidlast_last.png)](https://github.com/bilibili/Index-anisora/blob/main/assets/cartoon_films_ren_wu_shuo_hua_34_firstmidlast_last.png) | [![Demo](https://github.com/bilibili/Index-anisora/raw/main/assets/cartoon_films_ren_wu_shuo_hua_34_firstmidlast.gif)](https://github.com/bilibili/Index-anisora/blob/main/assets/cartoon_films_ren_wu_shuo_hua_34_firstmidlast.gif) |
| 夜晚，一位金发女子在车门后探出身子向外张望，星空与满月照亮场景，她神情担忧。 | [![](https://github.com/bilibili/Index-anisora/raw/main/assets/motion_comics_tui_la_5_firstlast_first.png)](https://github.com/bilibili/Index-anisora/blob/main/assets/motion_comics_tui_la_5_firstlast_first.png) | 无 | [![](https://github.com/bilibili/Index-anisora/raw/main/assets/motion_comics_tui_la_5_firstlast_last.jpeg)](https://github.com/bilibili/Index-anisora/blob/main/assets/motion_comics_tui_la_5_firstlast_last.jpeg) | [![Demo](https://github.com/bilibili/Index-anisora/raw/main/assets/motion_comics_tui_la_5_firstlast.gif)](https://github.com/bilibili/Index-anisora/blob/main/assets/motion_comics_tui_la_5_firstlast.gif) |
| 一只卡通猫闭眼张口，似在捣蛋或好奇中，准备惊叫。 | 无 | 无 | [![](https://github.com/bilibili/Index-anisora/raw/main/assets/motion_comics_zhi_dong_xi_2_last.jpeg)](https://github.com/bilibili/Index-anisora/blob/main/assets/motion_comics_zhi_dong_xi_2_last.jpeg) | [![Demo](https://github.com/bilibili/Index-anisora/raw/main/assets/motion_comics_zhi_dong_xi_2_last.gif)](https://github.com/bilibili/Index-anisora/blob/main/assets/motion_comics_zhi_dong_xi_2_last.gif) |

**空间控制示例：**

| 提示词 | 首帧 | 运动掩码 | 视频（含掩码可视化） |
| --- | --- | --- | --- |
| 在《海底总动员》的缤纷水下世界里，小丑鱼马林和尼莫在大型紫色珊瑚附近交谈…… | [![](https://github.com/bilibili/Index-anisora/raw/main/assets/132.png)](https://github.com/bilibili/Index-anisora/blob/main/assets/132.png) | [![](https://github.com/bilibili/Index-anisora/raw/main/assets/132_mask.png)](https://github.com/bilibili/Index-anisora/blob/main/assets/132_mask.png) | [![Demo](https://github.com/bilibili/Index-anisora/raw/main/assets/132.gif)](https://github.com/bilibili/Index-anisora/blob/main/assets/132.gif) |
| 同上 | 同上 | [![](https://github.com/bilibili/Index-anisora/raw/main/assets/133_mask.png)](https://github.com/bilibili/Index-anisora/blob/main/assets/133_mask.png) | [![Demo](https://github.com/bilibili/Index-anisora/raw/main/assets/133.gif)](https://github.com/bilibili/Index-anisora/blob/main/assets/133.gif) |

**更多示例视频： [作品画廊](https://pwz4yo5eenw.feishu.cn/docx/XN9YdiOwCoqJuexLdCpcakSlnkg)**

## 📑 评测结果

**VBench 结果：**

| 方法 | 运动平滑度 | 运动得分 | 美学质量 | 成像质量 | I2V 主体 | I2V 背景 | 整体一致性 | 主体一致性 |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Opensora‑Plan(V1.3) | 99.13 | 76.45 | 53.21 | 65.11 | 93.53 | 94.71 | 21.67 | 88.86 |
| Opensora(V1.2) | 98.78 | 73.62 | 54.30 | 68.44 | 93.15 | 91.09 | 22.68 | 87.71 |
| Vidu | 97.71 | **77.51** | 53.68 | 69.23 | 92.25 | 93.06 | 20.87 | 88.27 |
| CogVideo(5B‑V1) | 97.67 | 71.47 | **54.87** | 68.16 | 90.68 | 91.79 | 21.87 | 90.29 |
| MiniMax | 99.20 | 66.53 | 54.56 | **71.67** | 95.95 | **95.42** | 21.82 | 93.62 |
| **AniSora** | **99.34** | 45.59 | 54.31 | 70.58 | **97.52** | 95.04 | 21.15 | **96.99** |
| AniSora‑K | 99.12 | 59.49 | 53.76 | 68.68 | 95.13 | 93.36 | 21.13 | 94.61 |
| AniSora‑I | 99.31 | 54.96 | 54.67 | 68.98 | 94.16 | 92.38 | 20.47 | 95.75 |
| GT | 98.72 | 56.05 | 52.70 | 70.50 | 96.02 | 95.03 | 21.29 | 94.37 |

**AniSora 基准结果：**

| 方法 | 人工评分 | 视觉平滑 | 视觉运动 | 视觉吸引力 | 文本‑视频一致 | 图像‑视频一致 | 角色一致性 |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Vidu‑1.5 | 60.98 | 55.37 | **78.95** | 50.68 | 60.71 | 66.85 | 82.57 |
| Opensora‑V1.2 | 41.10 | 22.28 | 74.90 | 22.62 | 52.19 | 55.67 | 74.76 |
| Opensora‑Plan‑V1.3 | 46.14 | 35.08 | 77.47 | 36.14 | 56.19 | 59.42 | 81.19 |
| CogVideoX‑5B‑V1 | 53.29 | 39.91 | 73.07 | 39.59 | 67.98 | 65.49 | 83.07 |
| MiniMax-I2V01 | 69.63 | 69.38 | 68.05 | 70.34 | 76.14 | 78.74 | 89.47 |
| Wan-2.1 | \- | 81.70 | 61.88 | 82.05 | 87.80 | 88.50 | 90.65 |
| **AniSora-V1 (Ours)** | **70.13** | 71.88 | 48.45 | 65.38 | 74.26 | 82.66 | **94.88** |
| **AniSora-V2 (Ours)** | \- | **86.98** | 50.34 | **85.91** | **90.98** | **91.96** | 92.75 |
| AniSora-V1 (Interpolated Avg) | \- | 70.78 | 53.02 | 64.41 | 73.56 | 80.62 | 91.59 |
| AniSora-V1 (KeyFrame Interp) | \- | 70.03 | 58.10 | 64.57 | 74.57 | 80.78 | 91.98 |
| AniSora-V1 (KeyFrame Interp) | \- | 70.03 | 58.10 | 64.57 | 74.57 | 80.78 | 91.98 |
| GT | \- | 92.20 | 58.27 | 89.72 | 92.51 | 94.69 | 95.08 |

> **说明**  
> *AniSora* ：我们的 I2V 结果  
> *AniSora‑K* ：关键帧插帧结果  
> *AniSora‑I* ：帧插值（平均）结果

## 🐳 基准数据集

该基准数据集包含 948 段动画视频片段，每段标注不同动作。每个标签含 10–30 个视频，文本提示由 Qwen‑VL2 生成并经人工校对，确保文本‑视频对齐。  
请填写 [申请表](https://github.com/bilibili/Index-anisora/blob/main/assets/anisora_benchmark_agreement_form.doc) 并将 PDF 发送至 [yangsiqian@bilibili.com](https://github.com/bilibili/Index-anisora/blob/main/) 或 [xubaohan@bilibili.com](https://github.com/bilibili/Index-anisora/blob/main/) （须先同意 B 站协议）。

## 🤗 致谢

特别感谢 [CogVideoX](https://github.com/THUDM/CogVideo) 、 [Wan2.1](https://github.com/Wan-Video/Wan2.1) 、 [FasterCache](https://github.com/Vchitect/FasterCache) 以及 [OSS](https://github.com/bebebe666/OptimalSteps) 的宝贵工作。

## 📚 引用

如果本项目对您有帮助，请为我们的仓库点 Star，并引用下述论文：

```
@article{jiang2024anisora,
  title={AniSora: Exploring the Frontiers of Animation Video Generation in the Sora Era},
  author={Yudong Jiang, Baohan Xu, Siqian Yang, Mingyu Yin, Jing Liu, Chao Xu, Siqi Wang, Yidi Wu, Bingwen Zhu, Xinwen Zhang, Xingyu Zheng,Jixuan Xu, Yue Zhang, Jinlong Hou and Huyang Sun},
  journal={arXiv preprint arXiv:2412.10255},
  year={2024}
}
```