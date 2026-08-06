---
title: "Fusing Pixels and Genes: Spatially-Aware Learning in Computational Pathology"
title_zh: 融合像素与基因：计算病理学中的空间感知学习
authors: "Minghao Han, Dingkang Yang, Linhao Qu, Zizhi Chen, Gang Li, Han Wang, Jiacong Wang, Lihua Zhang"
date: 2026-01-26
pdf: "https://openreview.net/pdf?id=uVXO6gzVzj"
tags: ["query:immuno-topo"]
score: 8.0
evidence: 提出STAMP，一种空间转录组学指导的病理图像表示学习框架
tldr: 现有计算病理多模态模型主要依赖视觉与语言，缺乏分子特异性。本文提出STAMP框架，将空间分辨的基因表达谱与病理图像联合嵌入，通过自监督基因引导训练学习鲁棒的病理图像表示。该方法在多个下游任务中表现出色，为利用空间转录组学增强病理图像分析提供了新范式。
source: ICLR-2026-Accepted
selection_source: conference_retrieval
motivation: 现有病理多模态模型仅依赖视觉和语言模态，缺少分子特异性，导致表示瓶颈。
method: 提出STAMP框架，利用空间基因表达数据指导病理图像的联合嵌入学习。
result: 自监督基因引导训练为病理图像表示提供了稳健的任务无关信号。
conclusion: 空间感知的基因引导表示学习有望提升计算病理学的多任务性能。
---

## Abstract
Recent years have witnessed remarkable progress in multimodal learning within computational pathology. Existing models primarily rely on vision and language modalities; however, language alone lacks molecular specificity and offers limited pathological supervision, leading to representational bottlenecks. In this paper, we propose STAMP, a Spatial Transcriptomics-Augmented Multimodal Pathology representation learning framework that integrates spatially-resolved gene expression profiles to enable molecule-guided joint embedding of pathology images and transcriptomic data. Our study shows that self-supervised, gene-guided training provides a robust and task-agnostic signal for learning pathology image representations. Incorporating spatial context and multi-scale information further enhances model performance and generalizability. To support this, we constructed SpaVis-6M, the largest Visium-based spatial transcriptomics dataset to date, and trained a spatially-aware gene encoder on this resource. Leveraging hierarchical multi-scale contrastive alignment and cross-scale patch localization mechanisms, STAMP effectively aligns spatial transcriptomics with pathology images, capturing spatial structure and molecular variation. We validate STAMP across six datasets and four downstream tasks, where it consistently achieves strong performance. These results highlight the value and necessity of integrating spatially resolved molecular supervision for advancing multimodal learning in computational pathology. The code is included in the supplementary materials. The pretrained weights and SpaVis-6M are available at: https://github.com/Hanminghao/STAMP.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
提出STAMP，一种空间转录组学指导的病理图像表示学习框架。

### 2. 核心内容
现有计算病理多模态模型主要依赖视觉与语言，缺乏分子特异性。本文提出STAMP框架，将空间分辨的基因表达谱与病理图像联合嵌入，通过自监督基因引导训练学习鲁棒的病理图像表示。该方法在多个下游任务中表现出色，为利用空间转录组学增强病理图像分析提供了新范式。

### 3. 对应检索需求
digital pathology image analysis using deep learning。

### 4. 来源与原文
- Source：ICLR-2026-Accepted
- OpenReview：[https://openreview.net/forum?id=uVXO6gzVzj](https://openreview.net/forum?id=uVXO6gzVzj)
