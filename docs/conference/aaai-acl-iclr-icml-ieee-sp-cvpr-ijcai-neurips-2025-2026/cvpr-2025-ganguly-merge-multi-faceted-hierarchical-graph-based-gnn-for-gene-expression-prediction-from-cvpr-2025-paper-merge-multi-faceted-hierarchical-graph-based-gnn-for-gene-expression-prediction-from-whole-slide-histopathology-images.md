---
title: "MERGE: Multi-faceted Hierarchical Graph-based GNN for Gene Expression Prediction from Whole Slide Histopathology Images"
title_zh: MERGE：基于多层面层次图的GNN用于全切片组织病理图像基因表达预测
authors: "Ganguly, Aniruddha, Chatterjee, Debolina, Huang, Wentao, Zhang, Jie, Yurovsky, Alisa, Johnson, Travis Steele, Chen, Chao"
date: 2025-06-01
pdf: "https://openaccess.thecvf.com/content/CVPR2025/papers/Ganguly_MERGE_Multi-faceted_Hierarchical_Graph-based_GNN_for_Gene_Expression_Prediction_from_CVPR_2025_paper.pdf"
tags: ["query:profile"]
score: 6.0
evidence: 利用GNN建模全切片图像中的组织相互作用以预测基因表达
tldr: 空间转录组技术将组织图像与基因表达配对，但现有方法未能充分挖掘组织位置间相互作用。MERGE提出多层面层次图构建策略，结合图神经网络对全切片图像进行基因表达联合预测，在多个数据集上验证了准确性提升，为病理图像分析中的分子表型推断提供了有效框架，展示了图结构在组织微环境建模中的潜力。
source: CVPR-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-ganguly-merge-multi-faceted-hierarchical-graph-based-gnn-for-gene-expression-prediction-from-cvpr-2025-paper/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 853, \"height\": 361, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-ganguly-merge-multi-faceted-hierarchical-graph-based-gnn-for-gene-expression-prediction-from-cvpr-2025-paper/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1744, \"height\": 1015, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-ganguly-merge-multi-faceted-hierarchical-graph-based-gnn-for-gene-expression-prediction-from-cvpr-2025-paper/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 866, \"height\": 726, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-ganguly-merge-multi-faceted-hierarchical-graph-based-gnn-for-gene-expression-prediction-from-cvpr-2025-paper/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 856, \"height\": 857, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-ganguly-merge-multi-faceted-hierarchical-graph-based-gnn-for-gene-expression-prediction-from-cvpr-2025-paper/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 866, \"height\": 826, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-ganguly-merge-multi-faceted-hierarchical-graph-based-gnn-for-gene-expression-prediction-from-cvpr-2025-paper/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 859, \"height\": 559, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-ganguly-merge-multi-faceted-hierarchical-graph-based-gnn-for-gene-expression-prediction-from-cvpr-2025-paper/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 864, \"height\": 465, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-ganguly-merge-multi-faceted-hierarchical-graph-based-gnn-for-gene-expression-prediction-from-cvpr-2025-paper/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1806, \"height\": 446, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-ganguly-merge-multi-faceted-hierarchical-graph-based-gnn-for-gene-expression-prediction-from-cvpr-2025-paper/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 775, \"height\": 337, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-ganguly-merge-multi-faceted-hierarchical-graph-based-gnn-for-gene-expression-prediction-from-cvpr-2025-paper/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 712, \"height\": 292, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-ganguly-merge-multi-faceted-hierarchical-graph-based-gnn-for-gene-expression-prediction-from-cvpr-2025-paper/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 714, \"height\": 331, \"label\": \"Table\"}]"
motivation: 现有方法忽略全切片图像中不同组织位置间的交互作用。
method: 提出多层次图构建策略与图神经网络结合，预测空间基因表达。
result: 实现更准确的基因表达预测，有效捕获组织区域依赖关系。
conclusion: 为增强WSI下游任务提供一种利用组织交互的图形建模方法。
---

## Abstract
Recent advances in Spatial Transcriptomics (ST) pair histology images with spatially resolved gene expression profiles, enabling predictions of gene expression across different tissue locations based on image patches. This opens up new possibilities for enhancing whole slide image (WSI) prediction tasks with localized gene expression. However, existing methods fail to fully leverage the interactions between different tissue locations, which are crucial for accurate joint prediction. To address this, we introduce MERGE (Multi-faceted hiErarchical gRaph for Gene Expressions), which combines a multi-faceted hierarchical graph construction strategy with graph neural networks (GNN) to improve gene expression predictions from WSIs. By clustering tissue image patches based on both spatial and morphological features, and incorporating intra- and inter-cluster edges, our approach fosters interactions between distant tissue locations during GNN learning. As an additional contribution, we evaluate different data smoothing techniques that are necessary to mitigate artifacts in ST data, often caused by technical imperfections. We advocate for adopting gene-aware smoothing methods that are more biologically justified. Experimental results on gene expression prediction show that our GNN method outperforms state-of-the-art techniques across multiple metrics.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义
- **核心问题**：空间转录组学（ST）将组织病理图像与空间分辨的基因表达谱配对，使得从图像斑块预测基因表达成为可能。然而，现有方法未能充分利用不同组织位置（spots）之间的交互作用，特别是远距离但形态相似的斑块之间的信息传递，导致预测精度受限。
- **研究动机**：ST技术成本高昂且存在技术噪声（如高dropout率），从全切片图像（WSI）预测基因表达可低成本扩展空间分子分析。但现有方法要么忽略斑点交互，要么仅依赖短程空间近邻或全局自注意力，缺乏对生物学意义上远距离形态相似斑块的显式建模。
- **整体含义**：提出一种融合多层面层次图构建与图神经网络的框架MERGE，通过空间与形态双重聚类建立短程和长程交互，提升基因表达联合预测的准确性，并推荐基因感知的数据平滑方法以增强生物学合理性。

### 2. 方法论
- **概观**：MERGE分为斑块特征提取、多层面层次图构建和图神经网络预测三个阶段。
- **特征提取**：
  - 使用ResNet18作为骨干网络，在TCGA-BRCA数据集上预训练，后接线性投影层并在基因表达预测任务上微调（MSE损失），取倒数第二层输出256维特征向量作为斑块嵌入。
  - 可选的多分辨率编码器（TRIPLEX风格）也被试验，但最终采用ResNet18。
- **多层面层次图构建**（核心创新）：
  - 节点：每个组织斑点（spot）作为一个节点。
  - 空间聚类：根据二维坐标对斑点进行聚类（c个簇），每个簇选出一个最接近特征空间质心的斑点作为“质心点”（centroid）。
  - 特征空间聚类：根据斑块的图像特征嵌入进行聚类（c个簇），同样选出质心点。
  - 内部边：簇内所有节点连接到本簇的质心点（即每个非质心点有两条内部边，分别连接其空间簇质心和特征簇质心）。这些边传递局部形态或空间近邻信息。
  - 捷径边（shortcut edges）：所有质心点之间建立完全图（包括空间质心和特征质心共2c个节点）。这些边使任意两节点最多通过3跳连接，支持远距离形态相似斑块的快速信息传播。
  - 1-跳空间边：额外加入每个斑点的8个最邻接空间邻居作为边，保留局部空间上下文。
  - 整体图的稀疏性：边数约为O(n) + O(c²)，相较于全连接大幅降低计算开销。
- **图神经网络（GNN）**：
  - 采用图注意力网络（GAT），4层GATConv，前3层使用8个注意力头，层间应用Layer Normalization。
  - 每次前向传播时进行边dropout（p=0.2）。
  - 输出m维基因表达预测值（m个基因），训练目标为真实值与预测值的MSE损失。
- **基因表达平滑**：
  - 推荐使用SPCS（spatial and pattern combined smoothing），同时考虑空间距离（曼哈顿距离衰减）和基因表达模式相似性（基于PCA投影后皮尔逊相关距离），替代传统的8邻域空间平滑，可更好保留生物学相关模式并减少数据尺度缩水。

### 3. 实验设计
- **数据集**：
  - ST-Net（68个乳腺癌样本，23位患者，每样本平均约450个spot）
  - Her2ST（36个Her2阳性乳腺癌样本，8位患者，平均约378个spot）
  - SCC（12个皮肤鳞状细胞癌样本，4位患者，平均约723个spot）
  - 每个数据集选取表达量最高的250个基因作为预测目标。
- **数据预处理**：在20×放大倍率下提取224×224像素斑块，并应用SPCS平滑至基因表达矩阵。
- **评价指标**：均方误差（MSE）、平均绝对误差（MAE）、皮尔逊相关系数（PCC）。
- **基准对比方法**：
  - ResNet+FCN（简单基线）
  - BLEEP（对比学习增强特征）
  - HisToGene（基于Vision Transformer的位置感知）
  - Hist2ST（GNN + 空间邻居图）
  - THItoGene（多模态融合）
  - TRIPLEX（多分辨率编码器融合）
  - 为公平比较，所有方法使用相同的ResNet18编码器并均在SPCS平滑数据上重新训练。
- **验证策略**：在三个数据集上分别进行8倍交叉验证（按切片划分）。

### 4. 资源与算力
- 文中未明确说明使用的GPU型号、数量、训练时长或总计算消耗。仅提及网络结构（ResNet18, GAT）和训练框架，未给出算力规模。因此，无法评估其计算效率或复现所需资源。

### 5. 实验数量与充分性
- **主要实验（~3组大型对比）**：在三个数据集上与6种基线方法比较，覆盖MSE、MAE、PCC指标，结果汇总于主表（Table 1）。
- **消融实验（~5组）**：
  - 图构建变体：仅空间聚类、仅特征聚类、随机质心、空间质心 vs 默认特征质心的多层面图（Table 2）。
  - 聚类大小（簇内斑点数）从25到200对性能的影响（Table 3）。
  - 平滑方法对比：8n平滑 vs SPCS平滑，在ResNet+FCN、TRIPLEX、MERGE上测试（Table 4）。
- **定性分析**：展示特定基因（FASN, GNAS）的预测热力图，以及聚类结果的可视化。
- 整体实验设计较为充分，覆盖关键模块的有效性、超参数敏感性以及跨数据集泛化性；对比方法均在统一平滑和相同特征提取器下重训，保证了公平性。但仍缺乏在更大规模或不同组织类型（非癌）上的验证。

### 6. 主要结论与发现
- MERGE通过多层面层次图建摩长程和短程斑块交互，显著提高基因表达预测的准确性，尤其在PCC上提升明显。
- 特征空间聚类与空间聚类缺一不可，双重聚类并整合能得到最佳性能。
- 以特征空间质心作为簇代表比随机或空间质心更优。
- 每个簇的合理大小（约100个斑点）能平衡形态区分与信息丰富度，过大簇导致混合不同形态区域而降低性能。
- SPCS平滑相较于传统8邻域平滑在多数情况下（除TRIPLEX外）能更好地保留基因表达的尺度与组织结构对应性，有助于提高预测相关性。
- 预测结果在癌症相关标志基因上能够恢复高度一致的空间分布模式。

### 7. 优点
- **创新图设计**：巧妙结合空间邻接与形态相似性，通过层次化聚类和质心图实现稀疏但高效的长程信息传播，既保证3跳内全局连通，又控制计算成本。
- **生物学合理性**：采用基因感知平滑方法SPCS，减少ST技术噪声同时维持组织-基因表达对应关系，提升了数据预处理的质量。
- **全面消融验证**：对图构建各要素（聚类类型、质心选取、簇大小）和外部因素（平滑方法）进行细致剥离实验，清晰揭示每个组件的贡献。
- **强比较基准**：与多种主流方法（包括CNN、ViT、GNN和多尺度方法）进行公平比较，统一特征提取和预处理，结论可靠。
- **对下游任务的潜力**：该方法产生的局部基因表达预测可赋能多种基于WSI的分子推断任务（如肿瘤微环境分析、标志物发现）。

### 8. 不足与局限
- **算力未披露**：未报告GPU资源或训练时间，难以评估实际部署成本，尤其在处理全切片大规模推理时图构建和GNN的计算量未知。
- **数据集局限性**：三个数据集均为癌症组织（两种乳腺癌，一种皮肤癌），样本量虽较多但疾病类型单一，未测试正常组织或其他癌种，外部泛化性存疑。
- **特征提取依赖**：斑块编码器使用相对基础的ResNet18，未探索最新视觉基础模型（如病理专用ViT），可能在复杂形态特征提取上有提升空间。
- **图构建的静态性**：聚类和图结构基于预提取的特征和固定坐标，未能动态学习更优的连接关系，可能错过某些高级语义关联。
- **平滑方法评估受限**：虽然SPCS优于8n平滑，但未与更多先进ST数据矫正方法（如无需预定义基因集的深度学习方法）对比；同时TRIPLEX在8n平滑下表现更好，原因未充分解释。
- **预测基因数目有限**：仅预测250个高表达基因，未覆盖全转录组，许多低表达但重要的调控基因被忽略。
- **计算可扩展性**：随着斑点数量激增（如更高分辨率的ST技术），簇数目和完全图的连接可能显著增加，对大规模样本的效率有待验证。

（完）
