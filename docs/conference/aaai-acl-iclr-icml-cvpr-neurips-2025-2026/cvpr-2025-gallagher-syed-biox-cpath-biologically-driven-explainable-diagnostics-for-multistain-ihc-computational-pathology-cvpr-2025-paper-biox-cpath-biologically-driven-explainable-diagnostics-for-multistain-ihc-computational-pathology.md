---
title: "BioX-CPath: Biologically-driven Explainable Diagnostics for Multistain IHC Computational Pathology"
title_zh: "BioX-CPath: 基于生物驱动的可解释诊断方法用于多标记免疫组化计算病理学"
authors: "Gallagher-Syed, Amaya, Senior, Henry, Alwazzan, Omnia, Pontarini, Elena, Bombardieri, Michele, Pitzalis, Costantino, Lewis, Myles J., Barnes, Michael R., Rossi, Luca, Slabaugh, Gregory"
date: 2025-06-01
pdf: "https://openaccess.thecvf.com/content/CVPR2025/papers/Gallagher-Syed_BioX-CPath_Biologically-driven_Explainable_Diagnostics_for_Multistain_IHC_Computational_Pathology_CVPR_2025_paper.pdf"
tags: ["query:immuno-topo"]
score: 9.0
evidence: 利用可解释图神经网络对免疫组化全切片图像中免疫微环境的空间拓扑进行建模。
tldr: 现有计算病理学模型缺乏生物学可解释性，尤其对于多标记免疫组化分析。本文提出BioX-CPath，一种可解释的图神经网络架构，通过新颖的染色感知注意力池化模块生成具有生物学意义的患者嵌入，同时捕获多标记免疫微环境的空间拓扑特征。该方法在类风湿关节炎和干燥综合征数据集上取得最先进性能，并提供了可解释的洞察。其贡献在于为免疫微环境的空间表征提供了透明且高效的深度学习方法。
source: CVPR-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-gallagher-syed-biox-cpath-biologically-driven-explainable-diagnostics-for-multistain-ihc-computational-pathology-cvpr-2025-paper/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1814, \"height\": 1102, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-gallagher-syed-biox-cpath-biologically-driven-explainable-diagnostics-for-multistain-ihc-computational-pathology-cvpr-2025-paper/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 876, \"height\": 757, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-gallagher-syed-biox-cpath-biologically-driven-explainable-diagnostics-for-multistain-ihc-computational-pathology-cvpr-2025-paper/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 872, \"height\": 755, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-gallagher-syed-biox-cpath-biologically-driven-explainable-diagnostics-for-multistain-ihc-computational-pathology-cvpr-2025-paper/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1624, \"height\": 492, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-gallagher-syed-biox-cpath-biologically-driven-explainable-diagnostics-for-multistain-ihc-computational-pathology-cvpr-2025-paper/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 710, \"height\": 250, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-gallagher-syed-biox-cpath-biologically-driven-explainable-diagnostics-for-multistain-ihc-computational-pathology-cvpr-2025-paper/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 707, \"height\": 243, \"label\": \"Table\"}]"
motivation: 多标记免疫组化分析需要生物学可解释的模型来挖掘免疫微环境空间特征。
method: 提出染色感知注意力池化的可解释图神经网络，对WSI进行空间拓扑建模。
result: 在自身免疫病数据集上取得SOTA，且提供生物学可解释性。
conclusion: BioX-CPath为IHC计算病理学提供了建立于免疫空间拓扑之上的透明诊断框架。
---

## Abstract
The development of biologically interpretable and explainable models remains a key challenge in computational pathology, particularly for multistain immunohistochemistry (IHC) analysis. We present BioX-CPath, an explainable graph neural network architecture for whole slide image (WSI) classification that leverages both spatial and semantic features across multiple stains. At its core, BioXCPath introduces a novel Stain-Aware Attention Pooling (SAAP) module that generates biologically meaningful, stain-aware patient embeddings. Our approach achieves state-of-the-art performance on both Rheumatoid Arthritis and Sjogren's Disease multistain datasets. Beyond performance metrics, BioX-CPath provides interpretable insights through stain attention scores, entropy measures, and stain interaction scores, that permit measuring model alignment with known pathological mechanisms. This biological grounding, combined with strong classification performance, makes BioX-CPath particularly suitable for clinical applications where interpretability is key. Source code and documentation can be found at: https://github.com/AmayaGS/BioX-CPath.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义
- **研究背景**：计算病理学中，全切片图像（WSI）分析已成为癌症和自身免疫病诊断的黄金标准。然而，现有方法多集中于苏木精-伊红（H&E）单染色，对多标记免疫组化（IHC）的整合分析不足，且模型普遍缺乏生物学可解释性。
- **核心问题**：如何构建一个既能融合多染色空间与语义信息，又能生成生物学可解释决策依据的WSI分类模型。
- **整体含义**：BioX‑CPath 旨在通过图神经网络架构和专门的染色感知池化模块，在保证分类性能的同时，显式地输出染色重要性、熵值、染色间交互等指标，使模型的判断与已知病理机制对齐，从而提升临床可信度。

### 2. 方法论
- **核心思想**：将同一患者的多种染色WSI构建成一个特征空间‑空间邻近混合图，通过分层图神经网络学习节点表示，再经由“染色感知注意力池化”（SAAP）生成染色级和患者级的嵌入，最终用于分类。
- **关键技术细节**：
  - **图初始化**：分别构建特征空间K近邻图（语义相似）和区域邻接图（空间邻近），取边集并集得到 \( G_{FRA} \)。每个节点附带染色类型属性。
  - **位置编码**：使用随机游走位置编码（RWPE）为节点注入全局拓扑信息，并在每层重新拼接。
  - **层次化GNN骨干**：交替堆叠图注意力网络（GAT）层和SAAP池化层，以缓解过平滑并逐步筛选重要节点。
  - **SAAP模块**：利用自注意力图池化（SAGPool）计算节点重要性得分；按染色分组，求和归一化得分得到染色权重 \(\alpha_s\)；染色感知加权特征经均值‑最大化池化后拼接为患者级表示。
  - **分类头**：堆叠多层的SAAP输出经多头自注意力（MHSA）融合，再送入全连接层进行二分类。
- **可解释性指标**：
  - **SAAP 分数**：各染色的注意力权重，反映诊断重要性。
  - **染色熵分数**：\( H_s = -\sum a'_n \log a'_n \)，衡量染色内注意力分布的集中度（低熵 → 集中，高熵 → 弥散）。
  - **染色间交互分数**：基于GAT层注意力权重的边重要性聚合，量化不同染色节点间的信息流。
  - **GNN 热图**：将第一层SAAP的节点得分映射回空间位置，可视化关键区域。

### 3. 实验设计
- **数据集**：
  - **类风湿关节炎（RA）**：153例患者，607张WSI，包括H&E、CD20、CD68、CD138染色，二分类为低炎症 vs. 高炎症亚型。
  - **干燥综合征（Sjogren）**：93例患者，347张WSI，包括H&E、CD20、CD3、CD21、CD138染色，二分类为非特异性干燥症 vs. 干燥综合征。
- **基准方法**：对比7种前沿方法：ABMIL、CLAM‑SB、TransMIL、DeepGraphConv、PatchGCN、GTP、MUSTANG。
- **评估方式**：随机按标签分层抽取20%为留出测试集，其余部分进行5折交叉验证；报告准确率、宏观F1、精确率、召回率、AUC和平均精确率的均值±标准误。
- **消融实验**：逐步添加 MHSA、随机游走位置编码、SAAP 模块，验证各组件的贡献。

### 4. 资源与算力
- **GPU**：训练使用单张NVIDIA A100（40 GB）。
- **训练设置**：AdamW优化器，学习率1e‑3，权重衰减0.01，最多200个epoch，early stopping耐心值15，无学习率调度器。
- **其他**：文中给出了峰值显存和内存使用情况的补充表格，但未明确报告单次训练的墙钟时间或总GPU小时。

### 5. 实验数量与充分性
- **主实验**：在2个数据集上对7种baseline和自身模型进行完整对比（共16组主要结果）。
- **消融实验**：在2个数据集上分别进行了3项组件消融（baseline, +MHSA, +RW, +SAAP），共8组。
- **可解释性分析**：针对每个数据集，展示SAAP分数、熵分数箱线图，并进行了统计检验；补充材料中还有染色交互分数、GNN热图、层重要性分析等。
- **充分性与公平性**：实验覆盖面较好，包含独立测试集，baseline选择恰当，消融逻辑清晰。但数据集规模较小（均<200例），结果的外推性需进一步验证；此外，未与更近期的MIL变体（如基于Transformer或原型学习的方法）全面比较。

### 6. 主要结论与发现
- BioX‑CPath 在两个多染色数据集上均取得最优准确率（RA 0.90，Sjogren 0.84），并在AUC、平均精确率上具有竞争力。
- 消融实验证实SAAP模块是性能提升的关键，随机游走位置编码也带来显著增益。
- 可解释性分析表明，模型学习到的染色重要性（如RA中CD138和CD20在淋巴样/髓系亚型中更受关注）和熵模式（炎症浸润的有序/无序程度）与已知病理机制高度一致。

### 7. 优点
- **生物学可解释性强**：显式输出染色级权重、熵、交互分数等，使模型“黑盒”变得透明，且与病理学知识一致。
- **专为多染色设计**：SAAP模块原生支持多模态染色数据，并通过图边集合的方式将空间与语义信息有效融合。
- **性能领先**：在两个自身免疫病数据集中超越了当前SOTA多染色方法MUSTANG以及其他通用WSI分类方法。
- **全面的可解释性验证**：不仅给出注意力权重，还引入熵和交互分数，从多个维度提供证据。

### 8. 不足与局限
- **数据规模与多样性**：两个数据集均来自单中心、小样本（<160例），且集中在自身免疫病，缺乏在更大规模、多中心、癌种数据集上的验证。
- **对比方法可能不够新**：主要对比了2023年前的MIL和GNN方法，未纳入2024‑2025年最新的MIL变体（如基于多模态大模型的方案）。
- **性能‑可解释性权衡**：MHSA模块虽提升可解释性，但带来了轻微的性能回退，论文未深入探讨该权衡。
- **染色依赖性**：模型假设所有患者拥有相同的染色组合，对部分染色缺失的情况未讨论处理策略。
- **空间分辨率**：对IHC采用与H&E相同的10×/20×提取，未专门优化不同染色特性的放大倍率。
- **计算资源描述不足**：未提供训练时长、吞吐量等实际部署成本信息。

（完）
