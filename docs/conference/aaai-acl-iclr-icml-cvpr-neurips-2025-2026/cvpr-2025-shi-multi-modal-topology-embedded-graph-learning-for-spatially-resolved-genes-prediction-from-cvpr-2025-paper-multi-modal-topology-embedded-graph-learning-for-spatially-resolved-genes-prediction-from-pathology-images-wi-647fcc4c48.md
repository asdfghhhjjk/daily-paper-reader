---
title: Multi-modal Topology-embedded Graph Learning for Spatially Resolved Genes Prediction from Pathology Images with Prior Gene Similarity Information
title_zh: 多模态拓扑嵌入图学习：结合先验基因相似性信息从病理图像预测空间解析基因表达
authors: "Shi, Hang, Chi, Changxi, Wan, Peng, Zhang, Daoqiang, Shao, Wei"
date: 2025-06-01
pdf: "https://openaccess.thecvf.com/content/CVPR2025/papers/Shi_Multi-modal_Topology-embedded_Graph_Learning_for_Spatially_Resolved_Genes_Prediction_from_CVPR_2025_paper.pdf"
tags: ["query:immuno-topo"]
score: 8.0
evidence: 采用图学习从病理图像建模斑点的拓扑轮廓，适用于免疫微环境空间拓扑分析。
tldr: 空间转录组数据获取昂贵，现有方法未能系统融合手工与深度特征以构建反映拓扑结构的斑点表征。本文提出多模态拓扑嵌入图学习方法，结合病理图像中的手工特征和预训练网络特征，并利用先验基因相似性信息构建图，从而预测空间分辨基因表达。实验表明该方法能有效捕获组织空间的拓扑轮廓，提升预测精度。这项研究为从病理图像推断空间基因表达提供了图形化建模新思路。
source: CVPR-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-shi-multi-modal-topology-embedded-graph-learning-for-spatially-resolved-genes-prediction-from-cvpr-2025-paper/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 863, \"height\": 597, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-shi-multi-modal-topology-embedded-graph-learning-for-spatially-resolved-genes-prediction-from-cvpr-2025-paper/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1443, \"height\": 616, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-shi-multi-modal-topology-embedded-graph-learning-for-spatially-resolved-genes-prediction-from-cvpr-2025-paper/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1619, \"height\": 741, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-shi-multi-modal-topology-embedded-graph-learning-for-spatially-resolved-genes-prediction-from-cvpr-2025-paper/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1369, \"height\": 745, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-shi-multi-modal-topology-embedded-graph-learning-for-spatially-resolved-genes-prediction-from-cvpr-2025-paper/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1354, \"height\": 244, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-shi-multi-modal-topology-embedded-graph-learning-for-spatially-resolved-genes-prediction-from-cvpr-2025-paper/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 871, \"height\": 242, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-shi-multi-modal-topology-embedded-graph-learning-for-spatially-resolved-genes-prediction-from-cvpr-2025-paper/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 868, \"height\": 185, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-shi-multi-modal-topology-embedded-graph-learning-for-spatially-resolved-genes-prediction-from-cvpr-2025-paper/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 876, \"height\": 212, \"label\": \"Table\"}]"
motivation: 现有方法缺乏计算并融合多模态特征定义带有拓扑表达的斑点级表征的能力。
method: 提出多模态拓扑嵌入图学习，整合手工和深度特征，利用基因相似性先验构建图预测基因表达。
result: 模型有效捕获组织拓扑轮廓，提升了空间基因表达预测准确率。
conclusion: 图学习框架成功将病理图像拓扑信息引入空间基因表达预测。
---

## Abstract
The rapid development of spatial transcriptomics (ST) allows researchers to measure the spatial-level gene expression in tissues. Although powerful, the cost for collecting the ST data is expensive, and thus several studies aim to predict gene expression in ST by utilizing their corresponding H/E stained pathology images. The existing ST based gene expression prediction models either adopt the pre-trained networks or rely on the handcrafted features to describe the pathology images, which still lack a systematic way to combine them together to define a spot-level representation that can reflect the topological profiles of different spots. On the other hand, all the ST based gene prediction models treat the prediction task for each gene independently, which overlook the fact that the exploration of potential interrelationships among them can help improve the prediction performance for individual genes.To address the above issues, we propose a multi-modal topology-embedded graph learning algorithm guided by prior Gene Ontology similarity information (i.e., M2TGLGO) to predict the spatial resolved genes from pathology image. Specifically, M2TGLGO co-learns the image representation of different spots from both deep and handcrafted features by considering the within-modal and inter-modal interactions. Next, to keep the topological structure among different spots, a spatial-oriented ranking module is also incorporated to preserve their neighborhood similarity information. Finally, we present a Gene Ontology knowledge guided graph neural network for simultaneously predicting multiple gene expressions by considering their functional associations. We evaluate our method on three public available ST datasets, the experimental results show the effectiveness of our M2TGLGO in comparison with the existing studies.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
采用图学习从病理图像建模斑点的拓扑轮廓，适用于免疫微环境空间拓扑分析。

### 2. 核心内容
空间转录组数据获取昂贵，现有方法未能系统融合手工与深度特征以构建反映拓扑结构的斑点表征。本文提出多模态拓扑嵌入图学习方法，结合病理图像中的手工特征和预训练网络特征，并利用先验基因相似性信息构建图，从而预测空间分辨基因表达。实验表明该方法能有效捕获组织空间的拓扑轮廓，提升预测精度。这项研究为从病理图像推断空间基因表达提供了图形化建模新思路。

### 3. 对应检索需求
How to use graph neural networks to model spatial topology of immune microenvironment?

### 4. 来源与原文
- Source：CVPR-2025-Accepted
- OpenReview：[https://openaccess.thecvf.com/content/CVPR2025/html/Shi_Multi-modal_Topology-embedded_Graph_Learning_for_Spatially_Resolved_Genes_Prediction_from_CVPR_2025_paper.html](https://openaccess.thecvf.com/content/CVPR2025/html/Shi_Multi-modal_Topology-embedded_Graph_Learning_for_Spatially_Resolved_Genes_Prediction_from_CVPR_2025_paper.html)
