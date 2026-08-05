---
title: "Revisiting Data Challenges of Computational Pathology: A Pack-based Multiple Instance Learning Framework"
title_zh: 重新审视计算病理的数据挑战：一种基于打包的多实例学习框架
authors: "Wenhao Tang, Heng Fang, Ge Wu, Xiang Li, Ming-Ming Cheng"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=EAmn2k52T8"
tags: ["query:path-xai-sel"]
score: 7.0
evidence: 提出基于打包的多实例学习框架，用于全切片图像的计算病理
tldr: 针对全切片图像序列长度差异大、数据异质性高的问题，提出基于打包的多实例学习框架，通过将变长特征序列打包为定长序列，在有限监督下提升训练效率和优化效果。
source: ICLR-2026-Public
selection_source: conference_retrieval
motivation: 全切片图像序列长度差异极大，导致训练效率低和数据冗余。
method: 提出基于打包的多实例学习框架，将多个采样的变长特征序列打包为定长序列。
result: 在癌症诊断和预后任务上提升了训练效率和模型优化。
conclusion: 打包策略有效应对了全切片图像的数据挑战。
---

## Abstract
Computational pathology (CPath) digitizes pathology slides into whole slide images (WSIs), enabling analysis for critical healthcare tasks such as cancer diagnosis and prognosis. However, WSIs possess extremely long sequence lengths (up to 200K), significant length variations (from 200 to 200K), and limited supervision. These extreme variations in sequence length lead to high data heterogeneity and redundancy. Conventional methods often compromise on training efficiency and optimization to preserve such heterogeneity under limited supervision. To comprehensively address these challenges, we propose a pack-based MIL framework. It packs multiple sampled, variable-length feature sequences into fixed-length ones, enabling batched training while preserving data heterogeneity. Moreover, we introduce a residual branch that composes discarded features from multiple slides into a \textit{hyperslide} which is trained with tailored labels. It offers multi-slide supervision while mitigating feature loss from sampling. Meanwhile, an attention-driven downsampler is introduced to compress features in both branches to reduce redundancy. By alleviating these challenges, our approach achieves an accuracy improvement of up to 8\% while using only 12\% of the training time in the PANDA(UNI). Extensive experiments demonstrate that focusing data challenges in CPath holds significant potential in the era of foundation models. The code is https://anonymous.4open.science/r/PackMIL-A320.

---

## 论文详细总结（自动生成）

# 论文总结：重新审视计算病理的数据挑战：一种基于打包的多实例学习框架

## 1. 论文的核心问题与整体含义
- **研究背景**：计算病理学（CPath）将病理切片数字化为全切片图像（WSI），用于癌症诊断、预后等关键医疗任务。WSI 面临极其长的序列（可达 200K）、巨大的长度差异（200~200K）以及有限的监督信号。
- **核心挑战**：序列长度的极端变化导致**数据异质性高**与**冗余严重**，传统方法在有限监督下往往需要在保留异质性和训练效率之间做妥协，难以兼顾优化效果与计算开销。
- **整体含义**：论文旨在系统性地解决源于长度变化的数据挑战，提出一种打包策略，在保持数据多样性的同时实现批次训练，从而提升训练效率和模型性能。

## 2. 论文提出的方法论
- **核心思想**：将多个可变长度的特征序列（采样后）**打包（pack）成固定长度的序列**，使得原本无法直接进行批处理的变长 WSI 数据能够被高效并行训练，同时保留多切片间的异质信息。
- **关键技术细节**：
  - **打包多实例学习框架（Pack-based MIL）**：从不同 WSI 的变长特征序列中采样，并将这些片段拼接为固定长度的“包”作为训练输入。
  - **残差分支（Residual Branch）**：将多个切片中被丢弃的特征组合成一个**超切片（hyperslide）**，并以定制标签进行训练，提供多切片监督并缓解采样带来的信息丢失。
  - **注意力驱动的下采样器（Attention-driven Downsampler）**：在两个分支中对特征进行压缩，进一步降低冗余。
- **公式/算法流程（文字说明）**：
  1. 对每张 WSI 提取的变长特征序列进行采样。
  2. 将来自不同 WSI 的采样片段拼接或打包，构成一个固定长度的序列（批次输入）。
  3. 主分支基于打包序列进行多实例学习，同时残差分支利用被丢弃的特征构建超切片，并用聚合标签监督。
  4. 注意力下采样器减少特征维度，控制冗余。

## 3. 实验设计
- **数据集/场景**：论文明确提及 **PANDA (UNI)**，可能是一个癌症诊断或预后相关的公共 WSI 数据集。此外未提供具体数据集列表。
- **Benchmark 与对比方法**：文中未列出对比的基线方法名称，但指出传统方法通常在保留异质性与提升训练效率之间权衡，推测对比对象包含常规 MIL 变体、固定长度采样的方法等。
- **任务类型**：癌症诊断与预后。

**注意**：由于提供的材料仅为论文元数据，缺少完整的实验细节（如数据集规模、评估指标、对比方法列表），此处信息基于摘要及结果字段推断。

## 4. 资源与算力
- 原文未明确说明所使用的 GPU 型号、数量及具体训练时长。
- 结果中提到“仅使用 PANDA (UNI) 12% 的训练时间”，表明打包方法显著缩短训练时间，但未给出绝对时间值或算力配置。

## 5. 实验数量与充分性
- 基于现有材料无法准确统计实验组数，但摘要提到“广泛的实验”，可能包括：
  - 不同任务（诊断、预后）
  - 消融实验（例如有无残差分支、注意力下采样器）
  - 效率对比实验（训练时间、准确率提升）
- 由于仅提供元数据，无法全面评估实验的**充分性**，但声称准确率提升最高达 8%，训练时间降至 12%，表明其优化效果显著。
- **公平性**：难以判断是否与同等计算预算下的基线公平比较，需查看原文细节。

## 6. 论文的主要结论与发现
- 打包策略能够有效应对 WSI 的极端长度变化和有限监督问题。
- 所提框架在癌症诊断和预后任务上**既提升了训练效率（时间大幅缩短），又提高了模型优化效果（准确率提升高达 8%）**。
- 在基础模型时代，聚焦于 CPath 中的数据挑战具有巨大潜力。

## 7. 优点
- **直接针对现实痛点**：正视 WSI 长度变化大、冗余高的数据挑战，而非仅仅改进模型结构。
- **兼顾异质性与效率**：打包与残差分支的组合在保持多切片信息的同时实现批训练，创新性强。
- **多切片监督**：通过超切片标签提供额外的全局信号，缓解采样信息损失。
- **模块化设计**：注意力下采样器可灵活插入，进一步压缩冗余。

## 8. 不足与局限
- **信息缺失风险**：由于提供内容仅为元数据，无法评估实验覆盖面、统计显著性、泛化能力（如跨中心、跨染色）及潜在偏差。
- **可能局限**：
  - 打包策略依赖于采样，可能丢失关键局部信息，尽管有残差分支补救，但超切片构造效果未知。
  - 未提及对不同 MIL 池化方法（如注意力、Transformer）的兼容性。
  - 仅在一类任务（癌症）上验证，扩展至其他病理任务（如分级、分割）尚不明确。
  - 训练时间虽降至 12%，但打包引入的序列拼接可能增加显存压力，文中未讨论。

（完）
