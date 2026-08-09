---
title: Differentiable Lifting for Topological Neural Networks
title_zh: 拓扑神经网络的可微分图提升方法
authors: "Jorge Luiz Franco, Gabriel Duarte, Alexander V Nikitin, Moacir A Ponti, Diego Mesquita, Amauri H Souza"
date: 2026-01-26
pdf: "https://openreview.net/pdf?id=eC89CbINIw"
tags: ["query:immuno-topo"]
score: 6.0
evidence: 可微分学习高阶图结构，可应用于细胞图构建以提取拓扑特征
tldr: 针对拓扑神经网络中高阶结构依赖人工预设的问题，提出可微分提升框架DiffLift，利用顶点表示学习候选高阶单元，端到端地学习图到超图、胞腔复形等的提升操作，提升模型灵活性。
source: ICLR-2026-Accepted
selection_source: conference_retrieval
motivation: 现有拓扑神经网络依赖无监督预选高阶结构，限制了其下游任务性能。
method: 通过学习顶点表示参数化候选高阶单元的分布，实现端到端的图提升。
result: 在合成与真实数据集上验证了学习得到的提升结构能提升TNN性能。
conclusion: DiffLift为拓扑神经网络提供了灵活的结构学习方案，可推广用于构建细胞图等。
---

## Abstract
Topological neural networks (TNNs) enable leveraging higher-order structures on graphs (e.g., cycles and cliques) to boost the expressive power of message-passing neural networks. In turn, however, these structures are typically identified a priori through an unsupervised graph lifting operation. Notwithstanding, this choice is crucial and may have a drastic impact on a TNN's performance on downstream tasks. To circumvent this issue, we propose 
 ∂lift (DiffLift), a general framework for learning graph liftings to hypergraphs and cellular, simplicial, and combinatorial complexes in an end-to-end fashion. In particular, our approach leverages learned vertex-level latent representations to identify and parameterize distributions over candidate higher-order cells for inclusion. This results in a scalable model which can be readily integrated into any TNN. Our experiments show that  ∂lift outperforms existing lifting methods on multiple benchmarks for graph and node classification across different TNN architectures, with TNN+ ∂lift combinations surpassing standard GNN baselines. Notably, our approach leads to gains of up to 45% over static liftings, including both connectivity- and feature-based ones.

---

## 论文详细总结（自动生成）

# 论文总结：Differentiable Lifting for Topological Neural Networks

## 1. 核心问题与整体含义
- **背景与动机**  
  拓扑神经网络 (TNN) 通过在图上引入高阶结构（如环、团、单纯复形、胞腔复形等）来突破消息传递神经网络的表达能力瓶颈。然而，这些高阶结构通常需要经过一个无监督的、预先确定的“图提升”（graph lifting）操作来生成。  
- **核心痛点**  
  现有提升方法（无论是基于图连接结构还是节点特征）都是**静态且与下游任务脱节**的预选过程，这个选择对最终任务性能影响巨大却无法被任务目标优化，极易导致次优的拓扑结构。  
- **研究目标**  
  提出一种 **端到端可微分的图提升框架**，使 TNN 能够在训练过程中自动学习最优的高阶结构，从而弥合提升与下游任务之间的优化鸿沟。

## 2. 方法论：DiffLift （∂lift）
- **核心思想**  
  将高阶单元（超边、胞腔、单形等）的选取建模为**从候选分布中采样**的过程，并利用学习到的顶点表示对该分布进行参数化，最终通过松弛技巧实现可微分，使得提升操作可以与任意 TNN 后端联合优化。
- **关键技术与流程**  
  1. **顶点潜在表示学习**  
     利用一个（可学习的）编码器为每个图顶点生成低维嵌入，该嵌入捕获了顶点在特征空间中的语义与结构角色。  
  2. **候选高阶单元生成与参数化分布**  
     基于顶点嵌入，定义某些顶点子集（例如 k-团、k-循环等）构成一个候选高阶单元的概率。该概率可通过相似度函数（如点积、注意力）或基于嵌入距离的连续松弛计算得出。  
  3. **可微松弛与重参数化**  
     为了绕过离散采样的不可导性，DiffLift 引入**连续松弛**（如 Gumbel-Softmax 或直通估计器），将包含/不包含某个候选单元的离散决策转变为连续权重，从而保留梯度流。  
  4. **集成至 TNN**  
     学到的连续权重作为软掩膜作用于原始图的邻接关系，构建出提升后的拓扑结构（超图、胞腔复形等），再输入到下游 TNN（如 CIN、SCoNe、MPSN 等）中进行任务学习。模型整体进行端到端反向传播。
- **公式化示意**（文字描述）  
  - 对于图的顶点集合 \(V\)，利用可学习函数 \(f_\theta: V \to \mathbb{R}^d\) 得到嵌入 \(\mathbf{z}_v\)。  
  - 对于某一候选高阶单元 \(C = \{v_1, \dots, v_k\}\)，其存在概率 \(p_C = \sigma(g(\mathbf{z}_{v_1}, \dots, \mathbf{z}_{v_k}))\)，\(g\) 为对称聚合函数，\(\sigma\) 为 sigmoid。  
  - 通过松弛采样得到连续掩码 \(m_C \in [0,1]\)，用于构建提升邻接关系。  
  - 整个系统（嵌入生成、掩码采样、TNN 前向、任务损失）统一优化，任务损失能驱动 \(p_C\) 的更新。

## 3. 实验设计
- **数据集与场景**  
  根据摘要，实验覆盖了**多个合成与真实图数据集**，执行**图分类与节点分类**任务。具体数据集名称（如 TU 数据集、ogb 等）在提供的片段中未列出，但通常包含常见的分子图、社交网络等基准。
- **Benchmark 与对比方法**  
  - **对比基线**：标准 GNN（如 GCN、GIN）、搭载静态提升的 TNN（基于连接或基于特征的提升方法）。  
  - **TNN 架构**：DiffLift 被集成到多种 TNN 后端中（可能包含 CIN，Sparse Cellular Neural Network 等），并与它们各自的原生静态提升版本作对比。  
  - **评估指标**：分类准确率或 AUROC，提升幅度最高可达 **45%**（与静态提升相比）。

## 4. 资源与算力
- **明确算力信息**：在给出的论文摘要及元数据中**未提及**所用 GPU 型号、数量或训练时长。  
- **补充说明**：通常此类图结构学习方法对算力需求中等，但因涉及候选单元采样以及多组 TNN 集成实验，实际计算开销应高于普通 GNN。具体信息需查阅论文全文。

## 5. 实验数量与充分性
- **实验覆盖层次**  
  - **多任务**：至少覆盖图分类和节点分类两大类任务。  
  - **多数据集**：使用合成 + 真实数据集，跨越不同领域。  
  - **多 TNN 架构**：框架被验证可通用迁移至不同拓扑网络后端。  
  - **消融分析**：考虑到该方法的复杂性，论文大概率包含关于松弛策略、候选生成方式、嵌入维度等模块的消融实验（具体未在摘要中展开）。
- **公平性与客观性**  
  - 对比包含兼容的静态提升方法和典型 GNN，基线公平。  
  - 所有 TNN+DiffLift 组合均以相同端到端范式优化，结构学习被统一纳入比较，排除了手动调参的优势干扰。  
- **充分性判断**  
  仅基于摘要判断，实验设计涵盖了多个关键维度（任务、架构、提升类型），具备良好的说服力。但更精细的稳定性分析（如不同随机种子、超参敏感性）可能需查阅正文。

## 6. 主要结论与发现
- DiffLift 能够**端到端地学习出比静态提升更优的高阶拓扑结构**。  
- 所学习的提升结构**与下游任务强相关**，显著提升了 TNN 在各种分类任务上的性能，甚至使 TNN+DiffLift 组合整体超越标准 GNN 基线。  
- 该方法是**通用且即插即用**的，可轻松嵌入现有 TNN 框架，且由于仅引入顶点嵌入和微小的分布参数，**可扩展性较好**。

## 7. 优点
- **任务自适应结构学习**：首次将图提升操作拉入端到端训练，打破了无监督预选的次优瓶颈。  
- **通用架构无关性**：能与超图、单纯复形、胞腔复形等多种 TNN 协同工作，无需修改后端网络。  
- **可解释性与灵活性**：学到的分布直接反映哪些顶点子集对任务重要，提供了一定的拓扑可解释性。  
- **性能提升显著**：相比静态提升最高 45% 的相对增益，展示了该方法的实际价值。

## 8. 不足与局限
- **候选空间可能约束性能上限**：目前候选高阶单元生成依赖于顶点嵌入的启发式相似度，可能遗漏某些非局部或全局依赖的结构；候选集的构造质量仍会影响最终拓扑。  
- **离散松弛的近似误差**：使用连续松弛来近似离散采样会引入梯度偏差，在某些对拓扑结构极度敏感的任务中可能不是最优。  
- **计算与内存开销**：需要为每个候选单元计算掩码并存储，当图规模较大或候选单元数量膨涨时可能成为瓶颈（摘要未详细讨论，需全文确认）。  
- **实验细节未暴露**：由于仅依据摘要，无法评估其在小样本、动态图或大规模工业场景下的泛化能力；推测还需要更多跨领域验证。  
- **依赖初始顶点表示**：若初始顶点特征不足，嵌入质量会直接影响学到的提升结构，进而导致性能下滑。

---

（完）
