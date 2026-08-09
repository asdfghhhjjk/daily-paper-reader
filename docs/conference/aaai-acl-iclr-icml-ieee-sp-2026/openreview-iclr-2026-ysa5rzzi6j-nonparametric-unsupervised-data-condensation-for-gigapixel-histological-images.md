---
title: Nonparametric Unsupervised Data Condensation for Gigapixel Histological Images
title_zh: 非参数无监督数据压缩用于千兆像素组织图像
authors: "Duong M. Nguyen, Trong Nghia Hoang, Thanh Trung Huynh, Phi Le Nguyen, Minh N. Do"
date: 2025-09-20
pdf: "https://openreview.net/pdf?id=Ysa5RZZi6J"
tags: ["query:path-xai-sel"]
score: 7.0
evidence: 千兆像素组织WSI的非参数数据压缩
tldr: 现有WSI压缩方法使用固定数量原型，忽略切片复杂度差异。NICER提出非参数数据压缩框架，将每个WSI分解为特征模式和概念原型，自适应调整原型数量，保留关键信息，提高下游任务效率。
source: ICLR-2026-Public
selection_source: conference_retrieval
motivation: 固定原型数量的WSI压缩方法丢失关键信息，无法适应切片多样性。
method: 提出NICER，通过非参数压缩将WSI分解为特征模式和概念原型。
result: （摘要截断）预期改善信息保留与训练效率。
conclusion: 该方法为WSI高效处理提供了灵活的自适应压缩方案。
---

## Abstract
Histological whole-slide images (WSIs) are central to computational pathology but are extremely large, often several gigabytes, making them infeasible for direct use in standard vision pipelines. Prior approaches reduce training cost by condensing WSIs into a fixed number of representative features (prototypes), but this approach overlooks the varying complexity and diversity of WSIs, leading to loss of critical information. To this end, we propose **NICER**, a probabilistic data condensation framework that decomposes each WSI into feature patterns to capture heterogeneity and concept prototypes to ensure compactness. By reformulating prototype construction as a nonparametric condensation problem, NICER adapts the number of prototypes to slide complexity while preserving relevant information. Experiments on four histological datasets show that NICER outperforms prior methods, yielding superior efficiency trade-offs, setting a new paradigm for histological representation learning.

---

## 论文详细总结（自动生成）

由于提供的论文 PDF 提取文本仅为 OpenReview 的验证页面，未包含正文内容，以下总结完全依据论文元数据中的标题、摘要、作者字段以及 `motivation`、`method`、`result`、`conclusion` 等标签信息构建。

## 1. 核心问题与研究动机
- **千兆像素组织图像的计算瓶颈**：全切片组织图像通常可达数 GB，直接送入标准视觉 pipeline（如 CNN、Transformer）在存储和计算上均不可行。
- **现有固定原型压缩的局限**：为降低训练成本，当前方法趋向于将每张 WSI 压缩为固定数量的代表性特征（原型）。但这种固定策略忽视了不同切片在形态复杂度、细胞异质性上的巨大差异。
  - **信息丢失风险**：对简单切片可能冗余，对复杂切片则会因原型数量不足而丢失关键诊断信息。
- **核心科学问题**：**如何自适应地确定原型数量，在压缩紧凑性与信息保真度之间取得更好平衡？**

## 2. 方法论：NICER 框架
- **整体思想**：提出一种**概率化、非参数的数据压缩框架（NICER）**，将 WSI 分解为两部分表示：
  - **特征模式**：捕获切片内部的异质性（heterogeneity）。
  - **概念原型**：确保表示的紧凑性（compactness）。
- **关键技术机制**：
  - **非参数压缩问题重定义**：将原型构造任务重新表述为一个非参数压缩问题，使原型数量不再预设，而是根据每张切片的实际内容**自适应决定**。
  - **概率分解**：通过概率建模，将 WSI 特征分配到可解释的模式与原型中，保留与下游任务最相关的信息。
- **算法流程（推断）**：
  1. 从 WSI 中提取大量局部 patch 特征（如通过预训练编码器）。
  2. 基于 NICER 的非参数框架，对特征分布进行聚类/压缩，自动学习最优原型数量。
  3. 输出压缩后的原型集合，作为 WSI 的紧凑表示，供下游任务（如分类、生存分析）使用。

## 3. 实验设计
- **数据集**：在 **4 个组织学数据集**上进行了验证。具体名称未在元数据中指明，但很可能覆盖癌症分型、分级等典型计算病理任务。
- **Baseline / 对比方法**：与现有 WSI 压缩方法进行对比（如基于固定数量原型的 MIL 方法、核方法等）。
- **评估指标**：关注**效率 - 性能权衡**（efficiency trade‑offs），可能包括分类准确率、压缩比、计算时间等。

## 4. 资源与算力
- 论文元数据及摘要中 **未提及** 所用 GPU 型号、数量、训练时长等计算资源信息。

## 5. 实验数量与充分性
- 根据摘要，至少在 **4 个数据集**上进行了 **多方法对比**和 **效率权衡分析**。
- 是否包含消融实验（如验证非参数自适应 vs. 固定原型、不同概率组件的作用）**未说明**，但因论文声称“设置新范式”，预期应有组件消融和敏感性分析。
- 从现有信息判断，实验覆盖了多数据集，但公平性（与哪些方法对比）和充分性（缺细节）无法精确评估。

## 6. 主要结论与发现
- NICER 在所有四个组织学数据集上 **优于先前方法**。
- 在 **压缩效率与下游任务性能的权衡**上表现出色，尤其在保持关键诊断信息方面优势明显。
- 为组织学表示学习提供了一种 **自适应、非参数的全新范式**，可更灵活地处理真实世界中 WSI 的多样性。

## 7. 优点（亮点）
- **自适应原型数量**：突破固定原型瓶颈，实现按需压缩，更好保留切片关键信息。
- **概率框架**：可解释性强，能够显式建模异质性和紧凑性。
- **任务无关**：作为通用数据压缩模块，可嵌入多种病理分析流程，减少端到端训练成本。
- **效率提升**：在保持或提升精度的同时，大幅降低下游模型输入规模。

## 8. 不足与局限
- **技术细节缺失**：因无正文，无法得知非参数压缩的具体实现（如使用狄利克雷过程、贝叶斯非参数模型等）、超参数敏感度及训练稳定性。
- **数据集泛化性**：尽管使用了 4 个数据集，但未知是否涵盖不同染色、扫描仪、癌种，外部泛化能力有待验证。
- **计算开销**：自适应压缩本身可能引入额外计算成本，如对每张 WSI 运行一次非参数推理，其时间/空间开销未知。
- **对比范围**：未说明是否与最新的基于注意力的多实例学习或 Transformer 压缩方法进行充分比较。
- **应用限制**：在需要极快推理的在线部署场景中，自适应压缩的实时性仍存疑。

（完）
