---
title: "GROVER: Graph-guided Representation of Omics and Vision with Expert Regulation for Adaptive Spatial Multi-omics Fusion"
title_zh: GROVER：图引导的组学与视觉表示与专家调控自适应空间多组学融合
authors: "Yongjun Xiao, Dian Meng, Xinlei Huang, Yanran Liu, Shiwei Ruan, Ziyue Qiao, Xubin Zheng"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/37104/41066"
tags: ["query:profile"]
score: 8.0
evidence: 通过图引导表示融合空间多组学与组织病理图像，实现全面组织分析
tldr: 针对多组学与组织图像融合时的语义异质性和分辨率不匹配问题，提出GROVER框架，利用图引导表示和专家调控自适应融合空间多组学与组织病理学图像。实验表明该融合能增强组织分析，为精准医学提供多模态整合工具。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
motivation: 现有融合方法难以处理多组学与组织图像的语义异质性和空间分辨率不一致。
method: 采用图引导表示学习结合专家调控机制，自适应融合组学与组织学特征。
result: 在多组学数据集上，融合表示显著提升组织分析准确性。
conclusion: GROVER为多模态空间数据整合提供了有效框架。
---

## Abstract
Effectively modeling multimodal spatial omics data is critical for understanding tissue complexity and underlying biological mechanisms. While spatial transcriptomics, proteomics, and epigenomics capture molecular features, they lack pathological morphological context. Integrating these omics with histopathological images is thus critical for comprehensive disease tissue analysis. However, substantial heterogeneity across omics, imaging, and spatial modalities poses significant challenges. Naive fusion of semantically distinct sources often leads to ambiguous representations. Additionally, the resolution mismatch between high-resolution histology images and lower-resolution sequencing spots complicates spatial alignment. Biological perturbations during sample preparation further distort modality-specific signals, hindering accurate integration. To address these challenges, we propose Graph-guided Representation of Omics and Vision with Expert Regulation for Adaptive Spatial Multi-omics Fusion (GROVER), a novel framework for adaptive integration of spatial multi-omics data. GROVER leverages a Graph Convolutional Network encoder based on Kolmogorov–Arnold Networks to capture the nonlinear dependencies between each modality and its associated spatial structure, thereby producing expressive, modality-specific embeddings. To align these representations, we introduce a spot-feature-pair contrastive learning strategy that explicitly optimizes the correspondence across modalities at each spot. Furthermore, we design a dynamic expert routing mechanism that adaptively selects informative modalities for each spot while suppressing noisy or low-quality inputs. Experiments on real-world spatial omics datasets demonstrate that GROVER outperforms state-of-the-art baselines, providing a robust and reliable solution for multimodal integration.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
通过图引导表示融合空间多组学与组织病理图像，实现全面组织分析。

### 2. 核心内容
针对多组学与组织图像融合时的语义异质性和分辨率不匹配问题，提出GROVER框架，利用图引导表示和专家调控自适应融合空间多组学与组织病理学图像。实验表明该融合能增强组织分析，为精准医学提供多模态整合工具。

### 3. 对应检索需求
Papers central to 检索把跨patch或者全WSI级别的细胞形态学、微环境特征用于数字病理学下游任务的研究, especially work that connects or combines: 探索组织微环境特征在数字病理学分析中的应用; 利用细胞形态和微环境特征提升病理图像分割精度; integrating cross-patch information for WSI-level tasks; graph neural networks for tissue microenvironment modeling; fusing spatial features across patches for global prediction; cell-level feature extraction for downstream pathology tasks; 研究如何将细胞形态学与微环境特征应用到数字病理学的模型和任务中; 调查病理学下游任务中形态学和微环境特征的优化方法; How to aggregate cell morphology features from patches for whole slide image classification; Graph based representation of cellular interactions in digital pathology.

### 4. 来源与原文
- Source：AAAI-2026-Accepted
- OpenReview：[https://ojs.aaai.org/index.php/AAAI/article/view/37104](https://ojs.aaai.org/index.php/AAAI/article/view/37104)
