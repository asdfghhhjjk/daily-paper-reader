---
title: Sequential Attention-based Sampling for Histopathological Analysis
title_zh: 用于组织病理分析的顺序注意力采样
authors: "Tarun G, Naman Malpani, Gugan Thoppe, Devarajan Sridharan"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=wlqoUpuQrv"
tags: ["query:path-xai-sel"]
score: 8.0
evidence: 基于顺序注意力的强化学习采样，用于选取全切片图像中诊断重要的区域
tldr: 提出 SASHA 方法，通过深度强化学习与注意力机制顺序采样全切片图像中具有诊断信息的关键区域，显著提高分析效率，并仅依赖滑动窗级别标签进行训练。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
motivation: 全切片图像尺寸巨大且仅有整张切片标签，精细标注耗时昂贵。
method: 利用深度强化学习学习信息性采样策略，基于注意力顺序选择高价值补丁。
result: 在保持准确性的同时大幅降低了计算成本，提升了处理效率。
conclusion: 顺序注意力采样为大规模组织病理图像分析提供了高效、可解释的样板。
---

## Abstract
Deep neural networks are increasingly applied in automated histopathology. Yet, whole-slide images (WSIs) are often acquired at gigapixel sizes, rendering them computationally infeasible to analyze entirely at high resolution. Diagnostic labels are largely available only at the slide-level, because expert annotation of images at a finer (patch) level is both laborious and expensive. Moreover, regions with diagnostic information typically occupy only a small fraction of the WSI, making it inefficient to examine the entire slide at full resolution.
Here, we propose SASHA -- Sequential Attention-based Sampling for Histopathological Analysis -- a deep reinforcement learning approach for efficient analysis of histopathological images. 
First, SASHA learns informative features with a lightweight hierarchical, attention-based multiple instance learning (MIL) model. 
Second, SASHA samples intelligently and zooms selectively into a small fraction (10-20\%) of high-resolution patches to achieve reliable diagnoses.
We show that SASHA matches state-of-the-art methods that analyze the WSI fully at high resolution, albeit at a fraction of their computational and memory costs. In addition, it significantly outperforms competing, sparse sampling methods. 
We propose SASHA as an intelligent sampling model for medical imaging challenges that involve automated diagnosis with exceptionally large images containing sparsely informative features. Model implementation is available at: https://github.com/coglabiisc/SASHA.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
基于顺序注意力的强化学习采样，用于选取全切片图像中诊断重要的区域。

### 2. 核心内容
提出 SASHA 方法，通过深度强化学习与注意力机制顺序采样全切片图像中具有诊断信息的关键区域，显著提高分析效率，并仅依赖滑动窗级别标签进行训练。

### 3. 对应检索需求
Papers central to 在计算病理领域，通过HE切片中计算的可解释特征（细胞组成/空间纹理/组织结构等等）挑选重要区域或者patch的研究, especially work that connects or combines: computational pathology analysis; explainable features for tissue analysis; selecting important regions in whole slide images; morphological feature analysis for patch ranking; utilizing spatial texture characteristics for interpretable region selection; methods for selecting salient patches based on explainable features; selecting salient patches in whole slide images using explainable features; identifying diagnostically relevant regions through interpretable cell composition and spatial analysis; ranking image regions by interpretable morphological and cellular features; Methods for interpretable region of interest detection in H&E stained slides based on spatial texture.

### 4. 来源与原文
- Source：NeurIPS-2025-Accepted
- OpenReview：[https://openreview.net/forum?id=wlqoUpuQrv](https://openreview.net/forum?id=wlqoUpuQrv)
