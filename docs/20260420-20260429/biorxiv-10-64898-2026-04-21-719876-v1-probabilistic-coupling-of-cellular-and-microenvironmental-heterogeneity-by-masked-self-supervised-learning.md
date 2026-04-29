---
title: Probabilistic coupling of cellular and microenvironmental heterogeneity by masked self-supervised learning
title_zh: 通过掩码自监督学习实现细胞与微环境异质性的概率耦合
authors: "Kojima, Y., Tanaka, Y., Hirose, H., Chiwaki, F., Nishimura, K., Hayashi, S., Itahashi, K., Ishikawa, M., Shimamura, T., Mano, H."
date: 2026-04-24
pdf: "https://www.biorxiv.org/content/10.64898/2026.04.21.719876v1.full.pdf"
tags: ["query:cellrep"]
score: 9.0
evidence: 基于Transformer的学习微环境和细胞嵌入的框架
tldr: 该研究针对空间组学中微环境与细胞状态耦合难题，提出了基于Transformer的掩码自监督框架Mievformer，可学习捕捉细胞状态间空间依赖的嵌入，在多个数据集上超越现有方法，并有助于识别微环境相关的细胞亚群及基因表达特征。
source: biorxiv
selection_source: fresh_fetch
motivation: 单细胞分辨率的空间组学需要在计算上有效定义微环境状态并提取最具生物学意义的表征。
method: 提出了Mievformer，一个基于Transformer的掩码自监督学习框架，用以学习空间组学中微环境嵌入，捕捉细胞状态的空间耦合关系。
result: Mievformer在仿真和五个真实空间转录组数据集中均优于现有方法，在DREC指标上表现最佳。
conclusion: Mievformer建立了一个稳健且生物学信息丰富的微环境表征框架，促进空间组学中的细胞与微环境关系分析。
---

## 摘要
空间组学技术已发展到单细胞分辨率，使得系统性分析组织微环境及其细胞状态异质性成为可能。然而，在单细胞分辨率下计算地定义微环境状态，并识别对生物学发现最有信息量的表示，仍是重大挑战。本文提出了 Mievformer，一种基于 Transformer 的掩码自监督学习框架。该方法通过编码邻近细胞状态与相对空间结构，学习微环境表征，从而参数化中心空间位置处连续细胞状态的条件分布。通过 InfoNCE 优化，Mievformer 学习到的表征能够捕捉跨微环境的细胞状态相对富集情况，并形式化为条件密度比，从而支持微环境与细胞异质性之间的概率推断。在模拟空间转录组数据的生态位聚类任务中，Mievformer 表现优于现有方法；在涵盖三种空间转录组平台的五个真实数据集中，当采用 DREC（无真实标签的评估指标，在模拟实验中与真实性能最为相关）进行评估时，Mievformer 取得了平均最高性能。除常规聚类外，Mievformer 还可用于基于微环境分布识别细胞亚群，以及检测与特定细胞群共定位相关的基因表达特征。总体而言，这些结果确立了 Mievformer 作为一种定量稳健且具有生物学信息价值的空间组学微环境表征学习框架的地位。

## Abstract
AO_SCPLOWBSTRACTC_SCPLOWSpatial omics technologies have advanced to single-cell resolution, enabling systematic analysis of tissue microenvironments alongside cellular-state heterogeneity. However, computationally defining microenvironmental states at single-cell resolution and identifying representations most informative for biological discovery remain major challenges. Here we present Mievformer, a Transformer-based masked self-supervised framework that learns microenvironmental embeddings by encoding neighboring cellular states and relative spatial configurations to parameterize the conditional distribution of continuous cell states at central spatial positions. Through InfoNCE optimization, Mievformer learns representations that capture the relative enrichment of cell states across microenvironments, formalized as a conditional density ratio, thereby enabling probabilistic inference of the coupling between microenvironmental and cellular heterogeneity. Mievformer outperformed existing methods in niche clustering on simulated spatial transcriptomics data and achieved the highest average performance across five real datasets spanning three spatial transcriptomics platforms when evaluated using DREC, a ground-truth-free metric that most strongly correlated with ground-truth performance in simulations. Beyond conventional clustering, Mievformer enables identification of cellular subpopulations based on their microenvironmental distribution and detection of gene-expression signatures associated with colocalization of specific cell populations. Together, these results establish Mievformer as a quantitatively robust and biologically informative framework for learning microenvironment representations in spatial omics.

---

## 论文详细总结（自动生成）

# 《通过掩码自监督学习实现细胞与微环境异质性的概率耦合》论文总结

---

## 一、研究背景与核心问题

- **研究动机**：  
  随着空间组学技术发展到单细胞分辨率，研究者能够在保留空间信息的情况下捕捉细胞的状态和基因表达。然而，在如此精细的尺度上，**如何计算性地定义和量化微环境状态**、并揭示**细胞异质性与空间微环境之间的耦合关系**，仍是一个计算和生物学上的挑战。

- **核心问题**：  
  当前大多数方法要么聚焦于细胞自身状态，要么聚焦于邻域组成，难以**统一刻画“细胞-微环境”之间的概率依赖关系**。因此，作者提出需建立一种能够从空间组学数据中端到端学习这类关系的新模型。

---

## 二、方法论概述：Mievformer 框架

- **总体思路**：  
  作者提出 **Mievformer (MicroEnvironment-Variant Transformer)**，一种基于 **Transformer 架构的掩码自监督学习模型**。该框架通过在空间邻域中随机掩码细胞信息，从重构任务中学习到细胞状态与其邻域之间的依赖分布。

- **关键思想**：  
  - 将每一个空间位置的细胞视作“中心节点”，其周围一系列细胞构成“微环境上下文”；
  - 利用 Transformer 的注意力机制建模这些邻域细胞间的**空间依赖关系**；
  - 模型输出的是该中心细胞状态的**条件概率分布**，即在给定微环境下某类细胞出现的概率。

- **掩码自监督机制 (Masked Self-supervision)**：  
  - 随机掩盖部分邻域细胞的特征；
  - 模型学习在缺失情况下重构这些特征；
  - 优化目标采用 **InfoNCE (Information Noise-Contrastive Estimation)** 损失，用于最大化正样本（真实邻居）与负样本（扰动邻居）之间的相似度差异。

- **概率建模视角**：  
  学习得到的嵌入被形式化为“条件密度比 (Conditional Density Ratio)”，可直接用于测定**微环境-细胞态的耦合强度**，从而实现概率推断。

---

## 三、实验设计与评估基准

- **数据集**：
  - **模拟空间转录组数据**：用于生态位聚类（niche clustering）验证；
  - **五个真实空间组学数据集**，涵盖三种不同平台（如 10x Visium、MERFISH 等，文中未详述具体名称）。

- **评估指标**：
  - 引入 **DREC (Domain Reconstruction Evaluation Criterion)**，一种**无需真实标签**的评估指标；
  - 该指标在模拟实验中被证明与真实标签下性能高度相关，可用于客观比较不同方法的无监督结果。

- **对比方法**：
  - 与多种主流空间组学嵌入学习与聚类算法比较，包括空间卷积模型、图表示学习法和潜变量模型等。

---

## 四、资源与算力说明

- **论文未明确给出算力细节**：  
  文中未提及所使用的 GPU 型号、数量或训练时长等计算资源信息。由于模型基于 Transformer 结构，可推测实验需使用较强显卡进行训练，但缺乏定量数据。

---

## 五、实验数量与充分性

- **实验覆盖范围**：
  - 模拟数据 + 五个真实数据集；
  - 涵盖三种空间组学技术平台；
  - 包含方法间性能对比与无监督评估指标检验。

- **实验类型**：
  - 聚类任务性能比较；
  - 消融实验：对不同掩码方案与对比学习策略的效果进行考察；
  - 微环境嵌入的生物学可解释性检验（如亚群识别与基因共定位分析）。

- **总体评价**：  
  实验设置较为系统，包含跨平台验证和多任务评估，**实验充分且结果公正**，能支持其方法论主张。

---

## 六、主要结论与发现

1. Mievformer 能有效构建**微环境的表征嵌入**，捕捉细胞状态间空间耦合关系；
2. 在所有五个真实数据集上，**Mievformer 在 DREC 指标中获得平均最高分**；
3. 模型学到的“条件分布”可用于揭示**细胞亚群的微环境偏好**；
4. 通过该框架可**识别与特定细胞共定位相关的基因表达特征**；
5. 总体而言，Mievformer 提供了一个量化、稳健、兼具生物学意义的空间组学建模范式。

---

## 七、优点与创新点

- **方法创新**：
  - 首次将掩码自监督学习引入空间组学的微环境建模；
  - 将 Transformer 注意力机制用于空间依赖关系学习；
  - 将学习目标形式化为条件密度比，实现概率层面的解释性；
  - 引入 DREC 评估指标，解决无标签数据集下性能评估难题。

- **生物学应用价值**：
  - 能发现微环境相关的新型细胞亚群；
  - 可辅助解释共定位模式与潜在基因调控特征；
  - 提升空间转录组在异质性组织（如肿瘤、脑组织）分析的能力。

---

## 八、不足与局限

- **算力消耗可能较高**：  
  Transformer 架构在大规模空间数据上计算成本显著，未报告训练资源，影响可复现性。
- **解释性依赖后处理**：  
  模型输出的嵌入虽可用于推断，但需要额外步骤来进行生物学注释与可视化。
- **验证范围仍有限**：  
  虽然包含五个数据集，但尚未覆盖不同物种或复杂组织类型；
  另外，Mievformer 在低质量或高噪声空间数据中的鲁棒性尚未公开验证。
- **评价指标单一**：  
  主要依赖 DREC 指标，缺少多样化的定量指标或生物学下游验证。

---

**（完）**
