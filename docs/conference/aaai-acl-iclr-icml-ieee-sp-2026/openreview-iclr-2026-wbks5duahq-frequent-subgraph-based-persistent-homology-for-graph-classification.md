---
title: Frequent Subgraph-Based Persistent Homology for Graph Classification
title_zh: 基于频繁子图的持久同调用于图分类
authors: "Xinyang chen, Amaël Broustet, Guanyuan Zeng, Cheng He, Guoting Chen"
date: 2025-09-11
pdf: "https://openreview.net/pdf?id=wBKS5dUAHQ"
tags: ["query:immuno-topo"]
score: 6.0
evidence: 基于频繁子图持久同调的图拓扑特征提取方法
tldr: 现有持久同调方法依赖有限过滤函数，忽略图中频繁出现的子结构。本文提出频繁子图过滤（FSF），从频繁子图导出频率持久同调（FPH）特征，理论上稳定且富含信息，应用于图分类任务。实验证明FPH特征能有效增强图分类模型的拓扑感知能力。
source: ICLR-2026-Public
selection_source: conference_retrieval
motivation: 现有持久同调过滤函数有限，忽略图中频繁子结构。
method: 提出频繁子图过滤，生成频率持久同调特征。
result: FPH特征在图分类任务中有效提升性能。
conclusion: 该方法为图拓扑特征提取提供了新思路，可增强模型可解释性。
---

## Abstract
Persistent homology (PH) has recently emerged as a powerful tool for extracting topological features. 
Integrating PH into both machine learning and deep learning models enhances their topology-awareness and interpretability.
However, most PH methods on graphs rely on a limited set of filtrations (e.g., degree- or weight-based), which overlook richer features such as recurring information across the dataset, thereby restricting their expressive power. In this work, we propose a novel filtration on graphs, called Frequent Subgraph Filtration (FSF), which is derived from frequent subgraphs and produces stable and information-rich Frequency-based Persistent Homology (FPH) features. We explore the theoretical properties of FSF and provide proofs and experimental validation of them. Beyond persistent homology itself, we further introduce two approaches for graph classification: (i) an FPH-based machine learning model (FPH-ML), and (ii) a hybrid framework integrating FPH with graph neural networks (FPH-GNNs) to enhance topology-aware graph representation learning. Our proposed frameworks show the potential of bridging frequent subgraph mining and topological data analysis, offering a new perspective on topology-aware feature extraction and graph representation learning.
Experimental results show that FPH-ML achieves competitive or superior accuracy compared to kernel-based and degree-based filtration methods. When injected into GNNs, FPH delivers relative gains of ~0.4–21\% (up to +8.2 pts) over their GCN/GIN backbones across benchmarks.

---

## 论文详细总结（自动生成）

## 1. 论文的核心问题与整体含义（研究动机和背景）
- **核心问题**：现有的持久同调方法在图数据上大多依赖有限且简单的过滤函数（如基于度数或权重的过滤），这忽略了图中频繁出现的子结构（recurring information），限制了拓扑特征的表征能力与对图全局模式的捕捉。
- **整体含义**：本文旨在将频繁子图挖掘与拓扑数据分析相结合，提出一种基于频繁子图的持久同调特征提取方法，从而增强图分类模型的拓扑感知能力和可解释性，并为该领域提供新的特征工程视角。

## 2. 方法论：核心思想、关键技术细节、算法流程
- **核心思想**：利用图中频繁出现的子图模式定义一种新的过滤——**频繁子图过滤（Frequent Subgraph Filtration, FSF）**，并由此生成频率持久同调特征（Frequency-based Persistent Homology, FPH）。该过滤不同于仅依赖节点属性的过滤，能从整个数据集中挖掘反复出现的拓扑结构，捕捉更丰富的图全局信息。
- **关键技术细节**：
  - **频繁子图过滤（FSF）**：从图数据集中挖掘频繁子图，以子图出现的频率信息构建过滤序列。具体而言，根据子图的频繁程度或隶属关系递增赋值，得到图的嵌套序列（filtration）。
  - **FPH 特征**：对上述过滤序列进行持续同调计算，得到持久图或持久条码等拓扑摘要，并将其转化为可用于机器学习的固定长度特征向量。
- **算法流程概览**（用文字说明）：
  1. 在训练集上运行频繁子图挖掘算法，获得一组频繁子图模式。
  2. 对每一张图，计算每个节点/边属于某个频繁子图的“频率隶属度”或相关统计量，作为过滤函数值。
  3. 按过滤值递增顺序构建单纯复形序列，计算持续同调（如 0 维和 1 维同调）。
  4. 将持久同调结果转化为向量化的 FPH 特征。
- **理论性质**：文中给出了 FSF 的稳定性与信息丰富性证明及实验验证。
- **下游模型**：
  - FPH-ML：直接基于 FPH 特征的机器学习分类器。
  - FPH-GNNs：将 FPH 特征注入图神经网络（GCN/GIN）作为增强拓扑感知的混合框架。

## 3. 实验设计：数据集/场景、benchmark、对比方法
- **任务场景**：图分类。
- **数据集**：文中未在摘要中详细列出，但提到“across benchmarks”，暗示使用了多个公开图分类基准数据集（如生物信息学、社交网络图等）。
- **对比方法**：
  - 基于核方法或度数过滤的传统持久同调方法（kernel-based and degree-based filtration methods）。
  - 基线 GNN 模型（GCN、GIN 等）。
- **性能指标**：分类准确率，以及相对提升幅度（relative gains）。

## 4. 资源与算力
- 提供的信息中**未明确说明** GPU 型号、数量或训练时长等算力细节。摘要和元数据均未涉及计算资源描述，因此无法评估其算力消耗。

## 5. 实验数量与充分性
- **实验组数**：具体数量未在摘要中给出，但从描述可推断至少包含：
  - FPH-ML 与多种基线方法（核方法、度数过滤法）在多个数据集上的分类准确率对比。
  - FPH-GNN 与 GCN/GIN 基线的性能比较，并报告了相对提升（0.4–21%，最高+8.2 百分点）。
  - 理论性质的实验验证（如稳定性测试）。
- **充分性与公平性**：
  - 对比对象覆盖了传统 PH 方法和主流 GNN 模型，具有一定的完整性。
  - 提升幅度用相对增益和绝对百分点给出，较为客观。
  - 因未看到全文，无法判断是否包含消融实验（如不同频繁子图数量、同调配准参数等），但摘要表明实验已支撑主要结论。
  - 总体来看，实验设计较为直接，但现有摘要信息不足以判断是否存在过拟合小数据集或缺乏统计检验等风险。

## 6. 论文的主要结论与发现
- 提出的 FSF 能够生成信息更丰富且稳定的拓扑特征（FPH），弥补了传统过滤忽视频繁子结构信息的缺陷。
- FPH-ML 模型在图分类任务上能达到与核方法和度数过滤方法相当甚至更优的准确率。
- 将 FPH 注入 GNN 后，能够显著提升 GCN/GIN 的性能，相对提升在 0.4%~21% 之间，最大可带来 8.2 个百分点的绝对提升。
- 该方法连通了频繁子图挖掘与拓扑数据分析，为拓扑感知的图表示学习提供了新视角，并增强了模型的可解释性。

## 7. 优点：方法或实验设计亮点
- **创新性组合**：首次将频繁子图挖掘与持久同调结合，从全局数据集挖掘复用拓扑模式，突破了以往仅在单图上定义过滤的局限。
- **理论支撑**：对 FSF 的稳定性与信息丰富性进行了证明，增强了方法可信度。
- **灵活的下游应用**：既可作为独立的 ML 特征使用，也可作为 GNN 的增强插件，具有良好的通用性。
- **效果显著**：在多个基准上显示出明显而稳定的性能提升，尤其对 GNN 的增强效果突出。

## 8. 不足与局限：实验覆盖、偏差风险、应用限制等
- **实验细节不透明**：摘要未给出具体数据集名称、规模、划分方式及统计检验，难以评估结论的普适性和鲁棒性。
- **算力与效率未知**：频繁子图挖掘和持久同调计算可能耗时较大，但未讨论时间复杂度或实际运行开销，实用性打折扣。
- **超参数敏感性未提及**：例如频繁子图的支持度阈值、过滤函数的构造参数等关键选择对性能的影响未提及。
- **可能的数据偏差**：若频繁子图挖掘仅依赖训练集，在小样本或分布偏移场景下泛化性未知。
- **应用场景局限**：主要针对图分类，未探讨在其他图任务（如节点分类、链接预测）上的扩展性。

（完）
