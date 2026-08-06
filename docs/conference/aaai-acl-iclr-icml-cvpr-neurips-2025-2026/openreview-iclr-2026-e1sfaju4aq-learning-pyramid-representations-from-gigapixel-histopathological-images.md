---
title: Learning Pyramid Representations from Gigapixel Histopathological Images
title_zh: 从千兆像素组织病理图像中学习金字塔表示
authors: "Weiyi Wu, Xingjian Diao, Chunhui Zhang, Chongyang Gao, Xinwen Xu, Siting Li, Jiang Gui"
date: 2025-09-20
pdf: "https://openreview.net/pdf?id=E1sFAJU4Aq"
tags: ["query:immuno-topo"]
score: 9.0
evidence: 提出用于WSI分析的层次化稀疏金字塔注意力，直接对应数字病理学深度学习
tldr: 针对全切片图像千兆像素导致的信息区域稀疏和空间结构失真的问题，提出SPAN稀疏金字塔注意力网络，通过保留空间关系并高效分配计算资源构建多尺度表示，在WSI分类与分割任务上证明其精度与效率，为数字病理提供了一种层次化建模新范式。
source: ICLR-2026-Public
selection_source: conference_retrieval
motivation: 现有WSI分析方法破坏空间上下文，无法有效利用固有金字塔表示。
method: 提出稀疏金字塔注意力网络（SPAN），从单尺度输入构建多尺度表示，保留空间关系并高效聚焦信息区域。
result: SPAN在WSI分类和分割任务上优于现有方法，兼具精度与计算效率。
conclusion: SPAN成功解决了千兆像素WSI的空间建模瓶颈，广泛应用于数字病理任务。
---

## Abstract
Whole slide images (WSIs) pose fundamental computational challenges due to their gigapixel resolution and the sparse distribution of informative regions. Existing approaches often treat image patches independently—discarding spatial structure—or reshape them in ways that distort spatial context, thereby obscuring the hierarchical pyramid representations intrinsic to WSIs. We introduce Sparse Pyramid Attention Networks (SPAN), a hierarchical framework that preserves spatial relationships while efficiently allocating computation to informative regions. SPAN constructs multi-scale representations directly from single-scale inputs, enabling precise WSI modeling without sacrificing efficiency. We demonstrate SPAN’s versatility through two variants: SPAN-MIL for slide classification and SPAN-UNet for segmentation. Comprehensive evaluations across multiple public datasets show that SPAN captures the hierarchical structure and contextual relationships that existing methods fail to model. Our results provide clear evidence that architectural inductive biases and hierarchical representations enhance both slide-level and patch-level performance. By overcoming long-standing computational barriers, SPAN establishes a new paradigm for computational pathology and reveals foundational design principles for large-scale medical image analysis.

---

## 论文详细总结（自动生成）

# 论文总结：从千兆像素组织病理图像中学习金字塔表示

## 1. 论文的核心问题与整体含义
- **研究背景**：全切片图像（Whole slide images, WSIs）具有千兆像素级分辨率，且其中包含诊断意义的信息区域呈稀疏分布，这为计算分析带来了根本性挑战。
- **现有方法局限**：
  - 常将图像块（patch）独立处理，完全丢弃空间结构。
  - 或以扭曲空间上下文的方式重组图像，破坏了WSI固有的层次化金字塔表示。
- **研究动机与目标**：在保持空间关系的同时，高效地将计算资源聚焦于信息区域，直接从单尺度输入构建多尺度表示，从而精确建模WSI的全貌。

## 2. 论文提出的方法论
- **核心框架**：**稀疏金字塔注意力网络（Sparse Pyramid Attention Networks, SPAN）**，是一种层次化架构。
- **关键思想**：
  - **保留空间关系**：在网络中维持像素/块的空间对应关系。
  - **稀疏注意力**：计算只分配给信息丰富的区域，避免在空白背景上浪费算力。
  - **从单尺度到多尺度**：直接从单尺度输入（如最高分辨率图像）构建出多尺度表示，无需金字塔式输入。
- **具体变体**：
  - **SPAN-MIL**：针对切片级分类任务，结合多实例学习。
  - **SPAN-UNet**：针对像素级分割任务，结合U-Net架构。
- **流程简述**（基于摘要）：输入单个高分辨率WSI块序列 → 通过稀疏注意力机制筛选关键区域 → 逐步聚合成金字塔多尺度特征 → 用于分类或分割头预测。

## 3. 实验设计
- **使用数据集**：多个公开数据集（具体名称未在给定内容中列出）。
- **基准任务与对比方法**：
  - **WSI分类**：与现有独立的斑块处理方法对比。
  - **WSI分割**：与现有分割方法对比。
  - 对比的基准包括现有不保留空间结构或扭曲上下文的方法。
- **评估维度**：精度与计算效率。

## 4. 资源与算力
- 所提供的摘要和元数据中 **未明确说明** GPU型号、数量、训练时长等算力细节。

## 5. 实验数量与充分性
- 仅从摘要可知，实验为“在多个公共数据集上的综合评估”，并包含分类与分割两类任务。
- 摘要未提供具体实验组数、消融实验细节，因此无法据此判断实验是否全面客观；但摘要宣称其结果是“明确的证据”，暗示其内部实验设计应当较为充分。

## 6. 论文的主要结论与发现
- SPAN能够捕获现有方法无法建模的层次结构信息和上下文关系。
- 明确的架构归纳偏置和层次化表示能同时提升 **切片级** 和 **斑块级** 性能。
- SPAN克服了长期以来的计算瓶颈，为计算病理学建立了新范式，并揭示出大规模医学图像分析的基础设计原则。

## 7. 优点
- **空间保真**：在计算中始终维护组织空间关系，避免信息丢失。
- **效率与聚焦**：利用稀疏注意力仅在信息区域投入计算，兼顾千兆像素的处理速度。
- **通用性**：单一架构思想可延伸至分类（MIL）和分割（UNet），展现出跨任务迁移能力。
- **多尺度来源创新**：仅从单一尺度输入即构建出金字塔表示，简化了输入管线。

## 8. 不足与局限
- 受限于所给内容，无法得知：
  - 稀疏注意力的预定义规则或学习方式可能带来额外超参。
  - 在极度不平衡或罕见疾病亚型上的泛化性。
  - 对数据标注粒度的依赖程度。
- 未见具体算力报告，难以评估其实践中的资源门槛。

（完）
