---
title: "jennyzzt/dgm: Darwin Gödel Machine: Open-Ended Evolution of Self-Improving Agents"
source: "https://github.com/jennyzzt/dgm"
author:
  - "[[jennyzzt]]"
published:
created: 2025-10-01
description: "Darwin Gödel Machine: Open-Ended Evolution of Self-Improving Agents - jennyzzt/dgm"
tags:
  - "clippings"
---
**[dgm](https://github.com/jennyzzt/dgm)** Public

Darwin Gödel Machine: Open-Ended Evolution of Self-Improving Agents

[Apache-2.0 license](https://github.com/jennyzzt/dgm/blob/main/LICENSE)

[Open in github.dev](https://github.dev/) [Open in a new github.dev tab](https://github.dev/) [Open in codespace](https://github.com/codespaces/new/jennyzzt/dgm?resume=1)

Repository for **Darwin Gödel Machine (DGM)**, a novel self-improving system that iteratively modifies its own code (thereby also improving its ability to modify its own codebase) and empirically validates each change using coding benchmarks.

[![](https://github.com/jennyzzt/dgm/raw/main/misc/overview.gif)](https://github.com/jennyzzt/dgm/blob/main/misc/overview.gif)

## Setup

```
# API keys, add to ~/.bashrc
export OPENAI_API_KEY='...'
export ANTHROPIC_API_KEY='...'
```
```
# Verify that Docker is properly configured in your environment.
docker run hello-world
 
# If a permission error occurs, add the user to the Docker group
sudo usermod -aG docker $USER
newgrp docker
```
```
# Install dependencies
python3 -m venv venv
source venv/bin/activate
pip install -r requirements.txt

# Optional: for running analysis
sudo apt-get install graphviz graphviz-dev
pip install -r requirements_dev.txt
```
```
# Clone SWE-bench
cd swe_bench
git clone https://github.com/princeton-nlp/SWE-bench.git
cd SWE-bench
git checkout dc4c087c2b9e4cefebf2e3d201d27e36
pip install -e .
cd ../../

# Prepare Polyglot
# Make sure git is properly configured in your environment with username and email
python -m polyglot.prepare_polyglot_dataset
```
```
python DGM_outer.py
```

By default, outputs will be saved in the `output_dgm/` directory.

## File Structure

- `analysis/` scripts used for plotting and analysis
- `initial/` SWE-bench logs and performance of the initial agent
- `initial_polyglot/` Polyglot logs and performance of the initial agent
- `swe_bench/` code needed for SWE-bench evaluation
- `polyglot/` code needed for Polyglot evaluation
- `prompts/` prompts used for foundation models
- `tests/` tests for the DGM system
- `tools/` tools available to the foundation models
- `coding_agent.py` main implementation of the initial coding agent
- `DGM_outer.py` entry point for running the DGM algorithm

This [google drive folder](https://drive.google.com/drive/folders/1Kcu9TbIa9Z50pJ7S6hH9omzzD1pxIYZC?usp=sharing) contains all the foundation model output logs from the experiments shown in the paper.

## Safety Consideration

## Acknowledgement

The evaluation framework implementations are based on the [SWE-bench](https://github.com/swe-bench/SWE-bench) and [polyglot-benchmark](https://github.com/Aider-AI/polyglot-benchmark) repositories.

## Citing

If you find this project useful, please consider citing:

```
@article{zhang2025darwin,
  title={Darwin Godel Machine: Open-Ended Evolution of Self-Improving Agents},
  author={Zhang, Jenny and Hu, Shengran and Lu, Cong and Lange, Robert and Clune, Jeff},
  journal={arXiv preprint arXiv:2505.22954},
  year={2025}
}
```

## Languages

- [Python 55.6%](https://github.com/jennyzzt/dgm/search?l=python)
- [Shell 44.3%](https://github.com/jennyzzt/dgm/search?l=shell)
- [Dockerfile 0.1%](https://github.com/jennyzzt/dgm/search?l=dockerfile)