---
title: Multi-Instance Learning for Whole-Slide Image Classification Using  Higher-Order Moments
title_zh: 基于高阶矩的多实例学习实现全切片图像分类
authors: "Xia Zhixiang, wuji, Xiaofan Wu, Guosheng Yin, Bin Liu"
date: 2025-09-17
pdf: "https://openreview.net/pdf?id=KAZpuq2W4Y"
tags: ["query:path-xai-sel"]
score: 6.0
evidence: 利用高阶矩改进多实例学习以提升全切片分类
tldr: 针对全切片图像分类中一阶矩聚合信息有限的问题，提出使用高阶矩进行多实例学习，更充分地表征整张切片特征，提升分类性能。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 传统MIL仅利用一阶矩，无法完整捕捉切片信息。
method: 计算并聚合补丁特征的高阶矩，如二阶矩以丰富全局表示。
result: 在多个WSI分类任务上优于标准MIL方法。
conclusion: 高阶矩聚合为WSI分类提供了更全面的特征抽取方案。
---

## Abstract
Whole-slide images (WSIs) contain abundant pathological information. However, the extremely high resolution and substantial redundant information in WSIs pose significant challenges for both manual analysis and artificial intelligence processing. Multi-instance learning (MIL) is currently the predominant approach, which typically focuses on aggregating low-dimensional feature representations of all patches into a single vector. If the vectors of patches are regarded as random variables, this aggregation process is essentially equivalent to estimating the first-order moment of these random vectors. However, the first-order moment alone cannot fully capture the information of the entire slide, necessitating the computation of second-order moments. Specifically, we first employ attention-based multiple instance learning (ABMIL) to calculate the attention-weighted average of patches as an estimate of the first-order moment. Concurrently, we compute the covariance matrix of the patch representation vectors across the entire slide. By aggregating the information from both the first- and second-order moments, we can greatly enhance the classification  accuracy of WSIs. To improve computational efficiency, we employ DBSCAN clustering that adaptively forms large clusters for abundant normal tissues and small clusters for rare pathological regions, enabling variable-resolution processing that preserves diagnostic information while reducing computational cost. Experimental results on multiple real-world datasets demonstrate that our model significantly improves the state-of-the-art performance.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义（研究动机和背景）

- **核心问题**：全切片图像（WSI）分类中，现有多实例学习（MIL）方法通常将大量图像块（patches）的低维特征聚合为单一向量，该过程本质上是对随机向量的一阶矩估计，无法充分捕捉整张切片的完整信息，限制了分类性能。
- **研究动机**：WSI 包含丰富病理信息，但极高分辨率和大量冗余信息给人工分析与AI处理带来挑战。MIL 是主流方法，但仅利用一阶矩（均值）会丢失分布的高阶特性，因此需要引入更高阶统计量，如二阶矩，以更全面地表示切片级特征。
- **整体含义**：论文提出通过融合一阶矩（注意力加权均值）和二阶矩（协方差矩阵）来增强 WSI 分类，同时采用自适应聚类提升计算效率，在多个真实数据集上取得性能提升。

### 2. 论文提出的方法论

- **核心思想**：将图像块的特征向量视为随机变量，在传统一阶矩聚合的基础上，引入二阶矩（协方差矩阵）来捕捉特征间的相关性与全局分布信息，从而形成更丰富的切片级表示。
- **技术细节与流程**：
  - 使用基于注意力的多实例学习（ABMIL）获得所有图像块的注意力加权平均向量，作为一阶矩的估计。
  - 同时计算整张切片中所有图像块特征向量的协方差矩阵，作为二阶矩。
  - 将一阶矩和二阶矩信息联合聚合，用于最终的 WSI 分类。
- **计算效率优化**：
  - 采用 DBSCAN 聚类对图像块进行自适应分组，对富含正常组织的大区域形成大簇，对稀有病理区域形成小簇，实现变分辨率处理，在保留诊断信息的同时降低计算开销。

### 3. 实验设计

- **数据集/场景**：多个真实世界的 WSI 数据集（摘要中未具体列出名称，原文可能包含TCGA等癌症数据集）。
- **Benchmark 与对比方法**：以标准的多实例学习（尤其是一阶矩聚合的方法）作为对比基准，文中未展开具体方法名称，但从摘要可推测对比了仅使用一阶矩的 ABMIL 等。
- **评估任务**：WSI 分类性能（准确率等指标）。

### 4. 资源与算力

- **算力描述**：提供的摘要与元数据中**未提及**使用的 GPU 型号、数量或训练时长。DBSCAN 聚类的引入暗示了对效率的考虑，但具体硬件资源详情缺失。

### 5. 实验数量与充分性

- **实验数量**：基于现有信息，至少覆盖了“多个真实世界数据集”，并声称与现有方法进行了对比且性能有显著提升，但具体实验组数（如不同癌症类型、不同分辨率的消融实验）在摘要中未详细列出。
- **充分性评估**：摘要提到“实验结果表明模型显著提高了最先进性能”，表明实验具备一定说服力，但无法判断是否包含充分的消融研究（如仅用二阶矩、不同聚类策略的影响等），需结合正文内容进一步确认。从摘要来看，实验是客观公平的，因为其对比的是标准基准。

### 6. 论文的主要结论与发现

- 传统 MIL 仅用一阶矩不足以捕获切片全部信息。
- 融合一阶矩（均值）和二阶矩（协方差）能极大增强 WSI 分类精度。
- 结合 DBSCAN 的自适应聚类可在保持诊断信息的前提下有效降低计算成本。
- 在多个真实数据集上达到优于现有方法的（state-of-the-art）性能。

### 7. 优点

- **方法论创新**：将高阶矩（二阶）引入 MIL 聚合，从统计视角弥补了信息损失，思路清晰且有理论依据。
- **效率设计**：通过自适应聚类实现变分辨率处理，平衡了诊断准确性与计算成本，实用性强。
- **性能提升显著**：实验证明在多个真实数据集上有效改进。

### 8. 不足与局限

- **实验细节缺失**：摘要未透露具体数据集名称、对比方法列表、评价指标详细数值等，难以评估其在不同组织类型上的泛化性。
- **计算开销**：虽然提出聚类降本，但协方差矩阵的计算本身在大规模图像块上仍可能成为瓶颈，且未给出具体时间或资源消耗数据。
- **应用限制**：仅针对 WSI 分类问题，且依赖注意力机制获得加权平均，注意力的可解释性可能被高阶矩稀释，尚未讨论。
- **偏差风险**：若聚类效果依赖于特定病理形态（如大块正常区域），对于弥漫性病变或肿块型肿瘤的适应性未论证。

（完）
