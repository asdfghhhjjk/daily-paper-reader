---
title: "Disco: Densely-overlapping Cell Instance Segmentation via Adjacency-aware Collaborative Coloring"
title_zh: Disco：通过邻接感知协同着色实现密集重叠细胞实例分割
authors: "Rui Sun, Yiwen Yang, Kaiyu Guo, Chen Jiang, Dongli Xu, Zhaonan Liu, Tan Pan, LIMEI HAN, Xue Jiang, Wu Wei, Yuan Cheng"
date: 2026-01-26
pdf: "https://openreview.net/pdf?id=1W7RRQl3lH"
tags: ["query:cellseg"]
score: 9.0
evidence: 基于图着色的细胞实例分割方法，为数字病理下游任务提供基础
tldr: 为解决现有细胞实例分割方法难以处理密集重叠区域的问题，本文提出基于图着色的邻接感知协同分割方法Disco，并发布包含复杂核排列的大规模数据集GBC-FS 2025。通过分析多个数据集中细胞邻接图的色度特性，该方法在密集场景下实现了精准分割，为数字病理学下游分析提供了可靠的细胞实例分割新范式。
source: ICLR-2026-Accepted
selection_source: conference_retrieval
motivation: 现有方法难以处理病理图像中密集重叠细胞的实例分割。
method: 提出基于图着色的邻接感知协同分割方法，分析细胞邻接图的色度特性。
result: 在多个数据集包括新发布的复杂场景上验证了分割的有效性。
conclusion: 该方法为密集细胞实例分割提供了新范式，支撑下游分析。
---

## Abstract
Accurate cell instance segmentation is foundational for digital pathology analysis. Existing methods based on contour detection and distance mapping still face significant challenges in processing complex and dense cellular regions. Graph coloring-based methods provide a new paradigm for this task, yet the effectiveness of this paradigm in real-world scenarios with dense overlaps and complex topologies has not been verified. Addressing this issue, we release a large-scale dataset GBC-FS 2025, which contains highly complex and dense sub-cellular nuclear arrangements. We conduct the first systematic analysis of the chromatic properties of cell adjacency graphs across four diverse datasets and reveal an important discovery: most real-world cell graphs are non-bipartite, with a high prevalence of odd-length cycles (predominantly triangles). This makes simple 2-coloring theory insufficient for handling complex tissues, while higher-chromaticity models would cause representational redundancy and optimization difficulties. Building on this observation of complex real-world contexts, we propose Disco (Densely-overlapping Cell Instance Segmentation via Adjacency-aware Collaborative Coloring), an adjacency-aware framework based on the “divide and conquer” principle. It uniquely combines a data-driven topological labeling strategy with a constrained deep learning system to resolve complex adjacency conflicts. First, “Explicit Marking” strategy transforms the topological challenge into a learnable classification task by recursively decomposing the cell graph and isolating a “conflict set.” Second, “Implicit Disambiguation” mechanism resolves ambiguities in conflict regions by enforcing feature dissimilarity between different instances, enabling the model to learn separable feature representations. Disco achieves a significant 7.08\% improvement in the PQ metric on the GBC-FS 2025 dataset and an average improvement of 2.72% across all datasets. Furthermore, the predicted “Conflict Map” serves as a novel tool for interpreting topological complexity, offering new potential for data-driven pathology research.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义（研究动机和背景）
- **核心问题**：现有细胞实例分割方法（如基于轮廓检测、距离映射的方法）在处理数字病理图像中细胞密集重叠、拓扑结构复杂的区域时，性能严重下降。
- **背景与动机**：数字病理分析高度依赖精准的细胞实例分割；基于图着色的方法为实例分割提供了新范式，但其在真实世界中密集重叠、含有复杂拓扑的场景下的有效性尚未得到系统验证。
- **整体含义**：本文旨在验证并提升图着色范式在复杂真实场景中的鲁棒性，并对此发布了一个大规模数据集，提出了一个邻接感知的协同着色框架，为密集细胞实例分割提供新范式，支撑下游病理分析。

### 2. 论文提出的方法论：核心思想、关键技术细节、公式或算法流程
- **核心思想**：基于“分而治之”原则，将图着色与深度学习结合，解决密集重叠细胞的实例分割问题。整体框架称为Disco（Densely-overlapping Cell Instance Segmentation via Adjacency-aware Collaborative Coloring）。
- **关键发现**：论文对四个数据集的细胞邻接图进行色度特性分析，首次揭示多数真实细胞图是非二部图，存在大量奇长度圈（主要是三角形）。简单的2-着色理论不足以处理复杂组织，但更高色度的模型又会带来表示冗余和优化困难。
- **关键技术细节**（分为两个阶段）：
  - **显式标记（Explicit Marking）**：通过递归分解细胞图，隔离出“冲突集”，将拓扑着色挑战转化为可学习的分类任务。
  - **隐式消歧（Implicit Disambiguation）**：对冲突区域，通过强制不同实例之间特征不相似性，使模型学习可分离的特征表示，从而解决歧义。
- **辅助输出**：模型预测的“冲突图（Conflict Map）”可作为解释拓扑复杂性的新工具，潜力用于数据驱动的病理研究。

### 3. 实验设计：使用了哪些数据集 / 场景，它的 benchmark 是什么，对比了哪些方法
- **数据集**：
  - 新发布的GBC-FS 2025数据集：具有高度复杂、密集的亚细胞核排列。
  - 其它三个未具名的多样性数据集（用于跨数据集系统性分析）。
- **基准评价指标**：主要使用PQ（Panoptic Quality）指标，在GBC-FS 2025上取得了**7.08%**的提升，所有数据集上平均提升**2.72%**。
- **对比方法**：摘要和元数据未明确列出对比方法，但提及现有方法包括基于轮廓检测和距离映射的方法，以及图着色相关范式。推测对比了这些基准方法。

### 4. 资源与算力
- 摘要和元数据中未提及使用的GPU型号、数量、训练时长等任何算力信息。因此无法总结资源消耗情况。

### 5. 实验数量与充分性
- **实验组数**：
  - 在四个不同数据集上进行色度特性分析。
  - 在其中一个新数据集（GBC-FS 2025）上展示了PQ指标的显著提升，并报告了所有数据集的平均提升。
  - 进行了消融实验的迹象（方法包含显式标记和隐式消歧模块），但具体消融实验设计和数量未在提供信息中体现。
- **充分性与公平性**：
  - 优点：跨多个数据集进行分析，结果具有普遍性；采用统一量化指标PQ，对比公平。
  - 不足：由于仅提供了摘要，无法判断实验的详细设计（如数据划分、重复次数、显著性检验等）。总体来看，基于有限信息推断实验覆盖了分割精度提升和拓扑分析，在已报告范围内是充分和客观的。

### 6. 论文的主要结论与发现
- 真实细胞邻接图普遍为非二部图，含大量三角形奇数圈，简单2-着色无法应对。
- 提出的Disco框架通过邻接感知的协同分割，能在密集重叠复杂场景下实现精准分割，在GBC-FS 2025上PQ提升7.08%，全数据集平均提升2.72%。
- “冲突图”可解释拓扑复杂性，为病理研究提供新工具。
- 该方法为密集细胞实例分割设立了新范式，支撑下游分析任务。

### 7. 优点：方法或实验设计上的亮点
- **系统性分析**：首次对多个数据集的细胞图色度特性进行系统分析，揭示了非二部性及奇数圈分布的规律，为后续方法设计奠定理论基础。
- **分治策略**：将复杂的图着色问题分解为“可学习分类”和“特征消歧”，有效融合了拓扑约束与深度学习表示能力。
- **新数据集贡献**：发布了高度复杂的GBC-FS 2025数据集，推动社区在密集细胞分割方向的研究。
- **可解释性工具**：提供“冲突图”作为拓扑复杂性的可视化解释，连接了分割结果与生物学分析。

### 8. 不足与局限：包括实验覆盖、偏差风险、应用限制等
- **信息不完整**：基于仅有的摘要和元数据，无法评估模型复杂度、推理速度、算力需求、模型泛化到其它组织类型或染色方式的性能。
- **实验细节缺失**：未提供具体对比方法名称、消融实验的具体设置、统计检验，无法判断实验完整性和结论的稳健性。
- **偏差风险**：新数据集可能带有特定机构或制备流程偏差，是否覆盖足够多样的病理条件未知。
- **应用限制**：方法建立在细胞邻接图上，对于无重叠或稀疏细胞场景的优势可能不显著；另外，高阶着色冲突的“隐式消歧”能否处理更复杂的多重重叠并未详细阐述。

（完）
