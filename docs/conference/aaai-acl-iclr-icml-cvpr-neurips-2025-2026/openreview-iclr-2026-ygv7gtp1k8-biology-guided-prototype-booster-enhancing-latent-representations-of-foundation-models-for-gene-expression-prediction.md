---
title: "Biology-Guided Prototype Booster: Enhancing Latent Representations of Foundation Models for Gene Expression Prediction"
title_zh: 生物学引导的原型增强器：增强基础模型潜在表示用于基因表达预测
authors: "Chaoyi Li, Quan Nguyen"
date: 2025-09-19
pdf: "https://openreview.net/pdf?id=ygv7GTp1k8"
tags: ["query:immuno-topo"]
score: 8.0
evidence: "增强H&E组织学图像的深度学习以预测空间基因表达"
tldr: "针对基础模型从H&E染色组织图像预测基因表达时缺乏任务特定适用性的问题，提出生物学引导的原型增强器（BP-Booster），通过引入生物学原型自适应调整通用嵌入，提升预测精度。实验结果表明，该方法在多个癌症数据集上有效增强了基因表达预测能力，为精准病理学提供了新范式。"
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 弥补现有病理基础模型嵌入在基因表达预测任务上缺乏专用优化的问题。
method: 设计生物学原型增强模块，利用可学习的原型向量对齐和增强预训练嵌入，使其适应下游基因表达预测。
result: "在多种肿瘤类型上显著提升了从H&E图像预测空间转录组标志物的性能。"
conclusion: 通过生物学先验引导的特征增强，为数字病理中影像与分子关联分析提供了有效方案。
---

## Abstract
Spatial transcriptomics (ST) is a cutting-edge technology that enables the measurement of gene expression while preserving spatial context and generating detailed tissue images. However, ST technology remains time-consuming and costly. The ability to predict ST gene markers of cancer from histology-grade H&E-stained tissue images is opening new horizons for precision and personalised pathology. Despite the success of foundation models in generating general-purpose embeddings of H&E-images, these representations are not optimized for gene expression prediction and lack task-specific adaptability. To address this limitation, we introduce Biology-Guided Prototype Booster (BP-Booster), leveraging biological prior knowledge to guide the construction and training of learnable prototypes for embedding reconstruction, thereby improving gene expression prediction. We demonstrate superior performance of BP-Booster across datasets, various cancer tissue types and different ST platforms. We also show that BP-Booster can flexibly integrate various foundation models to enhance their task-specific representations, enhancing explainability and applicability in clinically relevant tasks like predicting cancer biomarkers. Code will be released upon acceptance.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
增强H&E组织学图像的深度学习以预测空间基因表达。

### 2. 核心内容
针对基础模型从H&E染色组织图像预测基因表达时缺乏任务特定适用性的问题，提出生物学引导的原型增强器（BP-Booster），通过引入生物学原型自适应调整通用嵌入，提升预测精度。实验结果表明，该方法在多个癌症数据集上有效增强了基因表达预测能力，为精准病理学提供了新范式。

### 3. 对应检索需求
digital pathology image analysis using deep learning。

### 4. 来源与原文
- Source：ICLR-2026-Rejected-Public
- OpenReview：[https://openreview.net/forum?id=ygv7GTp1k8](https://openreview.net/forum?id=ygv7GTp1k8)
