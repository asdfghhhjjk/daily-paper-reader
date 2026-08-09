---
title: "Disco: Densely-overlapping Cell Instance Segmentation via Adjacency-aware Collaborative Coloring"
title_zh: "Disco: 通过邻接感知协作着色的密集重叠细胞实例分割"
authors: "Rui Sun, Yiwen Yang, Kaiyu Guo, Chen Jiang, Dongli Xu, Zhaonan Liu, Tan Pan, LIMEI HAN, Xue Jiang, Wu Wei, Yuan Cheng"
date: 2026-01-26
pdf: "https://openreview.net/pdf?id=1W7RRQl3lH"
tags: ["query:immuno-topo"]
score: 9.0
evidence: "提出基于图着色的细胞实例分割方法，可处理密集重叠细胞核，适用于H&E数字病理分析"
tldr: 针对数字病理中密集重叠细胞核的分割难题，Disco提出基于邻接感知协同着色的实例分割方法，通过分析细胞邻接图色性特征实现高精度分割。在多个数据集上验证了其有效性，并贡献了高复杂度细胞核数据集GBC-FS 2025，为下游分析提供了可靠基础。
source: ICLR-2026-Accepted
selection_source: conference_retrieval
motivation: 现有细胞实例分割方法在处理密集重叠区域时仍面临挑战，缺乏对复杂拓扑的验证。
method: 提出Disco，一种基于邻接感知协同着色的细胞实例分割方法，利用图着色范式。
result: 在四个数据集上的系统分析揭示了细胞邻接图的色性特征，Disco在密集重叠场景下取得优异分割性能。
conclusion: Disco为数字病理中的细胞分割提供了新范式，有望提升下游任务如免疫微环境分析的准确性。
---

## Abstract
Accurate cell instance segmentation is foundational for digital pathology analysis. Existing methods based on contour detection and distance mapping still face significant challenges in processing complex and dense cellular regions. Graph coloring-based methods provide a new paradigm for this task, yet the effectiveness of this paradigm in real-world scenarios with dense overlaps and complex topologies has not been verified. Addressing this issue, we release a large-scale dataset GBC-FS 2025, which contains highly complex and dense sub-cellular nuclear arrangements. We conduct the first systematic analysis of the chromatic properties of cell adjacency graphs across four diverse datasets and reveal an important discovery: most real-world cell graphs are non-bipartite, with a high prevalence of odd-length cycles (predominantly triangles). This makes simple 2-coloring theory insufficient for handling complex tissues, while higher-chromaticity models would cause representational redundancy and optimization difficulties. Building on this observation of complex real-world contexts, we propose Disco (Densely-overlapping Cell Instance Segmentation via Adjacency-aware Collaborative Coloring), an adjacency-aware framework based on the “divide and conquer” principle. It uniquely combines a data-driven topological labeling strategy with a constrained deep learning system to resolve complex adjacency conflicts. First, “Explicit Marking” strategy transforms the topological challenge into a learnable classification task by recursively decomposing the cell graph and isolating a “conflict set.” Second, “Implicit Disambiguation” mechanism resolves ambiguities in conflict regions by enforcing feature dissimilarity between different instances, enabling the model to learn separable feature representations. Disco achieves a significant 7.08\% improvement in the PQ metric on the GBC-FS 2025 dataset and an average improvement of 2.72% across all datasets. Furthermore, the predicted “Conflict Map” serves as a novel tool for interpreting topological complexity, offering new potential for data-driven pathology research.

---

## 论文详细总结（自动生成）

## 1. 论文的核心问题与整体含义

- **研究背景**：精确的细胞实例分割是数字病理分析的基础任务，尤其在 H&E 染色全切片图像中对细胞核进行个体化分割，直接影响下游的免疫微环境分析、肿瘤分级等。
- **核心难题**：现有方法（基于轮廓检测、距离图等）在处理密集重叠、拓扑复杂的细胞区域时仍然面临显著挑战。图着色类方法提供了新的范式，但该方法在真实世界中密集重叠与复杂拓扑场景下的有效性尚未得到验证。
- **整体含义**：本文旨在揭示真实组织学图像中细胞邻接关系的**色性特征**（非二部图、奇数环高发），并提出一种基于“分而治之”的邻接感知协同着色框架（Disco），以解决密集重叠区域的实例分割难题，同时为数字病理提供一种新的拓扑复杂性分析工具。

## 2. 论文提出的方法论

- **核心思想**：将密集重叠细胞实例分割形式化为**图着色问题**，并提出“分而治之”的协同着色策略，以处理真实组织中的高阶邻接冲突。
- **关键技术细节**：
    - **拓扑分析与发现**：系统性分析四个数据集的细胞邻接图色性，发现真实细胞图多为非二部图，存在大量奇数长度环（主要是三角形），因此简单的 2-着色理论不够，但过高色数模型又会带来表示冗余和优化困难。
    - **Explicit Marking（显式标记）**：通过递归分解细胞邻接图，隔离出“冲突集”，将拓扑挑战转化为可学习的分类任务。
    - **Implicit Disambiguation（隐式消歧）**：在冲突区域通过强制不同实例间特征不相似性来消除歧义，使模型学习到可分离的特征表示。
    - **协同着色**：将数据驱动的拓扑标记策略与受约束的深度学习系统相结合，以解决复杂邻接冲突。
- **公式/算法流程**（文字描述）：
    1. 构建细胞邻接图（节点为细胞核，边表示接触或重叠）。
    2. 分析图的色数及奇数环分布。
    3. 递归识别并抽取冲突集（难以用局部规则着色的高阶结构）。
    4. 利用“显式标记”模块为可着色区域生成训练信号。
    5. 对冲突区域引入“隐式消歧”损失，促使不同实例特征分离。
    6. 最终对整图进行联合着色，输出实例分割结果及“冲突图”。

## 3. 实验设计

- **数据集**：
    - **自建数据集 GBC-FS 2025**：大规模、高复杂度、密集亚细胞核排列。
    - **其他三个公开/基准数据集**（文中未列出具体名称，摘要仅提及“四个数据集”）。
- **场景**：密集重叠细胞核、复杂拓扑的真实组织病理图像。
- **评价指标**：以 PQ（Panoptic Quality）为主要指标，评估实例分割精度。
- **对比方法**：现有基于轮廓检测、距离映射等方法，以及可能的其他图着色方法（具体名称未在摘要中给出）。

## 4. 资源与算力

- 论文摘要和元数据中**未提及**所使用 GPU 型号、数量、训练时长等具体算力信息。需查阅全文方可获知。

## 5. 实验数量与充分性

- **实验组数**：
    - 在 **4 个数据集**上进行了系统性分析（包括色性分析、分割性能评估）。
    - 在 GBC-FS 2025 上实现了 **7.08% PQ 提升**，在所有数据集上**平均提升 2.72%**。
    - 包含消融实验（推断存在，如显式标记与隐式消歧的有效性对比），但摘要未给出具体消融细节。
- **充分性评估**：基于摘要描述，实验覆盖了不同难度数据集，并与现有范式进行对比，且通过色性分析为方法提供理论支撑，整体实验设计较为充分和客观。但需查看全文确认对比方法的多样性和消融研究的完整性。

## 6. 论文的主要结论与发现

- **关键发现**：真实细胞邻接图多数是**非二部图**，奇数环（以三角形为主）广泛存在，这意味着 2-着色理论不足以处理复杂组织，而更高色数直接学习则面临表示冗余和优化困难。
- **方法效果**：Disco 在 GBC-FS 2025 上 PQ 指标显著提升 7.08%，全部数据集平均提升 2.72%，证明邻接感知协同着色在密集重叠场景下具有明显优势。
- **附加贡献**：预测的“冲突图”可作为解释拓扑复杂性的新工具，为数据驱动的病理研究提供潜在可能。
- **数据集贡献**：发布了高复杂度细胞核数据集 GBC-FS 2025。

## 7. 优点

- **理论创新**：首次系统分析细胞邻接图的色性特征，并基于非二部图特性设计方法，具有较强的几何和拓扑动机。
- **方法论亮点**：将图着色问题与深度学习深度融合，通过“显式标记”与“隐式消歧”的分治策略，既避免了高色数学习的冗余，又解决了冲突区域的表示混淆。
- **实用价值**：在极具挑战的密集重叠场景取得显著提升，并输出可解释的“冲突图”，为病理分析提供新的拓扑维度的信息。
- **基准贡献**：发布高复杂度数据集，填补了相应领域的空白。

## 8. 不足与局限

- **信息缺失**：由于仅能获取摘要及元数据，无法全面评估对比方法的多样性、消融实验的详细设计，以及方法在不同染色、器官、放大倍率下的泛化性。
- **潜在局限**：
    - 图构建对分割前处理（如核检测）的依赖程度未知，可能引入级联误差。
    - 显式冲突集提取的递归算法的可扩展性、对大图的处理效率有待验证。
    - 仅在 IQ、PQ 等指标上报告，未提及在更下游任务（如免疫浸润分析）中的生物验证。
    - 未交代算力需求，难以评估计算成本。
- **偏差风险**：自建数据集 GBC-FS 2025 可能存在选择偏倚（如特定癌种、特定实验室来源），其他三个数据集的性质未披露，影响结论的普适性声明。

（完）
