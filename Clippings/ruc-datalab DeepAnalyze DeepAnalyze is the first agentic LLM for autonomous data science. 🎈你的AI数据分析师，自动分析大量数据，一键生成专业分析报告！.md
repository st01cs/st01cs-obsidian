---
title: "ruc-datalab/DeepAnalyze: DeepAnalyze is the first agentic LLM for autonomous data science. 🎈你的AI数据分析师，自动分析大量数据，一键生成专业分析报告！"
source: "https://github.com/ruc-datalab/DeepAnalyze"
author:
  - "[[zhangshaolei1998]]"
published:
created: 2025-12-04
description: "DeepAnalyze is the first agentic LLM for autonomous data science. 🎈你的AI数据分析师，自动分析大量数据，一键生成专业分析报告！ - ruc-datalab/DeepAnalyze"
tags:
  - "clippings"
---
**[DeepAnalyze](https://github.com/ruc-datalab/DeepAnalyze)** Public

DeepAnalyze is the first agentic LLM for autonomous data science. 🎈你的AI数据分析师，自动分析大量数据，一键生成专业分析报告！

[ruc-deepanalyze.github.io](https://ruc-deepanalyze.github.io/ "https://ruc-deepanalyze.github.io")

[MIT license](https://github.com/ruc-datalab/DeepAnalyze/blob/main/LICENSE)

[Open in github.dev](https://github.dev/) [Open in a new github.dev tab](https://github.dev/) [Open in codespace](https://github.com/codespaces/new/ruc-datalab/DeepAnalyze?resume=1)

[![DeepAnalyze](https://github.com/ruc-datalab/DeepAnalyze/raw/main/assets/logo.png)](https://github.com/ruc-datalab/DeepAnalyze/blob/main/assets/logo.png)

> **Authors**: **[Shaolei Zhang](https://zhangshaolei1998.github.io/), [Ju Fan\*](http://iir.ruc.edu.cn/~fanj/), [Meihao Fan](https://scholar.google.com/citations?user=9RTm2qoAAAAJ), [Guoliang Li](https://dbgroup.cs.tsinghua.edu.cn/ligl/), [Xiaoyong Du](http://info.ruc.edu.cn/jsky/szdw/ajxjgcx/jsjkxyjsx1/js2/7374b0a3f58045fc9543703ccea2eb9c.htm)**
> 
> Renmin University of China, Tsinghua University

**DeepAnalyze** is the first agentic LLM for autonomous data science. It can autonomously complete a wide range of data-centric tasks without human intervention, supporting:

- 🛠 **Entire data science pipeline**: Automatically perform any data science tasks such as data preparation, analysis, modeling, visualization, and report generation.
- 🔍 **Open-ended data research**: Conduct deep research on diverse data sources, including structured data (Databases, CSV, Excel), semi-structured data (JSON, XML, YAML), and unstructured data (TXT, Markdown), and finally produce analyst-grade research reports.
- 📊 **Fully open-source**: The [model](https://huggingface.co/RUC-DataLab/DeepAnalyze-8B), [code](https://github.com/ruc-datalab/DeepAnalyze), [training data](https://huggingface.co/datasets/RUC-DataLab/DataScience-Instruct-500K), and [demo](https://huggingface.co/RUC-DataLab/DeepAnalyze-8B) of DeepAnalyze are all open-sourced, allowing you to deploy or extend your own data analysis assistant.

[![deepanalyze](https://github.com/ruc-datalab/DeepAnalyze/raw/main/assets/deepanalyze.jpg)](https://github.com/ruc-datalab/DeepAnalyze/blob/main/assets/deepanalyze.jpg)

## 🔥 News

- **\[2025.11.13\]**: DeepAnalyze now supports OpenAI-style API endpointsis and is accessible through the Command Line Terminal UI. Thanks to the contributor [@LIUyizheSDU](https://github.com/LIUyizheSDU/)
- **\[2025.11.08\]**: DeepAnalyze is now accessible through the JupyterUI, building based on [jupyter-mcp-server](https://github.com/datalayer/jupyter-mcp-server). Thanks to the contributor [@ChengJiale150](https://github.com/ChengJiale150).
- **\[2025.10.28\]**: We welcome all contributions, including improving the DeepAnalyze and sharing use cases (see [`CONTRIBUTION.md`](https://github.com/ruc-datalab/DeepAnalyze/blob/main/CONTRIBUTION.md)). All merged PRs will be listed as contributors.
- **\[2025.10.27\]**: DeepAnalyze has attracted widespread attention, gaining **1K+** GitHub stars and **200K+** Twitter views within a week.
- **\[2025.10.21\]**: DeepAnalyze's [paper](https://arxiv.org/abs/2510.16872), [code](https://github.com/ruc-datalab/DeepAnalyze), [model](https://huggingface.co/RUC-DataLab/DeepAnalyze-8B), [training data](https://huggingface.co/datasets/RUC-DataLab/DataScience-Instruct-500K) are released!

## 🖥 Demo

### WebUI

deepanalyze-8b.mp4<video src="https://private-user-images.githubusercontent.com/34680227/502958904-04184975-7ee7-4ae0-8761-7a7550c5c8fe.mp4?jwt=eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3NjQ4NDg2MjUsIm5iZiI6MTc2NDg0ODMyNSwicGF0aCI6Ii8zNDY4MDIyNy81MDI5NTg5MDQtMDQxODQ5NzUtN2VlNy00YWUwLTg3NjEtN2E3NTUwYzVjOGZlLm1wND9YLUFtei1BbGdvcml0aG09QVdTNC1ITUFDLVNIQTI1NiZYLUFtei1DcmVkZW50aWFsPUFLSUFWQ09EWUxTQTUzUFFLNFpBJTJGMjAyNTEyMDQlMkZ1cy1lYXN0LTElMkZzMyUyRmF3czRfcmVxdWVzdCZYLUFtei1EYXRlPTIwMjUxMjA0VDExMzg0NVomWC1BbXotRXhwaXJlcz0zMDAmWC1BbXotU2lnbmF0dXJlPTc1MTQ1YThhYjRlZmZiMWRmYzVlZjJlMTJiYmVhYjkwNmRiYjQxZTRjOWMzZWVhYWFiNjQ2ZTgwODUxMWQ0NjkmWC1BbXotU2lnbmVkSGVhZGVycz1ob3N0In0.NkcMtIoaLgy6W2csiDCxdvF534ihBEvpTDWcfJUMg5s" controls="controls"></video>

Upload the data, DeepAnalyze can perform data-oriented deep research 🔍 and any data-centric tasks 🛠

- Clone this repo and download [DeepAnalyze-8B](https://huggingface.co/RUC-DataLab/DeepAnalyze-8B).
- Deploy DeepAnalyze-8B via vllm: `vllm serve DeepAnalyze-8B`
- Run these scripts to launch the API and interface, and then interact through the browser ([http://localhost:4000](http://localhost:4000/)):
	```
	cd demo/chat
	npm install
	cd ..
	bash start.sh
	# stop the api and interface
	bash stop.sh
	```
- If you want to deploy under a specific IP, please replace localhost with your IP address in [./demo/backend.py](https://github.com/ruc-datalab/DeepAnalyze/blob/main/demo/backend.py) and [./demo/chat/lib/config.ts](https://github.com/ruc-datalab/DeepAnalyze/blob/main/demo/chat/lib/config.ts)

### JupyterUI

example\_compressed.mp4<video src="https://private-user-images.githubusercontent.com/147157657/511653571-a2335f45-be0e-4787-a4c1-e93192891c5f.mp4?jwt=eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3NjQ4NDg2MjUsIm5iZiI6MTc2NDg0ODMyNSwicGF0aCI6Ii8xNDcxNTc2NTcvNTExNjUzNTcxLWEyMzM1ZjQ1LWJlMGUtNDc4Ny1hNGMxLWU5MzE5Mjg5MWM1Zi5tcDQ_WC1BbXotQWxnb3JpdGhtPUFXUzQtSE1BQy1TSEEyNTYmWC1BbXotQ3JlZGVudGlhbD1BS0lBVkNPRFlMU0E1M1BRSzRaQSUyRjIwMjUxMjA0JTJGdXMtZWFzdC0xJTJGczMlMkZhd3M0X3JlcXVlc3QmWC1BbXotRGF0ZT0yMDI1MTIwNFQxMTM4NDVaJlgtQW16LUV4cGlyZXM9MzAwJlgtQW16LVNpZ25hdHVyZT04NjdlMWI1ZjdmMzg5ZmRhYWU4MDMwNzE0MDBkMzMwM2I1ZmZhYjliZDQ4ZmVmZDNlMzNhZTViNzhiM2UwMDE4JlgtQW16LVNpZ25lZEhlYWRlcnM9aG9zdCJ9.7ixApncvyu_x2pHDdArwsMyIHGckIfZpLrQQ42e7Q9g" controls="controls"></video>

Familiar with Jupyter Notebook? Try DeepAnalyze through the JupyterUI!

- This Demo runs Jupyter Lab as frontend, creating a new notebook, converting `<Analyze|Understand|Answer>` to Markdown cells, converting `<Code>` to Code cells and executing them as `<Execute>`.
- Go to [demo/jupyter](https://github.com/ruc-datalab/DeepAnalyze/blob/main/demo/jupyter) to see more and try!
- 👏Thanks a lot to the contributor [@ChengJiale150](https://github.com/ChengJiale150).

### CLI

api\_demo.mp4<video src="https://private-user-images.githubusercontent.com/115469795/513284526-018acae5-b979-4143-ae1e-5b74da453c1d.mp4?jwt=eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3NjQ4NDg2MjUsIm5iZiI6MTc2NDg0ODMyNSwicGF0aCI6Ii8xMTU0Njk3OTUvNTEzMjg0NTI2LTAxOGFjYWU1LWI5NzktNDE0My1hZTFlLTViNzRkYTQ1M2MxZC5tcDQ_WC1BbXotQWxnb3JpdGhtPUFXUzQtSE1BQy1TSEEyNTYmWC1BbXotQ3JlZGVudGlhbD1BS0lBVkNPRFlMU0E1M1BRSzRaQSUyRjIwMjUxMjA0JTJGdXMtZWFzdC0xJTJGczMlMkZhd3M0X3JlcXVlc3QmWC1BbXotRGF0ZT0yMDI1MTIwNFQxMTM4NDVaJlgtQW16LUV4cGlyZXM9MzAwJlgtQW16LVNpZ25hdHVyZT1kYjg2NjNjYTk0NDExMmFlZTg2YmRhMmRlNjljZWViYmM1NzA1OTZmMmYyYjRlODY1YzFkOTQ4YWM3MjNlNDFjJlgtQW16LVNpZ25lZEhlYWRlcnM9aG9zdCJ9.vNbnmakdq8DQyMMZo6VUpPO-o2eGBLc5eXAL7bt4cMI" controls="controls"></video>

Try DeepAnalyze through the command-line interface

- Deploy DeepAnalyze-8B via vllm: `vllm serve DeepAnalyze-8B`
- Start the API server and launch the CLI interface:
	```
	cd API
	python start_server.py  # In one terminal
	cd demo/cli
	python api_cli.py       # In another terminal (English)
	# or
	python api_cli_ZH.py    # In another terminal (Chinese)
	```
- The CLI provides a Rich-based beautiful interface with file upload support and real-time streaming responses.
- Supports both English and Chinese interfaces.

### Model Download

Download model in [RUC-DataLab/DeepAnalyze-8B · Hugging Face](https://huggingface.co/RUC-DataLab/DeepAnalyze-8B) or [DeepAnalyze-8B · 模型库](https://www.modelscope.cn/models/RUC-DataLab/DeepAnalyze-8B/summary)

| GPU Memory | Model Type | Recommended max-model-len | Use FP8 KV Cache |
| --- | --- | --- | --- |
| **16GB** | 8-bit Quantized | 8192 | ✓ |
| **16GB** | 4-bit Quantized | 49152 | ✓ |
| **24GB** | Original Model | 16384 | ✓ |
| **24GB** | 8-bit Quantized | 98304 | ✓ |
| **24GB** | 4-bit Quantized | 131072 | ✓ |
| **40GB** | Original Model | 131072 | ✓ |
| **40GB** | 8-bit Quantized | 131072 |  |
| **80GB** | Original Model | 131072 |  |

To obtain the quantized model, you can use `./quantize.py`.

```
python -m vllm.entrypoints.openai.api_server \
  --model <model_path> \
  --served-model-name DeepAnalyze-8B \
  --max-model-len <select_from_table_above> \
  --gpu-memory-utilization 0.95 \
  --port 8000 \
  <add_fp8_if_required> \
  --trust-remote-code
```

**Scenario 1: 16GB GPU Memory Users (Recommended: 4-bit Quantized Version)**

```
python -m vllm.entrypoints.openai.api_server \
  --model /path/to/deepanalyze/4bit \
  --served-model-name DeepAnalyze-8B \
  --max-model-len 49152 \
  --gpu-memory-utilization 0.95 \
  --port 8000 \
  --kv-cache-dtype fp8 \
  --trust-remote-code
```

**Scenario 2: 24GB GPU Memory Users (For Maximum Context Length)**

```
python -m vllm.entrypoints.openai.api_server \
  --model /path/to/deepanalyze/4bit \
  --served-model-name DeepAnalyze-8B \
  --max-model-len 131072 \
  --gpu-memory-utilization 0.95 \
  --port 8000 \
  --kv-cache-dtype fp8 \
  --trust-remote-code
```

**Scenario 3: 80GB GPU Memory Users (Best Performance)**

```
python -m vllm.entrypoints.openai.api_server \
  --model /path/to/original/model \
  --served-model-name DeepAnalyze-8B \
  --max-model-len 131072 \
  --gpu-memory-utilization 0.95 \
  --port 8000 \
  --trust-remote-code
```
- **Limited Memory (<24GB)**: Use 4-bit Quantized Version + FP8 KV Cache
- **Balanced Configuration (24-40GB)**: Choose model type based on requirements
- **Sufficient Memory (≥40GB)**: Use Original Model for best precision

After launching, the API service can be accessed via `http://localhost:8000/v1/completions`.

### Requirements

- Install packages: `torch`, `transformers`, `vllm>=0.8.5`
	```
	conda create -n deepanalyze python=3.12 -y
	conda activate deepanalyze
	pip install -r requirements.txt
	# For training
	(cd ./deepanalyze/ms-swift/ && pip install -e .)
	(cd ./deepanalyze/SkyRL/ && pip install -e .)
	```
- [`requirements.txt`](https://github.com/ruc-datalab/DeepAnalyze/blob/main/requirements.txt) lists the minimal dependencies required for DeepAnalyze inference. For training, please refer to [`./deepanalyze/ms-swift/requirements.txt`](https://github.com/ruc-datalab/DeepAnalyze/blob/main/deepanalyze/ms-swift/requirements.txt) and [`./deepanalyze/SkyRL/pyproject.toml`](https://github.com/ruc-datalab/DeepAnalyze/blob/main/deepanalyze/SkyRL/pyproject.toml)
- We recommend separating the inference and training environments to avoid dependency conflicts.

### Command Interaction

- Deploy DeepAnalyze-8B via vllm: `vllm serve DeepAnalyze-8B`
- Run these scripts for any data science tasks:
	- You can specify **any data science tasks**, including specific data tasks and open-ended data research.
	- You can specify **any number of data sources**, and DeepAnalyze will automatically explore them.
	- You can specify **any type of data sources**, e.g., structured data (Databases, CSV, Excel), semi-structured data (JSON, XML, YAML), and unstructured data (TXT, Markdown)
	```
	from deepanalyze import DeepAnalyzeVLLM
	prompt = """# Instruction
	Generate a data science report.
	# Data
	File 1: {"name": "bool.xlsx", "size": "4.8KB"}
	File 2: {"name": "person.csv", "size": "10.6KB"}
	File 3: {"name": "disabled.xlsx", "size": "5.6KB"}
	File 4: {"name": "enlist.csv", "size": "6.7KB"}
	File 5: {"name": "filed_for_bankrupcy.csv", "size": "1.0KB"}
	File 6: {"name": "longest_absense_from_school.xlsx", "size": "16.0KB"}
	File 7: {"name": "male.xlsx", "size": "8.8KB"}
	File 8: {"name": "no_payment_due.xlsx", "size": "15.6KB"}
	File 9: {"name": "unemployed.xlsx", "size": "5.6KB"}
	File 10: {"name": "enrolled.csv", "size": "20.4KB"}"""
	workspace = "/home/u2023000922/zhangshaolei/deepanalyze_public/DeepAnalyze/example/analysis_on_student_loan/"
	deepanalyze = DeepAnalyzeVLLM(
	    "/fs/fast/u2023000922/zhangshaolei/checkpoints/deepanalyze-8b/"
	)
	answer = deepanalyze.generate(prompt, workspace=workspace)
	print(answer["reasoning"])
	```
	You shoud get a deep research report, which can be rendered as a PDF.:
	```
	# Comprehensive Analysis of Student Enrollment Patterns and Institutional Transfers
	## Introduction and Research Context
	The analysis of student enrollment patterns represents a critical area of educational research with significant implications for institutional planning, resource allocation, and student support services. This comprehensive study examines a comprehensive dataset encompassing 1,194 enrollment records across six educational institutions, merged with supplementary demographic, financial, and employment status data. The research employs advanced analytical techniques including network analysis, predictive modeling, and temporal pattern recognition to uncover both macro-level institutional trends and micro-level student mobility patterns. The dataset's longitudinal nature, spanning fifteen months of enrollment records, provides unique insights into the complex dynamics of student pathways through higher education systems.
	Our methodological approach combines quantitative analysis of enrollment durations, transfer probabilities, and financial indicators with qualitative ...
	The research contributes to the growing body of literature on student mobility by providing empirical evidence of institutional transfer networks and their relationship to student outcomes...
	.....
	```
	[![deepanalyze](https://github.com/ruc-datalab/DeepAnalyze/raw/main/assets/report.png)](https://github.com/ruc-datalab/DeepAnalyze/blob/main/assets/report.png)
	> For more examples and task completion details, please refer to [DeepAnalyze's homepage](https://ruc-deepanalyze.github.io/).

### API

- You can build an OpenAI-Style API, using this script (note to change `MODEL_PATH = "DeepAnalyze-8B"` in [API/config.py](https://github.com/ruc-datalab/DeepAnalyze/blob/main/API/config.py) to your vllm model name):
	```
	python API/start_server.py
	```
- API usage:
	```
	FILE_RESPONSE=$(curl -s -X POST "http://localhost:8200/v1/files" \
	    -F "file=@data.csv" \
	    -F "purpose=file-extract")
	FILE_ID=$(echo $FILE_RESPONSE | jq -r '.id')
	curl -X POST http://localhost:8200/v1/chat/completions \
	     -H "Content-Type: application/json" \
	     -d "{
	        \"model\": \"DeepAnalyze-8B\",
	        \"messages\": [
	          {
	            \"role\": \"user\",
	            \"content\": \"Generate a data science report.\",
	            \"file_ids\": [\"$FILE_ID\"]
	          }
	        ]
	      }"
	# wait for a while
	```
- Refer to API/README.md for details.
- Download [DeepSeek-R1-0528-Qwen3-8B](https://huggingface.co/deepseek-ai/DeepSeek-R1-0528-Qwen3-8B). Or you can directly finetune based on [DeepAnalyze-8B](https://huggingface.co/RUC-DataLab/DeepAnalyze-8B).
	- If you use DeepSeek-R1-0528-Qwen3-8B as the base model, you should add the special tokens, using:
		```
		MODEL_PATH=path_to_DeepSeek-R1-0528-Qwen3-8B
		SAVE_PATH=path_to_save_DeepSeek-R1-0528-Qwen3-8B-addvocab
		python deepanalyze/add_vocab.py \
		  --model_path "$MODEL_PATH" \
		  --save_path "$SAVE_PATH" \
		  --add_tags
		```
- Download training data [DataScience-Instruct-500K](https://huggingface.co/datasets/RUC-DataLab/DataScience-Instruct-500K).
	- unzip `DataScience-Instruct-500K/RL/data.zip`
- Single-ability Fine-tuning: [./scripts/single.sh](https://github.com/ruc-datalab/DeepAnalyze/blob/main/scripts/single.sh)
- Multi-ability Agentic Training (cold start): [./scripts/multi\_coldstart.sh](https://github.com/ruc-datalab/DeepAnalyze/blob/main/scripts/multi_coldstart.sh)
- Multi-ability Agentic Training (RL): [./scripts/multi\_rl.sh](https://github.com/ruc-datalab/DeepAnalyze/blob/main/scripts/multi_rl.sh)

### 3\. Evaluation

- We have unified the evaluation of most existing data science benchmarks using vLLM (with more being continuously added...). You can directly follow the introduction in [./playground](https://github.com/ruc-datalab/DeepAnalyze/blob/main/playground) to quickly evaluate DeepAnalyze or your own agent.

## 👏 Contribution

> We welcome all forms of contributions, and merged PRs will be listed as contributors.

- We welcome all forms of contributions on DeepAnalyze's code, model and UI, such as Docker packaging, DeepAnalyze model conversion and quantization, and submitting DeepAnalyze workflows based on closed-source LLMs.
- You can submit a pull request directly.
- We also especially encourage you to share your use cases and feedback when using DeepAnalyze; these are extremely valuable for helping us improve DeepAnalyze.
- You can place your use cases in a new folder under [`.example/`](https://github.com/ruc-datalab/DeepAnalyze/blob/main/.example). We recommend following the folder structure of [`.example/analysis_on_student_loan/`](https://github.com/ruc-datalab/DeepAnalyze/blob/main/.example/analysis_on_student_loan), which includes three parts:
	- `data/`: stores the uploaded files
	- `prompt.txt`: input instructions
	- `README.md`: documentation. We suggest including the input, DeepAnalyze’s output, outputs from other closed-source LLMs (optional), and your evaluation/comments of the case.
- DeepAnalyze only has 8B parameters, so we also welcome examples where DeepAnalyze performs slightly worse than the closed-source LLMs — this will help us improve DeepAnalyze.

## 🤝 Acknowledgement

- Training framework: [ms-swift](https://github.com/modelscope/ms-swift), [SkyRL](https://github.com/NovaSky-AI/SkyRL)
- Source of Training Data: [Reasoning-Table](https://github.com/MJinXiang/Reasoning-Table), [Spider](https://yale-lily.github.io/spider), [BIRD](https://bird-bench.github.io/), [DABStep](https://huggingface.co/blog/dabstep)

## 🖋 Citation

If this repository is useful for you, please cite as:

```
@misc{deepanalyze,
      title={DeepAnalyze: Agentic Large Language Models for Autonomous Data Science}, 
      author={Shaolei Zhang and Ju Fan and Meihao Fan and Guoliang Li and Xiaoyong Du},
      year={2025},
      eprint={2510.16872},
      archivePrefix={arXiv},
      primaryClass={cs.AI},
      url={https://arxiv.org/abs/2510.16872}, 
}
```

If you have any questions, please feel free to submit an issue or contact `zhangshaolei98@ruc.edu.cn`.

## 🌟 Misc

Welcome to join the [DeepAnalyze WeChat group](https://github.com/ruc-datalab/DeepAnalyze/blob/main/assets/wechat.jpg), chat and share ideas with others!

[![DeepAnalyze](https://github.com/ruc-datalab/DeepAnalyze/raw/main/assets/wechat2.jpg)](https://github.com/ruc-datalab/DeepAnalyze/blob/main/assets/wechat2.jpg)

If you like DeepAnalyze, give it a GitHub Star ⭐.

[![Star History Chart](https://camo.githubusercontent.com/84f363cbf684c68c46e4936063e6675096374afe8da8c4fc69920474b9b287e2/68747470733a2f2f6170692e737461722d686973746f72792e636f6d2f7376673f7265706f733d7275632d646174616c61622f44656570416e616c797a6526747970653d64617465266c6567656e643d746f702d6c656674)](https://www.star-history.com/#ruc-datalab/DeepAnalyze&type=date&legend=top-left)

## Releases

No releases published

## Packages

No packages published