---
title: "HiST: Spatial Transcriptomics Prediction via Multi-Level Hyperbolic Representation Learning"
title_zh: HiST：通过多层双曲表示学习的空间转录组学预测
authors: "Chen Zhang, Yilu An, Ying Chen, Hao Li, Xitong Ling, Lihao Liu, Junjun He, Yuxiang Lin, Zihui Wang, Rongshan Yu"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=A9sAYUD3XB"
tags: ["query:path-xai-sel"]
score: 4.0
evidence: 使用组织学图像进行基因表达预测的计算病理学方法
tldr: 现有从组织学图像预测基因表达的方法未充分利用空间转录组数据的层次结构，且存在信息不对称问题。HiST提出多层双曲表示学习，在双曲空间中同时对齐图像与基因表达的层次特征，缓解信息不对称，实现更准确的基因表达预测。实验验证了该方法在多个数据集上的有效性。
source: ICLR-2026-Public
selection_source: conference_retrieval
motivation: 现有方法忽略ST数据层次结构，图像与基因信息不对称。
method: 提出多层双曲表示学习机制进行层次对齐。
result: 在多个数据集上实现更准确的基因表达预测。
conclusion: HiST有效利用层次结构，提升预测性能。
---

## Abstract
Spatial Transcriptomics (ST) merges the benefits of pathology images and gene expression, linking molecular profiles with tissue structure to analyze spot-level function comprehensively.
Predicting gene expression from histology images is a cost-effective alternative to expensive ST technologies.
However, existing methods mainly focus on spot-level image-to-gene matching but fail to leverage the full hierarchical structure of ST data, especially on the gene expression side, leading to incomplete image-gene alignment.
Moreover, a challenge arises from the inherent information asymmetry: gene expression profiles contain more molecular details that may lack salient visual correlates in histological images, demanding a sophisticated representation learning approach to bridge this modality gap.
We propose HiST, a framework for ST prediction that learns multi-level image-gene representations by modeling the data's inherent hierarchy within hyperbolic space, a natural geometric setting for such structures.
First, we design a Multi-Level Representation Extractor to capture both spot-level and niche-level representations from each modality, providing context-aware information beyond individual spot-level image-gene pairs.
Second, a Hierarchical Hyperbolic Alignment module is introduced to unify these representations, performing spatial alignment while hierarchically structuring image and gene embeddings.
This alignment strategy enriches the image representations with molecular semantics, significantly improving cross-modal prediction.
HiST achieves state-of-the-art performance on three public datasets from different tissues, paving the way for more scalable and accurate spatial transcriptomics prediction.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义
- **研究背景**：空间转录组学（ST）将组织病理图像与基因表达谱结合，可原位分析组织微环境中的分子功能。然而，ST 实验成本高昂，因此从组织学图像直接预测基因表达成为一种经济高效的替代方案。
- **核心问题**：现有方法主要聚焦于**斑点级（spot-level）** 的图像–基因匹配，**忽略了 ST 数据天然的层次结构**（如基因共表达模块、微环境生态位等），造成图像与基因之间的对齐不完整。同时，两种模态存在**信息不对称**：基因表达包含丰富的分子细节，但其中许多信息在组织学图像中缺乏明显的视觉对应物，导致跨模态预测困难。
- **整体含义**：提出 HiST 框架，在双曲空间中建模数据层次结构，通过多层次对齐缓解信息不对称，实现更准确的从图像到基因的预测。

### 2. 论文提出的方法论
- **核心思想**：将组织学图像与基因表达数据同时映射到**双曲空间**，利用双曲几何天然支持层次表示的特性，对齐两种模态的层次结构（斑点级与微环境生态位级）。
- **关键模块**：
  - **多层次表示提取器（Multi-Level Representation Extractor）**：对图像和基因分别提取两个层次的表示：
    - **斑点级**：单一测序位置（spot）的局部特征。
    - **生态位级（niche-level）**：包含周围组织上下文的区域特征，超越单个 spot 的图像-基因配对。
  - **层级化双曲对齐模块（Hierarchical Hyperbolic Alignment）**：将提取的多层次图像和基因嵌入统一到双曲空间，在层次结构中进行空间对齐。该策略将分子语义注入图像表示，从而显著提升跨模态预测性能。
- **技术路线**（基于摘要推断，具体公式未提供）：提取多层次特征 → 映射到双曲流形 → 层级结构对齐损失函数约束 → 最终通过解码器预测基因表达。

### 3. 实验设计
- **数据集**：在**三种不同组织**的公开 ST 数据集上进行评估（具体数据集名称未在摘要中列出）。
- **基准任务**：从组织学图像预测基因表达（图像→基因）。
- **对比方法**：与现有的 ST 预测方法进行了比较（未列出具体方法名），HiST 取得了最先进性能（state-of-the-art）。
- **评价指标**：未在摘要中具体说明，通常为预测基因表达值与真实值的相关系数（如 PCC）或均方误差等。

### 4. 资源与算力
- **未明确说明**：摘要和元数据中**均未提及**使用的 GPU 型号、数量、训练时长或具体算力消耗。需要查阅全文才能获知。

### 5. 实验数量与充分性
- **实验组数**：基于摘要，至少包含：
  - 在 3 个不同组织数据集上的主实验（与现有方法对比）。
  - 消融实验（验证多层次表示和双曲对齐模块的必要性，虽摘要未展开，但属于惯例）。
- **充分性与公平性**：
  - **充分性**：多组织、多数据集的验证表明实验具备一定的泛化性评估；消融实验若完整，则能支撑模块有效性。
  - **公平性**：提到“state-of-the-art performance”，暗示采用统一的数据划分与评价标准与公开基线对比，但摘要未给出具体公平性保障细节（如同一数据预处理、超参搜索等）。

### 6. 论文的主要结论与发现
- HiST 通过**多层次双曲表示学习**，有效捕获了 ST 数据从斑点到生态位的层次结构，克服了图像–基因信息不对称。
- 提出的**层级化双曲对齐**将分子语义成功融入视觉表示，显著提升了基因表达预测精度。
- 在多个不同组织数据集上取得最优性能，证明了方法的有效性和泛化能力。
- 为更可扩展、更准确的空间转录组学预测铺平了道路。

### 7. 优点
- **几何适配性**：利用双曲空间天然表征层次结构，与 ST 数据的内在嵌套特性（分子→细胞→组织）高度吻合。
- **多层级建模**：显式提取并对齐斑点和生态位级特征，提供上下文感知的跨模态交互，超越了传统单点对齐的范式。
- **信息不对称缓解**：通过层次对齐将分子语义注入图像嵌入，为弱监督/不对称模态对齐提供了新思路。
- **性能优势**：在多个数据集上达到最优，展现了方法的鲁棒性。

### 8. 不足与局限
- **实验细节缺失**：摘要未提供数据集规模、具体对比方法、算力需求等关键可复现信息。
- **偏差风险**：仅在三类组织上测试，未知在其他器官或罕见疾病组织上的表现；若所选数据集均为公开常用数据，可能过度拟合社区基准。
- **应用限制**：仍依赖配对的图像–基因表达数据进行训练，未探索真正无监督或弱标注场景（如无配对 ST 数据时）。
- **模型复杂性**：多层表征提取和双曲空间运算可能增加计算开销，摘要未讨论效率问题。
- **未验证下游任务**：仅评估基因表达预测准确性，未展示预测的基因表达是否能提升下游分析（如细胞类型注释、通路分析等），影响实际应用说服力。

（完）
