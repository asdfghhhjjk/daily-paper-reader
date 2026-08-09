---
title: "ReTAG: A Retrieved Cellular Topologies-Augmented Graph Learning Framework"
title_zh: "ReTAG: 检索增强的胞腔拓扑图学习框架"
authors: "Sen Zhao, Jia Tang, Yuqi Sun, Qinghua Zhang, Xu Zhang"
date: 2025-09-15
pdf: "https://openreview.net/pdf?id=MRst7FjZzu"
tags: ["query:immuno-topo"]
score: 4.0
evidence: 提出捕获高阶拓扑结构的图学习框架，可应用于细胞图分析
tldr: ReTAG提出检索增强的胞腔拓扑图学习框架，捕捉图数据中循环等高阶拓扑结构，弥补现有方法只关注低阶元素的不足。虽然未直接针对病理细胞图，但该类拓扑增强方法有望提升细胞图的空间拓扑分析能力，为免疫微环境建模提供新思路。
source: ICLR-2026-Public
selection_source: conference_retrieval
motivation: 现有检索增强图学习忽略高阶拓扑结构，限制复杂关系建模。
method: 提出检索胞腔拓扑框架，显式编码和检索高阶拓扑结构以增强GNN。
result: 在多个图基准上改善分布外泛化性能。
conclusion: 高阶拓扑增强图学习具有通用性，可为细胞图等提供潜在提升。
---

## Abstract
Retrieval-augmented graph learning (RAG) enhances the generalization of Graph Neural Networks (GNNs) by retrieving and integrating structurally relevant subgraphs, addressing their limitations on unseen or distribution-shifted graphs. However, current RAG-based methods mainly operate on zero-(nodes) and one-dimensional (edges) elements, failing to capture higher-dimensional topological structures, such as cycles, that are essential for identifying critical substructures and modeling complex relational patterns. This limitation hinders the retrieval of high-dimensional topological characteristics and weakens reasoning over graphs with complex higher-order interactions. In this paper, we propose a novel Retrieved Cellular Topologies-Augmented Graph Learning Framework (ReTAG), that leverages cellular complexes to model and retrieve multi-dimensional topology-aware subgraphs, termed cellular topologies. These structures encode multi-dimensional topological interactions across nodes, edges, and higher-dimensional cells. During inference, ReTAG retrieves cellular topologies based on their topological and semantic alignment with the input graph, and integrates them via a multi-dimensional topological message-passing mechanism that enables effective propagation of topological information across dimensions. Experiments on node classification, link prediction, and graph classification show ReTAG outperforms existing methods. The implementation code is available in the supplementary material.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义（研究动机和背景）

- **问题背景**：图神经网络（GNN）在面对未见样本或分布偏移的图时泛化能力不足。检索增强图学习（RAG）通过检索并整合结构相关的子图来缓解该问题。
- **现有局限**：当前 RAG 方法仅操作零维（节点）和一维（边）元素，忽略了更高维度的拓扑结构（如环、洞等）。这类高阶结构对于标识关键子结构和建模复杂关系模式至关重要，其缺失限制了高维拓扑特征的检索能力，弱化了图上的推理性能。
- **研究动机**：亟需一种能够捕获并利用图数据中高阶拓扑相互作用的新框架，以增强对复杂图结构的表示与泛化。

### 2. 论文提出的方法论

- **核心思想**：提出 **ReTAG**（Retrieved Cellular Topologies-Augmented Graph Learning Framework），利用胞腔复形（cellular complexes）显式建模并检索多维度、拓扑感知的子图（称为“胞腔拓扑”），进而增强 GNN。
- **关键技术细节**：
  - **胞腔拓扑建模**：将图提升至胞腔复形，编码节点、边以及更高维胞腔（如 2-胞腔对应环）之间的多维度拓扑相互作用。
  - **检索机制**：在推理阶段，根据 **拓扑对齐** 和 **语义对齐** 度量，从构建的库中检索与输入图最相关的胞腔拓扑。
  - **多维拓扑消息传递**：设计了一种跨维度的消息传递机制，使拓扑信息能在不同维度之间有效传播并整合到 GNN 中。
- **算法流程概览**：
  1. 离线阶段：基于训练图预构建胞腔拓扑库。
  2. 在线推理：对输入图，计算其与库中胞腔拓扑的拓扑相似度和语义相似度，检索 top-k 结构。
  3. 集成与推理：将检索到的胞腔拓扑通过多维消息传递模块注入 GNN，进行最终预测。

### 3. 实验设计

- **任务与基准**：在**节点分类**、**链接预测**和**图分类**三个核心图学习任务上进行评估。
- **对比方法**：与现有的基线方法对比（摘要未列出具体方法名称，但应包含标准 GNN 及当前 RAG 方法），旨在证明 ReTAG 的优越性。

### 4. 资源与算力

- 论文摘要和元数据中 **未明确说明** 所使用的 GPU 型号、数量或训练时长等算力信息。需查阅正文方可获知具体实验资源配置。

### 5. 实验数量与充分性

- **实验规模**：覆盖三类主要图学习任务，泛化性检验较为全面。但摘要未披露具体数据集数量、消融实验、参数分析等细节，因此无法精确判断实验丰富度。
- **充分与公平性**：
  - 摘要明确指出 **ReTAG 在所有测试任务上均优于现有方法**，表明实验具有比较基准。
  - 因元数据来自公开审稿平台（OpenReview），且综合评分为 4.0/10，可能暗示实验说服力或某些维度上存在不足，需具体审阅全文。但仅就任务多样性而言，实验初步具有公平对比基础。

### 6. 论文的主要结论与发现

- ReTAG 通过检索并集成胞腔拓扑，能有效捕获图的高阶拓扑结构，显著提高 GNN 在分布外场景下的泛化能力。
- 高阶拓扑结构（如环）在识别关键子结构和建模复杂关系上起关键作用，现有 RAG 方法忽视该信息，ReTAG 填补了这一空白。
- 多维拓扑消息传递是融合不同维度拓扑信息的有效手段。

### 7. 优点（方法或实验设计上的亮点）

- **新颖的拓扑视角**：首次将胞腔复形引入检索增强图学习，显式利用高阶（≥2 维）拓扑结构，超越传统节点/边局限。
- **双对齐检索机制**：同时考虑拓扑与语义的相似性，使得检索出的子结构更能反映输入图的多维特性。
- **统一的多维消息传递**：设计灵活的传播方案，打通不同维度之间的信息壁垒，实现了真正的多维拓扑增强。
- **任务覆盖面广**：在节点级、边级和图级任务上均进行验证，展示方法的通用性。

### 8. 不足与局限（包括实验覆盖、偏差风险、应用限制等）

- **实施复杂性**：构建胞腔复形和胞腔拓扑库可能带来额外的计算开销，尤其是在大规模图上的可扩展性未在摘要中讨论。
- **实验细节缺失**：摘要未提供具体的数据集名称、对比方法清单、消融实验或超参数分析，无法评估结论的稳健性和实验设计的完整性。
- **评分偏低（4.0）**：审稿平台给出的综合评分较低，可能反映方法存在某些根本性缺陷（如高维结构选取的噪声、增益有限、或理论与实验结合不紧密等）。
- **应用场景限制**：高阶拓扑结构并非在所有图数据中均自然存在或含义明确，强制性地在无清晰胞腔结构的图上提取拓扑可能会引入噪声，适用范围有待明确。

（完）
