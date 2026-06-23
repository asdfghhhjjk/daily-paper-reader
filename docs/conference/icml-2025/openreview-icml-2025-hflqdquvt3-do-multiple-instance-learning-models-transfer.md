---
title: Do Multiple Instance Learning Models Transfer?
title_zh: 多实例学习模型可迁移吗？
authors: "Daniel Shao, Richard J. Chen, Andrew H. Song, Joel Runevic, Ming Y. Lu, Tong Ding, Faisal Mahmood"
date: 2025-05-01
pdf: "https://openreview.net/pdf?id=hfLqdquVt3"
tags: ["query:wsi-mil"]
score: 8.0
evidence: 计算病理学多实例学习迁移研究
tldr: 首次系统研究计算病理学中多实例学习（MIL）模型的迁移学习能力。评估了11种MIL模型在19个预训练任务上的表现，涵盖组织分型、癌症分级和分子亚型预测。结果表明迁移学习可显著提升MIL在弱监督全切片图像分析场景下的性能，为重要图块识别和判别区域定位提供了重要指导。
source: ICML-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-icml-2025-hflqdquvt3/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 846, \"height\": 758, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-hflqdquvt3/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 836, \"height\": 811, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-hflqdquvt3/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 832, \"height\": 595, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-hflqdquvt3/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 846, \"height\": 544, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-hflqdquvt3/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 821, \"height\": 529, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-hflqdquvt3/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 808, \"height\": 599, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-hflqdquvt3/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1775, \"height\": 1937, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-hflqdquvt3/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1714, \"height\": 1709, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-icml-2025-hflqdquvt3/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1778, \"height\": 667, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-hflqdquvt3/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1690, \"height\": 633, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-hflqdquvt3/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 861, \"height\": 606, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-hflqdquvt3/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 892, \"height\": 252, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-hflqdquvt3/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 848, \"height\": 369, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-hflqdquvt3/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1665, \"height\": 480, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-hflqdquvt3/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1548, \"height\": 391, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-hflqdquvt3/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1122, \"height\": 412, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-hflqdquvt3/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1229, \"height\": 1957, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-hflqdquvt3/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 564, \"height\": 608, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-hflqdquvt3/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1821, \"height\": 1120, \"label\": \"Table\"}]"
motivation: 计算病理学MIL模型在小样本弱监督场景下性能受限，迁移学习的有效性尚不明确。
method: 对11种MIL模型在19个病理分类预训练任务上进行迁移学习实验，评估其跨任务迁移能力。
result: 发现预训练MIL模型具有良好的迁移性，可有效提升下游任务性能。
conclusion: 迁移学习是提升病理MIL模型在数据稀缺环境下表现的关键策略。
---

## Abstract
Multiple Instance Learning (MIL) is a cornerstone approach in computational pathology for distilling embeddings from gigapixel tissue images into patient-level representations to predict clinical outcomes. However, MIL is frequently challenged by the constraints of working with small, weakly-supervised clinical datasets. Unlike fields such as natural language processing and computer vision, which effectively use transfer learning to improve model quality in data-scarce environments, the transferability of MIL models remains largely unexplored. We conduct the first comprehensive investigation into transfer learning capabilities of pretrained MIL models, evaluating 11 MIL models across 19 pretraining tasks spanning tissue subtyping, cancer grading, and molecular subtype prediction. We observe a substantial performance boost with finetuning pretrained models over training from randomly initialized weights, even with domain differences between pretraining and target tasks. Pretraining on pan-cancer datasets enables consistent generalization across organs and task types compared to single-disease pretraining. Remarkably, this pan-cancer pretraining leads to better transfer than that of a state-of-the-art slide-level foundation model, while using only 6.5\% of the training data. These findings indicate that MIL architectures exhibit robust adaptability, offering insights into the benefits of leveraging pretrained models to enhance performance in computational pathology.

---

## 论文详细总结（自动生成）

# 论文《Do Multiple Instance Learning Models Transfer?》详细中文总结

## 1. 论文的核心问题与整体含义（研究动机和背景）

- **研究背景**：多实例学习（Multiple Instance Learning, MIL）是计算病理学（Computational Pathology, CPath）的核心范式，用于从千兆像素的全切片图像（WSI）中提取临床相关的幻灯片级表示。尽管MIL架构不断发展，但训练数据通常是小规模、弱监督的临床数据集，导致模型泛化能力受限。
- **核心问题**：与自然语言处理和计算机视觉中广泛使用的迁移学习不同，MIL模型在CPath中的可迁移性（transferability）尚不明确。具体问题包括：哪些MIL架构更易迁移？跨器官、跨任务迁移效果如何？迁移学习是否总是优于从头训练？预训练任务和数据规模如何影响迁移？
- **整体含义**：系统理解和利用MIL迁移学习，有望在数据稀缺场景下显著提升模型性能，为开发更高效的病理AI工具提供新范式，同时降低对大规模自监督预训练数据的依赖。

## 2. 论文提出的方法论：核心思想与关键技术细节

- **核心思想**：通过大规模监督预训练（特别是泛癌分类任务）得到MIL模型的权重，然后将这些权重迁移至下游任务进行微调或冻结特征评估，以验证MIL模型是否具备可迁移的聚合知识。
- **关键技术细节**：
  - **MIL模型架构**：评估了11种主流MIL架构，包括ABMIL、CLAM、DSMIL、DFTD、TransMIL、Transformer、ILRA、RRT、WIKG、MeanMIL、MaxMIL。它们的主要区别在于聚合函数（注意力、Transformer、图结构等）和辅助损失。
  - **预训练任务**：使用21个分类任务，包括19个公共数据集任务（涵盖乳腺癌、肺癌、前列腺癌、脑肿瘤等器官的形态分类、分级、分子亚型预测）以及2个泛癌任务PC-43（43类癌种）和PC-108（108类精细癌种）。PC-108和PC-43来自同一家医院（Brigham and Women’s Hospital）的3,944张WSI训练集和1,620张验证集。
  - **迁移评估方式**：两种评估设置：
    1. **端到端微调**（finetuning）：使用预训练权重初始化MIL聚合器，然后在目标任务上微调所有参数。
    2. **冻结特征评估**（KNN）：使用预训练模型提取幻灯片级嵌入，直接应用K近邻分类器（k=20）进行评估。
  - **预处理标准化**：所有WSI按统一流程处理：256×256非重叠组织块，20×放大倍率，使用UNI（DINOv2预训练的ViT-L/16）作为patch编码器提取特征。
  - **训练超参数**：AdamW优化器，学习率1e-4，余弦衰减，最大20轮，早停耐心5轮，批次大小1，权重衰减1e-5，dropout 0.25。
- **公式/算法说明**：无新公式提出，主要依赖现有MIL架构的官方实现，通过改变初始化权重（随机 vs. 预训练）来评估迁移效果。

## 3. 实验设计

- **使用的数据集/场景**：
  - **目标任务**：19个公开数据集任务，按器官和任务类型分组：
    - 乳腺癌：BRACS（粗/细粒度）、BCNB（ER/PR/HER2）、BRCA（ER/PR/HER2/PIK3CA）
    - 肺癌：NSCLC（形态分型、TP53/STK11/KRAS/EGFR突变预测）
    - 前列腺癌：PANDA（Gleason分级）
    - 脑肿瘤：EBRAINS（粗/细粒度）、GBMLGG（IDH状态、组织分子分型）
  - **预训练任务**：21个任务，包括上述19个任务中的部分以及PC-43、PC-108泛癌任务。
- **Benchmark**：
  - 与**随机初始化**对比（基线）。
  - 与**单器官预训练**（如仅用NSCLC任务预训练）对比。
  - 与**slide foundation models**对比：CHIEF（基于ABMIL，60,530张幻灯片，监督对比学习）和GigaPath（基于LongNet，171,189张WSI，自监督掩码自编码器）。
- **对比的方法**：
  - 11种MIL架构在同一设置下比较。
  - 不同patch编码器（ResNet-50、CTransPath、GigaPath ViT、UNIv2、CONCHv1.5）。
  - 不同模型规模（ABMIL参数量从0.16M到8.5M）。
  - 不同样本量（few-shot实验：K=4,16,32）。
  - 不同初始化策略（随机、PC-43、PC-108、单器官）。

## 4. 资源与算力

- 原文明确说明：实验在**四块NVIDIA RTX A4000、三块NVIDIA GeForce RTX 2080 Ti、三块RTX 3090**上进行，每项实验只使用**单块GPU**（附录B.2）。
- 未提供总训练时长或具体计算开销，但指出预处理使用UNI特征，训练最大20轮，早停。

## 5. 实验数量与充分性

- **实验数量**：涉及21个预训练任务、19个目标任务、11种MIL架构、多个消融（模型规模、few-shot、层重要性、patch编码器、跨器官迁移）。共生成数千个实验条件（例如，图2的KNN迁移矩阵含21×19个组合，每个组合取3种架构平均；表1展示11种架构在19个任务上的结果）。
- **充分性**：
  - **全面**：覆盖不同器官、任务类型、样本量、架构，验证了迁移学习的一般性结论。
  - **客观公平**：采用标准化预处理和统一超参数，确保架构间可比；使用多个随机种子（附录表A4）检验稳定性；使用多标签分层拆分避免数据泄露。
  - **不足之处**：未包含生存分析任务、状态空间模型（如Mamba）；预训练数据仅来自单一机构，存在偏差风险；few-shot实验仅对5种架构进行，未覆盖全部11种；SVCCA分析仅使用30张WSI的45,232个patch，样本量有限。

## 6. 论文的主要结论与发现

1. **预训练MIL模型显著优于随机初始化**：在所有19个目标任务上，使用PC-108预训练的ABMIL平均提升3.3%（表1），即使预训练任务与目标任务器官不同，也有提升。
2. **泛癌预训练（PC-108）效果最佳**：在KNN冻结评估中，PC-108预训练比随机基线平均提升+9.8%，优于单器官预训练；在微调中，PC-108也优于所有单器官预训练，且所需数据仅为自监督slide foundation models的6.5%（CHIEF）和2.3%（GigaPath）。
3. **架构影响迁移收益**：Transformer架构（TransMIL、Transformer）受益最大（+5.8%以上），而MeanMIL、MaxMIL提升较小，说明学习到的聚合策略是关键。ABMIL在预训练后表现最佳，超过更复杂的架构。
4. **模型规模与迁移效率**：PC-108预训练使模型在更大规模下保持稳定性能（单调提升直到5M参数），而随机初始化性能波动大；有效初始化解锁了有利的缩放趋势。
5. **迁移的本质**：SVCCA和层重置实验表明，**注意力层（aggregation layer）** 的预训练权重对迁移贡献最大。重置注意力层导致最大性能下降（-5.0%），而重置浅层MLP影响较小。注意力热图可视化显示，预训练模型从初始就聚焦于肿瘤区域，微调后保持稳定。
6. **与其他slide foundation models对比**：PC-108预训练的ABMIL在KNN和微调上均优于CHIEF和GigaPath，尽管后者使用了更大规模的自监督数据。这证明了监督泛癌预训练的数据效率优势。

## 7. 优点

- **系统性全面**：首次系统评估MIL迁移学习，涵盖多种架构、任务、评估范式，结论扎实。
- **实用性强**：提供开源资源（GitHub仓库MIL-Lab，包含模型权重FEATHER和标准化实现），降低复现和应用门槛。
- **发现具有启示性**：指出“简单架构+优质预训练”比复杂架构更有效，挑战了追求架构创新的趋势，为领域提供了实用建议。
- **方法严谨**：标准化预处理、多随机种子验证、防止数据泄露（多标签分层拆分）、与最先进基线公平对比。
- **可视化可解释性**：使用t-SNE和注意力热图直观展示预训练带来的特征分离和注意力聚焦，增强说服力。

## 8. 不足与局限

- **实验覆盖限制**：
  - 未评估状态空间模型（如Mamba-MIL）或基于图的MIL变体（如GCN）。
  - 未涉及生存分析任务（如风险预测），这是病理AI的重要应用。
  - 预训练数据仅来自单一机构（Brigham and Women’s Hospital），可能导致**机构偏差**和**人口统计偏差**（如种族、地域），影响向其他临床环境的泛化。论文在Impact Statement中承认了这一点。
- **基准对比局限**：
  - 与CHIEF、GigaPath对比时，使用了不同的patch编码器（UNI vs. CTransPath vs. GigaPath ViT），虽尽力控制变量，但并非完全对齐（例如CHIEF使用CTransPath，而PC-108 ABMIL也使用CTransPath）。
  - 未对比其他自监督slide foundation模型（如Prov-GigaPath、Prism、CONCH）。
- **分析深度有限**：
  - SVCCA分析仅基于少量样本（30张WSI），且仅对ABMIL两种规模进行，未扩展到其他架构。
  - 层重置实验仅针对ABMIL-Large，未探索其他架构的层贡献差异。
  - few-shot实验只对5种架构进行，未包含所有11种。
- **微调设置可能不最优**：所有实验使用固定超参数（学习率、dropout等），未针对每个任务单独调优，可能低估某些架构的微调潜力。但作者认为这保证了公平比较。
- **应用限制**：所有结果基于H&E染色的FFPE组织，不适用于其他染色（如IHC）或冷冻切片。方法依赖于高质量patch特征编码器（UNI），该编码器本身具有强表征能力，MIL迁移效果可能部分得益于编码器的泛化性（论文通过不同编码器实验控制了这一点）。

（完）
