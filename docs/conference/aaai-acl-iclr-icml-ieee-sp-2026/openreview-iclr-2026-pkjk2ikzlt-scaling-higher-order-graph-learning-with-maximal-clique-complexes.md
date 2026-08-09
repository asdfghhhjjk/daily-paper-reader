---
title: Scaling Higher-Order Graph Learning with Maximal Clique Complexes
title_zh: 利用极大团复形扩展高阶图学习
authors: "Antoine Vialle, Aref Einizade, Fragkiskos D. Malliaros, Jhony H. Giraldo"
date: 2025-09-19
pdf: "https://openreview.net/pdf?id=pKjk2iKZLT"
tags: ["query:immuno-topo"]
score: 6.0
evidence: 利用团复形进行可扩展的高阶图学习，可用于细胞图拓扑建模。
tldr: 针对图神经网络仅能建模成对关系的局限，通过极大团复形和简化细胞Weisfeiler-Leman测试提升高阶图学习的可扩展性和表达力，为细胞图等复杂拓扑结构提供实用工具。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 现有高阶图模型虽然表达力强但难以扩展，需要同时保持表达力并提升可扩展性。
method: 提出简化及因子化的细胞Weisfeiler-Leman测试，并利用极大团复形高效构建高阶结构。
result: 新方法在保持表达力的同时显著提高了大规模图学习的可扩展性。
conclusion: 所提方法为高阶图神经网络的实际应用开辟了道路，可有效用于细胞图等复杂系统。
---

## Abstract
Graph neural networks (GNNs) are widely used for learning on graphs but are fundamentally limited to modeling pairwise relationships.
Topological models based on simplicial or cell complexes can capture higher-order structure and match or surpass the expressive power of the Weisfeiler–Leman (WL) test, but they are difficult to scale because they require constructing higher-order complexes.
In this paper, we ask how to retain the expressivity of cellular Weisfeiler networks (CWNs) while improving their scalability, and how to exploit cliques efficiently on large graphs. First, we introduce simplified and factored cellular Weisfeiler–Leman (sCWL and fCWL) tests, and show that they are as expressive as the original CWL test, while achieving better scalability properties. We then define the maximal clique complex, a cell complex whose higher-order cells are the maximal cliques of the graph, and apply the corresponding simplified and factored CWNs (sCWN and fCWN) on this structure, achieving improved time and memory complexity. To avoid explicit enumeration of all maximal cliques, we propose CliqueWalk, a biased random walk that samples (maximal) cliques and scales quasi-linearly with the number of nodes.
Combining maximal clique complexes with CliqueWalk yields scalable clique-based architectures that preserve CWL-level expressivity.
Experiments on node and graph classification benchmarks, including large-scale datasets, show that our models are competitive with or better than GNN and higher-order baselines, while substantially reducing computational and memory costs.

---

## 论文详细总结（自动生成）

# 论文详细总结：利用极大团复形扩展高阶图学习

## 1. 核心问题与整体含义
*   **研究背景与动机**：常规图神经网络（GNN）仅能建模节点间的成对关系，表达力受限于 WL 测试，难以捕捉真实世界中普遍存在的高阶依赖（如社交圈、分子环、细胞群落等）。基于拓扑结构（单纯复形、胞腔复形）的高阶模型虽然能捕获团或环等结构，表达力可达甚至超越 WL 测试，但其构建高阶复形的计算与内存开销极高，难以扩展至大规模图。
*   **核心问题**：如何在**保持胞腔 Weisfeiler–Leman 网络 (CWN) 级别表达力**的同时，**显著提升其可扩展性**，并有效利用图上的团结构。
*   **整体含义**：该工作为高阶图学习提供了一种兼具强表达力与实用扩展性的新范式，使得基于团的高阶模型能够真正应用于大规模图数据，为分析细胞图等复杂拓扑系统铺平了道路。

## 2. 方法论
论文的核心思路围绕“简化高阶测试”与“高效构建高阶结构”展开，形成了一套可扩展的团感知架构。

*   **简化与因子化的胞腔 WL 测试 (sCWL / fCWL)**
    *   提出简化的胞腔 WL 测试 (sCWL) 和因子化的胞腔 WL 测试 (fCWL)。
    *   通过理论证明，这两种新测试在颜色细化能力上与原始 CWL 测试**完全等价**，但消息传递与聚合过程更简洁，消除了冗余计算，从而具备更好的可扩展特性。
    *   对应的网络实例化为 sCWN 与 fCWN。

*   **极大团复形 (Maximal Clique Complex)**
    *   定义了一种新的胞腔复形，其高阶胞腔直接由图中**所有的极大团**构成（而非所有团或传统单纯复形中的面）。
    *   在该复形上应用 sCWN/fCWN 进行消息传递，从结构上大幅缩减了需要处理的高阶单元数量，降低了复杂度。

*   **高效团采样：CliqueWalk**
    *   为避免显式枚举极大团（在最坏情况下呈指数级），提出了一种有偏随机游走策略——**CliqueWalk**。
    *   该游走能够高效地采样（极大）团，其时间复杂度与节点数成**拟线性**关系，使得整个框架真正具备大规模可扩展性。

**整体算法流程**：首先利用 CliqueWalk 从输入图中采样并构建极大团复形，然后在该复形上运行 sCWN 或 fCWN，进行高阶特征聚合与学习。

## 3. 实验设计
（注：提供材料中仅含摘要性描述，具体数据集名称未列出，以下基于摘要内容总结）
*   **任务与场景**：同时覆盖**节点分类**与**图分类**两类基准任务。
*   **数据集规模**：明确包含**大规模数据集**，以验证方法在可扩展性方面的优势。
*   **对比方法**：与**标准 GNN 基线**以及现有的**高阶拓扑模型**进行对比。
*   **评测维度**：主要考察分类性能以及**计算与存储开销**的降低幅度。

## 4. 资源与算力
论文元数据和摘要中**未明确披露**所使用 GPU 的型号、数量、单次训练时长或总算力消耗等具体资源信息。

## 5. 实验数量与充分性
*   根据摘要，实验至少覆盖了节点级和图级两种预测任务，并囊括了大规模数据场景，同时与多类基线（GNN、高阶模型）对比，并进行了复杂度分析。
*   从摘要无法获知具体进行了多少组参数实验、是否包含消融实验（如不同采样策略的影响），故难以精确评估实验的绝对充分性。但任务类型和基线选择较为主流，对比维度（性能+效率）客观，初步判断实验设计具有合理性。

## 6. 主要结论与发现
*   **表达力等价**：sCWL 和 fCWL 测试严格保持了原始 CWL 的表达力，但计算效率更高。
*   **结构高效**：极大团复形是一种既能保留高阶信息，又天然压缩冗余结构的高效拓扑载体。
*   **采样即扩展**：CliqueWalk 以拟线性复杂度完成极大团采样，使得基于团的模型首次能轻松处理大规模图。
*   **实际效果显著**：融合上述技术的最终模型在多个基准上达到或超越现有 GNN 和高阶基线，同时**大幅降低了计算时间与内存占用**。

## 7. 优点
*   **理论与实用并重**：对 CWL 进行等价简化，既提供了理论保证，又落实为具体的效率提升。
*   **巧妙的复形构建**：利用极大团代替所有团或单纯形定义胞腔复形，是平衡表达力与复杂度的关键创新。
*   **采样策略优雅**：CliqueWalk 以近线性的开销解决了困扰高阶模型的核心扩展瓶颈，设计极具实用性。
*   **应用前景明确**：方法天然适合对团等紧密耦合结构敏感的场景（如细胞图、生物网络），指向性清晰。

## 8. 不足与局限
*   **团结构的依赖性**：方法依赖图中存在有意义的极大团；对于极度稀疏或无团（如树状结构）的图，极大团复形可能退化为原始图，无法发挥高阶优势。
*   **实验细节缺失**：由于仅有摘要，无法获知具体数据集、参数设置及消融实验细节，对偏差来源（如采样随机性的影响）和通用性上限的评估受限。
*   **最大团规模的隐忧**：在包含超大尺寸极大团的稠密图中，即使采用采样，单个极大团的处理成本可能依然很高，摘要未讨论此极端情况。
*   **成果状态**：该论文为投递至 ICLR 2026 且被拒稿的公开稿件，部分潜在缺陷可能已在评审中指摘，需审慎参考。

（完）
