---
title: "DFin/Neural-Network-Visualisation: Interactive web visualisation for handwritting detection using a simple neural network"
source: "https://github.com/DFin/Neural-Network-Visualisation"
author:
  - "[[DFin]]"
published:
created: 2025-11-14
description: "Interactive web visualisation for handwritting detection using a simple neural network - DFin/Neural-Network-Visualisation"
tags:
  - "clippings"
---
David Finsterwalder开源了一款基于Three.js的神经网络可视化工具，展示了一个简单多层感知机（MLP）在MNIST手写数字上的训练过程。所有训练和可视化代码用PyTorch写成，完全开源，方便学生和开发者直观理解神经网络的动态变化。  
  
这款工具运行在浏览器上，权重数据以JSON形式存储，适合桌面大屏体验，手机端菜单显示有些重叠。尽管目前教学内容主要是德语且依赖现场讲解，作者计划未来翻译并丰富教育资料，甚至考虑通过WebRTC支持平板手写输入，提升互动体验。  
  
Finsterwalder称此项目100%“vibecoded”完成，得益于Three.js的强大以及PyTorch实现MLP的简洁。他的灵感部分来自3Blue1Brown的神经网络视频封面，强烈推荐该频道作为神经网络入门资源。  
  
该项目更适合教学核心原理，网络结构简单（约11万参数），相比大型模型如LLM更便于理解和演示。社区反响热烈，大家一致认为此类可视化是连接理论与实际的桥梁，有助学生直观感受模型训练，甚至激发研究者对架构互动式实验的兴趣。  
  
与现有类似项目相比，Finsterwalder强调自己更注重动态权重更新的展示和空间三维效果，避免了扁平神经元排列的视觉局限。他也在与展览方沟通，期待将此工具带入更多教学和展示场景。  
  
这不仅是一次技术展示，也是对可视化教学未来的探索。让深奥的神经网络变得“看得见、摸得着”，才能真正激发更多创新与理解。

Interactive web visualisation for handwritting detection using a simple neural network

[nn-vis.noelith.dev](https://nn-vis.noelith.dev/ "https://nn-vis.noelith.dev")

[Apache-2.0 license](https://github.com/DFin/Neural-Network-Visualisation/blob/main/LICENSE)

[Open in github.dev](https://github.dev/) [Open in a new github.dev tab](https://github.dev/) [Open in codespace](https://github.com/codespaces/new/DFin/Neural-Network-Visualisation?resume=1)

<table><thead><tr><th colspan="2"><span>Name</span></th><th colspan="1"><span>Name</span></th><th><p><span>Last commit message</span></p></th><th colspan="1"><p><span>Last commit date</span></p></th></tr></thead><tbody><tr><td colspan="3"><p><span><a href="https://github.com/DFin/Neural-Network-Visualisation/commit/18ca0bf5650c5f2668394ba81465fb0f62bee336">Added more info about the network.</a></span></p><p><span><a href="https://github.com/DFin/Neural-Network-Visualisation/commit/18ca0bf5650c5f2668394ba81465fb0f62bee336">18ca0bf</a> ·</span></p><p><a href="https://github.com/DFin/Neural-Network-Visualisation/commits/main/"><span><span><span>48 Commits</span></span></span></a></p></td></tr><tr><td colspan="2"><p><a href="https://github.com/DFin/Neural-Network-Visualisation/tree/main/assets">assets</a></p></td><td colspan="1"><p><a href="https://github.com/DFin/Neural-Network-Visualisation/tree/main/assets">assets</a></p></td><td><p><a href="https://github.com/DFin/Neural-Network-Visualisation/commit/18ca0bf5650c5f2668394ba81465fb0f62bee336">Added more info about the network.</a></p></td><td></td></tr><tr><td colspan="2"><p><a href="https://github.com/DFin/Neural-Network-Visualisation/tree/main/exports">exports</a></p></td><td colspan="1"><p><a href="https://github.com/DFin/Neural-Network-Visualisation/tree/main/exports">exports</a></p></td><td><p><a href="https://github.com/DFin/Neural-Network-Visualisation/commit/60b99a6fddf49971e10334d641bd22e1fee8f389">add mnist buttons + github link</a></p></td><td></td></tr><tr><td colspan="2"><p><a href="https://github.com/DFin/Neural-Network-Visualisation/tree/main/tools/mnist_assets"><span>tools/</span> <span>mnist_assets</span></a></p></td><td colspan="1"><p><a href="https://github.com/DFin/Neural-Network-Visualisation/tree/main/tools/mnist_assets"><span>tools/</span> <span>mnist_assets</span></a></p></td><td><p><a href="https://github.com/DFin/Neural-Network-Visualisation/commit/60b99a6fddf49971e10334d641bd22e1fee8f389">add mnist buttons + github link</a></p></td><td></td></tr><tr><td colspan="2"><p><a href="https://github.com/DFin/Neural-Network-Visualisation/tree/main/training">training</a></p></td><td colspan="1"><p><a href="https://github.com/DFin/Neural-Network-Visualisation/tree/main/training">training</a></p></td><td><p><a href="https://github.com/DFin/Neural-Network-Visualisation/commit/796cc7291faf75f3324c77af9f61d3eeace07639">Split up weigth file</a></p></td><td></td></tr><tr><td colspan="2"><p><a href="https://github.com/DFin/Neural-Network-Visualisation/blob/main/.gitignore">.gitignore</a></p></td><td colspan="1"><p><a href="https://github.com/DFin/Neural-Network-Visualisation/blob/main/.gitignore">.gitignore</a></p></td><td><p><a href="https://github.com/DFin/Neural-Network-Visualisation/commit/18ca0bf5650c5f2668394ba81465fb0f62bee336">Added more info about the network.</a></p></td><td></td></tr><tr><td colspan="2"><p><a href="https://github.com/DFin/Neural-Network-Visualisation/blob/main/LICENSE">LICENSE</a></p></td><td colspan="1"><p><a href="https://github.com/DFin/Neural-Network-Visualisation/blob/main/LICENSE">LICENSE</a></p></td><td><p><a href="https://github.com/DFin/Neural-Network-Visualisation/commit/998082f71a55cd5f05fc42f3e251242b872d24cd">Create LICENSE</a></p></td><td></td></tr><tr><td colspan="2"><p><a href="https://github.com/DFin/Neural-Network-Visualisation/blob/main/NOTICE.MD">NOTICE.MD</a></p></td><td colspan="1"><p><a href="https://github.com/DFin/Neural-Network-Visualisation/blob/main/NOTICE.MD">NOTICE.MD</a></p></td><td><p><a href="https://github.com/DFin/Neural-Network-Visualisation/commit/d81b6d316af38eade5ba328a25c7c99bd07edc49">free software notice</a></p></td><td></td></tr><tr><td colspan="2"><p><a href="https://github.com/DFin/Neural-Network-Visualisation/blob/main/README.md">README.md</a></p></td><td colspan="1"><p><a href="https://github.com/DFin/Neural-Network-Visualisation/blob/main/README.md">README.md</a></p></td><td><p><a href="https://github.com/DFin/Neural-Network-Visualisation/commit/6ac01a77226b90063de9545dd5da285a0a77b238">udpate readme with WIP notice</a></p></td><td></td></tr><tr><td colspan="2"><p><a href="https://github.com/DFin/Neural-Network-Visualisation/blob/main/deploy.sh">deploy.sh</a></p></td><td colspan="1"><p><a href="https://github.com/DFin/Neural-Network-Visualisation/blob/main/deploy.sh">deploy.sh</a></p></td><td><p><a href="https://github.com/DFin/Neural-Network-Visualisation/commit/5898e8f2b7b40f375d801497b74ec04cc55b13d9">Refactor deploy script to allow deployment of the current branch's HE…</a></p></td><td></td></tr><tr><td colspan="2"><p><a href="https://github.com/DFin/Neural-Network-Visualisation/blob/main/index.html">index.html</a></p></td><td colspan="1"><p><a href="https://github.com/DFin/Neural-Network-Visualisation/blob/main/index.html">index.html</a></p></td><td><p><a href="https://github.com/DFin/Neural-Network-Visualisation/commit/18ca0bf5650c5f2668394ba81465fb0f62bee336">Added more info about the network.</a></p></td><td></td></tr><tr><td colspan="3"></td></tr></tbody></table>

[![MNIST MLP Visualizer screenshot](https://raw.githubusercontent.com/DFin/Neural-Network-Visualisation/main/assets/screenshot.jpg)](https://raw.githubusercontent.com/DFin/Neural-Network-Visualisation/main/assets/screenshot.jpg)

Interactive web visualisation for a compact multi-layer perceptron trained on the MNIST handwritten digit dataset. Draw a digit, watch activations propagate through the network in 3D, and inspect real-time prediction probabilities.

## WIP

This is still in a rough state and under active development. If you want something useable for a museum etc check back later. I have a couple of features in mind (like being able to connect a tablet to draw a number) to make this a good educational visualisation.

## Repository Layout

- `index.html` / `assets/` – Static Three.js visualiser and UI assets.
- `exports/mlp_weights.json` – Default weights with timeline snapshots (generated from the latest training run).
- `training/mlp_train.py` – PyTorch helper to train the MLP (with Apple Metal acceleration when available) and export weights for the front-end.

## Quick Start

1. (Only for training) **Install Python dependencies** (PyTorch + torchvision):
	```
	python3 -m pip install torch torchvision
	```
2. **Launch a static file server** from the repository root (any server works; this example uses Python):
	```
	python3 -m http.server 8000
	```
3. Open `http://localhost:8000` in your browser. Draw on the 28×28 grid (left-click to draw, right-click to erase) and explore the 3D network with the mouse or trackpad.

`training/mlp_train.py` trains a small MLP on MNIST and writes a JSON export the front-end consumes. Metal (MPS) is used automatically when available on Apple Silicon; otherwise the script falls back to CUDA or CPU.

Typical usage:

```
python3 training/mlp_train.py \
  --epochs 5 \
  --hidden-dims 128 64 \
  --batch-size 256 \
  --export-path exports/mlp_weights.json
```

Key options:

- `--hidden-dims`: Hidden layer sizes (default `128 64`). Keep the network modest so the visualisation stays responsive.
- `--epochs`: Minimum training epochs (default `5`). The script will automatically extend the run so the timeline hits the 50× dataset milestone.
- `--batch-size`: Mini-batch size (default `128`).
- `--device`: Force `mps`, `cuda`, or `cpu`. By default the script picks the best available backend.
- `--skip-train`: Export the randomly initialised weights without running training (useful for debugging the pipeline).

After training, update `VISUALIZER_CONFIG.weightUrl` in `assets/main.js` if you export to a different location/name. Refresh the browser to load the new weights.

Every exported JSON now includes a `timeline` array spanning 35 checkpoints: densely spaced early snapshots (≈50, 120, 250, 500, 1k, 2k, 3.5k, 5.8k, 8.7k, 13k, 19.5k, 28.5k, 40k images), followed by dataset-multiple milestones from 1× through 50×. The JSON manifest stays small; each snapshot’s weights are stored separately as float16-encoded files under `exports/<stem>/NNN_<id>.json`, and the front-end streams them on demand so you can scrub the timeline without downloading the entire 50× run up front. Re-export the weights with the updated script to generate fresh timeline data for your own runs.

- The visualiser highlights the top-N (configurable) strongest incoming connections per neuron to keep the scene legible.
- Colors encode activation sign and magnitude (cool tones for negative/low, warm tones for strong positive contributions).
- The default export (`exports/mlp_weights.json`) already includes timeline milestones from a multi-epoch training run. Retrain (and re-export) if you want to showcase a different progression.
- If you adjust the architecture, ensure the JSON export reflects the new layer sizes; the front-end builds the scene dynamically from that metadata.

## Deployment

The server keeps live assets separate from active development under `releases/`:

- `releases/current/` – files served by your static HTTP server.
- `releases/backups/<timestamp>/` – point-in-time snapshots for quick rollback.
- `releases/.deploy_tmp/` – staging area used during deployment.

To publish the code you currently have checked out, run the deploy script from the repository root:

```
./deploy.sh
```

You can target a different commit or branch explicitly:

```
./deploy.sh <commit-ish>
```

The script exports the requested commit into the staging area, syncs it into `releases/current/`, and saves the same tree under `releases/backups/<timestamp>/` with the commit hash recorded in `.commit`.

## Releases

No releases published

## Packages

No packages published