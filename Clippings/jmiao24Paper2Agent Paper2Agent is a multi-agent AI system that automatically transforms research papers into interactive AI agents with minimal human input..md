---
title: "jmiao24/Paper2Agent: Paper2Agent is a multi-agent AI system that automatically transforms research papers into interactive AI agents with minimal human input."
source: https://github.com/jmiao24/Paper2Agent
author:
  - "[[jmiao24]]"
published:
created: 2025-10-01
description: Paper2Agent is a multi-agent AI system that automatically transforms research papers into interactive AI agents with minimal human input. - jmiao24/Paper2Agent
tags:
  - clippings
  - agent
---
**[Paper2Agent](https://github.com/jmiao24/Paper2Agent)** Public

Paper2Agent is a multi-agent AI system that automatically transforms research papers into interactive AI agents with minimal human input.

[MIT license](https://github.com/jmiao24/Paper2Agent/blob/main/LICENSE)

[Open in github.dev](https://github.dev/) [Open in a new github.dev tab](https://github.dev/) [Open in codespace](https://github.com/codespaces/new/jmiao24/Paper2Agent?resume=1)

[![Paper2Agent Logo](https://github.com/jmiao24/Paper2Agent/raw/main/logo/paper2agent_logo.png)](https://github.com/jmiao24/Paper2Agent/blob/main/logo/paper2agent_logo.png)

## 📖 Overview

`Paper2Agent` is a multi-agent AI system that automatically transforms research papers into interactive AI agents with minimal human input. Here are some [Demos](https://github.com/jmiao24/#-demos) of the Paper2Agent-generated agent.

### Basic Usage

Automatically detects and runs all relevant tutorials from a research paper’s codebase.

> **⚠️ Prerequisites**: Complete the [installation & setup](https://github.com/jmiao24/#%EF%B8%8F-installation--setup) below before running Paper2Agent.
> 
> **⏱️ Runtime & Cost**: Processing time varies from 30 minutes to 3+ hours based on codebase complexity. Estimated cost: ~$15 for complex repositories like AlphaGenome using Claude Sonnet 4 (one-time cost).

```
cd Paper2Agent

bash Paper2Agent.sh \
  --project_dir <PROJECT_DIR> \
  --github_url <GITHUB_URL>
```

### Advanced Usage

Process only specific tutorials by title or URL:

```
bash Paper2Agent.sh \
  --project_dir <PROJECT_DIR> \
  --github_url <GITHUB_URL> \
  --tutorials <TUTORIALS_URL or TUTORIALS_TITLE>
```

For repositories requiring authentication:

```
bash Paper2Agent.sh \
  --project_dir <PROJECT_DIR> \
  --github_url <GITHUB_URL> \
  --api <API_KEY>
```

### Parameters

**Required:**

- `--project_dir <directory>`: Name of the project directory to create
	- Example: `TISSUE_Agent`
- `--github_url <url>`: GitHub repository URL to analyze
	- Example: `https://github.com/sunericd/TISSUE`

**Optional:**

- `--tutorials <filter>`: Filter tutorials by title or URL
	- Example: `"Preprocessing and clustering"` or tutorial URL
- `--api <key>`: API key for repositories requiring authentication
	- Example: `your_api_key_here`

### Examples

#### TISSUE Agent

Create an AI agent from the [TISSUE](https://github.com/sunericd/TISSUE) research paper codebase for uncertainty-calibrated single-cell spatial transcriptomics analysis:

```
bash Paper2Agent.sh \
  --project_dir TISSUE_Agent \
  --github_url https://github.com/sunericd/TISSUE
```

Create an AI agent from the [Scanpy](https://github.com/scverse/scanpy) research paper codebase for single-cell analysis preprocessing and clustering:

```
# Filter by tutorial title
bash Paper2Agent.sh \
  --project_dir Scanpy_Agent \
  --github_url https://github.com/scverse/scanpy \
  --tutorials "Preprocessing and clustering"

# Filter by tutorial URL
bash Paper2Agent.sh \
  --project_dir Scanpy_Agent \
  --github_url https://github.com/scverse/scanpy \
  --tutorials "https://github.com/scverse/scanpy/blob/main/docs/tutorials/basics/clustering.ipynb"
```

#### AlphaGenome Agent

Create an AI agent from the [AlphaGenome](https://github.com/google-deepmind/alphagenome) research paper codebase for genomic data interpretation:

```
bash Paper2Agent.sh \
  --project_dir AlphaGenome_Agent \
  --github_url https://github.com/google-deepmind/alphagenome \
  --api <ALPHAGENOME_API_KEY>
```

### Prerequisites

- **Python**: Version 3.10 or higher
- **Claude Code**: Install following instructions at [anthropic.com/claude-code](https://www.anthropic.com/claude-code)

### Installation Steps

1. **Clone the Paper2Agent Repository**
	```
	git clone https://github.com/jmiao24/Paper2Agent.git
	cd Paper2Agent
	```
2. **Install Python Dependencies**
	```
	pip install fastmcp
	```
3. **Install and Configure Claude Code**
	```
	npm install -g @anthropic-ai/claude-code
	claude
	```

To streamline usage, we recommend creating Paper Agents by connecting Paper MCP servers to an AI coding agent, such as [Claude Code](https://www.anthropic.com/claude-code) or the [Google Gemini CLI](https://google-gemini.github.io/gemini-cli/) (it's free with a Google account!). We are also actively developing our own base agent, which will be released soon.

### Automatic Launch

After pipeline completion, Claude Code will automatically open with your new MCP server loaded.

To restart your agent later:

```
cd <working_dir>
fastmcp install claude-code <project_dir>/src/<repo_name>_mcp.py \
--python <project_dir>/<repo_name>-env/bin/python
```

To create a paper agent in Claude Code with the Paper MCP server of interest, use the following script with your own working directory, MCP name, and server URL:

```
bash launch_remote_mcp.sh \
  --working_dir <working_dir> \
  --mcp_name <mcp_name> \
  --mcp_url <remote_mcp_url>
```

For example, to create an AlphaGenome Agent, run:

```
bash launch_remote_mcp.sh \
  --working_dir analysis_dir \
  --mcp_name alphagenome \
  --mcp_url https://Paper2Agent-alphagenome-mcp.hf.space
```

✅ You will now have an **AlphaGenome Agent** ready for genomics data interpretation. You can input the query like:

```
Analyze heart gene expression data with AlphaGenome MCP to identify the causal gene
for the variant chr11:116837649:T>G, associated with Hypoalphalipoproteinemia.
```

To reuse the AlphaGenome agent, run

```
cd analysis_dir
claude
```

### Verification

Verify your agent is loaded:

```
claude mcp list
```

or use `\mcp` inside Claude Code. You should see your repository-specific MCP server listed.

After completion, your project will contain:

```
<project_dir>/
├── src/
│   ├── <repo_name>_mcp.py          # Generated MCP server
│   └── tools/
│       └── <tutorial_file_name>.py      # Extracted tools from each tutorial
├── <repo_name>-env/                # Isolated Python environment
├── repo/
│   └── <repo_name>/                # Cloned repository with original code
├── claude_outputs/
│   ├── step1_output.json           # Tutorial scanner results
│   ├── step2_output.json           # Tutorial executor results
│   ├── step3_output.json           # Tool extraction results
│   └── step4_output.json           # MCP server creation results
├── reports/
│   ├── tutorial-scanner.json       # Tutorial discovery analysis
│   ├── tutorial-scanner-include-in-tools.json  # Tools inclusion decisions
│   ├── executed_notebooks.json     # Notebook execution summary
│   └── environment-manager_results.md  # Environment setup details
├── tests/
│   ├── code/<tutorial_file_name>/       # Test code for extracted tools
│   ├── data/<tutorial_file_name>/       # Test data files
│   ├── results/<tutorial_file_name>/    # Test execution results
│   └── logs/                       # Test execution logs
├── notebooks/
│   └── <tutorial_file_name>/
│       ├── <tutorial_file_name>_execution_final.ipynb  # Executed tutorial
│       └── images/                 # Generated plots and visualizations
└── tools/                          # Additional utility scripts
```

| File/Directory | Description |
| --- | --- |
| `src/<repo_name>_mcp.py` | Main MCP server file that Claude Code loads |
| `src/tools/<tutorial_file_name>.py` | Individual tool modules extracted from each tutorial |
| `<repo_name>-env/` | Isolated Python environment with all dependencies |

## 🎬 Demos

Below, we showcase demos of AI agents created by Paper2Agent, illustrating how each agent applies the tools from its source paper to tackle scientific tasks.

Example query:

```
Analyze heart gene expression data with AlphaGenome MCP to identify the causal gene
for the variant chr11:116837649:T>G, associated with Hypoalphalipoproteinemia.
```

AlphaGenome\_chatbot.mov<video src="https://private-user-images.githubusercontent.com/56059516/487257420-34aad25b-42b3-4feb-b418-db31066e7f7b.mov?jwt=eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3NTg2MTY3ODUsIm5iZiI6MTc1ODYxNjQ4NSwicGF0aCI6Ii81NjA1OTUxNi80ODcyNTc0MjAtMzRhYWQyNWItNDJiMy00ZmViLWI0MTgtZGIzMTA2NmU3ZjdiLm1vdj9YLUFtei1BbGdvcml0aG09QVdTNC1ITUFDLVNIQTI1NiZYLUFtei1DcmVkZW50aWFsPUFLSUFWQ09EWUxTQTUzUFFLNFpBJTJGMjAyNTA5MjMlMkZ1cy1lYXN0LTElMkZzMyUyRmF3czRfcmVxdWVzdCZYLUFtei1EYXRlPTIwMjUwOTIzVDA4MzQ0NVomWC1BbXotRXhwaXJlcz0zMDAmWC1BbXotU2lnbmF0dXJlPTRlYTIxYTllOWMyODM4YWYyNzg0MmI1MGU3NDExMDQwODU2NmU3NzAzYTM3YjRlOTMxODk0ODI3MDgzMDYwZjYmWC1BbXotU2lnbmVkSGVhZGVycz1ob3N0In0.sk2IP8FEMyIEO0pwQSAcwprlNXZSEJp-SGoTV2oRufY" controls="controls"></video>

Example query:

```
Calculate the 95% prediction interval for the spatial gene expression prediction of gene Acta2 using TISSUE MCP.

This is my data:
Spatial count matrix: Spatial_count.txt
Spatial locations: Locations.txt
scRNA-seq count matrix: scRNA_count.txt
```

TISSUE\_chatbot.mov<video src="https://private-user-images.githubusercontent.com/56059516/487254777-2c8f6368-fa99-4e6e-b7b5-acc12f741655.mov?jwt=eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3NTg2MTY3ODUsIm5iZiI6MTc1ODYxNjQ4NSwicGF0aCI6Ii81NjA1OTUxNi80ODcyNTQ3NzctMmM4ZjYzNjgtZmE5OS00ZTZlLWI3YjUtYWNjMTJmNzQxNjU1Lm1vdj9YLUFtei1BbGdvcml0aG09QVdTNC1ITUFDLVNIQTI1NiZYLUFtei1DcmVkZW50aWFsPUFLSUFWQ09EWUxTQTUzUFFLNFpBJTJGMjAyNTA5MjMlMkZ1cy1lYXN0LTElMkZzMyUyRmF3czRfcmVxdWVzdCZYLUFtei1EYXRlPTIwMjUwOTIzVDA4MzQ0NVomWC1BbXotRXhwaXJlcz0zMDAmWC1BbXotU2lnbmF0dXJlPWE2YjFhOTY1MDkxMTZkMTQxMDhlOTFkYThjZjg4YWUxZjVhYjZkNTIxOTdjNDk3NWIwZDI4MDA3NWM1N2Y0NjAmWC1BbXotU2lnbmVkSGVhZGVycz1ob3N0In0.iP2MXiy70mfzGeWDHhOxlaQRNuTmcPyxqyrzY-vRLOQ" controls="controls"></video>

Example query:

```
Use Scanpy MCP to preprocess and cluster the single-cell dataset pbmc_all.h5ad.
```

- AlphaGenome: [https://Paper2Agent-alphagenome-mcp.hf.space](https://paper2agent-alphagenome-mcp.hf.space/)
- Scanpy: [https://Paper2Agent-scanpy-mcp.hf.space](https://paper2agent-scanpy-mcp.hf.space/)
- TISSUE: [https://Paper2Agent-tissue-mcp.hf.space](https://paper2agent-tissue-mcp.hf.space/)

## 📚 Citation

```
@misc{miao2025paper2agent,
      title={Paper2Agent: Reimagining Research Papers As Interactive and Reliable AI Agents}, 
      author={Jiacheng Miao and Joe R. Davis and Jonathan K. Pritchard and James Zou},
      year={2025},
      eprint={2509.06917},
      archivePrefix={arXiv},
      primaryClass={cs.AI},
      url={https://arxiv.org/abs/2509.06917}, 
}
```

## Releases

No releases published

## Packages

No packages published  

## Languages

- [Jupyter Notebook 92.5%](https://github.com/jmiao24/Paper2Agent/search?l=jupyter-notebook)
- [Python 4.0%](https://github.com/jmiao24/Paper2Agent/search?l=python)
- [Shell 3.5%](https://github.com/jmiao24/Paper2Agent/search?l=shell)