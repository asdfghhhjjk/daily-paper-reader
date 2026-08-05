---
title: "MERGE: Multi-faceted Hierarchical Graph-based GNN for Gene Expression Prediction from Whole Slide Histopathology Images"
title_zh: MERGE：基于多面层次图的GNN从全切片组织病理学图像预测基因表达
authors: "Ganguly, Aniruddha, Chatterjee, Debolina, Huang, Wentao, Zhang, Jie, Yurovsky, Alisa, Johnson, Travis Steele, Chen, Chao"
date: 2025-06-01
pdf: "https://openaccess.thecvf.com/content/CVPR2025/papers/Ganguly_MERGE_Multi-faceted_Hierarchical_Graph-based_GNN_for_Gene_Expression_Prediction_from_CVPR_2025_paper.pdf"
tags: ["query:profile"]
score: 8.0
evidence: 在全切片图像上使用层次图神经网络预测基因表达，建模组织微环境交互
tldr: 现有方法在从全切片组织病理图像预测基因表达时忽略了组织空间位置间的交互，本文提出MERGE框架，通过构建多面层次图并利用图神经网络捕获跨补丁的组织微环境依赖，提升基因表达预测精度。该方法在空间转录组数据上验证，显著优于基线模型，为利用WSI中空间结构进行下游分子预测提供了新思路。
source: CVPR-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-ganguly-merge-multi-faceted-hierarchical-graph-based-gnn-for-gene-expression-prediction-from-cvpr-2025-paper/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 853, \"height\": 361, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-ganguly-merge-multi-faceted-hierarchical-graph-based-gnn-for-gene-expression-prediction-from-cvpr-2025-paper/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1744, \"height\": 1015, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-ganguly-merge-multi-faceted-hierarchical-graph-based-gnn-for-gene-expression-prediction-from-cvpr-2025-paper/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 866, \"height\": 726, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-ganguly-merge-multi-faceted-hierarchical-graph-based-gnn-for-gene-expression-prediction-from-cvpr-2025-paper/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 856, \"height\": 857, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-ganguly-merge-multi-faceted-hierarchical-graph-based-gnn-for-gene-expression-prediction-from-cvpr-2025-paper/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 866, \"height\": 826, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-ganguly-merge-multi-faceted-hierarchical-graph-based-gnn-for-gene-expression-prediction-from-cvpr-2025-paper/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 859, \"height\": 559, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-ganguly-merge-multi-faceted-hierarchical-graph-based-gnn-for-gene-expression-prediction-from-cvpr-2025-paper/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 864, \"height\": 465, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-ganguly-merge-multi-faceted-hierarchical-graph-based-gnn-for-gene-expression-prediction-from-cvpr-2025-paper/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1806, \"height\": 446, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-ganguly-merge-multi-faceted-hierarchical-graph-based-gnn-for-gene-expression-prediction-from-cvpr-2025-paper/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 775, \"height\": 337, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-ganguly-merge-multi-faceted-hierarchical-graph-based-gnn-for-gene-expression-prediction-from-cvpr-2025-paper/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 712, \"height\": 292, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-ganguly-merge-multi-faceted-hierarchical-graph-based-gnn-for-gene-expression-prediction-from-cvpr-2025-paper/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 714, \"height\": 331, \"label\": \"Table\"}]"
motivation: 现有方法未能充分利用组织位置间的相互作用进行联合基因表达预测，限制了全切片预测性能。
method: 采用多面层次图构建策略，将组织补丁表示为图节点，通过图神经网络捕获跨位置交互以预测基因表达。
result: 在空间转录组数据上，MERGE优于基线方法，提高了基因表达预测的准确性。
conclusion: 通过多层次图神经网络对全切片图像进行组织微环境建模，可有效利用空间交互信息提升基因表达预测。
---

## Abstract
Recent advances in Spatial Transcriptomics (ST) pair histology images with spatially resolved gene expression profiles, enabling predictions of gene expression across different tissue locations based on image patches. This opens up new possibilities for enhancing whole slide image (WSI) prediction tasks with localized gene expression. However, existing methods fail to fully leverage the interactions between different tissue locations, which are crucial for accurate joint prediction. To address this, we introduce MERGE (Multi-faceted hiErarchical gRaph for Gene Expressions), which combines a multi-faceted hierarchical graph construction strategy with graph neural networks (GNN) to improve gene expression predictions from WSIs. By clustering tissue image patches based on both spatial and morphological features, and incorporating intra- and inter-cluster edges, our approach fosters interactions between distant tissue locations during GNN learning. As an additional contribution, we evaluate different data smoothing techniques that are necessary to mitigate artifacts in ST data, often caused by technical imperfections. We advocate for adopting gene-aware smoothing methods that are more biologically justified. Experimental results on gene expression prediction show that our GNN method outperforms state-of-the-art techniques across multiple metrics.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义
- **研究背景**：空间转录组学（ST）能够在组织切片上测定基因表达的空间分布，结合组织病理图像，可以预测任意位置的基因表达谱。这为全切片图像（WSI）分析带来新机遇。
- **问题与动机**：现有方法大多独立处理每个组织斑块（spot），未能有效建模**远距离、形态相似但空间上不邻接的组织区域之间的交互**，限制了联合预测的准确性。
- **整体含义**：论文提出 MERGE 框架，通过构建**多面层次图**（融合空间聚类与特征聚类）并利用图神经网络（GNN）传播信息，使模型能同时捕获局部与长程的组织微环境依赖，从而提升基因表达预测性能。同时，论文强调应采用**基因感知的数据平滑技术**来减轻 ST 数据的技术噪声。

### 2. 论文提出的方法论
- **核心思想**：将组织切片中的每个 spot 视为图节点，通过**空间聚类和图像特征空间聚类**构建层次化图结构，显式添加簇内边和跨簇捷径边，让 GNN 高效建模短程、长程交互。
- **关键技术细节**：
  - **图构建**（Multi-faceted Hierarchical Graph）：
    - 对 n 个 spot 分别进行**空间坐标聚类**和**图像块特征聚类**，各得 c 个簇。
    - 每个簇选取离特征中心最近的 spot 作为**质心节点**。
    - **簇内边**：将簇内所有 spot 与质心连接（两类聚类各产生一组簇内边）。
    - **捷径边**：将所有簇的质心（来自空间和特征聚类共 2c 个）两两相连，形成全连接图。这使得任意两节点最多经过 3 跳即可通信。
    - 同时保留每个 spot 的 8 个空间近邻边（1-hop 边）。
  - **GNN 架构**：使用**图注意力网络（GAT）**，4 层 GATConv（前 3 层 h=8 注意力头），层间加 LayerNorm，输入时进行概率 0.2 的边 dropout。输出为每个节点 m 维基因表达向量，优化目标为 MSE 损失。
  - **斑块编码器**：选用 ResNet18，先在 TCGA-BRCA 上预训练，再接线性层在 ST 数据上微调至基因表达预测任务（MSE 损失），最后取 256 维特征作为节点特征。
  - **平滑技术**：采用 **SPCS**（Spatial and Pattern Combined Smoothing），结合空间距离权重和基因表达模式相似性（基于 PCA 和相关系数）对基因表达矩阵进行平滑，相比传统的 8 邻域平均（8n smoothing），能更好地保留生物学相关模式并与组织形态对应。
- **算法流程（文字描述）**：
  1. 从 WSI 提取图像块，用微调后的 ResNet18 提取 256 维特征。
  2. 对 spot 进行空间聚类与特征聚类，按上述规则构建多面层次图。
  3. 将该图输入 GAT，所有节点联合预测基因表达。
  4. 使用 SPCS 平滑后的基因表达作为监督信号，训练 GNN。

### 3. 实验设计
- **数据集/场景**：
  - ST-Net（乳腺癌，68 样本 / 23 病人）
  - Her2ST（乳腺癌，36 样本 / 8 病人）
  - SCC（皮肤癌，12 样本 / 4 病人）
  - 所有数据集均选取前 250 个高表达基因作为预测目标。
- **基准（Benchmark）**：对比方法包括：
  - ResNet+FCN、BLEEP、HisToGene、Hist2ST、THItoGene、TRIPLEX。
- **评价指标**：均方误差（MSE）、平均绝对误差（MAE）、皮尔逊相关系数（PCC）。
- **实验设置**：8 折交叉验证（跨切片），所有方法均使用统一配置的 ResNet18 编码器，并在 SPCS 平滑数据上训练。

### 4. 资源与算力
- 论文**未明确提及**使用的 GPU 型号、数量、训练时长或显存消耗。文中仅给出了模型架构和边计算的复杂度分析，缺少具体的算力与资源说明。

### 5. 实验数量与充分性
- **总体实验组数**：
  - 主要结果：3 个数据集 × （1 个本文方法 + 6 个基线） = 21 组对比实验。
  - 消融实验（均在 ST-Net 数据集上）：
    - 图构建方式：仅 1-hop、仅空间聚类、仅特征聚类、随机质心、空间质心、默认 MERGE 共 6 组。
    - 聚类大小：25、75、100、150、200 共 5 组。
    - 平滑方法：ResNet+FCN、TRIPLEX、MERGE 分别用 8n 和 SPCS，共 6 组。
  - 定性分析：基因热图对比、聚类可视化。
- **充分性与客观性**：
  - 实验在多个数据集和多指标上进行，基线涵盖主流方法，消融实验覆盖关键设计选择，比较全面。
  - 交叉验证设置、统一编码器和数据处理保证了公平性。
  - 但对 HER2ST 和 SCC 数据集仅做了整体对比，未进行消融分析，略有不均。

### 6. 论文的主要结论与发现
- MERGE 通过多面层次图显式引入长程组织交互，在所有数据集上均取得最优或极具竞争力的结果。
- 相比于使用简单 1-hop 图的 GNN，层次图大幅提升 PCC。
- 基因感知的 SPCS 平滑方法能更好地保留组织形态相关的模式，优于简单的空间平滑。
- 簇大小需适中（如 ST-Net 中最优为 100），过大会破坏簇内形态同质性。

### 7. 优点
- **方法创新性**：提出多面层次图构建策略，将空间邻近和表型相似两种组织关系统一为图结构的边，设计精巧。
- **生物学合理性**：长程边使得形态相似但空间远离的 spots 能有效交互，更符合组织微环境特点。
- **实用的平滑选择**：系统比较并推荐 SPCS 平滑方法，对后续研究有参考价值。
- **实验扎实**：多数据集、多指标、多基线对比，消融实验充分验证各组件贡献。

### 8. 不足与局限
- **算力需求未知**：未提供计算资源与效率数据，难以评估实际部署成本。
- **超参数敏感**：聚类数目（簇大小）对性能有明显影响，需根据样本斑点数量调参，可能降低泛化性。
- **数据集规模有限**：ST-Net 和 Her2ST 均为乳腺癌，SCC 为皮肤癌，缺少更多癌种和更大规模数据集验证。
- **图构建依赖特征质量**：若特征提取器未能很好区分形态差异，特征空间聚类可能失效。
- **平滑技术争议**：SPCS 平滑使用了基因表达相似性，训练时存在信息泄漏风险（但本文用于监督信号之前，且并非完全无偏，这在文中未深入讨论）。
- **未在 WSI 级别的下游任务直接验证**：研究止步于基因表达预测指标，未展示其在癌症分类、预后等下游应用上的提升。

（完）
