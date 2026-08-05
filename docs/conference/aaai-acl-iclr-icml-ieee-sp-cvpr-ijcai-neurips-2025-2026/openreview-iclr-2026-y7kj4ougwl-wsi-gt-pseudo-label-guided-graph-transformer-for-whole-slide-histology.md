---
title: "WSI-GT: Pseudo-Label Guided Graph Transformer for Whole-Slide Histology"
title_zh: WSI-GT：伪标签引导的图Transformer用于全切片组织学分析
authors: "Zhongao Sun, Alexander Khvostikov, Andrey Krylov, Ilya Mikhailov, Pavel G. Malkov"
date: 2025-09-19
pdf: "https://openreview.net/pdf?id=Y7kJ4oUgwL"
tags: ["query:profile"]
score: 9.0
evidence: 图Transformer整合跨patch空间信息用于全切片组织学分类
tldr: WSI-GT针对全切片图像中忽略空间上下文或过度平滑的问题，提出局部图卷积与伪标签引导注意力机制。该方法在patch分类基础上整合邻域特征，保持类别内变异，有效提升WSI级分类性能，为数字病理下游任务提供了强大的跨patch上下文建模方案。
source: ICLR-2026-Public
selection_source: conference_retrieval
motivation: 现有WSI方法忽略patch间空间上下文或因图模型过平滑丢失组织细节。
method: 提出WSI-GT，结合局部图卷积和伪标签引导注意力机制。
result: 在WSI分类任务上，模型有效保留组织细节并缓解过平滑。
conclusion: 为全切片组织学分析提供了简单有效的空间上下文建模架构。
---

## Abstract
Whole-slide histology images (WSIs) can exceed 100k × 100k pixels, making direct pixel-level segmentation infeasible and requiring patch-level classification as a practical alternative. However, most approaches either treat patches independently, ignoring spatial and biological context, or rely on deep graph models that oversmooth, leading to loss of critical tissue details.

We present WSI-GT (Pseudo-Label Guided Graph Transformer), a simple yet effective architecture that addresses these challenges. WSI-GT combines a lightweight local graph convolution block for neighborhood feature aggregation with a pseudo-label guided attention mechanism that preserves intra-class variability and mitigates oversmoothing. To cope with sparse annotations, we introduce an area-weighted sampling strategy that balances class representation while maintaining tissue topology.

WSI-GT achieves a Macro F1 of 0.95 on PATH-DT-MSU WSS2v2, improving by up to 3 percentage points over tile-based CNNs and by about 2 points over strong graph baselines. It further generalizes well to the Placenta benchmark and standard graph node classification datasets, highlighting both clinical relevance and broader applicability. These results position WSI-GT as a practical and scalable solution for graph-based learning on extremely large images.

---

## 论文详细总结（自动生成）

## 论文核心问题与整体含义
- **研究背景**：全切片组织学图像（WSI）像素量极大（常超10万×10万），直接像素级分割不可行，必须依赖patch级分类。
- **核心问题**：现有方法要么独立处理每个图像块（patch），忽略组织空间和生物学上下文；要么采用深层图模型，导致特征过平滑，丢失关键组织细节。
- **整体含义**：论文旨在设计一种简单而有效的架构，既能充分聚合邻域空间信息，又能缓解图学习中的过平滑，从而提升WSI级分类性能，服务于数字病理下游任务。

## 方法论
- **核心思想**：通过**局部图卷积**聚合邻域特征，并引入**伪标签引导的注意力机制**来保持类别内部变异性、减轻过平滑。
- **关键技术细节**：
  - **轻量局部图卷积块**：在patch构建的图结构上，仅对邻域进行特征聚合，避免深层全局卷积带来的特征均化。
  - **伪标签引导注意力**：利用patch的伪标签（可由初始分类器生成）引导注意力计算，使同类patch内部保持差异，不同类间的边界更清晰。
  - **面积加权采样策略**：针对稀疏标注问题，在保持组织拓扑结构的同时，平衡类别分布，确保训练时各类别样本的代表性。
- **算法流程概括**：
  1. 将WSI切分为大量patch，提取patch级特征，并构建图（节点为patch，边基于空间邻近关系）。
  2. 对节点进行面积加权采样，缓解类别不平衡及稀疏标注影响。
  3. 通过局部图卷积块聚合每个patch的邻域信息。
  4. 图Transformer层利用伪标签引导的注意力机制进一步处理，产生节点（patch）的增强表示。
  5. 最终进行patch级或聚合后的WSI级分类。

## 实验设计
- **数据集/场景**：
  - PATH-DT-MSU WSS2v2（主要基准）
  - Placenta benchmark（泛化验证）
  - 标准图节点分类数据集（验证模型通用性）
- **对比方法**：基于tile的CNN方法、强图基线模型（具体名称未列出）。
- **评价指标**：Macro F1（主要），可能包含其他分类指标。

## 资源与算力
- 所提供元数据中**未明确说明**GPU型号、数量及训练时长。正文可能包含这部分信息，但基于现有文本无法确认。

## 实验数量与充分性
- **实验组数**：至少包含三个不同数据集的实验（WSI分类、胎盘基准、图节点分类），且可能包含消融研究（如验证局部图卷积、伪标签注意力、采样策略的贡献）。
- **充分性与客观性**：
  - 跨数据集的实验设计有助于验证泛化能力。
  - 与基于tile的CNN和图基线的对比可体现方法优势。
  - 由于缺少具体实验细节（如消融维度、重复次数、统计检验），无法严格判断客观公平性，但整体设计较为全面。

## 主要结论与发现
- WSI-GT在PATH-DT-MSU WSS2v2上Macro F1达到0.95，比tile-based CNN提升最多3个百分点，比强图基线提升约2个百分点。
- 模型能有效保留组织细节并缓解过平滑，在多个数据集上表现良好，证明了临床相关性和广泛适用性。
- 该架构为超大规模图像的图学习提供了实用且可扩展的解决方案。

## 优点
- **简单有效**：结合轻量局部图卷积和伪标签注意力，没有复杂深层结构，易于实施。
- **缓解过平滑**：伪标签引导注意力机制明确针对图模型在WSI中的关键缺陷。
- **兼顾上下文与细节**：既聚合了空间邻域信息，又保留了类内变异，避免信息丢失。
- **稀疏标注处理**：面积加权采样策略巧妙利用拓扑关系进行数据平衡。
- **实验广泛**：涵盖WSI专用、医学基准和通用图数据，验证了方法的鲁棒性。

## 不足与局限
- **资源细节缺失**：未提供计算资源和训练时间，难以评估实际部署成本。
- **对比方法有限**：对比方法仅提及基于tile的CNN和“强图基线”，未列出更前沿的WSI图方法（如基于Transformer的WSI模型），无法全面定位性能水平。
- **单一指标报告**：摘要仅给出Macro F1，缺少其他重要指标（如AUC、准确率等）和误差信息。
- **偏差风险**：数据集数量较少且具体构成不详，在不同种族、染色环境、机构数据下的泛化性未知。
- **应用限制**：当前主要验证分类任务，是否适用于分割、检测等更精细的病理任务仍需探索。

（完）
