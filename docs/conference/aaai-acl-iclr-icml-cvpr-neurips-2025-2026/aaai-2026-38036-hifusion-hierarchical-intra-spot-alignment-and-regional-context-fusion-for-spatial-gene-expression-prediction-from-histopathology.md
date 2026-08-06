---
title: "HiFusion: Hierarchical Intra-Spot Alignment and Regional Context Fusion for Spatial Gene Expression Prediction from Histopathology"
title_zh: HiFusion：层次化点内对齐与区域上下文融合用于组织病理学空间基因表达预测
authors: "Ziqiao Weng, Yaoyu Fang, Jiahe Qian, Xinkun Wang, Lee A D Cooper, Weidong Cai, Bo Zhou"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/38036/41998"
tags: ["query:immuno-topo"]
score: 8.0
evidence: "利用H&E全切片图像预测空间基因表达，通过层次化建模和上下文融合"
tldr: 针对现有方法难以捕捉点内生物异质性和易受形态噪声影响的问题，提出HiFusion框架，通过层次化点内建模提取细粒度形态表示，并结合区域上下文融合模块预测基因表达。在多个ST数据集上验证，性能优于现有方法，为低成本基因表达推断提供新思路。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38036/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1836, \"height\": 871}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38036/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 876, \"height\": 892}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38036/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1796, \"height\": 816}]"
tables_json: "[{\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38036/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1830, \"height\": 491}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38036/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 791, \"height\": 351}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38036/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 810, \"height\": 209}]"
motivation: 现有方法无法捕捉点内生物学异质性，且易受组织形态噪声干扰。
method: "设计层次化点内建模模块和区域上下文融合模块，从H&E图像中预测基因表达。"
result: 在空间转录组学数据集上，预测准确性显著超越基线。
conclusion: HiFusion有效融合多尺度组织信息，实现精准的基因表达预测。
---

## Abstract
Spatial transcriptomics (ST) bridges gene expression and tissue morphology but faces clinical adoption barriers due to technical complexity and prohibitive costs. While computational methods predict gene expression from H&E-stained whole-slide images (WSIs), existing approaches often fail to capture the intricate biological heterogeneity within spots and are susceptible to morphological noise when integrating contextual information from surrounding tissue. To overcome these limitations, we propose HiFusion, a novel deep learning framework that integrates two complementary components. First, we introduce the Hierarchical Intra-Spot Modeling module that extracts fine-grained morphological representations through multi-resolution sub-patch decomposition, guided by a feature alignment loss to ensure semantic consistency across scales. Concurrently, we present the Context-aware Cross-scale Fusion module, which employs cross-attention to selectively incorporate biologically relevant regional context, thereby enhancing representational capacity. This architecture enables comprehensive modeling of both cellular-level features and tissue microenvironmental cues, which are essential for accurate gene expression prediction. Extensive experiments on two benchmark ST datasets demonstrate that HiFusion achieves state-of-the-art performance across both 2D slide-wise cross-validation and more challenging 3D sample-specific scenarios. These results underscore HiFusion’s potential as a robust, accurate, and scalable solution for ST inference from routine histopathology.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
利用H&E全切片图像预测空间基因表达，通过层次化建模和上下文融合。

### 2. 核心内容
针对现有方法难以捕捉点内生物异质性和易受形态噪声影响的问题，提出HiFusion框架，通过层次化点内建模提取细粒度形态表示，并结合区域上下文融合模块预测基因表达。在多个ST数据集上验证，性能优于现有方法，为低成本基因表达推断提供新思路。

### 3. 对应检索需求
digital pathology image analysis using deep learning。

### 4. 来源与原文
- Source：AAAI-2026-Accepted
- OpenReview：[https://ojs.aaai.org/index.php/AAAI/article/view/38036](https://ojs.aaai.org/index.php/AAAI/article/view/38036)
