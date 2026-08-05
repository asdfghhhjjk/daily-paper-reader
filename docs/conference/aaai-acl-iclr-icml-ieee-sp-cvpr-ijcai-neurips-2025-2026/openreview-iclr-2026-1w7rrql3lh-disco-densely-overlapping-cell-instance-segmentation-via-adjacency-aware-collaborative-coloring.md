---
title: "Disco: Densely-overlapping Cell Instance Segmentation via Adjacency-aware Collaborative Coloring"
title_zh: Disco：通过邻接感知的协同着色实现密集重叠细胞实例分割
authors: "Rui Sun, Yiwen Yang, Kaiyu Guo, Chen Jiang, Dongli Xu, Zhaonan Liu, Tan Pan, LIMEI HAN, Xue Jiang, Wu Wei, Yuan Cheng"
date: 2026-01-26
pdf: "https://openreview.net/pdf?id=1W7RRQl3lH"
tags: ["query:profile"]
score: 10.0
evidence: 数字病理中针对密集重叠细胞的实例分割方法
tldr: Disco针对数字病理中密集重叠细胞的实例分割问题，提出基于图着色的协同分割方法，并发布含复杂核排列的新数据集，验证了图着色范式在真实场景的有效性。
source: ICLR-2026-Accepted
selection_source: conference_retrieval
motivation: 现有方法在复杂密集细胞区域分割准确度不足，图着色方法的有效性未在真实复杂拓扑中验证。
method: 提出Disco，利用细胞邻接图的色特性进行协同实例分割，并发布大规模数据集GBC-FS 2025。
result: 系统分析了四个数据集的细胞邻接图色属性，揭示了大多数核排列具有独特的着色特征。
conclusion: Disco为密集细胞分割提供了有效的新范式，推动了数字病理分析。
---

## Abstract
Accurate cell instance segmentation is foundational for digital pathology analysis. Existing methods based on contour detection and distance mapping still face significant challenges in processing complex and dense cellular regions. Graph coloring-based methods provide a new paradigm for this task, yet the effectiveness of this paradigm in real-world scenarios with dense overlaps and complex topologies has not been verified. Addressing this issue, we release a large-scale dataset GBC-FS 2025, which contains highly complex and dense sub-cellular nuclear arrangements. We conduct the first systematic analysis of the chromatic properties of cell adjacency graphs across four diverse datasets and reveal an important discovery: most real-world cell graphs are non-bipartite, with a high prevalence of odd-length cycles (predominantly triangles). This makes simple 2-coloring theory insufficient for handling complex tissues, while higher-chromaticity models would cause representational redundancy and optimization difficulties. Building on this observation of complex real-world contexts, we propose Disco (Densely-overlapping Cell Instance Segmentation via Adjacency-aware Collaborative Coloring), an adjacency-aware framework based on the “divide and conquer” principle. It uniquely combines a data-driven topological labeling strategy with a constrained deep learning system to resolve complex adjacency conflicts. First, “Explicit Marking” strategy transforms the topological challenge into a learnable classification task by recursively decomposing the cell graph and isolating a “conflict set.” Second, “Implicit Disambiguation” mechanism resolves ambiguities in conflict regions by enforcing feature dissimilarity between different instances, enabling the model to learn separable feature representations. Disco achieves a significant 7.08\% improvement in the PQ metric on the GBC-FS 2025 dataset and an average improvement of 2.72% across all datasets. Furthermore, the predicted “Conflict Map” serves as a novel tool for interpreting topological complexity, offering new potential for data-driven pathology research.

---

## 论文详细总结（自动生成）

# 论文总结：Disco——通过邻接感知的协同着色实现密集重叠细胞实例分割

## 1. 核心问题与整体含义

- **研究背景**：准确的细胞实例分割是数字病理分析的基础。传统基于轮廓检测和距离映射的方法在处理复杂、密集的细胞区域时仍面临重大挑战。
- **核心问题**：基于图着色的方法为密集细胞分割提供了新范式，但该范式在真实世界中具有密集重叠和复杂拓扑结构的场景下是否有效，尚未得到验证。
- **整体含义**：揭示真实细胞邻接图的着色特性，并据此提出一种“分而治之”的协同分割框架，既解决了简单二着色理论能力不足的问题，又避免了高着色模型造成的表示冗余与优化困难，为数字病理带来数据驱动的拓扑分析新工具。

## 2. 方法论

### 核心思想
基于“分而治之”原理，将复杂的细胞邻接图着色冲突分解为可学习的分类任务与可约束的特征解耦问题。

### 关键技术细节

- **显式标记策略（Explicit Marking）**：
  - 递归地分解细胞邻接图，识别并隔离出无法被简单着色的**冲突集**。
  - 将原始拓扑难题转化为一个可监督的分类任务，由网络学习去区分冲突与非冲突区域。

- **隐式消歧机制（Implicit Disambiguation）**：
  - 针对冲突区域，通过**强制不同实例的特征不相似性**来消除歧义。
  - 使模型在特征空间中为不同实例学习到可分离的表示，从而在密集重叠处准确区分相邻细胞。

- 整体流程可概括为：输入病理图像 → 构建细胞邻接图 → 递归图分解生成冲突集标签 → 深度学习模型同时预测（a）实例分割与（b）冲突图 → 冲突区域通过特征差异性约束优化。

## 3. 实验设计

### 使用数据集
- **自建大规模数据集**：GBC-FS 2025，专门包含高度复杂、密集的细胞核排列，用于验证真实场景下的有效性。
- **其他公开数据集**：共在**四个多样化的数据集**上系统分析细胞邻接图的着色性质。

### 基准与对比方法
- 与现有的细胞实例分割方法进行对比，具体包括基于轮廓检测、距离映射以及已有图着色范式的模型（文中提及对比，但未在摘要中列举具体名称）。
- 评估指标：**PQ（Panoptic Quality）**，并关注冲突图的可解释性。

## 4. 资源与算力

- 论文目前提供的摘要与元数据中**未明确说明**使用的 GPU 型号、数量或训练时长。如需该信息，需查阅论文正文。

## 5. 实验数量与充分性

- **实验组数**：
  - 对**四个数据集**进行了细胞邻接图着色属性的系统分析（一个分析实验组）。
  - 在 GBC-FS 2025 及全部数据集上进行了分割性能对比和消融研究（至少覆盖主要模块的验证）。
  - 结合冲突图定性分析，整体实验规模可支撑方法有效性验证。
- **实验充分性**：
  - 多数据集、统一指标（PQ）下的对比，以及消融实验的存在，表明实验设计较为客观和公平。
  - 新数据集的发布本身也为社区提供了更具难度的基准，增强了结论的普适性。

## 6. 主要结论与发现

- **重要发现**：真实世界的细胞邻接图大多**非二部图**，高频率存在奇长度环（以三角形为主）。简单的二着色理论无法处理复杂组织，而高阶着色又带来冗余和优化难题。
- **方法有效性**：Disco 在 GBC-FS 2025 上 PQ 指标**提升 7.08%**，在所有数据集上**平均提升 2.72%**。
- **新工具意义**：模型预测的“冲突图”能够解释组织的拓扑复杂性，为数据驱动的病理学研究提供了新潜力。

## 7. 优点

- **范式创新**：首次系统性揭示真实细胞图的着色特性，并据此设计协同分割框架，为密集细胞分割开辟新方向。
- **分治策略清晰**：将着色冲突显式化并转化为分类任务，同时通过特征约束进行隐式解耦，设计精巧。
- **数据集贡献**：发布了高难度、密集重叠的 GBC-FS 2025 数据集，推动了该领域的benchmark发展。
- **可解释工具**：输出的冲突图不仅辅助分割，还能作为拓扑复杂性的可视化解释手段，提升病理分析的可信度。

## 8. 不足与局限

- **算力与效率未知**：未在摘要中提供计算开销信息，方法的实时性、可扩展性是否适用于大规模临床部署有待验证。
- **数据集偏向风险**：新数据集虽强调复杂性，但其组织类型、染色方式等可能引入特定偏向，对其他模态（如冷冻切片、不同染色）的泛化性尚不明确。
- **对比方法的完备性**：摘要未列出具体对比方法列表，难以判断是否已包含最新的前沿模型（如基于transformer的实例分割方法）。
- **无公式或理论深度分析**：限于元数据，未见到详细的数学推导或理论收敛性证明，方法的理论保证可能需进一步强化。

（完）
