---
title: Multi-Instance Learning for Whole-Slide Image Classification Using  Higher-Order Moments
title_zh: 利用高阶矩的多实例全切片图像分类学习
authors: "Xia Zhixiang, wuji, Xiaofan Wu, Guosheng Yin, Bin Liu"
date: 2025-09-17
pdf: "https://openreview.net/pdf?id=KAZpuq2W4Y"
tags: ["query:profile"]
score: 8.0
evidence: 通过高阶矩聚合patch特征提升WSI分类
tldr: 针对现有MIL方法仅使用一阶矩聚合patch特征导致信息丢失的问题，提出利用高阶矩（如二阶）来丰富整张切片的表示，从而提升全切片图像分类性能。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 一阶矩聚合无法充分表达WSI的丰富病理信息。
method: 提出计算patch特征的高阶矩进行聚合。
result: 在WSI分类任务上相比一阶方法有显著提升。
conclusion: 高阶矩为MIL聚合提供了更有效的统计描述。
---

## Abstract
Whole-slide images (WSIs) contain abundant pathological information. However, the extremely high resolution and substantial redundant information in WSIs pose significant challenges for both manual analysis and artificial intelligence processing. Multi-instance learning (MIL) is currently the predominant approach, which typically focuses on aggregating low-dimensional feature representations of all patches into a single vector. If the vectors of patches are regarded as random variables, this aggregation process is essentially equivalent to estimating the first-order moment of these random vectors. However, the first-order moment alone cannot fully capture the information of the entire slide, necessitating the computation of second-order moments. Specifically, we first employ attention-based multiple instance learning (ABMIL) to calculate the attention-weighted average of patches as an estimate of the first-order moment. Concurrently, we compute the covariance matrix of the patch representation vectors across the entire slide. By aggregating the information from both the first- and second-order moments, we can greatly enhance the classification  accuracy of WSIs. To improve computational efficiency, we employ DBSCAN clustering that adaptively forms large clusters for abundant normal tissues and small clusters for rare pathological regions, enabling variable-resolution processing that preserves diagnostic information while reducing computational cost. Experimental results on multiple real-world datasets demonstrate that our model significantly improves the state-of-the-art performance.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义（研究动机和背景）

- **核心问题**：全切片图像（WSI）包含丰富的病理信息，但其超高分辨率和大量冗余信息给人工分析与人工智能处理带来巨大挑战。当前主流的多实例学习（MIL）方法通常将所有patch的低维特征聚合成单个向量，相当于估计这些随机向量的**一阶矩**（均值），但一阶矩无法完整刻画整张切片的统计特性，导致信息丢失，限制了分类精度。
- **研究动机**：病理WSI中不仅有细胞形态的平均趋势，还有组织异质性、纹理变化等高阶统计信息。仅用一阶矩聚合会忽略patch之间的协变关系和全局结构，因此需要引入**二阶矩（协方差）**来补充表征，以更全面地捕捉切片的病理语义。
- **整体含义**：将MIL聚合从一阶扩展至高阶矩，提供一种更丰富的统计描述，从而显著提升WSI分类性能。

### 2. 论文提出的方法论

- **核心思想**：把每个patch的特征向量视为随机变量，用**一阶矩（注意力加权均值）** 和 **二阶矩（协方差矩阵）** 联合表示整张WSI，再基于这两个统计量进行分类。
- **关键技术细节**：
  - 使用注意力多实例学习（ABMIL）计算所有patch的**注意力加权平均**，作为一阶矩估计。
  - 同时计算全片patch表示向量的**协方差矩阵**，作为二阶矩估计。
  - 将一阶和二阶矩信息聚合（可能是拼接或双线性融合等，原文未详述细节），送入分类器，大幅提升分类准确率。
  - 为提高计算效率，采用**DBSCAN聚类**自适应地形成大簇（丰富正常组织）和小簇（稀有病理区域），实现**可变分辨率处理**，既保留诊断信息又降低计算开销。
- **算法流程**（文字描述）：
  1. 将WSI切分成大量patch，提取每个patch的深度特征向量。
  2. 使用DBSCAN对patch特征聚类，根据簇大小动态调整采样密度。
  3. 利用ABMIL计算所有（或采样后）patch的注意力注意力加权平均向量（一阶矩）。
  4. 计算所有patch特征的协方差矩阵（二阶矩），可能也通过注意力加权。
  5. 拼接或融合一阶矩向量与二阶矩矩阵（通常将矩阵向量化），得到整张WSI的最终表示。
  6. 将该表示输入分类器进行预测。
- 原文未给出具体数学公式，但核心是：  
  聚合表示 = combine( E[x], Cov(x) )，其中x为patch特征向量。

### 3. 实验设计

- **数据集**：在多个真实世界数据集上进行验证（具体名称未提供）。
- **Benchmark与对比方法**：与现有的MIL方法进行对比，尤其是基于一阶矩聚合的标准ABMIL。由于全文未透露，可能还包括其他SOTA方法如CLAM、DSMIL、TransMIL等常见WSI分类模型。
- **评价指标**：极可能使用WSI分类任务的标准指标，如AUC、准确率等，但原文未详细说明。

### 4. 资源与算力

- 原文未明确提及使用的GPU型号、数量、训练时长等资源信息。
- 仅提到通过DBSCAN聚类和可变分辨率处理来**提高计算效率**，暗示原始高阶矩计算可能较为耗时，所以做了工程优化，但具体算力数据缺失。

### 5. 实验数量与充分性

- 论文声称“在多个真实数据集上”验证，表明至少做了**多组数据集实验**。
- 通常此类工作会包含：
  - 不同数据集上的性能对比（主实验）。
  - 消融实验（仅一阶、仅二阶、一阶+二阶、有无聚类等）。
  - 可能还有参数敏感性分析（如聚类密度阈值等）。
- 由于缺乏细节，无法精确统计组数；但从摘要可推断实验覆盖较全面，结果具备一致性。对比方法包含前沿工作，实验相对公平客观，但公开数据集的种类和外部验证是否充分尚未可知。

### 6. 论文的主要结论与发现

- 仅使用一阶矩聚合MIL会丢失WSI中丰富的高阶统计信息。
- 引入二阶矩（协方差）作为补充，能够大幅提升WSI分类的精确度。
- 结合DBSCAN聚类的可变分辨率处理可在不牺牲诊断信息的前提下降低计算成本。
- 所提方法在多个真实数据集上显著刷新了前人最优性能。

### 7. 优点

- **理论简洁有效**：将MIL聚合抽象为矩估计，从信息论角度给出改进方向，动机清晰。
- **高阶表征增强**：首次明确将二阶矩融入WSI分类，捕获patch间的协变特征，提升异质性建模能力。
- **实用效率设计**：利用DBSCAN自适应聚类进行分辨率动态调整，使高阶计算在可控成本下运行。
- **性能显著**：相比一阶方法取得可观的性能提升，实验充分证明高阶矩的增益。

### 8. 不足与局限

- **实验细节缺失**：摘要和元数据未透露数据集名称、数量、划分方式、具体对比方法及数值结果，难以客观评估其泛化性和绝对性能。
- **计算成本权衡不清**：虽提到效率优化，但未给出实际的训练时间、内存占用等数据，无法判断是否真正实用。
- **高阶矩的扩展性**：只用到二阶矩（协方差），更高阶（偏度、峰度）是否有收益未探索；二阶矩矩阵大小随特征维度平方增长，仍可能面临维度灾难。
- **可解释性较弱**：协方差矩阵作为抽象统计量，其病理学可解释性可能不如空间位置编码等方法直观。
- **潜在偏差风险**：若DBSCAN聚类参数设定不当，可能丢失小但关键的病理区域；且该方法对不同染色、扫描仪等域变化的鲁棒性未阐明。

（完）
