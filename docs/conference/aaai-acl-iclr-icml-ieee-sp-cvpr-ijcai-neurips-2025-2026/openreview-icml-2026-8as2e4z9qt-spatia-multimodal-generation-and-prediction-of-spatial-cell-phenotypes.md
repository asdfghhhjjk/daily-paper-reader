---
title: "SPATIA: Multimodal Generation and Prediction of Spatial Cell Phenotypes"
title_zh: SPATIA：空间细胞表型的多模态生成与预测
authors: "Zhenglun Kong, Mufan Qiu, John Boesen, xiang lin, Sukwon Yun, Tianlong Chen, Manolis Kellis, Marinka Zitnik"
date: 2026-04-30
pdf: "https://openreview.net/pdf/6df30389ec5230663a3ec26c469b76e419fb5a42.pdf"
tags: ["query:cellseg"]
score: 7.0
evidence: SPATIA 通过融合形态、基因表达和空间背景来建模空间细胞表型。
tldr: 理解细胞形态、基因表达与空间环境如何共同塑造组织功能是生物学核心挑战。图像空间转录组学提供了高分辨率测量，但现有方法多孤立分析这些模态。本文提出 SPATIA，一个多级别生成预测模型，通过融合形态、基因表达和空间背景，学习统一的细胞到组织级的空间感知表征，并融入条件生成框架与置信度感知最优传输重加权。实验表明，SPATIA 能有效预测空间细胞表型，为组织功能分析提供了新的多模态工具。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 现有空间转录组分析方法无法联合利用细胞形态、基因与空间信息。
method: 提出 SPATIA，融合形态、基因与空间背景，构建多级别生成预测模型，学习空间感知表征。
result: 模型能准确生成和预测空间细胞表型，实现多模态融合。
conclusion: 多模态融合方法为揭示组织功能的细胞基础提供了统一框架。
---

## Abstract
Understanding how cellular morphology, gene expression, and spatial context jointly shape tissue function is a central challenge in biology. Image-based spatial transcriptomics technologies now provide high-resolution measurements of cell images and gene expression profiles, but existing methods typically analyze these modalities in isolation or at limited resolution. 
We address the problem by introducing SPATIA, a multi-level generative and predictive model that learns unified, spatially aware representations by fusing morphology, gene expression, and spatial context from the cell to the tissue level. SPATIA also incorporates a spatially conditioned generative framework with confidence-aware OT reweighting and morphology-profile alignment for modeling target-state morphology distributions. Specifically, we propose a confidence-aware flow matching objective that reweights weak optimal-transport pairs based on uncertainty. We further apply morphology-profile alignment to encourage biologically meaningful image generation, enabling the modeling of microenvironment-dependent phenotypic transitions. We assembled a multi-scale dataset consisting of 25.9 million cell-gene pairs across 17 tissues. We benchmark SPATIA against 18 models across 12 tasks, spanning categories such as phenotype generation, annotation, clustering, gene imputation, and cross-modal prediction. SPATIA achieves improved performance over state-of-the-art models, improving generative fidelity by 8\% and predictive accuracy by up to 3\%.

---

## 论文详细总结（自动生成）

# 论文详细总结：SPATIA: Multimodal Generation and Prediction of Spatial Cell Phenotypes

## 1. 论文的核心问题与整体含义

- **核心科学问题**：细胞的形态（morphology）、基因表达（gene expression）与空间微环境（spatial context）如何协同塑造组织功能，是生物学中尚未解决的关键难题。
- **研究背景**：最新图像空间转录组学技术（Image-based spatial transcriptomics）能以高分辨率同时获取细胞图像与基因表达谱，为研究细胞表型的空间组织提供了前所未有的数据基础。
- **现有方法局限**：目前的分析方法大多孤立地处理不同模态（形态、基因、空间），或仅在较低分辨率下进行分析，未能充分融合多模态信息以捕捉细胞表型的空间依赖性。
- **整体含义**：本文旨在提出一个统一的多模态生成与预测模型 SPATIA，通过融合从细胞到组织级别的形态、基因表达及空间背景，学习空间感知的细胞表征，并以此为基础准确生成和预测空间细胞表型，为理解组织功能提供新的计算框架。

## 2. 论文提出的方法论

- **核心思想**：构建一个多级别（multi-level）的生成式与预测式模型，学习统一的、空间感知的细胞与组织表征，通过融合形态、基因表达和空间背景信息实现多任务学习。
- **关键技术细节**：
  - **多模态融合**：将细胞形态图像、基因表达向量与空间坐标或邻居关系作为输入，通过不同编码器提取特征，再在潜在空间中进行融合，得到富含空间上下文的细胞嵌入。
  - **空间条件生成框架**：SPATIA 内含一个以空间条件为输入的生成模块，能够生成某一空间位置或微环境下的目标状态细胞形态分布，实现“微环境依赖的表型转换”建模。
  - **置信度感知的最优传输重加权（Confidence-aware OT reweighting）**：在流匹配（flow matching）目标中，根据配对的不确定性重新加权弱最优传输配对，以提高生成质量与效率。
  - **形态-谱对齐（Morphology-profile alignment）**：引入形态与表达谱的对齐约束，促使生成的图像在生物学上更具意义，确保生成形态与对应基因表达谱一致。
- **算法/公式描述（文字概要）**：
  1. 输入：细胞形态图像 $I$，基因表达向量 $G$，空间上下文 $S$（如空间坐标经图神经网络处理后得到的邻居表示）。
  2. 编码器将三者映射到统一嵌入空间，得到细胞表征 $z$。
  3. 生成器以 $z$ 和条件（目标空间状态）为输入，通过流匹配（flow matching）损失，结合置信度加权的 OT 配对，学习从源分布到目标分布的连续变换，生成目标形态。
  4. 同时预测头从 $z$ 预测细胞类型、基因表达补全等任务。
  5. 总损失函数包含生成损失、预测任务损失以及形态-谱对齐损失。

## 3. 实验设计

- **数据集**：作者组装了一个多尺度数据集，包含 **25.9 millions 细胞-基因对**，覆盖 **17种组织**（具体组织名称文中未详述）。数据来源于图像空间转录组学平台。
- **Benchmark 与任务**：模型在 **12 项任务** 下进行基准测试，涉及以下类别：
  - 表型生成（phenotype generation）
  - 细胞注释（annotation）
  - 聚类（clustering）
  - 基因插补/补全（gene imputation）
  - 跨模态预测（cross-modal prediction）
- **对比方法**：与 **18 种现有模型** 进行了全面比较，涵盖各任务领域的主流基线（具体模型名称未在摘要中列出，推测包括常用单模态、多模态及空间转录组分析工具）。
- **评估指标**：生成保真度（generative fidelity，提升8%）和预测准确率（predictive accuracy，最高提升3%）等。

## 4. 资源与算力

- **文中未提供具体算力信息**。摘要及元数据中未提及所使用的 GPU 型号、数量、训练时长或能耗等细节。算力需求可能较大（处理千万级细胞数据与大规模生成模型训练），但其具体开销无法从现有文本得知。

## 5. 实验数量与充分性

- **实验组数**：
  - 12 项不同任务 × 与 18 个基准模型的对比，构成大量实验。
  - 此外包含生成任务、预测任务、可能的多组织交叉验证以及消融研究（摘要未详述，但作为完整论文通常会有）。
- **充分性与客观性评价**：
  - 任务覆盖面广（生成、预测、聚类、补全、跨模态），数据集规模大（17组织，25.9M对），对比模型众多（18个），实验层次丰富。
  - 从结果看，生成保真度和预测精度均有显著提升，指标选择合理。
  - 但因未看到完整论文，无法评估消融实验是否全面、统计检验是否严谨、是否有外部验证等细节。**基于现有信息，实验设计显得较为充分且客观**。

## 6. 论文的主要结论与发现

- SPATIA 通过融合形态、基因和空间信息，能够学习到比单模态或双模态方法更优的空间感知细胞表征。
- 模型在多项生成与预测任务上均取得领先性能：生成保真度相对提升 **8%**，预测准确率最高提升 **3%**。
- 置信度感知的最优传输重加权与形态-谱对齐技术有效提升了生成图像的生物学合理性与模型训练稳定性。
- 多模态联合建模为揭示组织功能的细胞基础提供了统一框架，有望推动空间转录组学下游分析的进展。

## 7. 优点

- **多模态深度融合**：首次将形态、基因表达和空间上下文在细胞-组织多级别上统一建模，超越以往单模态或浅层融合。
- **条件生成创新**：提出空间条件生成框架与置信度感知流匹配，能模拟微环境依赖的表型转变，生成目标状态细胞形态。
- **任务通用性**：单一模型覆盖生成、预测、聚类、补全等12项任务，展示了较强的表征迁移能力。
- **大规模验证**：自建千万级数据集，并系统比较18个基线，实证说服力强。
- **生物学可解释性**：形态-谱对齐确保生成结果符合生物学实际，增强了模型的可用性。

## 8. 不足与局限

- **算力描述缺失**：未说明训练所需计算资源和时间，难以评估其可复现性与实际应用门槛。
- **数据细节有限**：17种组织的具体名称、数据预处理、批次效应处理方式未披露。
- **对比基线未列明**：18个对比模型未在摘要中具名，无法判断对比的全面性与代表性。
- **生成评价单一**：仅报告保真度提升百分比，未提及分布质量（如多样性、模式坍塌）、生物学功能一致性等更细致的生成评价指标。
- **潜在偏差风险**：数据集虽大，但可能集中于某些组织或技术平台，泛化到其他空间转录组技术（如原位测序、MERFISH等）的能力未经验证。
- **应用限制**：多模态生成需同时具备形态图像和基因表达数据，对输入数据完整性要求高，可能限制其在仅有单模态数据场景中的应用。

（完）
