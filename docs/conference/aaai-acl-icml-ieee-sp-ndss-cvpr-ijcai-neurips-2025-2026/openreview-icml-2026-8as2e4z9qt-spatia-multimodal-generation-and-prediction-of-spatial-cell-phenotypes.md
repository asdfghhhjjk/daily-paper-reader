---
title: "SPATIA: Multimodal Generation and Prediction of Spatial Cell Phenotypes"
title_zh: SPATIA：空间细胞表型的多模态生成与预测
authors: "Zhenglun Kong, Mufan Qiu, John Boesen, xiang lin, Sukwon Yun, Tianlong Chen, Manolis Kellis, Marinka Zitnik"
date: 2026-04-30
pdf: "https://openreview.net/pdf/6df30389ec5230663a3ec26c469b76e419fb5a42.pdf"
tags: ["query:cell-graph"]
score: 4.0
evidence: 多层级生成模型融合细胞形态、基因表达和空间上下文用于组织表征
tldr: 针对细胞形态、基因表达和空间上下文联合建模困难的问题，本文提出SPATIA，一种多层级生成与预测模型。该方法从细胞到组织层级融合多模态信息，学习空间感知的统一表征，并包含置信度感知的最优传输重加权和形态特征对齐。实验表明，SPATIA在空间细胞表型预测上表现良好，为细胞级组织表征提供了新思路。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 图像空间转录组学需要联合分析形态、基因表达和空间上下文。
method: 提出SPATIA模型，融合多模态信息学习空间感知表征，含生成框架和对齐机制。
result: 在空间细胞表型预测上取得良好效果，展示了多层级表征能力。
conclusion: SPATIA为细胞级空间组织建模提供方法，对组织病理表示学习有借鉴意义。
---

## Abstract
Understanding how cellular morphology, gene expression, and spatial context jointly shape tissue function is a central challenge in biology. Image-based spatial transcriptomics technologies now provide high-resolution measurements of cell images and gene expression profiles, but existing methods typically analyze these modalities in isolation or at limited resolution. 
We address the problem by introducing SPATIA, a multi-level generative and predictive model that learns unified, spatially aware representations by fusing morphology, gene expression, and spatial context from the cell to the tissue level. SPATIA also incorporates a spatially conditioned generative framework with confidence-aware OT reweighting and morphology-profile alignment for modeling target-state morphology distributions. Specifically, we propose a confidence-aware flow matching objective that reweights weak optimal-transport pairs based on uncertainty. We further apply morphology-profile alignment to encourage biologically meaningful image generation, enabling the modeling of microenvironment-dependent phenotypic transitions. We assembled a multi-scale dataset consisting of 25.9 million cell-gene pairs across 17 tissues. We benchmark SPATIA against 18 models across 12 tasks, spanning categories such as phenotype generation, annotation, clustering, gene imputation, and cross-modal prediction. SPATIA achieves improved performance over state-of-the-art models, improving generative fidelity by 8\% and predictive accuracy by up to 3\%.

---

## 论文详细总结（自动生成）

# SPATIA 论文结构化总结

> 说明：本总结基于用户提供的论文元数据与摘要。由于 PDF 正文仅返回验证页面，无法获取完整方法、公式、实验消融和算力细节；涉及无法确认的部分将明确标注。

## 1. 论文的核心问题与整体含义

- **研究背景**：图像空间转录组学可同时提供细胞图像与基因表达的高分辨率测量，为理解组织功能提供丰富数据。
- **核心问题**：细胞形态、基因表达和空间上下文如何联合决定组织功能；现有方法通常孤立分析这些模态，或仅在有限分辨率下建模，难以捕捉从细胞到组织级别的复杂关系。
- **整体含义**：提出 SPATIA，通过多层级生成与预测模型融合形态、基因表达和空间上下文，学习空间感知的统一表征，用于空间细胞表型生成与预测，有助于理解微环境依赖的表型转变。

## 2. 方法论

- **核心思想**：SPATIA 将细胞形态、基因表达和空间上下文从细胞级到组织级进行融合，学习统一、空间感知的表征。
- **关键技术细节**：
  - **空间条件生成框架**：建模目标状态下的形态分布。
  - **置信度感知最优传输重加权**：对弱最优传输对依据不确定性进行重加权，缓解不可靠匹配问题。
  - **置信度感知流匹配目标**：将重加权机制嵌入流匹配训练过程。
  - **形态-轮廓对齐**：鼓励生成图像具有生物学意义，支持微环境依赖的表型转变建模。
- **公式/算法流程**：摘要未给出具体数学表达式；文字流程可概括为：多模态输入 → 多层级融合/编码 → 空间条件生成 → 流匹配/最优传输优化 + 形态对齐 → 表型生成或预测。

## 3. 实验设计

- **数据集**：自建多尺度数据集，包含 **25.9 million 细胞-基因对**，来自 **17 种组织**。
- **Benchmark 任务**：共 **12 个任务**，覆盖：
  - 表型生成
  - 细胞注释
  - 聚类
  - 基因填补
  - 跨模态预测
- **对比方法**：与 **18 个模型**进行比较。
- **主要评价指标**：生成保真度、预测准确率；摘要报告生成保真度提升 8%，预测准确率最高提升 3%。

## 4. 资源与算力

- **未提及**：摘要和元数据中未提供 GPU 型号、GPU 数量、训练时长、显存占用或浮点运算量等信息。
- 因此无法评估该方法的算力需求、训练成本或可复现性资源门槛。

## 5. 实验数量与充分性

- 从摘要看，实验规模较大：1 个大规模数据集、17 种组织、12 类任务、18 个基线模型。
- 但缺少以下信息，难以判断实验是否充分、客观、公平：
  - 消融实验数量和具体设置；
  - 多次随机重复、统计显著性检验；
  - 跨数据集或跨平台验证；
  - 各基线是否使用相同数据划分和超参数调优。
- 因此，基于摘要只能认为任务覆盖范围较广，但实验完整性和公平性需以论文正文为准。

## 6. 论文的主要结论与发现

- SPATIA 在多个任务上优于现有先进模型。
- 生成保真度相对现有方法提高 **8%**，预测准确率最高提高 **3%**。
- 结果表明，融合形态、基因表达和空间上下文的多层级统一表征能够提升空间细胞表型建模能力。

## 7. 优点

- **多模态、多层级建模**：避免单一模态或单一分辨率的局限。
- **生成与预测统一**：既可用于表型生成，也可用于注释、聚类、填补和跨模态预测。
- **考虑不确定性**：置信度感知最优传输重加权和流匹配可能提升鲁棒性。
- **生物学可解释性导向**：形态-轮廓对齐鼓励生成结果符合生物学意义。
- **评估范围广**：大规模数据、多组织、多任务、多基线。

## 8. 不足与局限

- 论文正文不可用，许多关键细节（公式、算力、消融、实现细节）无法核实。
- 未说明计算资源，难以评估可扩展性和实际部署成本。
- 数据来源可能存在组织或平台偏差，未提及跨平台、跨批次泛化验证。
- 摘要未报告统计显著性和不确定性区间，结果稳健性未知。
- 缺少对模型可解释性、训练稳定性、失败案例的说明。
- 可能存在选择性报告：仅报告提升幅度，未给出绝对性能或误差范围。

（完）
