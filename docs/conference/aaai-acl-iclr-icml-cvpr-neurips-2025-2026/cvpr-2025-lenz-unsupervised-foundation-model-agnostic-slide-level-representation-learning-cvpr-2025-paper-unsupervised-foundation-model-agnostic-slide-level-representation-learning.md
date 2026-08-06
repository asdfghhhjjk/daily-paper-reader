---
title: Unsupervised Foundation Model-Agnostic Slide-Level Representation Learning
title_zh: 无监督的基础模型无关的全切片级表示学习
authors: "Lenz, Tim, Neidlinger, Peter, Ligero, Marta, Wölflein, Georg, van Treeck, Marko, Kather, Jakob N."
date: 2025-06-01
pdf: "https://openaccess.thecvf.com/content/CVPR2025/papers/Lenz_Unsupervised_Foundation_Model-Agnostic_Slide-Level_Representation_Learning_CVPR_2025_paper.pdf"
tags: ["query:profile"]
score: 6.0
evidence: 通过融合多基础模型的tile嵌入学习全切片级表征，可用于利用跨patch信息的下游病理任务。
tldr: 当前全切片图像表示学习主要依赖弱监督多实例学习，导致表征高度任务特定。本文提出一种新的单模态自监督学习方法，通过融合来自多个病理基础模型的tile嵌入，学习无监督的、与任务无关的全切片级表示。该方法在多个下游任务上展现了竞争性能，且无需额外标注。其贡献在于提供了一种基础模型无关的通用WSI特征提取方案。
source: CVPR-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-lenz-unsupervised-foundation-model-agnostic-slide-level-representation-learning-cvpr-2025-paper/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1548, \"height\": 1142, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-lenz-unsupervised-foundation-model-agnostic-slide-level-representation-learning-cvpr-2025-paper/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 760, \"height\": 641, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-lenz-unsupervised-foundation-model-agnostic-slide-level-representation-learning-cvpr-2025-paper/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1141, \"height\": 568, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-lenz-unsupervised-foundation-model-agnostic-slide-level-representation-learning-cvpr-2025-paper/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 724, \"height\": 526, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-lenz-unsupervised-foundation-model-agnostic-slide-level-representation-learning-cvpr-2025-paper/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 858, \"height\": 392, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-lenz-unsupervised-foundation-model-agnostic-slide-level-representation-learning-cvpr-2025-paper/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1809, \"height\": 515, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-lenz-unsupervised-foundation-model-agnostic-slide-level-representation-learning-cvpr-2025-paper/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1809, \"height\": 542, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-lenz-unsupervised-foundation-model-agnostic-slide-level-representation-learning-cvpr-2025-paper/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1807, \"height\": 741, \"label\": \"Table\"}]"
motivation: 现有WSI表示学习依赖弱监督，缺乏任务无关的通用全切片表示。
method: 提出融合多基础模型tile嵌入的无监督自监督学习，学习全切片级通用表征。
result: 在下游任务中表现出竞争力，无需任务特定监督。
conclusion: 该方法为病理全切片提供了一种基础模型无关的通用特征表示范式。
---

## Abstract
Representation learning of pathology whole-slide images (WSIs) has primarily relied on weak supervision with Multiple Instance Learning (MIL). This approach leads to slide representations highly tailored to a specific clinical task. Self-supervised learning (SSL) has been successfully applied to train histopathology foundation models (FMs) for patch embedding generation. However, generating patient or slide level embeddings remains challenging. Existing approaches for slide representation learning extend the principles of SSL from patch level learning to entire slides by aligning different augmentations of the slide or by utilizing multimodal data. By integrating tile embeddings from multiple FMs, we propose a new single modality SSL method in feature space that generates useful slide representations. Our contrastive pretraining strategy, called COBRA, employs multiple FMs and an architecture based on Mamba-2. COBRA exceeds performance of state-of-the-art slide encoders on four different public Clinical Protemic Tumor Analysis Consortium (CPTAC) cohorts on average by at least +4.4% AUC, despite only being pretrained on 3048 WSIs from The Cancer Genome Atlas (TCGA). Additionally, COBRA is readily compatible at inference time with previously unseen feature extractors. Code available at https://github.com/KatherLab/COBRA

---

## 论文详细总结（自动生成）

### 1. 检索相关性
通过融合多基础模型的tile嵌入学习全切片级表征，可用于利用跨patch信息的下游病理任务。

### 2. 核心内容
当前全切片图像表示学习主要依赖弱监督多实例学习，导致表征高度任务特定。本文提出一种新的单模态自监督学习方法，通过融合来自多个病理基础模型的tile嵌入，学习无监督的、与任务无关的全切片级表示。该方法在多个下游任务上展现了竞争性能，且无需额外标注。其贡献在于提供了一种基础模型无关的通用WSI特征提取方案。

### 3. 对应检索需求
Papers central to 检索把跨patch或者全WSI级别的细胞形态学、微环境特征用于数字病理学下游任务的研究, especially work that connects or combines: 探索组织微环境特征在数字病理学分析中的应用; 利用细胞形态和微环境特征提升病理图像分割精度; integrating cross-patch information for WSI-level tasks; graph neural networks for tissue microenvironment modeling; fusing spatial features across patches for global prediction; cell-level feature extraction for downstream pathology tasks; 研究如何将细胞形态学与微环境特征应用到数字病理学的模型和任务中; 调查病理学下游任务中形态学和微环境特征的优化方法; How to aggregate cell morphology features from patches for whole slide image classification; Graph based representation of cellular interactions in digital pathology.

### 4. 来源与原文
- Source：CVPR-2025-Accepted
- OpenReview：[https://openaccess.thecvf.com/content/CVPR2025/html/Lenz_Unsupervised_Foundation_Model-Agnostic_Slide-Level_Representation_Learning_CVPR_2025_paper.html](https://openaccess.thecvf.com/content/CVPR2025/html/Lenz_Unsupervised_Foundation_Model-Agnostic_Slide-Level_Representation_Learning_CVPR_2025_paper.html)
