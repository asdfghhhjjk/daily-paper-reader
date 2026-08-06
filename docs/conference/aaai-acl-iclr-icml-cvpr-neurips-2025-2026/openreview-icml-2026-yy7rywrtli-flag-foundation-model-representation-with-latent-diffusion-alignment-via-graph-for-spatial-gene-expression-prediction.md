---
title: "FLAG: Foundation model representation with Latent diffusion Alignment via Graph for spatial gene expression prediction"
title_zh: FLAG：基于图潜在扩散对齐的基础模型表示用于空间基因表达预测
authors: "Qi Si, Penglei Wang, Yushuai Wu, Yifeng Jiao, Xuyang Liu, Xin Guo, Yuan Qi, Yuan Cheng"
date: 2026-04-30
pdf: "https://openreview.net/pdf/f5a1052a91be4f7d3e1bc8267d8ec32a3a250e26.pdf"
tags: ["query:immuno-topo"]
score: 4.0
evidence: "利用图增强扩散模型从 H&E 图像预测空间基因表达，属于组织学图像的深度学习分析"
tldr: "提出 FLAG 框架，通过空间图编码器结合基因基础模型，从 H&E 图像预测空间基因表达，解决高维基因表达联合建模难题，为组织学图像进行分子图谱分析提供了新方法。"
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: "当前模型将 H&E 到空间基因表达预测视为孤立点任务，忽略基因协调和空间分布等生物结构。"
method: 提出扩散框架 FLAG，集成空间图编码器保持拓扑一致性，并利用基因基础模型解决高维诅咒。
result: 有效解决了基因维度诅咒，在空间基因表达预测中保持了拓扑结构。
conclusion: 该方法揭示了结构化分布建模在组织学分子推断中的重要性。
---

## Abstract
Predicting spatial gene expression from routine H\&E enables large-scale molecular profiling, yet current models treat this as isolated pointwise tasks, thereby overlooking essential biological structures like gene coordination and spatial distribution. To preserve these relationships, we introduce \textbf{FLAG}, a diffusion-based framework that redefines this task as structured distribution modeling. At the same time, we identify the critical \textbf{Gene Dimension Curse}, where joint modeling gene expression and their spatial interactions fail in high-dimensional spaces, and FLAG solves this challenge by integrating a spatial graph encoder for topological consistency and utilizing Gene Foundation Model (GFM) alignment for gene-gene fidelity in the generation process. To rigorously assess model performance, we propose a set of novel structural evaluation metrics, including Gene Structural Correlation (\textbf{GSC}) and Spatial Structural Correlation (\textbf{SSC}). Our experiments demonstrate that FLAG is highly competitive in traditional accuracy (PCC/MSE) while achieving significantly enhanced structural fidelity in capturing both gene-gene and gene-spatial relationships. The code is available at https://github.com/darkflash03/FLAG.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
利用图增强扩散模型从 H&E 图像预测空间基因表达，属于组织学图像的深度学习分析。

### 2. 核心内容
提出 FLAG 框架，通过空间图编码器结合基因基础模型，从 H&E 图像预测空间基因表达，解决高维基因表达联合建模难题，为组织学图像进行分子图谱分析提供了新方法。

### 3. 对应检索需求
digital pathology image analysis using deep learning。

### 4. 来源与原文
- Source：ICML-2026-Accepted
- OpenReview：[https://openreview.net/forum?id=yY7rywRtlI](https://openreview.net/forum?id=yY7rywRtlI)
