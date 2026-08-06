---
title: "HiST: Spatial Transcriptomics Prediction via Multi-Level Hyperbolic Representation Learning"
title_zh: "HiST: 通过多级双曲表示学习预测空间转录组学"
authors: "Chen Zhang, Yilu An, Ying Chen, Hao Li, Xitong Ling, Lihao Liu, Junjun He, Yuxiang Lin, Zihui Wang, Rongshan Yu"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=A9sAYUD3XB"
tags: ["query:immuno-topo"]
score: 9.0
evidence: 基于组织学图像的深度学习进行基因表达预测
tldr: 现有方法仅关注斑点级别的图像-基因匹配，未利用ST数据的多层级结构，且存在信息不对称问题；HiST提出多层级双曲表示学习，同时建模图像和基因的层次关系，以实现更完整的图像-基因对齐，提升从组织学图像预测基因表达的准确性。
source: ICLR-2026-Public
selection_source: conference_retrieval
motivation: 空间转录组数据具有多层级结构，现有方法未充分利用，且基因表达与图像间信息不对称，导致对齐不完整。
method: 提出HiST，利用多级双曲表示学习，显式建模ST数据的层次结构，实现图像和基因表达的双侧嵌入对齐。
result: 预期在预测性能和对全层级信息的利用上超越现有方法，但摘要未给出具体结果。
conclusion: HiST为从组织学图像预测基因表达提供了更精细的表示学习框架。
---

## Abstract
Spatial Transcriptomics (ST) merges the benefits of pathology images and gene expression, linking molecular profiles with tissue structure to analyze spot-level function comprehensively.
Predicting gene expression from histology images is a cost-effective alternative to expensive ST technologies.
However, existing methods mainly focus on spot-level image-to-gene matching but fail to leverage the full hierarchical structure of ST data, especially on the gene expression side, leading to incomplete image-gene alignment.
Moreover, a challenge arises from the inherent information asymmetry: gene expression profiles contain more molecular details that may lack salient visual correlates in histological images, demanding a sophisticated representation learning approach to bridge this modality gap.
We propose HiST, a framework for ST prediction that learns multi-level image-gene representations by modeling the data's inherent hierarchy within hyperbolic space, a natural geometric setting for such structures.
First, we design a Multi-Level Representation Extractor to capture both spot-level and niche-level representations from each modality, providing context-aware information beyond individual spot-level image-gene pairs.
Second, a Hierarchical Hyperbolic Alignment module is introduced to unify these representations, performing spatial alignment while hierarchically structuring image and gene embeddings.
This alignment strategy enriches the image representations with molecular semantics, significantly improving cross-modal prediction.
HiST achieves state-of-the-art performance on three public datasets from different tissues, paving the way for more scalable and accurate spatial transcriptomics prediction.

---

## 论文详细总结（自动生成）

### 论文核心问题与整体含义
- **研究背景**：空间转录组学（Spatial Transcriptomics, ST）结合了病理图像和基因表达，可从组织中斑点的功能进行综合分析。从组织学图像预测基因表达是一种替代昂贵ST技术的低成本方案。
- **现存问题**：
  - 现有方法大多只关注斑点级别的图像‑基因匹配，未充分利用ST数据的多层级结构（尤其是基因表达侧的层次），导致图像‑基因对齐不完整。
  - 存在模态间信息不对称：基因表达谱包含的分子细节在组织学图像中缺乏明显的视觉对应，需要更精细的表示学习来弥补差异。
- **本文动机**：设计能显式建模ST数据层级结构的方法，实现更全面的图像‑基因对齐，从而提升从组织学图像预测基因表达的准确性。

### 方法论
- **核心思想**：通过多级双曲空间中的表示学习，同时捕捉图像和基因表达的层次关系，在统一空间中完成跨模态对齐与预测。
- **关键技术细节**（基于摘要）：
  - **多级表示提取器**（Multi‑Level Representation Extractor）：从每一模态中提取斑点级（spot‑level）和微环境级（niche‑level）的表示，提供超越单个斑点的上下文信息。
  - **层次化双曲对齐模块**（Hierarchical Hyperbolic Alignment）：将上述多级表示在双曲空间中进行空间对齐，并层次化地组织图像和基因嵌入，使图像表示富集分子语义，从而改善跨模态预测。
  - **几何选择**：利用双曲空间的自然层次特性来匹配ST数据的内在结构。

### 实验设计（基于摘要信息，全文缺失具体细节）
- **数据集**：在三个来自不同组织的公开数据集上进行评估（如摘要所述，但具体名称未透露）。
- **Benchmark与对比方法**：摘要声明“达到最先进性能”，但未列出对比的具体方法或评估指标。预期对比了当前主流ST预测模型（如HisToGene、ST‑Net等），但无法从本文本中获得详细清单。
- **实验内容推测**：可能包含跨数据集的预测性能对比、消融实验（验证多级表示、双曲空间等组件的有效性）等，但因全文缺失，无法确认实验设计的具体结构与公平性。

### 资源与算力
- 所提供的文本中**未提及任何算力信息**（如GPU型号、数量、训练时长）。无法评估计算开销。

### 实验数量与充分性
- 摘要仅提及在**三个不同组织的公开数据集**上进行了评估，且声称达到SOTA，但**未给出实验组数、消融实验数量或统计检验**等信息。由于无法获取全文，无法判断实验是否达到严格意义上的充分、客观与公平。

### 主要结论与发现
- HiST通过多级双曲表示学习，有效整合了组织学图像与基因表达的层次结构。
- 该方法成功缓解了模态间信息不对称，使图像表示获得更丰富的分子语义。
- 在三个独立数据集上取得了最优预测性能，为可扩展、高精度的空间转录组学预测铺平了道路。

### 优点
- **层级建模**：首次显式利用ST数据在图像和基因双边的多层级结构，而非局限于斑点级对齐。
- **几何适配**：选用双曲空间作为表示空间，天然适合树状或层次结构数据。
- **双向对齐**：同时将图像和基因嵌入进行层次化组织，实现了更完整的跨模态融合。
- **性能突破**：在多个组织类型的公开数据上均取得SOTA，展示了良好的泛化潜力。

### 不足与局限
- **信息缺失限制评估**：由于无法访问论文全文，无法评价其具体实验对比的客观性、消融实验的完整性、统计显著性检验以及泛化到临床样本的鲁棒性。
- **潜在局限**（基于摘要推断）：
  - 对“niche‑level”层次的定义可能需要先验知识（如空间邻域关系或聚类），对此泛化能力未在摘要中讨论。
  - 双曲空间训练的稳定性和计算开销可能成为部署瓶颈，但摘要未提及。
  - 缺少对低质量图像或跨平台数据表现的说明，实际应用中的域迁移能力未知。

（完）
