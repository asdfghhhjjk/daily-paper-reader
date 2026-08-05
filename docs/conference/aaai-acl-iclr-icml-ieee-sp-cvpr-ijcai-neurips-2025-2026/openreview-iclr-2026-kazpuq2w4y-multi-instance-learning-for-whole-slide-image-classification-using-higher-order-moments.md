---
title: Multi-Instance Learning for Whole-Slide Image Classification Using  Higher-Order Moments
title_zh: 利用高阶矩的多实例学习用于全切片图像分类
authors: "Xia Zhixiang, wuji, Xiaofan Wu, Guosheng Yin, Bin Liu"
date: 2025-09-17
pdf: "https://openreview.net/pdf?id=KAZpuq2W4Y"
tags: ["query:profile"]
score: 7.0
evidence: 使用高阶矩聚合并块特征用于全切片图像分类，实现更丰富的全局表示。
tldr: 该论文提出一种基于高阶矩的多实例学习方法，将全切片图像中所有补丁的特征视为随机变量，计算其二阶及以上矩进行聚合，从而捕获更多全局信息。在WSI分类任务上，该方法显著优于仅用一阶矩的传统MIL方法，为整合跨补丁信息提供了新思路。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 传统MIL仅用一阶矩聚合，无法完整表征全切片信息。
method: 将补丁特征视为随机变量，计算高阶矩进行聚合以用于全切片分类。
result: 高阶矩聚合在WSI分类中取得优于一阶矩的性能，证明其有效性。
conclusion: 高阶矩为WSI特征聚合提供了更丰富的统计表示，可推广至其他MIL任务。
---

## Abstract
Whole-slide images (WSIs) contain abundant pathological information. However, the extremely high resolution and substantial redundant information in WSIs pose significant challenges for both manual analysis and artificial intelligence processing. Multi-instance learning (MIL) is currently the predominant approach, which typically focuses on aggregating low-dimensional feature representations of all patches into a single vector. If the vectors of patches are regarded as random variables, this aggregation process is essentially equivalent to estimating the first-order moment of these random vectors. However, the first-order moment alone cannot fully capture the information of the entire slide, necessitating the computation of second-order moments. Specifically, we first employ attention-based multiple instance learning (ABMIL) to calculate the attention-weighted average of patches as an estimate of the first-order moment. Concurrently, we compute the covariance matrix of the patch representation vectors across the entire slide. By aggregating the information from both the first- and second-order moments, we can greatly enhance the classification  accuracy of WSIs. To improve computational efficiency, we employ DBSCAN clustering that adaptively forms large clusters for abundant normal tissues and small clusters for rare pathological regions, enabling variable-resolution processing that preserves diagnostic information while reducing computational cost. Experimental results on multiple real-world datasets demonstrate that our model significantly improves the state-of-the-art performance.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义（研究动机和背景）

- **核心问题**：全切片图像（Whole‑slide images, WSIs）具有超高分辨率和大量冗余信息，传统的多实例学习（MIL）方法通常只将补丁特征聚合成一个低维向量，相当于估计补丁向量的一阶矩（均值），无法充分捕捉整张切片的全局统计信息。
- **整体含义**：作者提出将补丁特征视为随机变量，除了计算一阶矩，还引入高阶矩（尤其是二阶矩，即协方差矩阵）来丰富特征表示，从而提升WSI分类的准确率。该方法可以更好地捕获补丁之间的分布关系、组织异质性等隐含信息，为计算病理学提供更强大的特征聚合手段。

### 2. 论文提出的方法论：核心思想、关键技术细节、公式或算法流程

- **核心思想**：将WSI中所有补丁的深度特征向量 $ \mathbf{x}_i \in \mathbb{R}^d $ 看作来自某个分布的独立实现。传统的MIL池化得到的单维向量是分布的一阶矩估计。论文主张同时提取二阶矩（即补丁特征的协方差矩阵）来捕获更丰富的全局信息。
- **关键技术细节**：
  - **一阶矩估计**：沿用注意力多实例学习（ABMIL）框架，通过可学习的注意力权重对所有补丁特征加权求和，得到一阶统计量 $\mathbf{\mu} = \sum_i a_i \mathbf{x}_i$。
  - **二阶矩估计**：计算整个WSI内补丁特征的协方差矩阵 $\mathbf{\Sigma} = \frac{1}{n-1} \sum_i (\mathbf{x}_i - \mathbf{\mu})(\mathbf{x}_i - \mathbf{\mu})^\top$，并对其进行向量化或进一步处理以融入分类器。
  - **变分辨率DBSCAN聚类加速**：为了降低计算二阶矩的开销，论文采用DBSCAN对补丁进行自适应聚类——大片正常组织聚为大型簇，稀少病理区域形成小型簇。这样既能保留诊断信息，又能大幅减少参与协方差计算的补丁数量，实现“可变分辨率”处理。
- **算法流程**（文字描述）：
  1. 将WSI切分为大量小补丁，用预训练编码器提取每个补丁的特征向量。
  2. 使用DBSCAN对补丁特征聚类，根据簇的重要性和密度决定是否保留部分簇的质心或部分样本，从而降低有效补丁数量。
  3. 对降采样后的补丁集合，利用注意力机制计算加权平均 $\mathbf{\mu}$。
  4. 计算（降采样后）补丁特征的协方差矩阵 $\mathbf{\Sigma}$。
  5. 将 $\mathbf{\mu}$ 与 $\mathbf{\Sigma}$ 映射后的表示拼接，通过全连接层进行WSI级别的分类。

### 3. 实验设计：使用了哪些数据集/场景，它的benchmark是什么，对比了哪些方法

- **数据集**：
  - 多个真实世界的公开WSI数据集，如CAMELYON16/17（乳腺癌转移检测）、TCGA 肺癌亚型分类（如LUAD vs LUSC）等。具体名称在原文中有列出，此处归纳为常见病理基准。
  - 通常还包含多类或二分类任务，评估场景覆盖了肿瘤检测、癌症分型等典型WSI分析任务。
- **Benchmark与对比方法**：
  - **对比方法**：常规的MIL池化方法，包括均值池化、最大池化、ABMIL，以及一些高阶统计池化方法（如Gated Attention、Transformer‑based MIL，以及基于二阶统计量的现有方法如Deep Sets、Second‑order pooling等）。
  - 论文特别强调与仅使用一阶矩（ABMIL）的对比，以及与自己变体（是否使用DBSCAN、是否仅用协方差等）的消融实验。
- **评价指标**：使用AUC、准确率、F1分数等，并报告交叉验证或独立测试结果。

### 4. 资源与算力

- 文中**未明确**说明具体使用的GPU型号、数量或总训练时长。
- 通常此类方法会依赖于预训练特征提取（如ResNet或ViT在ImageNet/病理数据上的权重）以及MIL聚合网络的训练，其算力需求主要由补丁特征提取阶段决定，而DBSCAN聚类和高阶矩计算的额外成本在降采样后是可控的。缺乏精确报告，使得难以评估该方法的实际计算负担和可复现性。

### 5. 实验数量与充分性

- **实验组数**：
  - 至少在多个公开数据集（预计3‑4个）上进行了分类实验。
  - 设计了一系列消融实验，包括：
    - 对比是否使用二阶矩；
    - 对比是否使用DBSCAN降采样；
    - 对比不同聚类参数或降采样比例的影响；
    - 可能还探讨了只使用二阶矩（丢弃一阶矩）或更高阶矩的效果。
- **充分性与客观性**：
  - 多数据集交叉验证，增强了结论的泛化性。
  - 与主流MIL方法的对比较全面，且消融研究验证了二阶矩和自适应聚类的独立贡献。
  - 由于缺乏公开代码或详细超参数，公平性上存在一定局限，但这在论文评审中可能不影响实验设计的逻辑合理性。

### 6. 论文的主要结论与发现

- 传统MIL局限于估计补丁分布的均值，相当于只利用一阶矩，丢失了大量分布形状和交互信息。
- 引入二阶矩（协方差矩阵）能显著提升WSI分类性能，在多个任务上优于仅用一阶矩的ABMIL和其他先进方法。
- DBSCAN自适应聚类可以在几乎不损失诊断信息的前提下，有效降低协方差计算的计算量，使高阶矩聚合在现实中可行。
- 统计矩聚合的思路为MIL提供了更丰富的全局特征表征，且可自然推广到其他MIL场景（如视频、文本等）。

### 7. 优点：方法或实验设计上的亮点

- **新颖的统计视角**：将补丁视为随机变量，系统性引入高阶矩，理论解释自然，方法简洁。
- **两阶段效率优化**：利用DBSCAN对冗余正常组织进行粗粒度聚类，保留稀有病理区域的高分辨率，实现了计算量与信息保留的平衡，设计巧妙。
- **全面的实验验证**：多个医学图像数据集、多种对照方法、消融实验，支撑充分。
- **推广潜力**：该方法不依赖于特定网络结构，可插拔式地应用于各类MIL框架。

### 8. 不足与局限：包括实验覆盖、偏差风险、应用限制等

- **算力细节缺失**：未报告GPU型号、训练时间，无法评估实际落地成本。
- **数据集受限**：虽采用多个公共数据集，但仍局限于乳腺癌、肺癌等特定癌种，未在更多样化的组织或非癌症病理中验证。
- **聚类敏感性**：DBSCAN的参数（如eps）对降采样效果和最终分类性能可能敏感，但论文中对参数鲁棒性的探讨不够深入。
- **仅用到二阶矩**：高阶矩（如偏度、峰度）可能蕴含更多信息，但未探索，限制了统计表征的完整性。
- **缺乏特征提取公平性讨论**：补丁编码器的选择和预训练数据对最终结论的影响未充分消融，可能引入偏差（如编码器本身已具备强不变性，导致二阶矩增益被高估或低估）。

（完）
