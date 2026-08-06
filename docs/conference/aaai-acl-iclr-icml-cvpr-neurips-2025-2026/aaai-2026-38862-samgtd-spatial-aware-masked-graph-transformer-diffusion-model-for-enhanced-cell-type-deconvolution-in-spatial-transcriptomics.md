---
title: "SAMGTD: Spatial-Aware Masked Graph Transformer-Diffusion Model for Enhanced Cell Type Deconvolution in Spatial Transcriptomics"
title_zh: SAMGTD：空间感知掩码图transformer扩散模型用于增强空间转录组细胞类型去卷积
authors: "Shilin Zhang, Suixue Wang, Qingchen Zhang, Xiulong Liu"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/38862/42824"
tags: ["query:immuno-topo"]
score: 4.0
evidence: 增强空间转录组中细胞类型去卷积，助力肿瘤免疫微环境组成分析
tldr: 针对空间转录组中dropout事件影响细胞类型去卷积的问题，提出SAMGTD框架，结合空间感知掩码图transformer和扩散模型，有效恢复基因表达并提高去卷积精度。实验表明在肿瘤研究中可促进免疫治疗策略开发。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
motivation: 空间转录组的dropout事件限制细胞类型精确鉴定，影响肿瘤免疫研究。
method: 结合空间感知掩码图transformer和扩散模型，对基因表达进行去噪增强。
result: 在多个数据集上，细胞类型去卷积准确性显著提升。
conclusion: 该方法为空间转录组解析和免疫治疗提供有力工具。
---

## Abstract
Recent advances in spatial transcriptomics have enabled the integration of gene expression profiles with precise spatial coordinates, which have facilitated the exploration of tumor occurrence and development mechanisms, as well as the development of more effective targeted and immunotherapy approaches for tumor treatment. Deciphering cell type represents a critical challenge in spatial transcriptomics research. Existing methods are limited by the pervasive “dropout” events in spatial transcriptomics, hindering their ability to fully capture the relationship between spatial location and gene expression, thereby compromising the performance of cell type deconvolution. To address these limitations, we propose a spatial-aware masked graph transformer-diffusion model (SAMGTD) for enhanced cell type deconvolution in spatial transcriptomics. For spatial transcriptomics, the masked graph transformer model is designed to adaptively capture complex dependencies between spatial locations and gene expression. It employs a masking strategy that guides the model to focus on important local information during training, while the multi-head attention mechanism captures global context. More importantly, the spatial diffusion model is constructed to achieve the dual enhancement of spatial transcriptomics, including denoising and data imputation. It incorporates the multi-head attention mechanism and residual blocks, effectively addressing the “dropout” issue commonly encountered in spatial transcriptomics. For scRNA-seq, we construct a variational autoencoder to reduce noise interference while preserving key gene expression information. Finally, we construct a spatial-aware contrastive learning model to integrate scRNA-seq and spatial transcriptomics for cell type deconvolution. Experiments conducted on three datasets demonstrate that SAMGTD outperforms baseline methods.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
增强空间转录组中细胞类型去卷积，助力肿瘤免疫微环境组成分析。

### 2. 核心内容
针对空间转录组中dropout事件影响细胞类型去卷积的问题，提出SAMGTD框架，结合空间感知掩码图transformer和扩散模型，有效恢复基因表达并提高去卷积精度。实验表明在肿瘤研究中可促进免疫治疗策略开发。

### 3. 对应检索需求
analysis of immune microenvironment composition and spatial organization。

### 4. 来源与原文
- Source：AAAI-2026-Accepted
- OpenReview：[https://ojs.aaai.org/index.php/AAAI/article/view/38862](https://ojs.aaai.org/index.php/AAAI/article/view/38862)
