---
title: "MAPLE: Multi-scale Attribute-enhanced Prompt Learning for Few-shot Whole Slide Image Classification"
title_zh: MAPLE：面向少样本全切片图像分类的多尺度属性增强提示学习
authors: "Junjie Zhou, WEI SHAO, Yagao Yue, Wei Mu, Peng Wan, Qi Zhu, Daoqiang Zhang"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=yHi8Ao6GAe"
tags: ["query:immuno-topo"]
score: 6.0
evidence: 多尺度提示学习捕获组织学实体用于全切片分类
tldr: 针对现有方法仅使用切片级提示而忽视关键组织实体亚型特异性变异的问题，本文提出MAPLE框架，通过多尺度属性增强提示学习，联合整合多尺度视觉语义并进行预测。该方法在少样本全切片分类中有效提升了性能，展示了利用细胞级别信息增强病理图像分析的潜力。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
motivation: 现有提示学习方法依赖切片级提示，无法捕获对癌症诊断至关重要的组织实体亚型变异。
method: 提出多尺度属性增强提示学习框架，分层整合多尺度视觉语义用于少样本WSI分类。
result: 该方法有效提升了少样本全切片分类的性能。
conclusion: MAPLE为利用多尺度组织学特征进行病理图像分类提供了有效方案，可推广至其他下游任务。
---

## Abstract
Prompt learning has emerged as a promising paradigm for adapting pre-trained vision-language models (VLMs) to few-shot whole slide image (WSI) classification by aligning visual features with textual representations, thereby reducing annotation cost and enhancing model generalization. Nevertheless, existing methods typically rely on slide-level prompts and fail to capture the subtype-specific phenotypic variations of histological entities (e.g., nuclei, glands) that are critical for cancer diagnosis. To address this gap, we propose Multi-scale Attribute-enhanced Prompt Learning (MAPLE), a hierarchical framework for few-shot WSI classification that jointly integrates multi-scale visual semantics and performs prediction at both the entity and slide levels. Specifically, we first leverage large language models (LLMs) to generate entity-level prompts that can help identify multi-scale histological entities and their phenotypic attributes, as well as slide-level prompts to capture global visual descriptions. Then, an entity-guided cross-attention module is proposed to generate entity-level features, followed by aligning with their corresponding subtype-specific attributes for fine-grained entity-level prediction. To enrich entity representations, we further develop a cross-scale entity graph learning module that can update these representations by capturing their semantic correlations within and across scales.  The refined representations are then aggregated into a slide-level representation and aligned with the corresponding prompts for slide-level prediction. Finally, we combine both entity-level and slide-level outputs to produce the final prediction results. Results on three cancer cohorts confirm the effectiveness of our approach in addressing few-shot pathology diagnosis tasks.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
多尺度提示学习捕获组织学实体用于全切片分类。

### 2. 核心内容
针对现有方法仅使用切片级提示而忽视关键组织实体亚型特异性变异的问题，本文提出MAPLE框架，通过多尺度属性增强提示学习，联合整合多尺度视觉语义并进行预测。该方法在少样本全切片分类中有效提升了性能，展示了利用细胞级别信息增强病理图像分析的潜力。

### 3. 对应检索需求
digital pathology image analysis using deep learning。

### 4. 来源与原文
- Source：NeurIPS-2025-Accepted
- OpenReview：[https://openreview.net/forum?id=yHi8Ao6GAe](https://openreview.net/forum?id=yHi8Ao6GAe)
