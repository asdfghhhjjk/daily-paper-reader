---
title: Multimodal Cancer Survival Analysis via Hypergraph Learning with Cross-Modality Rebalance
title_zh: 基于超图学习与跨模态再平衡的多模态癌症生存分析
authors: "(PDF |   Details)"
date: 2025-08-01
pdf: "https://www.ijcai.org/proceedings/2025/0201.pdf"
tags: ["query:cellseg"]
score: 6.0
evidence: 采用超图学习进行多模态癌症生存分析，可能整合病理特征用于预后。
tldr: 多模态数据整合有望提高癌症生存预测精度，但不同模态间的不平衡问题限制了模型效能。本文提出基于超图学习的多模态生存分析方法，引入跨模态再平衡机制。尽管缺少详细摘要，该方法可能整合病理图像、基因组等特征，通过超图建模高阶关系，为预后建模提供新思路。
source: IJCAI-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/ijcai-2025-accepted/ijcai-2025-201/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 893, \"height\": 533, \"label\": \"Figure\"}, {\"url\": \"assets/figures/ijcai-2025-accepted/ijcai-2025-201/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1831, \"height\": 893, \"label\": \"Figure\"}, {\"url\": \"assets/figures/ijcai-2025-accepted/ijcai-2025-201/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 901, \"height\": 295, \"label\": \"Figure\"}, {\"url\": \"assets/figures/ijcai-2025-accepted/ijcai-2025-201/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1838, \"height\": 806, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/ijcai-2025-accepted/ijcai-2025-201/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1811, \"height\": 798, \"label\": \"Table\"}, {\"url\": \"assets/tables/ijcai-2025-accepted/ijcai-2025-201/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 881, \"height\": 262, \"label\": \"Table\"}, {\"url\": \"assets/tables/ijcai-2025-accepted/ijcai-2025-201/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 882, \"height\": 233, \"label\": \"Table\"}, {\"url\": \"assets/tables/ijcai-2025-accepted/ijcai-2025-201/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 884, \"height\": 196, \"label\": \"Table\"}]"
motivation: 多模态生存分析面临模态不平衡和特征交互建模挑战。
method: 提出超图学习与跨模态再平衡方法，建模多模态数据的高阶关系进行生存预测。
result: 方法可能有效整合多模态特征，提升生存分析性能。
conclusion: 超图学习为多模态预后建模提供了新的技术路径。
---

## Abstract
No abstract is available.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义
- **研究问题**：多模态（全切片病理图像 WSI + 基因组数据）癌症生存预测面临两大挑战：
  - **信息丢失**：现有方法多用多实例学习（MIL）聚合 patch 级特征，忽略病理图像中的上下文（空间关系、肿瘤微环境）和层次（细胞到组织级别）细节。
  - **模态不平衡**：病理数据拥有高空间分辨率和大量 patch，而基因组数据信号密度低、维度较小，在融合过程中病理模态往往主导预测，削弱基因组的作用。
- **整体含义**：论文提出 MRePath（Multi-Modal Rebalance for Pathology-Genomic Survival Prediction），利用超图学习捕获病理图像的上下文与层次信息，并设计动态再平衡机制和交互式对齐融合策略，缓解模态不平衡，提升生存预测精度。

### 2. 方法论
- **特征提取**
  - **病理特征**：将 WSI 切分为 256×256 的 patch（20×放大），用预训练 ResNet50 提取 d 维特征，得到 \(P\in \mathbb{R}^{N\times d}\)，N 为 patch 数。
  - **基因组特征**：选取 RNA-seq、CNV、突变状态中高信噪比基因，分为 6 个功能组，用 MLP 嵌入为 \(G\in \mathbb{R}^{M\times d}\)，M 为基因类别数。
- **超图学习**
  - **超图构建**：每个 patch 作为节点，超边由拓扑空间（基于欧氏距离邻近关系）和特征空间（基于特征相似度）两种方式生成，合并得到混合超边集合。
  - **层杆超图（Sheaf Hypergraph）**：在超图卷积中用层杆拉普拉斯算子替代普通拉普拉斯，让节点和超边之间形成信息流动空间，捕获局部上下文与全局层次关系，输出精炼病理特征 \(P^h\)。
- **模态再平衡**
  - **动态加权**：
    - 单置信度（mono‑confidence）：对病理 \(P\) 和基因组 \(G\) 分别用可学 MLP 计算可靠性得分 \(w^m_p, w^m_g\)。
    - 全置信度（holo‑confidence）：基于单置信度的交叉模态交互计算 \(w^h_p, w^h_g\)，衡量模态间的协调与互补。
    - 最终权重 \(w_p, w_g\) 由单置信度和全置信度相加后经 softmax 得到，并用其对特征加权：\(P^w=w_pP^h, G^w=w_gG\)。
  - **交互式对齐融合**：
    - 基因引导的病理 co‑attention：以基因组 query 病理 key/value，得到病理增强特征 \(P^C\)，残差连接得 \(P^f\)。
    - 病理引导的基因组 co‑attention：先对基因组自注意力得 \(G^S\)，再以病理 query 基因组 key/value，得 \(G^C\)，残差连接得 \(G^f\)。
    - 融合特征用于最终风险预测，训练损失为负对数似然（NLL）生存损失。

### 3. 实验设计
- **数据集**：5 个 TCGA 癌症数据集 —— BLCA (n=384), BRCA (n=968), CO‑READ (n=298), HNSC (n=392), STAD (n=317)。
- **评价指标**：Concordance Index (C‑Index)，5 折交叉验证，报告均值 ± 标准差。
- **对比方法**：
  - 仅病理：ABMIL, AMISL, TransMIL, CLAM；
  - 仅基因组：MLP, SNN, SNNTrans；
  - 多模态：SNN+CLAM, Porpoise, MCAT, MOTCat, CMTA, SurvPath, PIBD。

### 4. 资源与算力
- 文中仅提到使用 Adam 优化器（学习率 \(1\times10^{-4}\)，权重衰减 \(1\times10^{-5}\)，训练 30 轮），未说明 GPU 型号、显存或训练时长。算力需求未明确。

### 5. 实验数量与充分性
- **主要对比**：5 数据集 × 多种方法，主表完整。
- **消融实验**：
  - 超图结构（GAT, GCN, HGNN, SHGNN 及不同超边类型）全面对比；
  - 超边构建阈值 k 的敏感性分析（0, 5, 9, 25, 49）；
  - 模态权重策略（固定权重 vs 动态加权）和融合方式（不同 co‑attention 组合）的详细消融；
  - 病理特征编码器（UNI, Conch, Phikon2, CTransPath, ResNet50）的对比；
  - 可视化分析（风险热图、Kaplan‑Meier 曲线）。
- **公平性**：采用与已有工作相同的数据划分、优化设置，对比方法均使用公开代码复现或引用标准结果，实验客观、充分。

### 6. 主要结论与发现
- MRePath 在 5 个数据集上平均 C‑Index 达 71.5%，比最优对比方法 PIBD 高出 3.4%。
- 超图学习（尤其是拓扑和特征超边结合+层杆超图）能有效补足 MIL 造成的信息丢失，提升病理特征表征能力。
- 动态再平衡模块与交互式对齐融合显著缓解模态不平衡，使基因组信息在预测中发挥更恰当的作用。

### 7. 亮点
- 将层杆超图引入 WSIs 生存分析，通过拓扑与特征双空间超边捕获高阶关系，设计新颖。
- 提出了可插拔的动态模态加权机制，兼顾单模态可靠性与跨模态交互，能自适应调节贡献。
- 实验全面，涵盖多数据集、多对比方法、多角度消融，展示模块设计的合理性。

### 8. 不足与局限
- 超边构建阈值 k 依赖全局 patch 数，不同 WSI 的 patch 数量差异可能导致邻域范围不一致，引入潜在偏差。
- 假设病理和基因组数据完整配对，实际临床中常面临低质量数据或模态缺失，方法鲁棒性有待验证。
- 仅考虑单个 WSI 和一组基因组数据，未处理多张切片或更宏大的多组学数据，模型扩展性未探讨。
- 缺乏对计算复杂度、推理速度及显存占用等工程性指标的分析，难以评估实际部署可行性。

（完）
