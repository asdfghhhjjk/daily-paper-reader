---
title: "SPATIA: Multimodal Generation and Prediction of Spatial Cell Phenotypes"
title_zh: SPATIA：空间细胞表型的多模态生成与预测
authors: "Zhenglun Kong, Mufan Qiu, John Boesen, xiang lin, Sukwon Yun, Tianlong Chen, Manolis Kellis, Marinka Zitnik"
date: 2026-04-30
pdf: "https://openreview.net/pdf/6df30389ec5230663a3ec26c469b76e419fb5a42.pdf"
tags: ["query:immuno-topo"]
score: 6.0
evidence: 通过融合细胞形态、基因表达和空间上下文学习空间感知表示
tldr: 针对细胞形态、基因表达和空间上下文如何共同塑造组织功能这一挑战，本文提出SPATIA模型，通过多层级生成预测框架融合这些模态，学习统一的、空间感知的细胞至组织级表示。该方法可生成和预测空间细胞表型，为空间转录组学分析提供了新工具，有望应用于肿瘤微环境的空间表征。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 现有方法通常孤立或低分辨率地分析细胞形态、基因表达和空间背景，难以揭示它们如何共同塑造组织功能。
method: 提出多层级生成预测模型SPATIA，融合形态、表达和空间上下文，学习统一的空间感知表示。
result: SPATIA能够生成和预测空间细胞表型，实现多模态联合建模。
conclusion: 该模型为空间生物学研究提供了强大的生成与预测工具，有助于理解组织功能的空间基础。
---

## Abstract
Understanding how cellular morphology, gene expression, and spatial context jointly shape tissue function is a central challenge in biology. Image-based spatial transcriptomics technologies now provide high-resolution measurements of cell images and gene expression profiles, but existing methods typically analyze these modalities in isolation or at limited resolution. 
We address the problem by introducing SPATIA, a multi-level generative and predictive model that learns unified, spatially aware representations by fusing morphology, gene expression, and spatial context from the cell to the tissue level. SPATIA also incorporates a spatially conditioned generative framework with confidence-aware OT reweighting and morphology-profile alignment for modeling target-state morphology distributions. Specifically, we propose a confidence-aware flow matching objective that reweights weak optimal-transport pairs based on uncertainty. We further apply morphology-profile alignment to encourage biologically meaningful image generation, enabling the modeling of microenvironment-dependent phenotypic transitions. We assembled a multi-scale dataset consisting of 25.9 million cell-gene pairs across 17 tissues. We benchmark SPATIA against 18 models across 12 tasks, spanning categories such as phenotype generation, annotation, clustering, gene imputation, and cross-modal prediction. SPATIA achieves improved performance over state-of-the-art models, improving generative fidelity by 8\% and predictive accuracy by up to 3\%.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
通过融合细胞形态、基因表达和空间上下文学习空间感知表示。

### 2. 核心内容
针对细胞形态、基因表达和空间上下文如何共同塑造组织功能这一挑战，本文提出SPATIA模型，通过多层级生成预测框架融合这些模态，学习统一的、空间感知的细胞至组织级表示。该方法可生成和预测空间细胞表型，为空间转录组学分析提供了新工具，有望应用于肿瘤微环境的空间表征。

### 3. 对应检索需求
spatial characterization of tumor immune microenvironment。

### 4. 来源与原文
- Source：ICML-2026-Accepted
- OpenReview：[https://openreview.net/forum?id=8As2E4z9qt](https://openreview.net/forum?id=8As2E4z9qt)
