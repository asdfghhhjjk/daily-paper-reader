---
title: Learning Heterogeneous Tissues with Mixture of Experts for Gigapixel Whole Slide Images
title_zh: 利用混合专家学习异质组织以处理十亿像素级全切片图像
authors: "Wu, Junxian, Chen, Minheng, Ke, Xinyi, Xun, Tianwang, Jiang, Xiaoming, Zhou, Hongyu, Shao, Lizhi, Kong, Youyong"
date: 2025-06-01
pdf: "https://openaccess.thecvf.com/content/CVPR2025/papers/Wu_Learning_Heterogeneous_Tissues_with_Mixture_of_Experts_for_Gigapixel_Whole_CVPR_2025_paper.pdf"
tags: ["query:profile"]
score: 6.0
evidence: PAMoE 模块学习组织特异性专家，捕捉微环境异质性用于下游任务
tldr: 提出病理感知混合专家模块 PAMoE，通过将不同组织区域路由到专长专家，有效建模全切片图像中的微环境异质性，广泛应用于癌症分析和预测任务。
source: CVPR-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-wu-learning-heterogeneous-tissues-with-mixture-of-experts-for-gigapixel-whole-cvpr-2025-paper/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 793, \"height\": 759}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-wu-learning-heterogeneous-tissues-with-mixture-of-experts-for-gigapixel-whole-cvpr-2025-paper/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 837, \"height\": 833}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-wu-learning-heterogeneous-tissues-with-mixture-of-experts-for-gigapixel-whole-cvpr-2025-paper/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1498, \"height\": 820}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-wu-learning-heterogeneous-tissues-with-mixture-of-experts-for-gigapixel-whole-cvpr-2025-paper/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1472, \"height\": 996}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-wu-learning-heterogeneous-tissues-with-mixture-of-experts-for-gigapixel-whole-cvpr-2025-paper/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 694, \"height\": 554}]"
tables_json: "[{\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-wu-learning-heterogeneous-tissues-with-mixture-of-experts-for-gigapixel-whole-cvpr-2025-paper/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1802, \"height\": 659}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-wu-learning-heterogeneous-tissues-with-mixture-of-experts-for-gigapixel-whole-cvpr-2025-paper/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1797, \"height\": 373}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-wu-learning-heterogeneous-tissues-with-mixture-of-experts-for-gigapixel-whole-cvpr-2025-paper/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1797, \"height\": 246}]"
motivation: 复杂的病理组织环境和缺乏目标驱动的领域知识阻碍了 WSI 分析的可扩展性。
method: 设计可插拔的混合专家模型，根据组织类型自动路由到专家，学习病理相关知识。
result: 在多种下游任务上性能提升，并发现了新的预后相关因素。
conclusion: 混合专家架构为异质组织建模提供了可扩展的解决方案，推动了个性化病理研究。
---

## Abstract
Analyzing gigapixel Whole Slide Images (WSIs) is challenging due to the complex pathological tissue environment and the absence of target-driven domain knowledge. Previous methods incorporated pathological priors to mitigate this issue but relied on additional inference steps and specialized workflows, restricting scalability and the model's capacity to identify novel outcome-related factors. To address these challenges, we propose a plug-and-play Pathology-Aware Mixture-of-Experts (PAMoE) module, which based on mixture of experts to learn pathology-related knowledge and extract useful information. We train the experts to become 'specialists' in specific intratumoral tissues by learning to route each tissue to its mapped expert. In addition, to reduce the impact of irrelevant content on the model, we introduce a new routing rule that discards patches in which none of the experts express interest, which helps the model better capture the relationships between relevant patches. Through a comprehensive evaluation of PAMoE on survival task, we demonstrate that 1) Our module enhances the performance of baseline models in most cases, and 2) The sparse expert processing across different tissues enhances the learning of patch representations by addressing tissue heterogeneity.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
PAMoE 模块学习组织特异性专家，捕捉微环境异质性用于下游任务。

### 2. 核心内容
提出病理感知混合专家模块 PAMoE，通过将不同组织区域路由到专长专家，有效建模全切片图像中的微环境异质性，广泛应用于癌症分析和预测任务。

### 3. 对应检索需求
Papers central to 检索把跨patch或者全WSI级别的细胞形态学、微环境特征用于数字病理学下游任务的研究, especially work that connects or combines: 探索组织微环境特征在数字病理学分析中的应用; 利用细胞形态和微环境特征提升病理图像分割精度; integrating cross-patch information for WSI-level tasks; graph neural networks for tissue microenvironment modeling; fusing spatial features across patches for global prediction; cell-level feature extraction for downstream pathology tasks; 研究如何将细胞形态学与微环境特征应用到数字病理学的模型和任务中; 调查病理学下游任务中形态学和微环境特征的优化方法; How to aggregate cell morphology features from patches for whole slide image classification; Graph based representation of cellular interactions in digital pathology.

### 4. 来源与原文
- Source：CVPR-2025-Accepted
- OpenReview：[https://openaccess.thecvf.com/content/CVPR2025/html/Wu_Learning_Heterogeneous_Tissues_with_Mixture_of_Experts_for_Gigapixel_Whole_CVPR_2025_paper.html](https://openaccess.thecvf.com/content/CVPR2025/html/Wu_Learning_Heterogeneous_Tissues_with_Mixture_of_Experts_for_Gigapixel_Whole_CVPR_2025_paper.html)
