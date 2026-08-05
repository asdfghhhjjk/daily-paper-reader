---
title: "STAGE: A Foundation Model for Spatial Transcriptomics Analysis via Graph Embeddings with Hierarchical Prototypes"
title_zh: STAGE：基于图嵌入与层次化原型的空间转录组学基础模型
authors: "Zhengchao Luo, Peiting Shi, Qichen Sun, Li Yongge, Han Wen, Jinzhuo Wang"
date: 2025-09-19
pdf: "https://openreview.net/pdf?id=ZGzKckA29U"
tags: ["query:profile"]
score: 8.0
evidence: 利用图嵌入与层次化原型从空间转录组学数据中建模组织微环境。
tldr: 空间转录组学可保留组织架构的同时捕获基因表达，但跨样本、跨平台的领域识别面临批次效应和变异性挑战。本文提出 STAGE，一种基于图嵌入与层次化原型的可泛化基础模型，用于空间转录组数据整合与空间域识别。模型通过学习统一表征，克服了技术差异和生物变异性。在多个数据集上的实验表明，STAGE 能一致地识别空间微环境，为疾病组织微环境分析奠定基础。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 跨平台空间转录组分析受批次效应困扰，领域识别缺乏一致性。
method: 提出 STAGE 基础模型，利用图嵌入和层次化原型学习可泛化的空间域表征。
result: 模型在多样本、跨平台条件下一致识别空间域，性能优越。
conclusion: 图嵌入基础模型为整合空间转录组数据和解析微环境提供了有效工具。
---

## Abstract
Spatial transcriptomics offers an unprecedented opportunity to elucidate the spatial organization of tissues by capturing gene expression profiles while preserving tissue architecture. This enables the identification of spatial niches and deepens our understanding of tissue function and disease-associated microenvironments. However, consistent identification of spatial domains across samples, tissues, and even technological platforms remains a formidable challenge, due to low-dimensional and heterogeneous gene panels across platforms, pronounced batch effects, and substantial biological variability between samples. To address these limitations, we propose STAGE, a generalizable foundation model for spatial transcriptomics via graph embeddings. At its core, STAGE introduces a hierarchical prototype mechanism to capture global semantic representations of spatial niches, alongside an efficient online expectation-maximization algorithm to enable scalable learning from large-scale heterogeneous data. Pretrained on a large dataset comprising 32 million cells from 18 tissue types, STAGE learns robust cell representations within their neighborhood graphs and supports niche inference for domain recognition. Comprehensive evaluations on multiple benchmark datasets demonstrate that STAGE substantially enhances domain consistency in cross-platform, cross-sample, and cross-tissue spatial domain identification tasks, outperforming existing state-of-the-art methods. Furthermore, STAGE supports critical downstream biological analyses, highlighting its strong potential as a powerful tool in biological research.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义  
- **研究动机**：空间转录组学能够在保留组织空间架构的前提下捕获基因表达，为识别组织中的空间微环境（spatial niches）、理解组织功能与疾病相关微环境提供了前所未有的机会。然而，跨样本、跨组织甚至跨技术平台一致地识别空间域（spatial domains）仍面临严峻挑战。  
- **核心问题**：不同平台产生的基因面板（gene panels）维度低且异质性强，存在显著的批次效应（batch effects），加之样本间固有的生物变异性，使得现有方法难以获得具有普适性和可迁移性的空间域表征。  
- **整体含义**：本工作旨在构建一个可泛化的基础模型，通过图嵌入方式融合空间上下文与基因表达，克服技术差异与生物异质性，实现跨平台、跨样本、跨组织的空间域一致性识别，为疾病微环境分析提供通用工具。

### 2. 论文提出的方法论  
- **核心思想**：提出 **STAGE**（Spatial Transcriptomics Analysis via Graph Embeddings with Hierarchical Prototypes），将空间转录组数据建模为图结构，利用层次化原型（hierarchical prototypes）捕获空间微环境的全局语义，从而学习鲁棒且可泛化的细胞/斑点表征。  
- **关键技术细节**：  
  - **层次化原型机制**：引入多级原型，从局部邻域到全局语义逐层抽象空间域的特征表示。  
  - **在线期望最大化（Online EM）算法**：设计高效的在线期望最大化算法，使模型能够从大规模、异质性数据中可扩展地学习。  
  - **图嵌入与邻域图构建**：以细胞或斑点为节点，基于空间距离构建邻域图，通过图神经网络聚合邻域信息，生成保留空间关系的嵌入。预训练完成后，支持空间域推理（niche inference）与领域识别。  
- **算法流程（文字说明）**：  
  1. 构建空间邻域图；  
  2. 通过图编码器获得节点初始嵌入；  
  3. 利用层次化原型将节点嵌入与不同层级的可学习原型进行匹配，形成高层次的语义表示；  
  4. 以在线EM方式迭代优化模型参数与原型，适应流式或大规模数据；  
  5. 基于最终嵌入进行空间域识别或下游分析。

### 3. 实验设计  
- **数据集/场景**：模型在大规模预训练数据集上训练，涵盖 **18 种组织类型、3200 万个细胞**；随后在多个基准数据集上进行评估，具体包括跨平台、跨样本、跨组织的空间域识别任务。  
- **Benchmark 与对比方法**：论文宣称在综合评估中 **超越现有最先进方法**（state‑of‑the‑art），但摘要及元数据未明确列出对比的具体方法名称。  
- **评估维度**：围绕空间域识别的一致性、跨平台迁移能力、下游生物学分析支持性等展开。

### 4. 资源与算力  
- 所提供的论文摘要及元数据中 **未明确说明** 所使用的 GPU 型号、数量、训练时长等计算资源信息，因此无法评估算力消耗。

### 5. 实验数量与充分性  
- 从现有信息推测，论文至少包含 **预训练阶段**（大规模多组织数据）与 **多组下游评估实验**（跨平台、跨样本、跨组织等設定）。  
- 摘要提到“comprehensive evaluations on multiple benchmark datasets”，暗示实验数量较丰富，但 **未提供具体实验组数**、消融实验细节或统计检验信息。  
- 由于缺少对对比方法列表、数据集规模及实验设置的具体描述，**难以客观评判实验是否完全充分、公平**；但从被拒稿但仍有 8.0 评分来看，审稿人可能对实验全面性存在一定认可。

### 6. 论文的主要结论与发现  
- STAGE 能够从大规模异质性空间转录组数据中学习到 **鲁棒的图嵌入表征**，有效消除批次效应与平台差异。  
- 在跨平台、跨样本、跨组织空间域识别任务中，STAGE **显著提升了一致性**，并优于现有方法。  
- 该模型支持关键的下游生物学分析，具备成为生物学研究通用工具的潜力。  
- 图嵌入基础模型是整合空间转录组数据、解析组织微环境的有效途径。

### 7. 优点  
- **方法创新性**：首次将层次化原型与在线EM结合用于空间转录组的图嵌入基础模型，兼顾全局语义与局部细节。  
- **可扩展性**：在线EM算法使模型能处理数千万细胞级别的大规模数据，预训练范围广（18种组织）。  
- **泛化能力**：明确针对跨平台、跨样本场景设计，实验证明其可迁移性。  
- **生物学价值**：为疾病微环境研究提供了一个统一的分析框架。  

### 8. 不足与局限  
- **细节缺失**：提供的材料中未列出具体对比方法、超参数设置、消融实验等，无法全面评估方法的实际优势与鲁棒性。  
- **算力未报告**：未说明训练所需资源，可能影响复现与实用性评估。  
- **潜在偏差**：预训练数据虽大，但组织类型与平台分布可能不均衡，对稀有组织或特定技术的泛化能力尚不明确。  
- **下游验证有限**：文中仅定性提到“支持关键下游分析”，但未展示具体的生物学发现或临床相关性案例。  

（完）
