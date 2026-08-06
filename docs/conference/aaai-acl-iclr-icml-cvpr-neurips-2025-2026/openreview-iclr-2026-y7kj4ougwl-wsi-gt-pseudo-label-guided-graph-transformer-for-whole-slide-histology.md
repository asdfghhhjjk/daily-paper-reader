---
title: "WSI-GT: Pseudo-Label Guided Graph Transformer for Whole-Slide Histology"
title_zh: WSI-GT：伪标签引导的图Transformer用于完整切片组织学图像
authors: "Zhongao Sun, Alexander Khvostikov, Andrey Krylov, Ilya Mikhailov, Pavel G. Malkov"
date: 2025-09-19
pdf: "https://openreview.net/pdf?id=Y7kJ4oUgwL"
tags: ["query:profile"]
score: 8.0
evidence: 伪标签引导的图Transformer整合跨块信息用于WSI分类
tldr: WSI-GT结合局部图卷积和伪标签引导注意力机制，在WSI中建模块间空间上下文，通过保持类内差异和减轻过平滑，提升了组织病理学图像分类的准确性，为WSI级任务提供了有效的图学习方法。
source: ICLR-2026-Public
selection_source: conference_retrieval
motivation: 现有方法忽略块间空间上下文或使用深层图模型导致过平滑，损失关键细节。
method: 提出WSI-GT，结合轻量级图卷积块和伪标签引导注意力以聚合邻域特征并缓解过平滑。
result: 在稀疏标注下，WSI-GT在WSI分类任务中性能优于现有方法。
conclusion: WSI-GT通过伪标签引导和图Transformer有效整合跨块信息，改进了WSI分析。
---

## Abstract
Whole-slide histology images (WSIs) can exceed 100k × 100k pixels, making direct pixel-level segmentation infeasible and requiring patch-level classification as a practical alternative. However, most approaches either treat patches independently, ignoring spatial and biological context, or rely on deep graph models that oversmooth, leading to loss of critical tissue details.

We present WSI-GT (Pseudo-Label Guided Graph Transformer), a simple yet effective architecture that addresses these challenges. WSI-GT combines a lightweight local graph convolution block for neighborhood feature aggregation with a pseudo-label guided attention mechanism that preserves intra-class variability and mitigates oversmoothing. To cope with sparse annotations, we introduce an area-weighted sampling strategy that balances class representation while maintaining tissue topology.

WSI-GT achieves a Macro F1 of 0.95 on PATH-DT-MSU WSS2v2, improving by up to 3 percentage points over tile-based CNNs and by about 2 points over strong graph baselines. It further generalizes well to the Placenta benchmark and standard graph node classification datasets, highlighting both clinical relevance and broader applicability. These results position WSI-GT as a practical and scalable solution for graph-based learning on extremely large images.

---

## 论文详细总结（自动生成）

# WSI-GT：伪标签引导的图Transformer用于完整切片组织学图像

## 1. 核心问题与研究动机
- **背景**：全切片组织学图像（WSI）分辨率极高（可超10万×10万像素），直接进行像素级分割不现实，因此常采用基于图像块（patch）的分类。
- **现有局限**：
  - 多数方法将块独立处理，忽略块之间的空间与生物学上下文关系。
  - 部分方法使用深度图模型来建模块间关系，但深层图网络易导致**过平滑（oversmoothing）**，丢失关键组织细节。
- **研究目标**：设计一种既能有效整合跨块空间信息，又能保留类内差异、避免过平滑的WSI分类方法。

## 2. 方法论（WSI-GT）
- **核心思想**：结合轻量局部图卷积与伪标签引导的注意力机制，在保持类内多样性的同时聚合邻域特征。
- **关键技术细节**：
  - **局部图卷积块**：用于邻域特征聚合，提取空间上下文，但保持模型较轻量，避免过深。
  - **伪标签引导注意力**：利用伪标签信息引导注意力计算，使同类别内的块在特征融合时保持差异，降低过平滑风险。
  - **面积加权采样策略**：针对标注稀疏问题，提出基于面积的采样方法，在保持组织拓扑结构的同时平衡类别表示。
- **算法流程**（据摘要推断）：
  1. 将WSI切分为图像块，提取块特征。
  2. 基于空间关系构建图结构。
  3. 局部图卷积聚合邻域信息。
  4. 伪标签引导注意力模块计算块间交互，生成更具判别力的表示。
  5. 最终进行WSI级别分类。

## 3. 实验设计
- **主要数据集**：
  - **PATH-DT-MSU WSS2v2**（组织病理学WSI分类主打基准）
  - **Placenta benchmark**（胎盘组织切片，验证泛化性）
  - **标准图节点分类数据集**（展示方法在图学习任务上的通用性）
- **对比方法**：
  - 基于图像块的CNN方法（tile-based CNNs）
  - 强图模型基线（strong graph baselines）
- **评价指标**：宏平均F1（Macro F1）

## 4. 资源与算力
- 原文**未提供**GPU型号、数量、训练时长等具体算力信息。摘要及元数据中均未提及相关细节。

## 5. 实验数量与充分性
- **实验规模**：至少在3类不同数据集（WSI诊断、胎盘分类、图节点分类）上进行评估，并包含与两类主要基线的对比。
- **消融研究**：摘要未提及具体消融实验，但声称分析了伪标签引导和面积加权采样的作用（需全文确认）。
- **公平性与充分性**：
  - 对比了基于块的CNN和强图基线，覆盖代表性方法。
  - 在稀疏标注条件下进行测试，贴近真实场景。
  - 但摘要未报告交叉验证、统计检验或详细消融，难以从现有信息判断实验的全面性。

## 6. 主要结论与发现
- WSI-GT在PATH-DT-MSU WSS2v2上达到0.95的宏F1，比基于块的CNN**高3个百分点**，比强图基线**高约2个百分点**。
- 在Placenta基准和标准图节点分类任务上也表现良好，证明方法具有**临床相关性**和**广泛适用性**。
- 伪标签引导与轻量图结构有效缓解过平滑，保持类内差异。
- 面积加权采样策略可应对稀疏标注问题。

## 7. 优点与亮点
- **轻量高效**：仅用局部图卷积，避免深层模型带来的过平滑与计算负担。
- **伪标签引导注意力**：创新性地利用伪标签保留类内差异，提升细粒度表征能力。
- **采样策略**：面积加权采样兼顾类别平衡与组织拓扑，贴合实际标注情况。
- **多场景验证**：不仅限于特定WSI任务，还在胎盘组织及标准图数据集上验证，展示通用性。
- **性能提升显著**：在稀疏标注条件下实现较明显增益。

## 8. 不足与局限
- **算力信息缺失**：未说明训练/推理的硬件成本，实用性参考不足。
- **实验细节不透明**：消融研究、交叉验证、统计检验等未在摘要中呈现，严谨性待查。
- **依赖伪标签质量**：伪标签生成方法未详述，若伪标签噪声大可能影响性能。
- **WSI场景受限**：仅在少数病理数据集上测试，未涉及更多癌种或染色类型，泛化性存疑。
- **无实时性分析**：未讨论推理速度或实际部署可行性，临床应用中的延迟不明确。

（完）
