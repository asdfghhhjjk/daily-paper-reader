---
title: "HiST: Spatial Transcriptomics Prediction via Multi-Level Hyperbolic Representation Learning"
title_zh: HiST：通过多级双曲表示学习进行空间转录组学预测
authors: "Chen Zhang, Yilu An, Ying Chen, Hao Li, Xitong Ling, Lihao Liu, Junjun He, Yuxiang Lin, Zihui Wang, Rongshan Yu"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=A9sAYUD3XB"
tags: ["query:immuno-topo"]
score: 6.0
evidence: 利用层次双曲表示学习从组织学图像预测基因表达
tldr: "空间转录组学（ST）结合病理图像与基因表达分析，但从组织学图像预测基因表达面临信息不对称和层次结构利用不足的问题。HiST提出多级双曲表示学习方法，通过层次化对齐图像特征和基因表达矩阵，捕获不同尺度下的组织-分子关联。在多个ST数据集上，HiST优于现有方法，能更完整地重建基因表达谱，并提供了更合理的生物学解释。该研究为从可获取的H&E图像成本较低地推断分子特征提供了有效工具，对数字病理中多模态信息的充分利用具有重要意义。"
source: ICLR-2026-Public
selection_source: conference_retrieval
motivation: 空间转录组数据存在层次结构，且图像与基因表达信息不对称，现有方法未能有效利用。
method: 采用多级双曲空间表示学习，对图像和基因表达进行层次化对齐。
result: 提升了组织学图像到基因表达的预测性能，更完整地捕获分子模式。
conclusion: 层次化建模是处理空间转录组图像-基因对齐的有效途径。
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

### 1. 检索相关性
利用层次双曲表示学习从组织学图像预测基因表达。

### 2. 核心内容
空间转录组学（ST）结合病理图像与基因表达分析，但从组织学图像预测基因表达面临信息不对称和层次结构利用不足的问题。HiST提出多级双曲表示学习方法，通过层次化对齐图像特征和基因表达矩阵，捕获不同尺度下的组织-分子关联。在多个ST数据集上，HiST优于现有方法，能更完整地重建基因表达谱，并提供了更合理的生物学解释。该研究为从可获取的H&E图像成本较低地推断分子特征提供了有效工具，对数字病理中多模态信息的充分利用具有重要意义。

### 3. 对应检索需求
digital pathology image analysis using deep learning。

### 4. 来源与原文
- Source：ICLR-2026-Public
- OpenReview：[https://openreview.net/forum?id=A9sAYUD3XB](https://openreview.net/forum?id=A9sAYUD3XB)
