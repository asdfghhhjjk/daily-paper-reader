---
title: "STAGE: A Foundation Model for Spatial Transcriptomics Analysis via Graph Embeddings with Hierarchical Prototypes"
title_zh: "STAGE: 基于图嵌入与层次化原型的空间转录组学基础模型分析"
authors: "Zhengchao Luo, Peiting Shi, Qichen Sun, Li Yongge, Han Wen, Jinzhuo Wang"
date: 2025-09-19
pdf: "https://openreview.net/pdf?id=ZGzKckA29U"
tags: ["query:immuno-topo"]
score: 8.0
evidence: 使用图嵌入分析组织微环境中的空间域
tldr: 针对空间转录组学跨样本、组织和技术平台一致性分析空间域存在批次效应与异质性数据等挑战，提出一种通用型基础模型STAGE，利用图嵌入与层次化原型学习空间表示，实现不同条件下组织微环境空间域的可重复识别。实验表明模型在多平台数据上均取得优异泛化性能，有助于加深对疾病相关微环境空间组织的理解。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 克服当前空间转录组学中跨批次、跨平台识别空间域的不一致性问题。
method: 构建基于图嵌入与可学习层次化原型的表示框架，通过图神经网络编码空间邻近关系并学习分层的域原型，实现跨域泛化的空间域识别。
result: 模型在多个空间转录组学平台上均显示出强泛化能力，能够一致地划分组织空间域。
conclusion: 为空间转录组学提供了鲁棒的分析工具，推动了组织微环境空间组织研究的可重复性。
---

## Abstract
Spatial transcriptomics offers an unprecedented opportunity to elucidate the spatial organization of tissues by capturing gene expression profiles while preserving tissue architecture. This enables the identification of spatial niches and deepens our understanding of tissue function and disease-associated microenvironments. However, consistent identification of spatial domains across samples, tissues, and even technological platforms remains a formidable challenge, due to low-dimensional and heterogeneous gene panels across platforms, pronounced batch effects, and substantial biological variability between samples. To address these limitations, we propose STAGE, a generalizable foundation model for spatial transcriptomics via graph embeddings. At its core, STAGE introduces a hierarchical prototype mechanism to capture global semantic representations of spatial niches, alongside an efficient online expectation-maximization algorithm to enable scalable learning from large-scale heterogeneous data. Pretrained on a large dataset comprising 32 million cells from 18 tissue types, STAGE learns robust cell representations within their neighborhood graphs and supports niche inference for domain recognition. Comprehensive evaluations on multiple benchmark datasets demonstrate that STAGE substantially enhances domain consistency in cross-platform, cross-sample, and cross-tissue spatial domain identification tasks, outperforming existing state-of-the-art methods. Furthermore, STAGE supports critical downstream biological analyses, highlighting its strong potential as a powerful tool in biological research.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
使用图嵌入分析组织微环境中的空间域。

### 2. 核心内容
针对空间转录组学跨样本、组织和技术平台一致性分析空间域存在批次效应与异质性数据等挑战，提出一种通用型基础模型STAGE，利用图嵌入与层次化原型学习空间表示，实现不同条件下组织微环境空间域的可重复识别。实验表明模型在多平台数据上均取得优异泛化性能，有助于加深对疾病相关微环境空间组织的理解。

### 3. 对应检索需求
Spatial analysis methods for tumor immune microenvironment using graph neural networks.

### 4. 来源与原文
- Source：ICLR-2026-Rejected-Public
- OpenReview：[https://openreview.net/forum?id=ZGzKckA29U](https://openreview.net/forum?id=ZGzKckA29U)
