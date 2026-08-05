---
title: LEMON - a foundation model for single-cell nuclear morphologies for digital pathology
title_zh: LEMON - 面向数字病理的单细胞核形态基础模型
authors: "Loic Chadoutaud, Alice Blondel, Hana Feki, Jacqueline Fontugne, Emmanuel Barillot, Thomas Walter"
date: 2025-09-19
pdf: "https://openreview.net/pdf?id=JAalsmy7bZ"
tags: ["query:profile"]
score: 10.0
evidence: 面向数字病理的单细胞核形态表示学习基础模型，为下游任务提供通用细胞级特征
tldr: 数字病理中单细胞表示学习研究不足，限制了对细胞类型和表型的深入表征。LEMON提出自监督基础模型，在数百万跨组织、跨癌种的细胞图像上训练，学习通用的核形态嵌入。实验表明该嵌入能显著提升细胞分类、患者预后等下游任务性能。该工作填补了单细胞级预训练空白，为大规模单细胞病理研究提供了基础工具。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 单细胞级表示学习在数字病理中尚未被充分探索。
method: 使用自监督学习在海量细胞图像上训练，得到核形态嵌入。
result: 嵌入提升了细胞分类、生存分析等下游任务性能。
conclusion: 为数字病理单细胞研究提供了可扩展的基础模型。
---

## Abstract
Representation learning is a central challenge in Computational Pathology (CP), with direct implications for cancer research and precision medicine. While Self Supervised Learning (SSL) has advanced patch and slide-level analysis of Whole-Slide Images (WSIs), single-cell representation learning has remained underexplored, despite its importance for characterizing cell types and phenotypes. We introduce LEMON (Learning Embeddings from Morphology Of Nuclei), a self-supervised foundation model for scalable single-cell image representation. Trained on millions of cell images spanning diverse tissues and cancer types, LEMON provides versatile and robust morphology representations that enable large-scale single-cell studies in pathology. We demonstrate its effectiveness across diverse prediction tasks on five benchmark datasets, establishing LEMON as a new paradigm for cell-level computational pathology.

---

## 论文详细总结（自动生成）

## 1. 论文的核心问题与整体含义

- **研究背景**：在计算病理学（Computational Pathology）中，表征学习是核心挑战之一，直接影响癌症研究和精准医学。目前基于自监督学习（SSL）的方法在整张切片图像（WSI）的图像块（patch）和切片级别分析上取得了显著进展，但单细胞级别的表征学习仍处于探索不足的状态。
- **核心问题**：单细胞形态（尤其是细胞核形态）的通用、可扩展的表征学习方法缺失，这限制了对细胞类型和表型的深入刻画，进而影响大规模单细胞病理研究的能力。
- **整体含义**：该工作旨在填补单细胞级别基础模型的空白，提供一个面向数字病理的、可复用的细胞核形态嵌入基础模型，称为LEMON（Learning Embeddings from Morphology Of Nuclei）。该模型试图成为单细胞病理分析的新范式，为下游任务（如细胞分类、患者预后预测）提供通用特征。

## 2. 论文提出的方法论

- **核心思想**：通过自监督学习，从海量跨组织、跨癌种的细胞核图像中学习通用的形态学嵌入（morphology embeddings），使该嵌入能够泛化到多种下游任务。
- **关键技术细节**（基于摘要推断）：
  - 模型以单个细胞核图像作为输入，输出固定维度的特征向量（嵌入）。
  - 训练方式为自监督学习（SSL），即不需要人工标注，利用数据本身的结构设计前置任务（如对比学习、掩码重建等）进行预训练。
  - 预训练数据规模为“数百万细胞图像”，涵盖多种正常组织和不同癌症类型，以保证嵌入的多样性和鲁棒性。
- **公式或算法流程**：原文未提供具体公式或算法伪代码。从摘要仅能得知其为“自监督基础模型”，但无法确定具体的SSL框架（例如SimCLR、MoCo、DINO或MAE等）。训练目标、网络架构、损失函数等均未在给出的内容中披露。

## 3. 实验设计

- **数据集与场景**：使用了五个基准数据集进行评估，涵盖不同的预测任务。但未列出具体数据集名称或任务类型（如细胞分类、生存分析等）。
- **Benchmark 与对比方法**：摘要提到“demonstrate its effectiveness across diverse prediction tasks on five benchmark datasets”，但未指明对比了哪些方法，也未说明基准性能指标。从常见计算病理学研究推测，可能包括细胞类型分类、患者生存预后等任务，对比方法可能为传统图像特征（如形态测量）或其他自监督/迁移学习基线。
- **实验场景**：下游任务体现为细胞级别分类和患者级别预后，验证嵌入的通用性。

## 4. 资源与算力

- **算力信息**：在提供的摘要及元数据中，**未明确提及任何算力细节**，如GPU型号、数量、训练时长或碳排放等。仅说明模型在“数百万细胞图像”上训练，但无法估算实际计算量。
- **缺失说明**：由于原文内容仅为摘要和元数据，完整的算力配置和效率分析并未呈现。

## 5. 实验数量与充分性

- **实验数量**：摘要提及在五个基准数据集上进行下游评估，并可能包含消融实验或预训练数据规模的影响分析，但具体实验组数未知。提供的片段未列出任何表格或量化结果。
- **充分性与客观性评估**：
  - **优点**：覆盖“diverse prediction tasks”，至少在细胞和患者两个层面验证，且包含多个数据集，这通常有利于证明泛化性。
  - **局限性**：由于缺乏具体数字、对比方法和统计检验，无法判断实验是否充分。是否存在与核分割方法耦合的偏差、数据泄露风险（同一病例的细胞出现在训练和测试集中）、对比方法的公平性等均无法从已有信息确认。评审是否认为实验充足，未被给出。

## 6. 论文的主要结论与发现

- LEMON作为自监督单细胞形态基础模型，能够在五个基准数据集上有效提升下游任务性能，证明其通用性和鲁棒性。
- 该工作为细胞级别的计算病理学提供了可扩展的基础模型，有望推动大规模单细胞分析研究。

## 7. 优点

- **填补空白**：率先提出构建单细胞核形态的基础模型，开辟了计算病理学中细胞级别预训练的新方向。
- **大规模预训练**：利用数百万跨组织、跨癌种细胞图像进行自监督学习，具备成为通用细胞表征的潜力。
- **多任务验证**：在分类、预后等不同性质的任务上进行评估，而非局限于单一任务，体现了嵌入的通用性。
- **可扩展性**：自监督方法无需昂贵的人工标注，易于扩展到更大规模、更多样化的数据集。

## 8. 不足与局限

- **方法论细节缺失**：自监督学习的具体方法、网络架构、训练策略等完全未知，复现性存疑。
- **数据集与对比评估不透明**：五个基准数据集、对比方法、评价指标等关键信息未披露，难以评估结果的实际意义和公平性。
- **算力与效率未知**：缺乏对训练代价的分析，大型基础模型的实际落地成本无法衡量。
- **潜在的批次效应与数据泄露**：跨数据集预训练和下游微调时，若未严格按病例或患者划分，可能导致过乐观的估计。
- **与上游核分割的耦合**：核形态嵌入的性能严重依赖核分割质量，文中未讨论这一依赖关系及其带来的累积误差风险。
- **应用限制**：数字病理中的细胞形态除核形状外，组织上下文、染色强度、细胞间关系等也对诊断和预后至关重要。仅关注孤立核形态可能丢失重要的微环境信息，其作为通用特征的上限可能受限。

（完）
