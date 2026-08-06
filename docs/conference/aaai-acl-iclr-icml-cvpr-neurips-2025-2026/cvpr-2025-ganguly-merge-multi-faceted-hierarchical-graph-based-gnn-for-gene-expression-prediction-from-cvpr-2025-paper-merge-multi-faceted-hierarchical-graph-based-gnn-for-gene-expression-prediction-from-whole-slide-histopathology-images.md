---
title: "MERGE: Multi-faceted Hierarchical Graph-based GNN for Gene Expression Prediction from Whole Slide Histopathology Images"
title_zh: MERGE：基于多方面层次图GNN的全切片组织病理图像基因表达预测
authors: "Ganguly, Aniruddha, Chatterjee, Debolina, Huang, Wentao, Zhang, Jie, Yurovsky, Alisa, Johnson, Travis Steele, Chen, Chao"
date: 2025-06-01
pdf: "https://openaccess.thecvf.com/content/CVPR2025/papers/Ganguly_MERGE_Multi-faceted_Hierarchical_Graph-based_GNN_for_Gene_Expression_Prediction_from_CVPR_2025_paper.pdf"
tags: ["query:immuno-topo"]
score: 6.0
evidence: 基于层次图GNN从全切片组织病理图像预测基因表达，属于数字病理深度学习方法。
tldr: 为充分利用组织不同位置间的交互作用以提升空间基因表达预测，本文提出MERGE，通过多面层次图构建策略结合GNN，从全切片组织病理图像中同时预测多个位置的基因表达。该方法可加强与免疫微环境相关的基因表达推断，为后续免疫治疗响应预测等任务提供基础。
source: CVPR-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-ganguly-merge-multi-faceted-hierarchical-graph-based-gnn-for-gene-expression-prediction-from-cvpr-2025-paper/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 853, \"height\": 361}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-ganguly-merge-multi-faceted-hierarchical-graph-based-gnn-for-gene-expression-prediction-from-cvpr-2025-paper/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1744, \"height\": 1015}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-ganguly-merge-multi-faceted-hierarchical-graph-based-gnn-for-gene-expression-prediction-from-cvpr-2025-paper/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 866, \"height\": 726}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-ganguly-merge-multi-faceted-hierarchical-graph-based-gnn-for-gene-expression-prediction-from-cvpr-2025-paper/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 856, \"height\": 857}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-ganguly-merge-multi-faceted-hierarchical-graph-based-gnn-for-gene-expression-prediction-from-cvpr-2025-paper/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 866, \"height\": 826}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-ganguly-merge-multi-faceted-hierarchical-graph-based-gnn-for-gene-expression-prediction-from-cvpr-2025-paper/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 859, \"height\": 559}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-ganguly-merge-multi-faceted-hierarchical-graph-based-gnn-for-gene-expression-prediction-from-cvpr-2025-paper/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 864, \"height\": 465}]"
tables_json: "[{\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-ganguly-merge-multi-faceted-hierarchical-graph-based-gnn-for-gene-expression-prediction-from-cvpr-2025-paper/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1806, \"height\": 446}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-ganguly-merge-multi-faceted-hierarchical-graph-based-gnn-for-gene-expression-prediction-from-cvpr-2025-paper/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 775, \"height\": 337}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-ganguly-merge-multi-faceted-hierarchical-graph-based-gnn-for-gene-expression-prediction-from-cvpr-2025-paper/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 712, \"height\": 292}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-ganguly-merge-multi-faceted-hierarchical-graph-based-gnn-for-gene-expression-prediction-from-cvpr-2025-paper/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 714, \"height\": 331}]"
motivation: 现有方法未能充分利用组织不同位置间的交互关系进行联合预测。
method: 提出MERGE，构建多方面层次图，用GNN同时预测多个位置的基因表达。
result: 能够提升空间基因表达预测的准确性。
conclusion: MERGE通过图网络捕获组织空间关系，为WSI相关下游任务提供丰富信息。
---

## Abstract
Recent advances in Spatial Transcriptomics (ST) pair histology images with spatially resolved gene expression profiles, enabling predictions of gene expression across different tissue locations based on image patches. This opens up new possibilities for enhancing whole slide image (WSI) prediction tasks with localized gene expression. However, existing methods fail to fully leverage the interactions between different tissue locations, which are crucial for accurate joint prediction. To address this, we introduce MERGE (Multi-faceted hiErarchical gRaph for Gene Expressions), which combines a multi-faceted hierarchical graph construction strategy with graph neural networks (GNN) to improve gene expression predictions from WSIs. By clustering tissue image patches based on both spatial and morphological features, and incorporating intra- and inter-cluster edges, our approach fosters interactions between distant tissue locations during GNN learning. As an additional contribution, we evaluate different data smoothing techniques that are necessary to mitigate artifacts in ST data, often caused by technical imperfections. We advocate for adopting gene-aware smoothing methods that are more biologically justified. Experimental results on gene expression prediction show that our GNN method outperforms state-of-the-art techniques across multiple metrics.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义  
- **研究动机**：空间转录组学（ST）能够将组织图像与空间分辨的基因表达谱配对，但由于 ST 数据获取昂贵且存在噪声（高缺失率、稀疏性），直接从全切片组织病理图像（WSI）预测局部基因表达具有重要价值。  
- **核心问题**：现有方法未能充分利用不同组织位置之间的交互，尤其是距离较远但形态相似的区域，导致联合预测精度不足。  
- **整体含义**：通过构建能够同时捕捉局部和长程依赖关系的图结构，并联合基因感知的数据平滑，提升从 WSI 预测基因表达的准确性和生物学合理性。  

### 2. 论文提出的方法论  
- **核心思想**：利用“多面层次图”结合图神经网络（GNN），同时对组织内所有位置进行基因表达预测。  
- **关键技术细节**：  
  - **图像块编码**：使用 ResNet18 作为主干，在海量 TCGA-BRCA 数据上预训练后，在本任务上微调（用 MSE 回归 250 个基因），丢弃最后一层，取 256 维特征作为块嵌入。  
  - **多面层次图构建**：  
    - **空间聚类**：依据组织坐标对块进行聚类。  
    - **特征空间聚类**：依据块嵌入（形态特征）进行聚类。  
    - **代表节点（质心）**：每个簇选取离特征空间质心最近的块作为质心。  
    - **内部边**：簇内所有节点均连接至该簇质心。  
    - **捷径边**：所有簇（空间簇和特征簇）的质心之间形成完全图。  
    - **1-hop 近邻边**：额外加入每个块的 8 邻接边。  
    - 图结构保证任意两节点之间最多 3 跳，保持稀疏的同时实现长程信息传递。  
  - **图神经网络**：采用图注意力网络（GAT），堆叠 4 个 GATConv 层（除最后一层外均使用 8 头注意力），层间使用层归一化，并在前向传播时以 0.2 概率对边进行 dropout。  
  - **损失函数**：MSE 损失，联合预测所有 250 个基因的表达值。  
  - **数据平滑**：推荐并采用 SPCS（空间与模式结合平滑）代替传统的 8 邻域空间平滑。SPCS 同时考虑空间距离（曼哈顿距离）和基因表达模式相似性（基于 PCA 和皮尔逊相关距离），产生与组织形态更一致的训练目标。  

### 3. 实验设计  
- **数据集**：  
  - ST-Net（乳腺癌，68 样本，平均约 450 个组织内斑点）  
  - Her2ST（乳腺癌，36 样本，平均约 378 个斑点）  
  - SCC（皮肤癌，12 样本，平均约 723 个斑点）  
  - 仅选取 250 个高表达基因作为预测目标。  
- **评估指标**：均方误差（MSE）、平均绝对误差（MAE）、皮尔逊相关系数（PCC）。  
- **对比方法**：ResNet+FCN、BLEEP、HisToGene、Hist2ST、THItoGene、TRIPLEX。为保证公平，所有方法均使用相同的 ResNet18 骨干并训练在相同的 SPCS 平滑数据上。  
- **消融实验**：验证不同图构建策略（仅空间、仅特征、组合）、质心选择方式、聚类大小以及平滑方法（8n vs. SPCS）的影响。  

### 4. 资源与算力  
- 文中未明确提及所使用的 GPU 型号、数量或具体训练时长。  
- 仅说明编码器在 TCGA-BRCA 上进行预训练，之后在 ST 数据集上微调，GNN 训练使用 8 折交叉验证，但无算力开销的量化描述。  

### 5. 实验数量与充分性  
- **实验组数**：  
  - 3 个数据集上的主实验对比 6 个基线方法，以及 MERGE 的两种变体（1-hop 图、层次图）。  
  - 消融实验：图组件消融（3 种配置）、质心选择（3 种）、聚类大小（5 种）、平滑技术对比（ResNet、TRIPLEX、MERGE 分别用 8n 和 SPCS）。  
  - 定性分析：基因表达空间热图对比、多面聚类可视化。  
- **充分性与公平性**：实验覆盖多个数据集、多种指标和消融维度，使用统一编码器和数据预处理，结果客观。交叉验证采用 8 折，报告平均值，具备统计参考性。  

### 6. 论文的主要结论与发现  
- MERGE 通过多面层次图有效建模组织微环境中短程和长程交互，在三个数据集上 PCC 显著优于所有现有方法（ST-Net 上达到 0.6795，对比 TRIPLEX 的 0.2320）。  
- 特征空间聚类能捕获远距离的形态同质性，空间聚类则加强局部依赖，二者组合获得最优效果。  
- 基因感知的 SPCS 平滑在绝大多数情况下优于传统空间平滑，使基因表达分布与组织形态高度对应，且避免了数值坍塌。  
- GNN 架构相比 Transformer 等方案在 ST 数据有限的情况下更具数据效率，能更好地利用先验结构。  

### 7. 优点  
- **图构建创新**：多面聚类与捷径边的设计，既保留了图稀疏性，又让任意节点在 3 跳内可交互，成功将生物学先验（形态相似→表达相似）结构化地融入模型。  
- **系统性平滑验证**：明确对比了空间平滑与基因感知平滑，并通过实验和可视化强调其必要性，提供了独立的平滑技术贡献。  
- **统一的对比基准**：对所有基线使用相同的骨干和预处理，消除了特征提取差异造成的混淆，保证了公平性。  
- **消融细致**：对聚类策略、质心选择、簇大小等关键设计均进行了定量分析，支撑了最终方案的选择。  

### 8. 不足与局限  
- **算力信息缺失**：未提供训练时间或 GPU 配置，难以评估实际部署开销。  
- **依赖聚类超参数**：簇大小需要根据数据集调整（文中指出最大有效簇大小为 100），扩展到更大差异样本时可能需要额外调参。  
- **图构建离线化**：层次图依赖预提取的图像特征进行聚类，若特征编码器更换，图结构可能发生变化，对编码器有较强依赖性。  
- **应用限制**：模型训练要求 ST 数据（图像-基因配对），推理时虽仅需图像，但图构建仍需对 WSI 所有块进行聚类，大尺寸 WSI 可能面临计算瓶颈；此外，仅限于 Visium 等网格型 ST 数据，对其他不规则点位 ST 技术未做验证。  
- **平滑依赖性**：训练目标为平滑后的表达值，可能滤除部分真实的生物学变异（如罕见细胞类型信号），在后续生物学发现中存在信息丢失风险。  

（完）
