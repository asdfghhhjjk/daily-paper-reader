---
title: Learning Pyramid Representations from Gigapixel Histopathological Images
title_zh: 从千兆像素组织病理图像中学习金字塔表示
authors: "Weiyi Wu, Xingjian Diao, Chunhui Zhang, Chongyang Gao, Xinwen Xu, Siting Li, Jiang Gui"
date: 2025-09-20
pdf: "https://openreview.net/pdf?id=E1sFAJU4Aq"
tags: ["query:profile"]
score: 9.0
evidence: 保留空间关系的层次框架用于WSI建模，整合跨补丁信息
tldr: SPAN是一个层次注意力网络，从千兆像素WSI中构建多尺度金字塔表示，保留空间结构并高效分配计算到信息区域，解决了现有方法忽略空间上下文或扭曲上下文的问题。
source: ICLR-2026-Public
selection_source: conference_retrieval
motivation: 现有WSI方法忽略空间结构或扭曲上下文，未能利用WSI内在的金字塔表示。
method: 提出SPAN，稀疏金字塔注意力网络，从单尺度输入构建多尺度表示，保留空间关系。
result: 展示了两种变体，在WSI建模任务中兼顾精度和效率。
conclusion: SPAN为WSI分析提供了一种尊重空间层次的高效建模框架。
---

## Abstract
Whole slide images (WSIs) pose fundamental computational challenges due to their gigapixel resolution and the sparse distribution of informative regions. Existing approaches often treat image patches independently—discarding spatial structure—or reshape them in ways that distort spatial context, thereby obscuring the hierarchical pyramid representations intrinsic to WSIs. We introduce Sparse Pyramid Attention Networks (SPAN), a hierarchical framework that preserves spatial relationships while efficiently allocating computation to informative regions. SPAN constructs multi-scale representations directly from single-scale inputs, enabling precise WSI modeling without sacrificing efficiency. We demonstrate SPAN’s versatility through two variants: SPAN-MIL for slide classification and SPAN-UNet for segmentation. Comprehensive evaluations across multiple public datasets show that SPAN captures the hierarchical structure and contextual relationships that existing methods fail to model. Our results provide clear evidence that architectural inductive biases and hierarchical representations enhance both slide-level and patch-level performance. By overcoming long-standing computational barriers, SPAN establishes a new paradigm for computational pathology and reveals foundational design principles for large-scale medical image analysis.

---

## 论文详细总结（自动生成）

由于所提供的论文内容仅包含摘要与元数据，未提供完整正文，本总结严格基于现有信息展开，缺失部分将如实说明。

### 1. 论文核心问题与整体含义
- **研究动机**：全切片图像（WSI）具有千兆像素级分辨率和信息区域稀疏分布的特点，带来巨大计算挑战。现有方法要么将图像块独立处理，丢弃空间结构；要么在重组时扭曲空间上下文，模糊了WSI内在的层次化金字塔表示。
- **核心问题**：如何在保留空间关系的前提下，高效地对WSI进行建模，并利用其多尺度金字塔特性提升分类与分割性能。
- **整体含义**：提出一种尊重WSI空间层次的高效建模框架，为计算病理学建立新范式，并揭示大规模医学图像分析的基础设计原则。

### 2. 方法论
- **核心思想**：设计稀疏金字塔注意力网络（SPAN），通过保留空间关系的层次化架构，从单尺度输入直接构建多尺度表示，将计算资源高效分配至信息丰富的区域。
- **关键技术细节**：
  - 提出稀疏金字塔注意力机制，在不牺牲效率的前提下构建多尺度特征金字塔。
  - 构建两种变体，分别针对不同下游任务：
    - **SPAN-MIL**：用于全切片分类，将多尺度表示融入多实例学习框架。
    - **SPAN-UNet**：用于像素级分割，整合金字塔表示到UNet架构中。
- **算法流程**（文字概括）：基于单尺度图像块输入，通过层次化稀疏注意力模块逐步聚合上下文，生成多尺度特征，保留空间结构，最终输出用于分类或分割的表示。

### 3. 实验设计
- **数据集**：摘要声明在多个公共数据集上进行了全面评估，但未列出具体数据集名称。
- **任务场景与Benchmark**：涵盖幻灯片级分类与补丁级分割两个任务，与现有WSI建模方法进行对比（对比方法名称未在摘要中给出）。
- **对比方法**：未提供具体方法列表。

### 4. 资源与算力
- 摘要及元数据中**均未提及**使用的GPU型号、数量及训练时长等资源信息，无法评估算力消耗。

### 5. 实验数量与充分性
- **实验组数**：基于“Comprehensive evaluations across multiple public datasets”可推测在多个数据集上进行了分类和分割实验，且可能包含消融实验（如变体对比），但具体数量未列出。
- **充分性与公平性**：由于缺乏详细实验设置（如数据集规模、划分方式、超参数、对比方法的选择依据），无法判断实验是否充分、客观和公平。摘要仅定性描述了性能提升，未给出量化指标或统计检验。

### 6. 主要结论与发现
- SPAN能够捕获现有方法无法建模的层次化结构与上下文关系。
- 架构归纳偏置和层次化表示可同时提升幻灯片级别和补丁级别性能。
- 该方法克服了长期存在的计算障碍，在精度与效率之间取得平衡。
- 为大规模医学图像分析提供了新的设计范式。

### 7. 优点
- **空间保真**：保留完整的空间关系，避免上下文扭曲。
- **高效计算**：通过稀疏注意力分配计算至信息区域，兼顾效率。
- **任务灵活性**：通过两种变体（MIL/UNet）统一了分类与分割任务。
- **内在金字塔利用**：直接从单尺度输入构建多尺度表示，符合WSI天然属性。

### 8. 不足与局限
- **信息不完整**：摘要未提供具体数据集、对比基线、量化结果和资源消耗，评估的可信度与可复现性存疑。
- **泛化边界未知**：未说明模型在不同癌种、不同染色协议或不同扫描仪下的鲁棒性。
- **技术细节缺失**：缺乏公式、网络结构图、训练策略等细节，难以深入判断方法的创新性和局限性。
- **潜在偏差风险**：若实验仅选用特定公开数据集，可能存在评估偏差，无法验证真实临床场景的适用性。
- **无算力分析**：无法评估其在资源受限环境中的实际部署可行性。

（完）
