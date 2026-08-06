---
title: Predicting Gene Expression in Spatially Resolved Transcriptomics Across Samples Through Probabilistic Fusion of Hierarchical Histology and Spatial Information
title_zh: 跨样本空间转录组学中通过组织学和空间信息的概率融合预测基因表达
authors: "Yinbo Liu, QiWu, Keyang Ye, Xiao He, Tian Tian"
date: 2025-09-20
pdf: "https://openreview.net/pdf?id=C1hAtImSHo"
tags: ["query:immuno-topo"]
score: 4.0
evidence: 从组织学预测基因表达进行空间表征，与肿瘤微环境分析相关
tldr: 针对空间转录组学成本高、捕获区域有限的问题，提出STevs深度生成模型，通过概率融合组织学和空间信息预测基因表达，实现跨样本的高维预测，为从常规组织病理推断分子特征提供了新途径。
source: ICLR-2026-Public
selection_source: conference_retrieval
motivation: 现有方法无法有效预测高维基因表达且跨样本泛化差。
method: 提出STevs，采用深度生成模型概率融合图像和空间信息。
result: 在跨样本预测中，STevs优于现有方法，能够生成高质量基因表达图谱。
conclusion: STevs可扩展空间转录组学的应用，对肿瘤微环境特征化有价值。
---

## Abstract
Spatially resolved transcriptomics (SRT) is a transformative technology in biomedical research, yet its scalability is hindered by high costs and restricted capture areas. Computational methods for predicting high-quality gene expression are needed. However, existing methods are ineffective at predicting high-dimensional gene expression and generalizing to multiple spatial slices, primarily due to  inter-sample heterogeneity and ineffective integration of visual and spatial information. To address these challenges, we propose STevs, a deep generative model designed to predict gene expression from tissue histology through a probabilistic fusion of image and spatial representations. STevs employs a multimodal variational autoencoder (VAE) architecture featuring parallel encoders that process distinct modalities: a Swin Transformer for hierarchical visual representation extraction and a multilayer perceptron (MLP) for spatial coordinates. The latent representations from these modalities are fused under uncertainty using a Product of Experts (PoE) mechanism. Furthermore, we introduce a latent alignment loss to explicitly promote a shared representation across modalities, thereby ensuring consistency between the image and spatial latent spaces. Comprehensive experimental evaluations demonstrate that STevs not only achieves state-of-the-art performance on standard within-slice gene prediction tasks but also significantly outperforms existing methods in the more challenging cross-slice prediction scenario. Our work provides a powerful computational tool capable of predicting gene expression directly from histology images, reducing the need for costly SRT experiments.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
从组织学预测基因表达进行空间表征，与肿瘤微环境分析相关。

### 2. 核心内容
针对空间转录组学成本高、捕获区域有限的问题，提出STevs深度生成模型，通过概率融合组织学和空间信息预测基因表达，实现跨样本的高维预测，为从常规组织病理推断分子特征提供了新途径。

### 3. 对应检索需求
spatial characterization of tumor immune microenvironment。

### 4. 来源与原文
- Source：ICLR-2026-Public
- OpenReview：[https://openreview.net/forum?id=C1hAtImSHo](https://openreview.net/forum?id=C1hAtImSHo)
