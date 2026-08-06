---
title: "HistoPrism: Unlocking Functional Pathway Analysis from Pan-Cancer Histology via Gene Expression Prediction"
title_zh: HistoPrism：通过基因表达预测从泛癌组织学中解锁功能通路分析
authors: "Susu Hu, Qinghe Zeng, Nithya Bhasker, Jakob Nikolas Kather, Stefanie Speidel"
date: 2026-01-26
pdf: "https://openreview.net/pdf?id=6dTHxb9JuA"
tags: ["query:immuno-topo"]
score: 8.0
evidence: "基于Transformer的架构从H&E组织切片预测基因表达，实现泛癌功能通路分析"
tldr: "为了解决现有方法局限于单一癌症和方差评估、忽视功能相关性的问题，提出HistoPrism，通过高效Transformer架构从H&E组织图像预测泛癌基因表达，并引入通路级基准评估生物意义，实现功能通路分析。"
source: ICLR-2026-Accepted
selection_source: conference_retrieval
motivation: 现有工作多限于单一癌症和基于方差的评估，未充分挖掘预测基因表达的功能相关性。
method: 提出HistoPrism，一个高效的Transformer架构，用于从组织学图像预测泛癌基因表达，并设计通路级基准进行评估。
result: 在基因表达预测上超越当前最优模型，并且通路级分析显示出更强的生物学一致性。
conclusion: HistoPrism将组织学与功能通路联系起来，为临床可及的基因表达推断提供了可泛化的解决方案。
---

## Abstract
Predicting spatial gene expression from H\&E histology offers a scalable and clinically accessible alternative to sequencing, but realizing clinical impact requires models that generalize across cancer types and capture biologically coherent signals. Prior work is often limited to per-cancer settings and variance-based evaluation, leaving functional relevance underexplored. We introduce HistoPrism, an efficient transformer-based architecture for pan-cancer prediction of gene expression from histology. To evaluate biological meaning, we introduce a pathway-level benchmark, shifting assessment from isolated gene-level variance to coherent functional pathways. HistoPrism not only surpasses prior state-of-the-art models on highly variable genes and, but more importantly, achieves substantial gains on pathway-level prediction, demonstrating its ability to recover biologically coherent transcriptomic patterns. With strong pan-cancer generalization and improved efficiency, HistoPrism establishes a new standard for clinically relevant transcriptomic modeling from routinely available histology.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义（研究动机和背景）

- **核心问题**  
  现有从H&E组织病理图像预测基因表达的方法存在两大局限：  
  - **癌症类型局限性**：多数模型仅针对单一癌症训练和评估，难以泛化到新的癌症类型。  
  - **评估指标单一**：仅以高变基因的方差解释度（variance-based）作为评价标准，忽略了预测结果的生物学功能相关性。  
  这导致预测的基因表达虽在统计上显著，但未必反映真实的生物学通路活动，限制了临床转化价值。

- **整体含义**  
  作者提出 **HistoPrism**，旨在实现泛癌（pan-cancer）范围内的组织学→基因表达预测，并建立以功能通路为单位的生物意义评估框架，从而将组织形态与分子功能直接关联，为基于常规H&E切片推断肿瘤分子特征提供可推广的临床辅助工具。

### 2. 论文提出的方法论：核心思想、关键技术细节

- **核心思想**  
  利用高效的Transformer架构，从泛癌组织图像中同时学习多癌种共享的形态-分子映射，并引入通路级别的评估基准以强调功能一致性。

- **关键技术细节**  
  - **模型架构**：HistoPrism 基于高效Transformer（efficient transformer），处理H&E全切片图像或多实例图像块，预测每个样本的基因表达谱。  
  - **训练策略**：采用泛癌联合训练，将多种癌症类型的样本混合训练，促使模型学习跨癌种的通用组织形态特征。  
  - **评估设计**：    
    - 传统基准：基于高变基因的逐基因方差评估。  
    - **新通路级基准**：将基因按照已知生物学通路（如信号通路、代谢通路）聚合，评估模型对通路整体活性的预测能力，从而衡量预测结果的生物相干性（biological coherence）。  
  - 文中未给出具体公式或伪代码，但整体流程可概括为：图像→Transformer编码器→基因表达预测头→与真实RNA-seq数据计算损失（可能为回归损失）。

### 3. 实验设计：数据集、基准与对比方法

- **数据集与场景**  
  - 使用了泛癌H&E组织学图像及其配对的RNA-seq/空间转录组数据（具体癌种名称原文未详述，但摘要强调“pan-cancer”）。  
  - 场景覆盖多种不同癌症类型，用于验证模型的跨癌种泛化能力。

- **基准（Benchmark）**  
  - **基因水平基准**：与现有方法相同，比较高变基因的预测准确度。  
  - **通路水平基准**：新引入的评估方式，将基因聚合成通路分数，比较通路活性的预测准确性。

- **对比方法**  
  对比了“先前的当前最优模型（prior state-of-the-art models）”，具体名称未在摘要中列出，但可理解为领域内已有的组织学→基因表达预测模型（如基于CNN或注意力的单癌种模型）。

### 4. 资源与算力

- **文中信息**  
  提供的摘要及元数据中未提及使用的GPU型号、数量、训练时长等算力细节。  
- **说明**  
  考虑到这是ICLR 2026接收论文的摘要，完整PDF可能包含详细系统配置，但此处无法获取。因此关于算力部分，**文中未明确说明**。

### 5. 实验数量与充分性

- **实验组数推测**  
  基于摘要描述，至少包括：  
  - 多癌种（>1）的泛癌预测实验。  
  - 基因水平评估和通路水平评估两组主实验。  
  - 与先前SOTA方法的对比实验。  
  - 可能有消融实验（如模型组件分析、高效架构验证等），但摘要未详细展开。

- **充分性与客观性**  
  - **充分性**：新引入的通路级基准弥补了现有评价体系的不足，从功能角度增加了实验维度，使评估更全面。  
  - **客观性**：与先前最优方法直接对比，采用统一的外部基准，对比公平；泛癌训练和测试设计避免了对单一癌种的过拟合，结果更具说服力。  
  - 由于缺少完整论文，无法确认消融实验、统计检验等细节，但就摘要而言，实验设计方向合理。

### 6. 论文的主要结论与发现

- HistoPrism 不仅在传统的高变基因方差预测指标上超越现有最优模型。  
- 更关键的是，在**通路水平预测**上取得了显著增益（substantial gains），证明其恢复的转录组模式具有更强的生物一致性。  
- 模型具有强泛癌泛化能力和更高的计算效率，为通过常规组织学实现临床相关的转录组建模建立了新标准。

### 7. 优点：方法或实验设计上的亮点

- **方法论亮点**  
  - 采用**高效Transformer架构**，在保证性能的同时提升计算效率，更适合大规模临床部署。  
  - 首次系统性地从**功能通路视角**评估组织学→基因表达预测，把评价从统计相关性提升到生物意义层面。  
  - 通过泛癌联合训练，突破单癌种限制，模型可推广性显著增强。

- **实验设计亮点**  
  - 引入通路级基准，为领域提供了更贴近生物学问题的评价工具。  
  - 同时报告基因水平和通路水平结果，多维度展示模型优势。

### 8. 不足与局限：包括实验覆盖、偏差风险、应用限制等

- **信息缺失带来的局限**  
  - 摘要未提供数据集的具体癌种数、样本量、队列分布，无法评估实验覆盖广度和潜在数据偏差。  
  - 无算力细节和训练时间，难以复现或评估资源需求。  
  - 缺少与其他新兴的方法（如基于图网络或MIL的模型）的详细对比。

- **潜在偏差与应用限制**  
  - 泛癌训练虽提升泛化，但若癌种间组织形态过于异质，仍可能限制某些罕见癌的预测精度。  
  - 通路评估依赖于预先定义的通路数据库，数据库的完整性和癌种特异性可能影响评估结论。  
  - 从组织学预测基因表达本质上是关联性推断，不能替代实际测序中的因果机制，临床应用需谨慎验证。

（完）
