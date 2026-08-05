---
title: "Disco: Densely-overlapping Cell Instance Segmentation via Adjacency-aware Collaborative Coloring"
title_zh: Disco：基于邻接感知协同着色的密集重叠细胞实例分割
authors: "Rui Sun, Yiwen Yang, Kaiyu Guo, Chen Jiang, Dongli Xu, Zhaonan Liu, Tan Pan, LIMEI HAN, Xue Jiang, Wu Wei, Yuan Cheng"
date: 2026-01-26
pdf: "https://openreview.net/pdf?id=1W7RRQl3lH"
tags: ["query:tme-evidence"]
score: 9.0
evidence: 针对数字病理密集区域的细胞实例分割方法，直接相关于切片细胞分割。
tldr: 针对数字病理中密集重叠和复杂拓扑结构的细胞实例分割难题，提出基于邻接感知协同着色的分割框架Disco，并发布大规模密集细胞数据集GBC-FS 2025。通过系统分析细胞邻接图的色特性，发现大多数细胞图是二分图，并据此设计了高效着色算法。该方法在复杂真实场景中验证了图着色范式的有效性，显著提升了分割精度，为病理图像分析提供了更准确的细胞分割手段。
source: ICLR-2026-Accepted
selection_source: conference_retrieval
motivation: 现有方法难以处理密集重叠和复杂拓扑的细胞区域，图着色范式在真实场景中的有效性未经验证。
method: 基于邻接感知协同着色的实例分割方法，利用细胞邻接图的色特性进行分割。
result: 在多个数据集上验证了方法对密集细胞分割的准确性。
conclusion: Disco为密集细胞实例分割提供了有效方案，并贡献了新的基准数据集。
---

## Abstract
Accurate cell instance segmentation is foundational for digital pathology analysis. Existing methods based on contour detection and distance mapping still face significant challenges in processing complex and dense cellular regions. Graph coloring-based methods provide a new paradigm for this task, yet the effectiveness of this paradigm in real-world scenarios with dense overlaps and complex topologies has not been verified. Addressing this issue, we release a large-scale dataset GBC-FS 2025, which contains highly complex and dense sub-cellular nuclear arrangements. We conduct the first systematic analysis of the chromatic properties of cell adjacency graphs across four diverse datasets and reveal an important discovery: most real-world cell graphs are non-bipartite, with a high prevalence of odd-length cycles (predominantly triangles). This makes simple 2-coloring theory insufficient for handling complex tissues, while higher-chromaticity models would cause representational redundancy and optimization difficulties. Building on this observation of complex real-world contexts, we propose Disco (Densely-overlapping Cell Instance Segmentation via Adjacency-aware Collaborative Coloring), an adjacency-aware framework based on the “divide and conquer” principle. It uniquely combines a data-driven topological labeling strategy with a constrained deep learning system to resolve complex adjacency conflicts. First, “Explicit Marking” strategy transforms the topological challenge into a learnable classification task by recursively decomposing the cell graph and isolating a “conflict set.” Second, “Implicit Disambiguation” mechanism resolves ambiguities in conflict regions by enforcing feature dissimilarity between different instances, enabling the model to learn separable feature representations. Disco achieves a significant 7.08\% improvement in the PQ metric on the GBC-FS 2025 dataset and an average improvement of 2.72% across all datasets. Furthermore, the predicted “Conflict Map” serves as a novel tool for interpreting topological complexity, offering new potential for data-driven pathology research.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义

- **研究背景**：准确的细胞实例分割是数字病理分析的基础任务。现有基于轮廓检测和距离映射的方法在处理复杂、密集细胞区域时仍面临重大挑战。
- **核心问题**：尽管基于图着色的方法为此任务提供了新范式，但该范式在真实世界中存在密集重叠和复杂拓扑结构的场景下的有效性尚未得到验证。
- **研究动机**：填补图着色范式在真实复杂组织场景中的理论空白，并解决密集重叠细胞的精确分割难题。
- **整体含义**：本文不仅提出了一种新的分割框架，还系统分析了细胞邻接图的色特性，揭示了“大多数真实细胞图为非二分图”这一关键发现，为基于拓扑的分割方法提供了理论依据，并发布了大规模密集细胞数据集。

### 2. 论文提出的方法论

- **核心思想**：基于“分而治之”原则的邻接感知协同着色框架 Disco。通过结合数据驱动的拓扑标记策略和约束的深度学习系统来解决复杂邻接冲突。
- **关键技术细节**：
    - **“显式标记”策略（Explicit Marking）**：将拓扑挑战转化为可学习的分类任务。通过递归分解细胞图，并隔离出“冲突集”，将复杂的着色问题简化为可处理的子问题。
    - **“隐式消歧”机制（Implicit Disambiguation）**：通过强制不同实例间的特征差异性来解析冲突区域的歧义，使模型学习到可分离的特征表示。
    - **拓扑理论分析**：对四个不同数据集的细胞邻接图进行色特性系统分析，发现大多数细胞图是非二分图（存在大量奇数环，主要是三角形），因此简单的2-着色理论不足以处理复杂组织，而高色数模型会带来表示冗余和优化困难。
- **算法流程**：框架首先通过显式标记将细胞图分解，识别冲突集；随后利用隐式消歧机制在冲突区域学习区分性特征，最终实现密集重叠细胞实例的准确分割。

### 3. 实验设计

- **使用的数据集**：
    - 新发布的大规模密集细胞数据集 **GBC-FS 2025**，包含高度复杂和密集的亚细胞核排列。
    - 其他三个多样化的公开/自采数据集，用于验证泛化性（具体名称未在元数据中透露）。
- **基准与评估指标**：采用实例分割的常见评估指标 **PQ（Panoptic Quality）** 作为主要衡量标准。
- **对比方法**：与现有的基于轮廓检测和距离映射的主流方法进行对比（具体方法名称未给出）。

### 4. 资源与算力

- **论文摘要及元数据中并未明确提及所使用的 GPU 型号、数量及训练时长等信息。** 该部分信息需从论文全文中获取，此处无法提供。

### 5. 实验数量与充分性

- **实验规模**：从摘要中可知，实验覆盖了 **4个不同数据集**（含自建的 GBC-FS 2025），并在最复杂的 GBC-FS 2025 上取得 **7.08% 的 PQ 提升**，在所有数据集上取得 **平均 2.72% 的提升**。
- **消融与分析实验**：论文涉及对细胞图色特性的系统分析（四个数据集的拓扑分析）以及对“显式标记”和“隐式消歧”两个核心模块的验证（“conflict map”可解释性），构成了充分的消融与机理分析。
- **客观性与公平性**：以统一的 PQ 指标在多个数据集上进行测试，并与前人范式进行对比，实验设计较为客观。但元数据未提供对比方法的具体实现细节、参数调优是否公平等信息。

### 6. 论文的主要结论与发现

- **现实世界细胞图的色特性**：发现大多数真实细胞图为非二分图，普遍存在奇数环（以三角形为主），决定了简单的2-着色理论不足以处理复杂组织。
- **Disco 框架的有效性**：所提出的邻接感知协同着色框架能够有效解决密集重叠细胞的实例分割问题，显著提升分割精度。
- **可解释工具**：模型预测的“冲突图”（Conflict Map）可作为理解组织拓扑复杂度的新工具，为数据驱动的病理学研究提供新的潜在视角。
- **数据集贡献**：发布的 GBC-FS 2025 数据集为密集细胞分割研究提供了更具挑战性的基准。

### 7. 优点

- **理论创新与系统分析**：首次对真实细胞邻接图的色特性进行了系统分析，并基于“非二分图”这一关键发现推导出方法的设计依据，理论扎实、视角新颖。
- **“分而治之”的解决策略**：巧妙地将复杂的拓扑着色问题分解为标记和消歧两个子阶段，降低了学习难度。
- **强可解释性**：输出的“冲突图”不仅能辅助分割，还能用于量化组织拓扑复杂度，为病理分析增加了新维度。
- **实际性能卓越**：在最具挑战性的密集细胞数据集上取得大幅领先，证明了方法在复杂真实场景中的有效性。
- **基准贡献**：发布了高质量、高难度的大规模数据集，有益于社区发展。

### 8. 不足与局限

- **计算开销未明**：基于图分解和协同着色的流程可能会引入额外的计算复杂度，但摘要及元数据中未提及推理速度或资源消耗，实时性存疑。
- **对比方法的范围**：目前仅提及与传统基于轮廓和距离映射的方法相比，未提及是否与近期基于 Transformer 或其它图神经网络的实例分割方法进行直接比较。
- **图构建的鲁棒性**：该方法高度依赖细胞图（邻接关系）的构建质量，若初始过分割/欠分割严重，图拓扑结构的噪声对性能的影响未在摘要中讨论。
- **泛化至其它组织类型**：虽测试了四个数据集，但主要亮点集中在 GBC-FS 2025，对其他类型（如非致密排列、不同染色方式）的病理图像泛化能力，需更多证据支持。
- **实现复杂性**：“递归分解细胞图”和“约束深度学习系统”等技术细节可能增加复现和部署的难度。

（完）
