---
title: "BioX-CPath: Biologically-driven Explainable Diagnostics for Multistain IHC Computational Pathology"
title_zh: BioX-CPath：面向多重染色IHC计算病理学的生物学驱动可解释诊断
authors: "Gallagher-Syed, Amaya, Senior, Henry, Alwazzan, Omnia, Pontarini, Elena, Bombardieri, Michele, Pitzalis, Costantino, Lewis, Myles J., Barnes, Michael R., Rossi, Luca, Slabaugh, Gregory"
date: 2025-06-01
pdf: "https://openaccess.thecvf.com/content/CVPR2025/papers/Gallagher-Syed_BioX-CPath_Biologically-driven_Explainable_Diagnostics_for_Multistain_IHC_Computational_Pathology_CVPR_2025_paper.pdf"
tags: ["query:immuno-topo"]
score: 7.0
evidence: 基于GNN的IHC全切片图像免疫微环境空间分析与可解释注意力。
tldr: BioX-CPath提出一种带有染色感知注意力池化的图神经网络，用于多重染色IHC全切片图像的可解释分类，在自身免疫疾病数据集上达到最优性能，并提供免疫微环境空间组织的可解释洞察。
source: CVPR-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-gallagher-syed-biox-cpath-biologically-driven-explainable-diagnostics-for-multistain-ihc-computational-pathology-cvpr-2025-paper/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1814, \"height\": 1102, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-gallagher-syed-biox-cpath-biologically-driven-explainable-diagnostics-for-multistain-ihc-computational-pathology-cvpr-2025-paper/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 876, \"height\": 757, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-gallagher-syed-biox-cpath-biologically-driven-explainable-diagnostics-for-multistain-ihc-computational-pathology-cvpr-2025-paper/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 872, \"height\": 755, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-gallagher-syed-biox-cpath-biologically-driven-explainable-diagnostics-for-multistain-ihc-computational-pathology-cvpr-2025-paper/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1624, \"height\": 492, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-gallagher-syed-biox-cpath-biologically-driven-explainable-diagnostics-for-multistain-ihc-computational-pathology-cvpr-2025-paper/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 710, \"height\": 250, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-gallagher-syed-biox-cpath-biologically-driven-explainable-diagnostics-for-multistain-ihc-computational-pathology-cvpr-2025-paper/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 707, \"height\": 243, \"label\": \"Table\"}]"
motivation: 多染色IHC计算病理学中可解释诊断模型不足。
method: 提出BioX-CPath，包含新型染色感知注意力池化模块的图神经网络。
result: 在类风湿关节炎和干燥症数据集上取得最优性能，并生成有生物学意义的嵌入。
conclusion: 该方法为多染色IHC病理分析提供了可解释且高性能的框架，实现了免疫微环境的空间拓扑建模。
---

## Abstract
The development of biologically interpretable and explainable models remains a key challenge in computational pathology, particularly for multistain immunohistochemistry (IHC) analysis. We present BioX-CPath, an explainable graph neural network architecture for whole slide image (WSI) classification that leverages both spatial and semantic features across multiple stains. At its core, BioXCPath introduces a novel Stain-Aware Attention Pooling (SAAP) module that generates biologically meaningful, stain-aware patient embeddings. Our approach achieves state-of-the-art performance on both Rheumatoid Arthritis and Sjogren's Disease multistain datasets. Beyond performance metrics, BioX-CPath provides interpretable insights through stain attention scores, entropy measures, and stain interaction scores, that permit measuring model alignment with known pathological mechanisms. This biological grounding, combined with strong classification performance, makes BioX-CPath particularly suitable for clinical applications where interpretability is key. Source code and documentation can be found at: https://github.com/AmayaGS/BioX-CPath.

---

## 论文详细总结（自动生成）

## BioX-CPath 论文详细总结

### 1. 论文的核心问题与整体含义
- **研究动机**：在计算病理学中，尤其是针对多重免疫组织化学（IHC）的全切片图像（WSI）分析，现有方法多聚焦于单染色的 H&E 图像，难以整合多重染色所揭示的复杂细胞景观。同时，当前模型普遍缺乏生物可解释性，难以验证其预测与已知病理机制的一致性，限制了在临床诊断中的信任与应用。
- **核心问题**：如何设计一个既能对未配准、未标注的多重染色 IHC 数据进行精准分类，又能从生物学角度提供可解释诊断洞察的框架。
- **整体含义**：提出的 BioX-CPath 架构通过图神经网络将多染色间的空间与语义特征相融合，并引入染色感知注意力池化，使得模型不仅取得领先的分类性能，还能输出染色重要性、染色内熵、染色间交互等具有病理学意义的指标，连接了性能与生物学可解释性之间的鸿沟。

### 2. 论文提出的方法论
- **整体思路**：构建一个层次化图神经网络，以患者为单位，将多重染色 WSI 的补丁表示为图节点，并联合特征空间和空间相邻两种边关系，通过染色感知注意力池化（SAAP）模块提炼具有诊断分辨力的、按染色划分的患者级表征。
- **关键技术细节**：
    - **图构建**：对每个患者的 WSIs 提取补丁并用 UNI 特征编码器得到特征矩阵。分别构建特征空间 k-近邻图（GF_S）和空间区域邻接图（GRA），取两者边集的并集得到混合图 GF_RA，以同时捕获语义相似性和跨切片的物理邻近关系。节点属性包含其来源的染色类型。
    - **位置编码**：为每个节点计算固定长度的随机游走位置编码，并追加至节点特征，以提供全局拓扑结构信息。
    - **层次化图块**：主干网络交替堆叠图注意力网络（GAT）层和 SAAP 模块。GAT 用于消息传递，SAAP 用于下采样并提炼染色特异的摘要。
    - **SAAP 模块**：基于 SAGPool 方法计算节点注意力分数 a；取 top-k 个节点并用注意力分数对特征加权；然后按节点所属的染色类型 s 汇总归一化注意力得分，得到染色层级权重 α_s；最后对各染色加权特征做染色内池化，并连接全局均值与最大池化，生成染色感知的患者嵌入。公式为：α_s = Σ (归一化注意力得分)，然后 Readout = [mean_p(SA) ∥ max_p(SA)]。
    - **分类头**：将多层的染色感知嵌入拼接后经多头自注意力（MHSA）融合，送入全连接分类层。
    - **可解释性指标**：基于 SAAP 和 GAT 注意力权重导出 SAAP 分数（染色重要性）、染色熵分数（注意力集中度）、染色间交互分数（边注意力均值）以及 GNN 节点热图。

### 3. 实验设计
- **数据集**：
    - **类风湿关节炎（RA）**：153 例患者，607 张 WSI，包含 H&E 和 CD20、CD68、CD138 等 IHC 标记，任务为区分低炎症与高炎症亚型（二分类）。
    - **干燥综合征（Sjögren）**：93 例患者，347 张 WSI，包含 H&E 和 CD3、CD20、CD21、CD138 等标记，任务为区分非特异性干燥（Sicca）与干燥综合征（二分类）。
- **Benchmark 与方法**：对比了 ABMIL、CLAM‑SB、TransMIL、DeepGraphConv、Patch‑GCN、GTP 以及 MUSTANG 共 7 种 SOTA 方法。
- **评估指标**：准确率、AUC、平均精度（AP），均报告 5 折交叉验证在 20% 独立测试集上的均值和标准误。

### 4. 资源与算力
- 训练均在 **1 张 NVIDIA A100 GPU（40 GB 显存）** 上完成。
- 文中提供了峰值显存和内存占用表（补充材料 SM.4），但未明确提及单次训练的时长。训练最多设为 200 个 epoch，早停耐心值为 15。

### 5. 实验数量与充分性
- **主要实验**：在两个独立数据集上，分别与 7 个基线方法进行了全面比较，覆盖 ACC、AUC、AP 三项核心指标。
- **消融研究**：在两个数据集上均进行了组件消融（基线/仅 GAT+SAAP+MHSA）、添加随机游走位置编码（+RW）、添加 SAAP（+SAAP），共约 8 组消融结果，验证了各模块的贡献。
- **可解释性分析**：通过箱线图、统计检验（p 值）和热图深入分析了模型决策与生物学机制的对齐，包括染色重要性分布、熵差异、染色间交互等。
- **充分性与公平性**：实验设计较完整，包含多种 SOTA 对比、交叉验证和标准误计算，消融实验清晰。基线方法均采用原文默认设置或最优参数，对比基本公平。局限性在于未在更多外部数据集或不同特征提取器上进行验证。

### 6. 论文的主要结论与发现
- BioX-CPath 在 RA 和 Sjögren 数据集的分类准确率上均超越所有基线方法，分别达到 0.90 和 0.84，展现了对多染色 IHC 数据的强大建模能力。
- 提出的 SAAP 模块和可解释性指标能够有效捕捉生物学上有意义的模式：例如，在 RA 中贫免疫亚型 CD20/CD138 注意力低且熵低，符合淋巴浆细胞浸润稀少的特点；在 Sjögren 中，CD138 注意力显著低于 Sicca 组且熵值更低，揭示了浆细胞的组织化分布差异，与异位淋巴结构形成一致。
- 模型不仅实现了高性能诊断，更能提供与已知病理机制高度吻合的生物学线索，验证了其临床应用的潜力。

### 7. 优点
- **创新的染色感知池化**：SAAP 模块显式地为不同染色学习可解释的权重，使患者嵌入具备生物学意义。
- **双图融合设计**：联合特征空间图与区域邻接图，有效捕获跨染色、跨位置的语义和空间关联。
- **多层次可解释性**：系统性地提出 SAAP 分数、染色熵、染色间交互分数和 GNN 热图，将黑盒模型转化为可验证的病理学洞察工具。
- **SOTA 性能**：在两个真实临床多染色数据集上均取得最优结果，证明了方法的泛化性和有效性。
- **开源代码**：提供完整代码与文档，利于复现和社区发展。

### 8. 不足与局限
- **数据集限制**：两个数据集均来自自身免疫病，且样本量相对有限（RA 153 例，Sjögren 93 例），未在癌症等其他多染色场景中测试，普适性有待验证。
- **特征提取器单一**：仅使用 UNI 特征编码器，未探讨不同预训练特征对图构建及最终结果的影响。
- **运算代价**：整个流水线需构建并处理大规模图，训练使用 A100(40GB)，对计算资源和显存有较高要求，文中未对比推理效率。
- **可解释性验证**：可解释性分析仍主要为回顾性，虽有统计检验，但未进行前瞻性临床验证或让病理学家直接评估模型所提供解释的可用性。
- **模块间权衡**：引入 MHSA 层在部分数据集上带来了轻微的性能下降，显示出模型复杂度与性能之间存在未完全调优的权衡空间。

（完）
