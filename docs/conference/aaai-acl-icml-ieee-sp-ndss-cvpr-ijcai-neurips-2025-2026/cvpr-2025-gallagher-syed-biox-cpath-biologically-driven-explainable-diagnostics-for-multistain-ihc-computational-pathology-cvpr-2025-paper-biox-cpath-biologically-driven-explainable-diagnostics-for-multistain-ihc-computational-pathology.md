---
title: "BioX-CPath: Biologically-driven Explainable Diagnostics for Multistain IHC Computational Pathology"
title_zh: BioX-CPath：生物驱动的多染色IHC计算病理可解释诊断
authors: "Gallagher-Syed, Amaya, Senior, Henry, Alwazzan, Omnia, Pontarini, Elena, Bombardieri, Michele, Pitzalis, Costantino, Lewis, Myles J., Barnes, Michael R., Rossi, Luca, Slabaugh, Gregory"
date: 2025-06-01
pdf: "https://openaccess.thecvf.com/content/CVPR2025/papers/Gallagher-Syed_BioX-CPath_Biologically-driven_Explainable_Diagnostics_for_Multistain_IHC_Computational_Pathology_CVPR_2025_paper.pdf"
tags: ["query:cell-graph"]
score: 6.0
evidence: 跨染色全切片图像分类的可解释GNN，融合空间/语义特征
tldr: 针对多染色免疫组化计算病理中缺乏可解释模型的问题，该研究提出BioX-CPath，一种可解释的图神经网络架构，用于全切片图像分类。其核心是新颖的染色感知注意力池化模块，能生成具有生物学意义的患者级嵌入。在类风湿关节炎和干燥综合征数据集上取得了最先进性能，并提供了可解释的洞察，展示了空间与语义特征融合在多染色病理分析中的潜力。
source: CVPR-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-gallagher-syed-biox-cpath-biologically-driven-explainable-diagnostics-for-multistain-ihc-computational-pathology-cvpr-2025-paper/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1814, \"height\": 1102}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-gallagher-syed-biox-cpath-biologically-driven-explainable-diagnostics-for-multistain-ihc-computational-pathology-cvpr-2025-paper/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 876, \"height\": 757}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-gallagher-syed-biox-cpath-biologically-driven-explainable-diagnostics-for-multistain-ihc-computational-pathology-cvpr-2025-paper/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 872, \"height\": 755}]"
tables_json: "[{\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-gallagher-syed-biox-cpath-biologically-driven-explainable-diagnostics-for-multistain-ihc-computational-pathology-cvpr-2025-paper/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1624, \"height\": 492}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-gallagher-syed-biox-cpath-biologically-driven-explainable-diagnostics-for-multistain-ihc-computational-pathology-cvpr-2025-paper/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 710, \"height\": 250}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-gallagher-syed-biox-cpath-biologically-driven-explainable-diagnostics-for-multistain-ihc-computational-pathology-cvpr-2025-paper/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 707, \"height\": 243}]"
motivation: 多染色免疫组化计算病理中可解释模型缺乏，难以提供生物学可信的诊断依据。
method: 提出可解释GNN架构，通过染色感知注意力池化融合空间和语义特征生成患者嵌入。
result: 在类风湿关节炎和干燥综合征多染色数据集上达到最优性能，并提供可解释洞察。
conclusion: BioX-CPath有效融合多染色空间语义信息，实现高性能且可解释的病理诊断。
---

## Abstract
The development of biologically interpretable and explainable models remains a key challenge in computational pathology, particularly for multistain immunohistochemistry (IHC) analysis. We present BioX-CPath, an explainable graph neural network architecture for whole slide image (WSI) classification that leverages both spatial and semantic features across multiple stains. At its core, BioXCPath introduces a novel Stain-Aware Attention Pooling (SAAP) module that generates biologically meaningful, stain-aware patient embeddings. Our approach achieves state-of-the-art performance on both Rheumatoid Arthritis and Sjogren's Disease multistain datasets. Beyond performance metrics, BioX-CPath provides interpretable insights through stain attention scores, entropy measures, and stain interaction scores, that permit measuring model alignment with known pathological mechanisms. This biological grounding, combined with strong classification performance, makes BioX-CPath particularly suitable for clinical applications where interpretability is key. Source code and documentation can be found at: https://github.com/AmayaGS/BioX-CPath.

---

## 论文详细总结（自动生成）

## 1. 论文的核心问题与整体含义

- **核心问题**：在计算病理学中，多染色免疫组化（IHC）全切片图像（WSI）分析缺乏既具备生物学可解释性、又能有效融合多染色信息的模型。
- **研究背景与动机**：
  - 现有大多数方法聚焦于 H&E 单染色，主要面向癌症诊断与预后。
  - IHC 常被用于细胞定量、生物标志物预测、图像配准或虚拟染色，但很少直接用于多染色、未配准、未标注的 WSI 分类。
  - 自身免疫病（如类风湿关节炎 RA、干燥综合征 Sjögren）的诊断与分型需要同时理解多种免疫细胞标志物（如 CD20、CD138、CD3 等），因此多染色信息至关重要。
  - 可解释性不足会限制模型在临床中的可信度，需要模型不仅能给出预测，还能提供与病理机制一致的生物学证据。
- **整体含义**：BioX-CPath 旨在将高性能多染色病理分类与可解释的生物学指标相结合，为临床应用提供可信、可验证的决策支持。

## 2. 论文提出的方法论

- **总体框架**：BioX-CPath 是一个可解释图神经网络（GNN）架构，用于多染色 IHC WSI 分类，融合空间与语义特征。
- **预处理与特征提取**：
  - 对每个患者的多染色 WSI 切分 patch，仅保留组织覆盖度达标的 patch。
  - 使用 UNI 特征编码器提取每个 patch 的嵌入向量，得到特征矩阵 \(X_p \in \mathbb{R}^{N \times d}\)。
- **图构建**：
  - **特征空间图 \(G_{FS}\)**：基于特征相似度构建 k 近邻图，捕获语义相似 patch 之间的关系。
  - **区域邻接图 \(G_{RA}\)**：基于 patch 的 \((x,y)\) 坐标以及 WSI 堆叠的 z 轴信息，构建空间相邻连接，允许跨切片连接。
  - 将两者边集合并，得到统一图 \(G_{FRA}\)，节点带有染色类型属性，边带有连接类型属性。
- **位置编码**：
  - 使用随机游走位置编码（RWPE），将节点返回自身的多步概率拼接到特征中，以增强长距离拓扑信息，缓解跨 WSI 堆叠连接中的过平滑问题。
- **骨干网络**：
  - 采用分层图结构，交替堆叠图注意力网络（GAT）层与 **Stain-Aware Attention Pooling（SAAP）** 模块。
  - 最后对每一层 SAAP 输出的染色感知患者嵌入进行拼接，并通过多头自注意力（MHSA）与全连接分类头完成预测。
- **SAAP 模块细节**：
  1. 使用 SAGPool 类似机制计算节点注意力分数 \(a\)，该分数融合节点特征与图拓扑信息。
  2. 按注意力分数排序，保留 top-k 节点，并用注意力分数对特征进行加权，使高相关节点获得更高权重。
  3. 对每个染色 \(s\)，将其所有节点的归一化注意力分数求和，得到染色级权重 \(\alpha_s\)。
  4. 将染色级权重与该染色对应特征加权求和，得到染色感知聚合结果：
     \[
     \text{SA scores} = \sum_{s \in S} \alpha_s \cdot X'_s
     \]
  5. 最终 readout 由均值池化和最大池化拼接而成：
     \[
     \text{Readout} = [\text{mean}_p(\text{SA}) \| \max_p(\text{SA})]
     \]
- **可解释性指标**：
  - **SAAP 分数**：反映各染色对下游任务的诊断相关性。
  - **染色熵分数**：衡量某一染色内注意力分布的集中程度；低熵代表局部、有序的细胞结构，高熵代表弥散、无序的细胞分布。
  - **染色间交互分数**：基于 GAT 边注意力权重，量化不同染色节点之间信息交互的重要性。
  - **GNN 热图**：将第一层 SAAP 的节点注意力分数经 min-max 归一化后映射回空间位置，突出对分类贡献最大的组织区域。

## 3. 实验设计

- **数据集**：
  - **类风湿关节炎（RA）数据集**：
    - 153 名患者，607 张 WSI，分为低炎症（N=66）与高炎症（N=87）两类。
    - 染色类型：H&E、CD20+ B 细胞、CD68+ 巨噬细胞、CD138+ 巨噬细胞；平均每名患者约 3.9 张染色切片。
    - 在 10× 放大倍率下提取 patch，保留组织覆盖率 >40% 的区域，共约 275k patch。
  - **干燥综合征（Sjögren）数据集**：
    - 93 名患者，347 张 WSI，分为非特异性干燥（Sicca，N=46）与 Sjögren 病（N=47）。
    - 染色类型：H&E、CD20、CD3、CD21、CD138；平均每名患者约 3.7 张染色切片。
    - 在 20× 放大倍率下提取 patch，保留组织覆盖率 >30% 的区域，共约 237k patch。
- **评估协议**：
  - 随机标签分层划分 20% 作为测试集，其余数据做 5 折交叉验证（train:val:test = 60:20:20）。
  - 评价指标：准确率、AUC、平均精确率（AP），并报告均值与标准误。
- **对比方法（Benchmark）**：
  - ABMIL、CLAM-SB、TransMIL、DeepGraphConv、Patch-GCN、GTP、MUSTANG。
- **消融实验**：
  - 基线模型（GNN backbone）
  - 增加 MHSA
  - 增加随机游走位置编码（RW）
  - 增加 SAAP 模块（完整 BioX-CPath）

## 4. 资源与算力

- **GPU 信息**：论文明确提到训练在 **NVIDIA A100 GPU（40GB）** 上进行。
- **其他算力细节**：
  - 论文提到在补充材料表 SM.4 中提供了峰值显存（VRAM）和内存使用信息，但正文未给出具体数字。
  - **未明确说明**：GPU 数量、单次训练时长、总训练时间等均未在正文中给出。
- **训练设置**：最大训练 200 个 epoch，早停耐心为 15；使用 AdamW 优化器，学习率 1e-3，权重衰减 0.01，未使用学习率调度器。

## 5. 实验数量与充分性

- **实验组数量**：
  - 2 个独立数据集（RA 与 Sjögren）。
  - 与 7 种 SOTA 方法对比，共产生 14 组基准结果（每数据集 7 个）加上 BioX-CPath 自身结果。
  - 各数据集分别进行 4 组消融实验（Baseline、+MHSA、+RW、+SAAP），共 8 组消融结果。
  - 进一步的可解释性分析：SAAP 分数、染色熵、染色间交互分数、GNN 热图、层级重要性等。
- **充分性评价**：
  - 实验覆盖了两个不同自身免疫病数据集，并对比了多种基于 MIL 和图神经网络的代表性方法，具有较好的方法多样性与任务多样性。
  - 消融实验验证了关键模块（RW 和 SAAP）的贡献，实验设计较完整。
- **客观性与公平性**：
  - 采用随机分层划分与 5 折交叉验证，报告均值和标准误，评估较规范。
  - 所有模型使用相同的数据划分和评价指标，公平性较好；但未说明对比方法的超参数是否针对每个数据集单独调优。
- **不足**：
  - 样本量较小（RA 153 例，Sjögren 93 例），可能限制结论的泛化能力。
  - 只有二分类任务，缺乏多分类或预后预测等更丰富任务验证。
  - 补充材料中的 GNN 热图和交互分数等分析未在正文详细展示，削弱了可解释性证据的完整性。

## 6. 论文的主要结论与发现

- **分类性能**：
  - RA 数据集：BioX-CPath 准确率达到 **0.90 ± 0.019**，比第二好的 MUSTANG（0.86 ± 0.021）高 4 个百分点；AUC 为 0.96 ± 0.007，AP 为 0.98 ± 0.004。
  - Sjögren 数据集：BioX-CPath 准确率为 **0.84 ± 0.018**，优于 CLAM-SB 和 MUSTANG 的 0.80；AUC 为 0.88 ± 0.023，AP 为 0.86 ± 0.032，全面优于其他方法。
- **消融结论**：
  - 随机游走位置编码显著提升性能（例如 RA 从 0.79 升至 0.86，Sjögren 从 0.756 升至 0.80）。
  - SAAP 模块进一步带来巨大提升（RA 升至 0.90，Sjögren 升至 0.84）。
  - MHSA 略有性能下降或波动，但作者认为其带来的可解释性收益值得保留。
- **生物学发现**：
  - RA 的 Pauci-Immune 类型中，CD138 和 CD20 的 SAAP 分数较低，熵也较低，反映淋巴/浆细胞浸润稀少、组织结构较有序。
  - RA 的 Lymphoid/Myeloid 类型中，CD68 和 CD138 注意力分布更均衡，熵更高，符合巨噬细胞与浆细胞在严重疾病中的活跃作用。
  - Sjögren 病中 CD138 注意力显著低于 Sicca，且熵更低，提示浆细胞的组织模式（而非单纯数量）对疾病具有鉴别意义；CD21 的注意力差异与异位淋巴结构形成一致。
  - 这些模式与已知病理机制高度吻合，证明模型学到了具有生物学意义的特征。

## 7. 优点

- **染色感知池化**：SAAP 模块显式建模不同染色的相对重要性，优于简单将所有染色 patch 混合池化的方法。
- **融合空间与语义信息**：图构建同时利用特征相似度和空间邻接关系，并允许跨切片连接，适应未配准多染色数据。
- **可解释性强**：
  - 提供染色级注意力、熵、染色间交互分数和热图等多种可视化与量化指标。
  - 这些指标不仅解释模型决策，还能验证模型与已知生物病理机制的一致性。
- **结构设计合理**：
  - 随机游走位置编码缓解了深层 GNN 的过平滑和长距离信息丢失问题。
  - 分层 GAT + SAAP 结构在保持性能的同时降低计算复杂度。
- **实验对比充分**：与多种 SOTA MIL/GNN 方法比较，并进行了系统的消融实验。
- **开源与可复现**：提供源代码和文档，便于社区进一步验证和扩展。

## 8. 不足与局限

- **数据规模与多样性有限**：
  - 仅使用了两个自身免疫病数据集，且样本量较小（RA 153 例，Sjögren 93 例）。
  - 任务均为二分类，缺乏多分类、生存分析或治疗响应预测等更复杂的临床任务验证。
- **缺乏外部验证**：未在其他机构或独立队列上验证模型的泛化能力。
- **计算资源信息不完整**：
  - 仅说明使用 A100 GPU，未报告 GPU 数量、训练时长和具体显存占用，难以评估实际算力需求。
- **可解释性分析部分未完全展开**：
  - GNN 热图、染色间交互分数和层级重要性等核心可解释性结果放在补充材料中，正文只展示了部分 SAAP 分数和熵分布。
  - 缺少与病理医生人工判读的定量一致性评估。
- **MHSA 带来的性能波动**：尽管作者为可解释性保留 MHSA，但其对性能的提升不明显甚至略有下降，可能增加模型复杂度但收益有限。
- **特征提取器依赖**：仅使用 UNI 作为特征提取器，未系统比较其他病理基础模型，结论可能受特征提取器选择影响。
- **染色数量不一致处理**：论文提到患者平均染色数可变，但未详细说明如何处理缺失染色或不平衡染色数量的具体策略
