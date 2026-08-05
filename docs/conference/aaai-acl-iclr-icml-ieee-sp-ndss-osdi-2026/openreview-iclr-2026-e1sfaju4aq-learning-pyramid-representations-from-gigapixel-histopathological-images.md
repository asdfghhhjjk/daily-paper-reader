---
title: Learning Pyramid Representations from Gigapixel Histopathological Images
title_zh: 从千兆像素组织病理学图像学习金字塔表示
authors: "Weiyi Wu, Xingjian Diao, Chunhui Zhang, Chongyang Gao, Xinwen Xu, Siting Li, Jiang Gui"
date: 2025-09-20
pdf: "https://openreview.net/pdf?id=E1sFAJU4Aq"
tags: ["query:path-xai-sel"]
score: 7.0
evidence: 在WSI中保持空间关系并将计算分配到信息丰富的区域
tldr: 针对全切片图像中信息区域稀疏且空间结构常被忽略的问题，提出稀疏金字塔注意力网络（SPAN），通过层级注意力在保持空间关系的同时将计算分配给关键区域，从而以更低开销实现精确的WSI建模，并在多项任务中验证了有效性。
source: ICLR-2026-Public
selection_source: conference_retrieval
motivation: 全切片图像分辨率高且信息区域稀疏，现有方法常忽略空间结构，导致表示效率低。
method: 提出SPAN框架，构建多尺度稀疏金字塔注意力，在单尺度输入下高效分配计算到信息区域。
result: SPAN在WSI分类和分割任务上能以更低计算量达到高精度。
conclusion: 稀疏金字塔注意力实现了WSI中信息区域的有效定位和高效建模。
---

## Abstract
Whole slide images (WSIs) pose fundamental computational challenges due to their gigapixel resolution and the sparse distribution of informative regions. Existing approaches often treat image patches independently—discarding spatial structure—or reshape them in ways that distort spatial context, thereby obscuring the hierarchical pyramid representations intrinsic to WSIs. We introduce Sparse Pyramid Attention Networks (SPAN), a hierarchical framework that preserves spatial relationships while efficiently allocating computation to informative regions. SPAN constructs multi-scale representations directly from single-scale inputs, enabling precise WSI modeling without sacrificing efficiency. We demonstrate SPAN’s versatility through two variants: SPAN-MIL for slide classification and SPAN-UNet for segmentation. Comprehensive evaluations across multiple public datasets show that SPAN captures the hierarchical structure and contextual relationships that existing methods fail to model. Our results provide clear evidence that architectural inductive biases and hierarchical representations enhance both slide-level and patch-level performance. By overcoming long-standing computational barriers, SPAN establishes a new paradigm for computational pathology and reveals foundational design principles for large-scale medical image analysis.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义（研究动机和背景）
- **核心问题**：全切片组织病理图像（WSI）具有千兆像素级分辨率和信息区域稀疏分布的特点，现有方法常将图像块独立处理而丢失空间结构，或通过形变破坏空间上下文，导致无法有效建模WSI中固有的层次化金字塔表示。
- **整体含义**：论文旨在解决WSI分析中因忽略空间关系和金字塔结构而导致表示效率低下的问题，提出一种既能保持空间关系又能将计算聚焦于信息区域的架构，从而以更低开销实现精准的WSI建模，为计算病理学建立新范式。

### 2. 论文提出的方法论
- **核心思想**：通过稀疏金字塔注意力机制，在单尺度输入上直接构建多尺度表示，将计算资源动态分配到信息丰富的区域，同时保留空间结构。
- **关键技术细节**：
  - 提出 **稀疏金字塔注意力网络（SPAN）**，一种层次化框架，利用层级注意力在保持空间关系的同时，让模型自动关注关键区域。
  - 设计了两个变体：**SPAN-MIL**（用于切片分类）和 **SPAN-UNet**（用于分割），证明框架的通用性。
- **算法流程（文字说明）**：
  - 输入单尺度WSI，通过金字塔结构逐步聚合多尺度特征。
  - 在每个层级施加稀疏注意力，仅对信息量大的位置进行计算，降低整体开销。
  - 最终输出可用于分类或分割的表示，实现从切片级到像素级的层次化建模。

### 3. 实验设计
- **数据集**：在多个公开数据集上进行评估（具体名称未在给定文本中列出，但涉及WSI分类和分割任务）。
- **基准与对比方法**：与现有方法对比，这些方法通常独立处理图像块或扭曲空间结构，未能有效建模金字塔表示；SPAN在分类和分割任务上均表现出优势。
- **场景**：覆盖了切片级分类和像素级分割两种典型WSI分析任务。

### 4. 资源与算力
- **文中提及情况**：给定文本仅包含摘要和元数据，**未明确说明**使用的GPU型号、数量、训练时长等资源信息。但从“更低计算量”“高效分配计算”等表述推断，SPAN在同等精度下具有更低的计算开销。

### 5. 实验数量与充分性
- **实验数量**：据摘要描述，进行了“全面评估”（comprehensive evaluations），涵盖多数据集、两个变体（SPAN-MIL和SPAN-UNet）、分类与分割任务；具体实验组数未给出，但声明捕获了现有方法无法建模的层次结构与上下文关系。
- **充分性与公平性**：比较对象明确（独立块处理或空间扭曲方法），且用“清晰证据”表明架构归纳偏置和层次表示的好处。实验设计旨在验证效率和精度的双重提升，推断较为充分和公平，但缺乏消融实验等细节佐证。

### 6. 论文的主要结论与发现
- SPAN能够有效定位WSI中的信息区域并实现高效建模。
- 层次化金字塔表示和架构归纳偏置显著提升了切片级和块级性能。
- 通过克服长期存在的计算障碍，SPAN为计算病理学确立了新范式，并揭示大规模医学图像分析的基础设计原则。

### 7. 优点
- **方法亮点**：
  - 首次将稀疏注意力与金字塔结构结合，解决WSI信息稀疏与空间保持的矛盾。
  - 从单尺度输入直接构建多尺度表示，避免传统多尺度预处理。
  - 提供两个针对性变体，覆盖分类和分割，展示通用性。
- **实验设计亮点**：
  - 在多个公开数据集上验证，兼顾效率和精度。
  - 明确对比忽略空间结构的现有范式，凸显所提方法的优势。

### 8. 不足与局限
- **实验覆盖缺失**：未见到具体的数据集名称、消融研究细节、性能数值，无法评估结果的普适性和稳定性。
- **偏差风险**：公开数据集可能存在机构或人群偏差，文中未讨论。
- **应用限制**：未说明SPAN对染色变异、扫描仪差异或罕见病变的鲁棒性；资源开销虽声称更低，但无具体数据支撑。
- **信息不完整**：因仅提供摘要和元数据，许多关键细节（如算力、实验规模、局限性讨论）均缺失，完整评审需查阅全文。

（完）
