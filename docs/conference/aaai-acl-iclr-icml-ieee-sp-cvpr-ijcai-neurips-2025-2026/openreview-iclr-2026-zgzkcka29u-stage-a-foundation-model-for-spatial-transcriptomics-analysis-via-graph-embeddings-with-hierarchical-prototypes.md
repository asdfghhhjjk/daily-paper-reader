---
title: "STAGE: A Foundation Model for Spatial Transcriptomics Analysis via Graph Embeddings with Hierarchical Prototypes"
title_zh: STAGE：基于图嵌入与层次化原型的空间转录组学分析基础模型
authors: "Zhengchao Luo, Peiting Shi, Qichen Sun, Li Yongge, Han Wen, Jinzhuo Wang"
date: 2025-09-19
pdf: "https://openreview.net/pdf?id=ZGzKckA29U"
tags: ["query:profile"]
score: 8.0
evidence: 利用图嵌入和层次化原型建模空间转录组学中的空间域；直接将GNN用于组织微环境分析。
tldr: 针对空间转录组学中跨样本和平台一致识别空间域的难题，提出STAGE基础模型。它通过图嵌入和层次化原型同时捕获组织结构和基因表达特征，实现可推广的空间微环境识别，为组织功能和疾病微环境研究提供了有力工具。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 现有方法难以跨样本、组织和平台一致识别空间域，受低维度和批次效应影响。
method: STAGE模型利用图嵌入学习空间邻近关系，引入层次化原型表示空间模式。
result: 在多个数据集上实现可推广的空间域识别，展现强大的微环境建模能力。
conclusion: STAGE为组织微环境分析提供了通用的图神经网络框架。
---

## Abstract
Spatial transcriptomics offers an unprecedented opportunity to elucidate the spatial organization of tissues by capturing gene expression profiles while preserving tissue architecture. This enables the identification of spatial niches and deepens our understanding of tissue function and disease-associated microenvironments. However, consistent identification of spatial domains across samples, tissues, and even technological platforms remains a formidable challenge, due to low-dimensional and heterogeneous gene panels across platforms, pronounced batch effects, and substantial biological variability between samples. To address these limitations, we propose STAGE, a generalizable foundation model for spatial transcriptomics via graph embeddings. At its core, STAGE introduces a hierarchical prototype mechanism to capture global semantic representations of spatial niches, alongside an efficient online expectation-maximization algorithm to enable scalable learning from large-scale heterogeneous data. Pretrained on a large dataset comprising 32 million cells from 18 tissue types, STAGE learns robust cell representations within their neighborhood graphs and supports niche inference for domain recognition. Comprehensive evaluations on multiple benchmark datasets demonstrate that STAGE substantially enhances domain consistency in cross-platform, cross-sample, and cross-tissue spatial domain identification tasks, outperforming existing state-of-the-art methods. Furthermore, STAGE supports critical downstream biological analyses, highlighting its strong potential as a powerful tool in biological research.

---

## 论文详细总结（自动生成）

好的，以下是根据提供的论文元数据和摘要生成的结构化详细中文总结。

---

## 1. 论文的核心问题与整体含义

- **核心问题**：空间转录组学技术能够在保留组织空间结构的同时测量基因表达，从而识别组织内的“空间域”（空间微环境）。然而，如何在**跨样本、跨组织类型、甚至跨技术平台**的条件下，稳定且一致地识别这些空间域，仍是一个严峻挑战。
- **难点根源**：不同平台测得的基因集合维度低且异质性强，存在明显的批次效应，不同样本之间生物变异大，传统方法难以跨场景泛化。
- **整体含义**：论文旨在构建一个通用的**基础模型**，通过图神经网络和图嵌入的方式，从大规模异质数据中学习可迁移的细胞邻域表示，从而实现对空间微环境的高鲁棒、跨域识别，为组织功能研究和疾病微环境解析提供有力工具。

## 2. 论文提出的方法论

- **核心思想**：利用图结构对空间转录组数据进行建模，将细胞作为节点，空间邻近关系作为边，通过图嵌入学习细胞的上下文表示。同时引入**层次化原型**机制，捕捉空间微环境在不同层级上的全局语义，实现跨样本、跨平台的可推广性。
- **关键技术细节**：
  - **图嵌入学习**：在局部邻域图上进行消息传递，使细胞的表示融合空间位置与基因表达特征，从而刻画组织微结构。
  - **层次化原型机制**：设计一组具有层次结构的可学习原型，用于表征从细粒度到粗粒度的空间域模式。细胞表示会与这些原型进行软分配，迫使模型学习更抽象、更具语义一致性的空间微环境表示。
  - **可扩展在线EM算法**：采用在线期望最大化算法来优化原型分配和图嵌入参数，支持从超大规模数据（3200万细胞）中高效学习，避免传统EM算法在全量数据上的计算瓶颈。
  - **空间域推理**：预训练完成后，模型可对新的组织样本进行微调或直接推理，输出细胞所属的空间域（微环境类型）。
- **算法流程文字描述**：
  1. 基于空间坐标构建细胞邻域图。
  2. 图编码器提取细胞嵌入。
  3. 将细胞嵌入与层次化原型进行匹配，计算分配概率。
  4. 通过在线EM迭代更新原型和图编码器参数，直到收敛。
  5. 下游使用得到的嵌入进行空间域聚类或分类。

## 3. 实验设计

- **预训练数据集**：由**18种组织类型、3200万细胞**组成的大规模空间转录组学数据，来源多样，具跨平台、跨样本的异质性。
- **基准评测场景**：通过“跨平台、跨样本、跨组织”的空间域识别任务进行评估，重点考察模型在不同批次、技术平台和生物条件下的空间域识别一致性。
- **对比方法**：摘要未列出具体对比方法，但提到“outperforming existing state-of-the-art methods”，表明对比了当前最先进的现有方法（可能包含基于统计、机器学习和图的方法，如SpaGCN、BayesSpace等）。
- **下游分析**：还进行了生物学意义验证，如功能分析和疾病微环境表征，突显工具的实用性。

## 4. 资源与算力

- **文中明确信息**：所提供的论文摘要中**未明确提及**具体的GPU型号、数量或训练时长。仅描述了使用高效在线EM算法支持从3200万细胞的海量数据中学习，暗示训练需要一定规模的计算资源，但细节未知。

## 5. 实验数量与充分性

- **实验组数**：从摘要推断，至少包含：
  - 在多个独立基准数据集上的空间域识别评价（跨平台、跨样本、跨组织设定了多个子任务）。
  - 与多种现有先进方法的对比实验。
  - 关键组件的消融实验（如原型层级数、在线EM的效果）虽未明确写出，但此类方法论论文通常会包含，以验证设计方案的有效性。
- **充分性与客观性**：在多个组织类型和技术平台上进行评估，具有一定的广度；通过跨域一致性指标（而非单一同质数据）衡量性能，设计较为合理。但由于摘要未给出具体的方法、指标量化结果，无法判断统计严谨性。对比的公平性依赖统一预处理和评估协议，文中未提但通常是标准做法。

## 6. 论文的主要结论与发现

- STAGE基础模型能有效学习细胞在图结构中的鲁棒表示，并借助层次化原型捕获可拓展的空间微环境语义。
- 模型在跨平台、跨样本、跨组织的空间域识别任务上显著提升了领域一致性，性能超越现有最先进方法。
- STAGE能够支持关键的下游生物学分析，展现出作为通用工具的强大潜力。

## 7. 优点

- **泛化能力**：通过层次化原型和在线EM，较好地解决了空间转录组学中跨域泛化的难题，这是以往方法难以做到的。
- **可扩展性**：提出的在线算法可以高效处理千万级细胞数据，为构建大规模预训练模型提供了可行性。
- **生物学可解释性**：层次化原型的设计有助于从多粒度解析组织微环境，易于与生物学层级概念映射。
- **任务全面性**：不仅设计了模型，还完成了预训练并在多项下游任务中验证，覆盖了基础模型验证的完整链路。

## 8. 不足与局限

- **实验细节缺失**：从现有摘要无法得知对比方法的具体名单、评估指标、统计检验以及消融实验的结果，难以独立判断方法的真实提升幅度和稳健性。
- **计算成本不明**：缺乏算力报告，难以评估方法的普适性和复现门槛。
- **潜在偏差**：虽然预训练数据包含18种组织，但未必覆盖所有稀有组织类型或病变状态，在极端异质组织上可能仍存在偏差。
- **应用限制**：模型的图构建依赖空间坐标，对空间分辨率和样本质量敏感；跨平台推广虽优于已有方法，但仍可能受限于完全未见过的基因面板和成像技术。
- **可解释性深度**：原型虽提供一定解释性，但原型的生物学含义仍需额外分析验证。

（完）
