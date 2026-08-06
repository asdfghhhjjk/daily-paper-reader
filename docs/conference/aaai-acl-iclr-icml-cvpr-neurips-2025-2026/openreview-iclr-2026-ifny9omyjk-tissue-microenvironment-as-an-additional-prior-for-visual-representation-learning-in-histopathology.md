---
title: Tissue Microenvironment as an Additional Prior for Visual Representation Learning in Histopathology
title_zh: 组织微环境作为组织病理学视觉表示学习的额外先验
authors: "Swaraj Nanda, Neeraj Kumar, Siddharth Singi, Amir Momeni Boroujeni, Jie-Fu Chen, David Kim, Jamal Benhamida, Gregory M. Goldgof, Chad Vanderbilt"
date: 2025-09-19
pdf: "https://openreview.net/pdf?id=iFNY9Omyjk"
tags: ["query:profile"]
score: 8.0
evidence: 将组织微环境结构作为先验用于自监督组织病理图像表示学习
tldr: 针对现有自监督学习方法未充分利用组织微环境结构的问题，提出将组织微环境作为额外先验，通过对抗语义掩码增强DINOv2管道，在55M TCGA病理瓦片上预训练。结果显示结合微环境先验能提升下游任务性能，为数字病理学表示学习提供新方向。
source: ICLR-2026-Public
selection_source: conference_retrieval
motivation: 现有自监督病理模型忽略组织微环境的结构信息，限制了下游任务性能。
method: 采用对抗掩码生成器识别组织结构，将语义掩码作为增强融入DINOv2自监督学习。
result: 在55M TCGA瓦片预训练后，下游任务表现显著提升。
conclusion: 引入组织微环境先验可有效改善组织病理图像的表示学习。
---

## Abstract
Self-supervised learning has transformed histopathology by enabling foundation models to learn from vast unlabeled image archives, with methods developed using natural images, such as DINOv2, establishing powerful baselines. We propose augmenting these approaches by incorporating tissue microenvironment structure as an additional prior through semantic masking. We train adversarial mask generators adapted from ADIOS with perceptual reconstruction losses to identify tissue structures, then integrate these semantic masks as augmentations within DINOv2 self-supervised learning pipelines. Using a set of 55 million TCGA histopathology tiles of 224$\times$224 pixels at a resolution of 0.5 $\mu$m/pixel, we pre-train vision transformers to evaluate three augmentation strategies: standard DINOv2 augmentations, mixed (combining standard and semantic masking), and semantic masking only. The mixed augmentation strategy, when used in DINOv2, demonstrates consistent improvements over baseline across four patch-level classification benchmarks (PCam, MiDOG, MHIST, BRACS) and on two slide-level mutation prediction tasks (EGFR in LUAD, FGFR3 in BLCA). Qualitative PCA visualization of patch tokens shows that semantic masks combined with standard augmentations enable a better decomposition of tissue into biologically interpretable components without supervision, with DINOv2-mixed achieving clear separation of cellular structures, vasculature, and stromal elements. Therefore, incorporating domain-specific tissue priors through semantic masking enhances representation learning in self-supervised frameworks, alongside standard augmentations.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
将组织微环境结构作为先验用于自监督组织病理图像表示学习。

### 2. 核心内容
针对现有自监督学习方法未充分利用组织微环境结构的问题，提出将组织微环境作为额外先验，通过对抗语义掩码增强DINOv2管道，在55M TCGA病理瓦片上预训练。结果显示结合微环境先验能提升下游任务性能，为数字病理学表示学习提供新方向。

### 3. 对应检索需求
Papers central to 检索把跨patch或者全WSI级别的细胞形态学、微环境特征用于数字病理学下游任务的研究, especially work that connects or combines: 探索组织微环境特征在数字病理学分析中的应用; 利用细胞形态和微环境特征提升病理图像分割精度; integrating cross-patch information for WSI-level tasks; graph neural networks for tissue microenvironment modeling; fusing spatial features across patches for global prediction; cell-level feature extraction for downstream pathology tasks; 研究如何将细胞形态学与微环境特征应用到数字病理学的模型和任务中; 调查病理学下游任务中形态学和微环境特征的优化方法; How to aggregate cell morphology features from patches for whole slide image classification; Graph based representation of cellular interactions in digital pathology.

### 4. 来源与原文
- Source：ICLR-2026-Public
- OpenReview：[https://openreview.net/forum?id=iFNY9Omyjk](https://openreview.net/forum?id=iFNY9Omyjk)
