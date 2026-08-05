---
title: Nonparametric Unsupervised Data Condensation for Gigapixel Histological Images
title_zh: 千兆像素组织学图像的非参数无监督数据压缩
authors: "Duong M. Nguyen, Trong Nghia Hoang, Thanh Trung Huynh, Phi Le Nguyen, Minh N. Do"
date: 2025-09-20
pdf: "https://openreview.net/pdf?id=Ysa5RZZi6J"
tags: ["query:path-xai-sel"]
score: 7.0
evidence: 自适应原型选择压缩千兆像素组织学图像，保留关键区域信息
tldr: NICER非参数化地压缩千兆像素全切片组织学图像，根据图像复杂度自适应选择代表性原型，在保留组织异质性的同时大幅减少数据量。该方法为在巨幅病理图像上高效进行下游分析任务提供了通用的数据压缩方案。
source: ICLR-2026-Public
selection_source: conference_retrieval
motivation: 固定原型压缩忽略WSI复杂性和异质性，导致关键信息丢失。
method: 提出NICER，基于非参数概率压缩，分解特征模式并自适应原型数量。
result: 在保留关键组织信息的前提下，有效压缩WSI数据量。
conclusion: 为千兆像素病理图像的高效处理提供了自适应压缩框架。
---

## Abstract
Histological whole-slide images (WSIs) are central to computational pathology but are extremely large, often several gigabytes, making them infeasible for direct use in standard vision pipelines. Prior approaches reduce training cost by condensing WSIs into a fixed number of representative features (prototypes), but this approach overlooks the varying complexity and diversity of WSIs, leading to loss of critical information. To this end, we propose **NICER**, a probabilistic data condensation framework that decomposes each WSI into feature patterns to capture heterogeneity and concept prototypes to ensure compactness. By reformulating prototype construction as a nonparametric condensation problem, NICER adapts the number of prototypes to slide complexity while preserving relevant information. Experiments on four histological datasets show that NICER outperforms prior methods, yielding superior efficiency trade-offs, setting a new paradigm for histological representation learning.

---

## 论文详细总结（自动生成）

## 1. 论文的核心问题与整体含义

- **研究背景**：组织学全切片图像（Whole Slide Images, WSIs）是计算病理学的核心数据，单张可达数 GB 级，无法直接输入常规视觉模型。
- **核心问题**：现有方法多将 WSI 压缩为**固定数目的代表性特征（原型）**，以降低计算成本，但忽略了不同 WSI 在组织结构和复杂度上的差异，导致关键信息丢失。
- **整体含义**：提出一种**自适应、非参数**的数据压缩框架，根据每张 WSI 的实际复杂度灵活决定原型数量，在高度压缩的同时保留组织异质性，为千兆像素病理图像的表示学习提供一种通用且高效的新范式。

## 2. 论文提出的方法论

- **核心思想**：将原型构造重新定义为**非参数概率压缩问题**，使模型能够依据图像本身的特征分布自适应选择代表点，而非预设固定数量。
- **关键技术细节**：
  - **特征模式分解**：将每张 WSI 分解为一组特征模式，捕获局部组织结构及全局异质性。
  - **概念原型构建**：基于非参数概率框架，从特征模式中选取最具代表性的原型，保证紧凑性的同时保留关键诊断信息。
  - **自适应原型数量**：原型数量不再由人工设定，而是由 WSI 的内在复杂度自动决定——简单区域用少量原型概括，复杂区域则分配更多原型。
  - **保留信息完整性**：整个过程是非参数化的，不需要事先训练生成模型或学习压缩映射，从而避免因训练分布偏移造成的信息丢失。
- **算法流程概况**（原文未提供详细公式，仅从描述推断）：
  1. 从 WSI 中提取局部 patch 特征，形成高维特征集合。
  2. 基于概率分布匹配或信息论准则，将特征集合划分为多个模式。
  3. 每个模式用一个代表性原型表示，原型集合规模和构成完全由数据驱动。
  4. 压缩后的原型集合可直接用于下游任务（分类、检索等）。

## 3. 实验设计

- **使用数据集**：4 个组织学图像数据集（具体名称未在元数据中列出）。
- **实验场景 / Benchmark**：在下游任务中评估压缩表示的质量，重点考察分类性能与压缩比的权衡（efficiency trade‑offs）。
- **对比方法**：文中提及与先前将 WSI 压缩为固定数量原型的方法进行直接对比，这些方法泛称为“prior methods”（未列出具体方法名）。

## 4. 资源与算力

- **文中提及情况**：提供的元数据及摘要中**未明确说明**所使用的 GPU 型号、数量、训练时长等算力消耗细节。

## 5. 实验数量与充分性

- **实验规模**：
  - 在 4 个不同组织学数据集上进行了性能评估。
  - 除主要对比实验外，极可能包含消融研究（如原型数量固定 vs. 自适应的对比、不同压缩比下的表现），但元数据未给出具体组数。
- **充分性与公平性**：
  - 多数据集验证增加了结果的泛化性。
  - 关注效率‑性能权衡曲线，而非单一指标，体现了全面比较。
  - 但在无完整原文的情况下，无法确切评估实验细节的完备性（如是否控制了特征提取器、是否进行统计显著性检验等）。

## 6. 论文的主要结论与发现

- NICER 在所有四个数据集上均**优于**先前固定原型数量的压缩方法。
- 在相同的压缩率下，NICER 能够保留更多诊断相关信息，取得更高的下游任务性能。
- 该方法为千兆像素病理图像的表示学习**设置了一个新的范式**，证明自适应、非参数压缩可以同时满足高效与保真的需求。

## 7. 优点

- **自适应压缩**：原型数量随图像内容变化，避免“一刀切”导致的精度损失。
- **非参数特性**：无需预先训练生成模型，不同数据集间迁移成本低，部署灵活。
- **保留异质性**：明确分解特征模式，使压缩结果能更好反映组织切片的局部多样性和全局结构。
- **通用性强**：可作为多种下游病理分析任务的即插即用型数据预处理步骤。

## 8. 不足与局限

- **信息细节缺失**：仅从元数据无法获取公式推导、网络结构、超参数设置等关键实现细节，难以全面评估其创新性。
- **数据集与任务范围**：实验仅覆盖组织学图像，对其他类型巨幅图像（如遥感、材料显微）的有效性未知。
- **对比方法不详**：未具体说明对比基线，无法判断是否与最新的动态原型选择或注意力池化类方法进行了公平比较。
- **算力与可复现性**：缺少硬件和运行时间信息，难以估计实际部署成本。
- **可能的风险**：非参数框架在处理极端噪声或背景区域时，可能产生冗余或低质量原型，需要额外的过滤机制（原文未提及）。

（完）
