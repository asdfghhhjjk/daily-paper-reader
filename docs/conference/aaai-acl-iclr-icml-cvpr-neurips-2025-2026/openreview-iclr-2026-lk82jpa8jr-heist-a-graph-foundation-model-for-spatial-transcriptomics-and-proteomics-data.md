---
title: "HEIST: A Graph Foundation Model for Spatial Transcriptomics and Proteomics Data"
title_zh: HEIST：空间转录组学与蛋白质组学数据的图基础模型
authors: "Hiren Madhu, João Felipe Rocha, Tinglin Huang, Siddharth Viswanath, Smita Krishnaswamy, Rex Ying"
date: 2026-01-26
pdf: "https://openreview.net/pdf?id=lK82jpa8jr"
tags: ["query:immuno-topo"]
score: 4.0
evidence: 空间组学数据的图基础模型，用GNN建模空间拓扑
tldr: HEIST提出了一个针对空间转录组学和蛋白质组学数据的图基础模型，结合空间坐标和细胞内多组学信息，实现对细胞微环境的建模，可用于免疫微环境等分析。
source: ICLR-2026-Accepted
selection_source: conference_retrieval
motivation: 现有模型忽视空间信息或复杂的细胞内程序，难以充分表征组织微环境。
method: 构建图基础模型，整合空间坐标、转录组和蛋白质组数据进行单细胞水平建模。
result: 模型能学习到反映细胞状态和空间关系的嵌入表示。
conclusion: HEIST为空间多组学数据提供了一种统一的图基础模型，推进了组织生物学理解。
---

## Abstract
Single-cell transcriptomics and proteomics have become a great source for data-driven insights into biology, enabling the use of advanced deep learning methods to understand cellular heterogeneity and gene expression at the single-cell level. With the advent of spatial-omics data, we have the promise of characterizing cells within their tissue context as it provides both spatial coordinates and intra-cellular transcriptional or protein counts. Beyond transcriptomics, proteomics offers a complementary view by directly measuring proteins, which are the primary effectors of cellular function and key therapeutic targets. However, existing models either ignore the spatial information or the complex genetic and proteomic programs within cells. Thus they cannot infer how cell internal regulation adapts to microenvironmental cues. Furthermore, these models often utilize fixed gene vocabularies, hindering their generalizability to datasets with different genes than pretraining. In this paper, we introduce HEIST, a hierarchical graph transformer foundation model for spatial transcriptomics and proteomics. HEIST models tissues as hierarchical graphs. The higher level graph is a spatial cell graph, and each cell in turn, is represented by its lower level gene co-expression network graph. Rather than using a fixed gene vocabulary, HEIST computes gene embeddings from its co-expression network and cellular context. HEIST  achieves this by performing both intra-level and cross-level message passing to utilize the hierarchy in its embeddings and can thus generalize to novel datatypes including spatial proteomics without retraining. HEIST is pretrained on 22.3M cells from 124 tissues across 15 organs using spatially-aware contrastive and masked autoencoding objectives. Unsupervised analysis of HEIST embeddings reveals spatially informed subpopulations missed by prior models. Downstream evaluations demonstrate generalizability to proteomics data and state-of-the-art performance in clinical outcome prediction, cell type annotation, and gene imputation across multiple technologies.

---

## 论文详细总结（自动生成）

# HEIST：空间转录组学与蛋白质组学数据的图基础模型

## 1. 论文的核心问题与整体含义
- **研究背景**：单细胞转录组学与蛋白质组学能够以数据驱动的方式揭示细胞异质性和基因表达程序。空间组学数据（如空间转录组学、空间蛋白质组学）进一步提供了细胞在组织中的空间坐标，使得刻画细胞在组织微环境中的状态成为可能。
- **核心问题**：
  - 现有模型往往**忽略空间信息**，无法建模细胞如何响应微环境信号调整内部调控程序。
  - 或者模型使用**固定的基因词汇表**，难以泛化到预训练中未出现的新基因或模态（如蛋白质组学数据）。
  - 因此，需要一个能够同时编码空间上下文与细胞内多组学程序，并具备强泛化能力的统一基础模型。

## 2. 方法论
- **整体框架**：HEIST 是一个**分层图 Transformer 基础模型**，将组织建模为两级层次图。
- **层次图构建**：
  - **高层图（细胞级空间图）**：节点为细胞，边基于空间邻近关系构建，反映组织内细胞的物理排布。
  - **低层图（基因共表达网络图）**：每个细胞内部又建模为一个基因共表达网络，节点为基因，边代表共表达关系。
- **关键技术创新**：
  - **动态基因嵌入**：不使用固定基因词汇表，而是从基因共表达网络和细胞上下文信息中计算基因的表征，从而可泛化到未见的基因或蛋白质。
  - **层内与跨层消息传递**：设计消息传递机制，在细胞层和基因层内部及两层之间进行信息交互，充分利用层次结构融合空间与分子信息。
- **预训练任务**：
  - **空间感知对比学习**：拉近空间邻近细胞的嵌入，推远非邻近细胞，迫使模型学习空间上下文。
  - **掩码自编码**：掩蔽部分基因表达或蛋白质丰度信息，要求模型重建被掩蔽内容，学习细胞内调控模式。
- **泛化能力**：模型可通过对新的共表达图计算基因嵌入，直接应用于空间蛋白质组学等新型数据，无需重新训练。

## 3. 实验设计
- **预训练数据**：22.3M 个细胞，来自 15 个器官的 124 个组织，涵盖多技术、多模态的空间组学数据。
- **下游基准任务**：
  - 临床结果预测
  - 细胞类型注释
  - 基因（或蛋白质）插补
- **对比方法**：摘要中提及与 “prior models” 对比，未列出具体名称，但应涵盖主流空间组学分析方法与单细胞基础模型。
- **无监督分析**：直接对 HEIST 嵌入进行可视化与聚类，检验是否能够恢复空间定位的功能亚群。

## 4. 资源与算力
- **文中提及情况**：提供的摘要及元数据中**未明确说明**所使用的 GPU 型号、数量、训练时长或总计算量（如 petaFLOPs）。
- **推测**：考虑到预训练 22.3M 细胞的大规模图模型，训练通常需要数十或数百块高性能 GPU（如 A100）及数周时间，但这一点无法从当前信息得到证实。

## 5. 实验数量与充分性
- **实验规模**：从摘要描述看，下游实验覆盖了**三个不同性质的任务**（临床预测、细胞注释、基因插补）以及**跨技术、跨模态**（转录组学→蛋白质组学）的评估。
- **消融实验**：未在摘要中提及是否包含详细的组件消融（如去除层次图、去除对比学习目标等），但通常顶会论文会包含此类验证。
- **客观性与公平性**：采用标准公开数据集和预训练-微调范式，与现有方法在相同下游任务上比较，框架较为公平。无监督嵌入分析也提供了定性验证。总体来看，实验设计相对充分，但具体指标和统计检验细节需查阅正文。

## 6. 主要结论与发现
- HEIST 学习到的嵌入能够**捕获空间信息与细胞内调控程序**，无监督分析可揭示先前模型遗漏的空间定义亚群。
- 在下游任务上**达到了最先进的性能**，并展示了从转录组学到蛋白质组学的**零样本泛化能力**。
- 层次图设计和动态基因嵌入使得模型能够克服固定词汇表限制，为空间多组学提供了统一的基础模型。

## 7. 优点
- **层次化设计**：同时建模组织空间结构和细胞内分子网络，更完整地表征组织微环境。
- **泛化性**：摆脱固定基因集约束，可零样本应用于新基因、新模态（如蛋白质组学），实用性高。
- **预训练规模大**：基于千万级细胞预训练，为下游任务提供了强健的表示。
- **任务设置合理**：结合对比学习与掩码重建，多维度提取生物学语义。

## 8. 不足与局限
- **计算与数据需求**：层次图消息传递和千万级细胞预训练需要大量算力，可能限制部分研究者复现或扩展。
- **空间图构建依赖**：性能受空间坐标标定质量和细胞分割精度影响，若空间关系定义不准，模型可能失效。
- **跨模态泛化边界**：虽然可泛化至蛋白质组学，但未提及其他更复杂的成像质谱流式或代谢组学数据，泛化范围有待验证。
- **可解释性**：作为深层 Transformer，对内部表征的生物学解释仍有限，可能影响在临床决策中的可信度。
- **文献信息缺失**：本分析仅基于摘要，对具体对比方法、超参数、训练成本及失败案例等评价可能不完整。

（完）
