---
title: Efficient Patch Search in Whole Slide Images via Morphological Momentum Prototype Learning
title_zh: 基于形态动量原型学习的全切片图像高效补丁搜索
authors: "Sihyeon Park, Jungwoo Park, Hyunjae Kim, Jaewoo Kang, Bumsoo Kim"
date: 2025-09-20
pdf: "https://openreview.net/pdf?id=rYbYbgeaEv"
tags: ["query:path-xai-sel"]
score: 7.0
evidence: 通过形态动量原型学习实现高效的全切片图像补丁搜索，避免多阶段流水线
tldr: 针对 WSI 分析中多阶段流水线复杂度高的问题，提出形态动量原型学习方法，通过形态特征高效检索有信息的补丁，简化了全切片表示构建。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 现有 WSI 处理严重依赖多阶段流水线，高倍率下复杂度剧增。
method: 利用形态动量原型学习，根据形态特征快速定位关键补丁区域。
result: 在保证性能的同时显著降低了计算开销，提升了效率。
conclusion: 形态驱动的高效搜索为大规模病理图像筛选提供了实用工具。
---

## Abstract
Digital histopathology images play a crucial role in cancer diagnosis, therapeutic response prediction, and identification of clinically relevant morphological features. However, processing Whole Slide Images (WSI) with gigapixel resolution introduces significant challenges in computer vision, exceeding the memory capacity of standard vision encoders. To address this, recent methods employ a multi-stage pipeline: dissecting the image into small patches, extracting patch-level features, and aggregating these features using global pooling through Multi-Instance Learning (MIL) to form a final slide-level representation. Despite achieving clinical-grade performance, this approach becomes increasingly complex with higher magnification due to the quadratic increase in patch numbers and the generation of numerous irrelevant or redundant patches. This complexity burdens the global pooling network, resulting in long inference times and excessive computational resources, while redundant patches introduce noise during the MIL process, limiting the model’s ability to utilize high-magnification features fully. To overcome these challenges, we propose Momentum Morphological Prototype Learning (MMPL), an efficient method that redefines WSI diagnosis as a searching process of relevant patch-level representations with a learned set of global prototypes. MMPL trains a fixed set of prototypes to retrieve the most informative patches, computing the diagnostic score using only the retrieved patches. Evaluated on WSI classification benchmarks, MMPL achieves state-of-the-art performance across various pathology tasks, including metastasis detection, tumor grading, and tumor subtyping.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
通过形态动量原型学习实现高效的全切片图像补丁搜索，避免多阶段流水线。

### 2. 核心内容
针对 WSI 分析中多阶段流水线复杂度高的问题，提出形态动量原型学习方法，通过形态特征高效检索有信息的补丁，简化了全切片表示构建。

### 3. 对应检索需求
Papers central to 在计算病理领域，通过HE切片中计算的可解释特征（细胞组成/空间纹理/组织结构等等）挑选重要区域或者patch的研究, especially work that connects or combines: computational pathology analysis; explainable features for tissue analysis; selecting important regions in whole slide images; morphological feature analysis for patch ranking; utilizing spatial texture characteristics for interpretable region selection; methods for selecting salient patches based on explainable features; selecting salient patches in whole slide images using explainable features; identifying diagnostically relevant regions through interpretable cell composition and spatial analysis; ranking image regions by interpretable morphological and cellular features; Methods for interpretable region of interest detection in H&E stained slides based on spatial texture.

### 4. 来源与原文
- Source：ICLR-2026-Rejected-Public
- OpenReview：[https://openreview.net/forum?id=rYbYbgeaEv](https://openreview.net/forum?id=rYbYbgeaEv)
