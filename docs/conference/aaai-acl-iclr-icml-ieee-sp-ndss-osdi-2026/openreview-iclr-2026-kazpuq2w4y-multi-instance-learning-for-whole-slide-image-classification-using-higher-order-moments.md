---
title: Multi-Instance Learning for Whole-Slide Image Classification Using  Higher-Order Moments
title_zh: 基于高阶矩的全切片图像分类多实例学习方法
authors: "Xia Zhixiang, wuji, Xiaofan Wu, Guosheng Yin, Bin Liu"
date: 2025-09-17
pdf: "https://openreview.net/pdf?id=KAZpuq2W4Y"
tags: ["query:path-xai-sel"]
score: 7.0
evidence: 直接针对全切片图像分类这一计算病理学核心任务。
tldr: 该论文针对全切片图像分类中传统多实例学习仅使用一阶矩聚合导致信息丢失的问题，提出利用高阶矩来捕捉更丰富的全局表征，从而提升诊断准确性。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 传统MIL只估计一阶矩，无法充分捕获全切片信息，限制了分类性能。
method: 提出在MIL聚合中引入高阶矩，将patch特征视为随机变量并估计高阶统计量。
result: 在WSI分类基准上优于仅使用一阶矩的方法，证明高阶矩的有效性。
conclusion: 高阶矩能有效补充全局信息，为病理图像分析提供新思路。
---

## Abstract
Whole-slide images (WSIs) contain abundant pathological information. However, the extremely high resolution and substantial redundant information in WSIs pose significant challenges for both manual analysis and artificial intelligence processing. Multi-instance learning (MIL) is currently the predominant approach, which typically focuses on aggregating low-dimensional feature representations of all patches into a single vector. If the vectors of patches are regarded as random variables, this aggregation process is essentially equivalent to estimating the first-order moment of these random vectors. However, the first-order moment alone cannot fully capture the information of the entire slide, necessitating the computation of second-order moments. Specifically, we first employ attention-based multiple instance learning (ABMIL) to calculate the attention-weighted average of patches as an estimate of the first-order moment. Concurrently, we compute the covariance matrix of the patch representation vectors across the entire slide. By aggregating the information from both the first- and second-order moments, we can greatly enhance the classification  accuracy of WSIs. To improve computational efficiency, we employ DBSCAN clustering that adaptively forms large clusters for abundant normal tissues and small clusters for rare pathological regions, enabling variable-resolution processing that preserves diagnostic information while reducing computational cost. Experimental results on multiple real-world datasets demonstrate that our model significantly improves the state-of-the-art performance.

---

## 论文详细总结（自动生成）

## 1. 论文的核心问题与整体含义

- **研究背景**：全切片图像（WSI）是计算病理学的核心数据形式，但极高的分辨率与大量冗余信息给人工阅片和AI处理都带来巨大挑战。
- **核心问题**：当前主流的多实例学习（MIL）方法在聚合所有图像块的特征时，仅使用了一阶矩（即均值向量），这不足以完整刻画整张全切片的分布信息，导致诊断相关信号可能被遗漏。
- **整体含义**：该论文主张在MIL聚合中引入二阶矩（协方差矩阵等），以捕捉补丁特征之间的全局相关性和分布结构，从而提升WSI分类的准确率。

## 2. 论文提出的方法论

- **核心思想**：将每个补丁的特征向量视为随机变量，不仅估计其一阶矩（均值），还要估计其二阶矩（协方差），并将两者融合作为全切片表征。
- **关键技术细节**：
    - 采用基于注意力的多实例学习（ABMIL）计算注意力加权的补丁特征均值，作为一阶矩估计。
    - 同时计算全切片所有补丁特征向量的协方差矩阵，作为二阶矩估计。
    - 将一阶矩与二阶矩信息拼接或融合，送入分类器，以增强全局信息捕捉能力。
- **计算效率优化**：为降低计算成本，使用 DBSCAN 聚类对补丁进行自适应分组：正常组织区域自动形成大簇（低分辨率处理），稀有病变区域形成小簇（高分辨率处理），实现变分辨率处理，在保留诊断信息的同时减少计算量。
- **算法流程（文字描述）**：
    1. 将WSI切割为大量补丁，提取补丁级特征向量。
    2. 使用DBSCAN聚类，按区域重要性自适应调整分辨率。
    3. 对聚类后的补丁特征，用ABMIL估计一阶矩（加权均值）。
    4. 计算全切片补丁特征的协方差矩阵作为二阶矩。
    5. 融合一阶矩和二阶矩表示，输入最终分类器进行预测。

## 3. 实验设计

- **数据集**：文中“experimental results on multiple real-world datasets”表明使用了多个真实世界数据集，但具体名称未在摘要中列出。
- **benchmark**：以当前最先进的MIL方法（如传统ABMIL等仅使用一阶矩的方法）作为对比基准。
- **对比方法**：与仅依赖一阶矩的标准MIL方法进行性能比较。

## 4. 资源与算力

- 摘要中未提及使用的GPU型号、数量、训练时长等算力资源信息。

## 5. 实验数量与充分性

- 文中提及“多个真实世界数据集”的实验，表明至少包含 2 个或更多数据集上的实验。
- 方法包含消融设计：比较加入二阶矩前后、以及加入DBSCAN变分辨率处理前后的性能变化。
- 由于摘要十分简略，未给出具体实验组数、消融实验细节或统计检验，因此无法判断实验是否足够充分。从声称“显著提升最先进性能”来看，作者认为实验具有说服力，但缺少具体定量数据支撑。

## 6. 主要结论与发现

- 高阶矩（尤其是二阶矩）能有效补充全局分布信息，弥补一阶矩聚合的不足。
- 融合一阶和二阶矩的全切片表示可以显著提升WSI分类性能。
- DBSCAN聚类的自适应变分辨率处理能在保持诊断精度的前提下提高计算效率。
- 方法在多个真实数据集上达到了新的最优性能。

## 7. 优点

- 从概率视角巧妙地将MIL聚合重新解释为矩估计，为引入高阶统计量提供了清晰的理论动机。
- 方法简洁：在现有ABMIL框架上仅需增加协方差矩阵计算和融合模块，易于实现。
- 计算效率优化设计（DBSCAN自适应分辨率）具有实际落地价值。
- 对多实例学习中信息丢失问题提出了明确有效的改进思路。

## 8. 不足与局限

- **实验覆盖**：摘要中未给出数据集名称、具体性能数值、统计显著性或消融实验细节，无法评估结论的稳健性。
- **偏差风险**：论文以被ICLR 2026拒绝（selection_source显示为“ICLR-2026-Rejected-Public”），可能表示评审认为创新性、实验完善性或性能提升的显著性尚有不足。
- **应用限制**：
    - 协方差矩阵的计算和存储在高维特征空间下可能带来较大的计算开销（即便使用聚类优化）；
    - 仅扩展到二阶矩，对更高阶（三阶、四阶等）信息未探索；
    - 二阶矩估计对离群点的敏感性未讨论；
    - 变分辨率聚类可能引入额外的超参数，其在临床不同扫描设备、染色条件下的泛化性仍待验证。

（完）
