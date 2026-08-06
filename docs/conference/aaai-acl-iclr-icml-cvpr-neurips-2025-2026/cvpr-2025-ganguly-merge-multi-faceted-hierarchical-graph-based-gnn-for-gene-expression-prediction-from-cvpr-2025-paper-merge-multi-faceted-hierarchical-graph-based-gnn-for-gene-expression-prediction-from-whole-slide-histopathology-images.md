---
title: "MERGE: Multi-faceted Hierarchical Graph-based GNN for Gene Expression Prediction from Whole Slide Histopathology Images"
title_zh: MERGE：基于多面层次图神经网络的基因表达预测——从全切片组织病理图像
authors: "Ganguly, Aniruddha, Chatterjee, Debolina, Huang, Wentao, Zhang, Jie, Yurovsky, Alisa, Johnson, Travis Steele, Chen, Chao"
date: 2025-06-01
pdf: "https://openaccess.thecvf.com/content/CVPR2025/papers/Ganguly_MERGE_Multi-faceted_Hierarchical_Graph-based_GNN_for_Gene_Expression_Prediction_from_CVPR_2025_paper.pdf"
tags: ["query:immuno-topo"]
score: 6.0
evidence: 在全切片图像上使用图神经网络进行基因表达预测
tldr: 目前从全切片组织病理图像预测基因表达的方法多聚焦于单点图像-基因匹配，忽略了不同组织位置间的相互作用，限制了联合预测精度。MERGE提出多面层次图构建策略，结合图神经网络（GNN）有效建模组织空间关系，从WSI中联合预测多位置基因表达。在空间转录组数据集上，该方法显著提升了预测性能，证明了整合多位置上下文信息对于全切片级分子推断的重要性，为数字病理中利用组织拓扑信息进行下游分析提供了新思路。
source: CVPR-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-ganguly-merge-multi-faceted-hierarchical-graph-based-gnn-for-gene-expression-prediction-from-cvpr-2025-paper/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 853, \"height\": 361}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-ganguly-merge-multi-faceted-hierarchical-graph-based-gnn-for-gene-expression-prediction-from-cvpr-2025-paper/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1744, \"height\": 1015}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-ganguly-merge-multi-faceted-hierarchical-graph-based-gnn-for-gene-expression-prediction-from-cvpr-2025-paper/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 866, \"height\": 726}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-ganguly-merge-multi-faceted-hierarchical-graph-based-gnn-for-gene-expression-prediction-from-cvpr-2025-paper/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 856, \"height\": 857}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-ganguly-merge-multi-faceted-hierarchical-graph-based-gnn-for-gene-expression-prediction-from-cvpr-2025-paper/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 866, \"height\": 826}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-ganguly-merge-multi-faceted-hierarchical-graph-based-gnn-for-gene-expression-prediction-from-cvpr-2025-paper/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 859, \"height\": 559}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-ganguly-merge-multi-faceted-hierarchical-graph-based-gnn-for-gene-expression-prediction-from-cvpr-2025-paper/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 864, \"height\": 465}]"
tables_json: "[{\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-ganguly-merge-multi-faceted-hierarchical-graph-based-gnn-for-gene-expression-prediction-from-cvpr-2025-paper/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1806, \"height\": 446}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-ganguly-merge-multi-faceted-hierarchical-graph-based-gnn-for-gene-expression-prediction-from-cvpr-2025-paper/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 775, \"height\": 337}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-ganguly-merge-multi-faceted-hierarchical-graph-based-gnn-for-gene-expression-prediction-from-cvpr-2025-paper/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 712, \"height\": 292}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-ganguly-merge-multi-faceted-hierarchical-graph-based-gnn-for-gene-expression-prediction-from-cvpr-2025-paper/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 714, \"height\": 331}]"
motivation: 全切片图像中不同组织位置间的相互作用对基因表达预测至关重要，但现有方法未有效建模。
method: 提出多面层次图构建策略与图神经网络结合，建模组织空间关系以联合预测基因表达。
result: 通过捕获跨位置依赖，提升了基因表达预测的准确性。
conclusion: 多位置交互建模能显著增强全切片图像中的基因表达推断能力。
---

## Abstract
Recent advances in Spatial Transcriptomics (ST) pair histology images with spatially resolved gene expression profiles, enabling predictions of gene expression across different tissue locations based on image patches. This opens up new possibilities for enhancing whole slide image (WSI) prediction tasks with localized gene expression. However, existing methods fail to fully leverage the interactions between different tissue locations, which are crucial for accurate joint prediction. To address this, we introduce MERGE (Multi-faceted hiErarchical gRaph for Gene Expressions), which combines a multi-faceted hierarchical graph construction strategy with graph neural networks (GNN) to improve gene expression predictions from WSIs. By clustering tissue image patches based on both spatial and morphological features, and incorporating intra- and inter-cluster edges, our approach fosters interactions between distant tissue locations during GNN learning. As an additional contribution, we evaluate different data smoothing techniques that are necessary to mitigate artifacts in ST data, often caused by technical imperfections. We advocate for adopting gene-aware smoothing methods that are more biologically justified. Experimental results on gene expression prediction show that our GNN method outperforms state-of-the-art techniques across multiple metrics.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
在全切片图像上使用图神经网络进行基因表达预测。

### 2. 核心内容
目前从全切片组织病理图像预测基因表达的方法多聚焦于单点图像-基因匹配，忽略了不同组织位置间的相互作用，限制了联合预测精度。MERGE提出多面层次图构建策略，结合图神经网络（GNN）有效建模组织空间关系，从WSI中联合预测多位置基因表达。在空间转录组数据集上，该方法显著提升了预测性能，证明了整合多位置上下文信息对于全切片级分子推断的重要性，为数字病理中利用组织拓扑信息进行下游分析提供了新思路。

### 3. 对应检索需求
digital pathology image analysis using deep learning。

### 4. 来源与原文
- Source：CVPR-2025-Accepted
- OpenReview：[https://openaccess.thecvf.com/content/CVPR2025/html/Ganguly_MERGE_Multi-faceted_Hierarchical_Graph-based_GNN_for_Gene_Expression_Prediction_from_CVPR_2025_paper.html](https://openaccess.thecvf.com/content/CVPR2025/html/Ganguly_MERGE_Multi-faceted_Hierarchical_Graph-based_GNN_for_Gene_Expression_Prediction_from_CVPR_2025_paper.html)
