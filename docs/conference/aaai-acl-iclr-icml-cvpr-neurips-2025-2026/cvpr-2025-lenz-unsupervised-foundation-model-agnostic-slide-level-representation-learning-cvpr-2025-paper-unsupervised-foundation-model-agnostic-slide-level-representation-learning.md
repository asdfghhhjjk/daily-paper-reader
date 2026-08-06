---
title: Unsupervised Foundation Model-Agnostic Slide-Level Representation Learning
title_zh: 无监督的基础模型无关切片级表示学习
authors: "Lenz, Tim, Neidlinger, Peter, Ligero, Marta, Wölflein, Georg, van Treeck, Marko, Kather, Jakob N."
date: 2025-06-01
pdf: "https://openaccess.thecvf.com/content/CVPR2025/papers/Lenz_Unsupervised_Foundation_Model-Agnostic_Slide-Level_Representation_Learning_CVPR_2025_paper.pdf"
tags: ["query:immuno-topo"]
score: 9.0
evidence: 使用多种基础模型的自监督学习方法进行切片级表示学习
tldr: 该论文提出了一种无监督学习方法，通过整合来自多个组织病理学基础模型的块嵌入来学习切片级表示，从而生成与任务无关的完整切片图像表示，为数字病理学分析提供基础。
source: CVPR-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-lenz-unsupervised-foundation-model-agnostic-slide-level-representation-learning-cvpr-2025-paper/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1548, \"height\": 1142, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-lenz-unsupervised-foundation-model-agnostic-slide-level-representation-learning-cvpr-2025-paper/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 760, \"height\": 641, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-lenz-unsupervised-foundation-model-agnostic-slide-level-representation-learning-cvpr-2025-paper/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1141, \"height\": 568, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-lenz-unsupervised-foundation-model-agnostic-slide-level-representation-learning-cvpr-2025-paper/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 724, \"height\": 526, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-lenz-unsupervised-foundation-model-agnostic-slide-level-representation-learning-cvpr-2025-paper/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 858, \"height\": 392, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-lenz-unsupervised-foundation-model-agnostic-slide-level-representation-learning-cvpr-2025-paper/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1809, \"height\": 515, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-lenz-unsupervised-foundation-model-agnostic-slide-level-representation-learning-cvpr-2025-paper/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1809, \"height\": 542, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-lenz-unsupervised-foundation-model-agnostic-slide-level-representation-learning-cvpr-2025-paper/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1807, \"height\": 741, \"label\": \"Table\"}]"
motivation: 现有切片表示学习方法多依赖弱监督或特定任务，缺乏通用性。
method: 提出一种新的单模态自监督方法，整合多个基础模型提取的块嵌入进行切片级表示学习。
result: 方法在多个下游任务上取得与弱监督方法相当的性能，且无需任务特定标注。
conclusion: 无需任务特定标签即可学习通用的切片表示，推动了计算病理学基础模型的发展。
---

## Abstract
Representation learning of pathology whole-slide images (WSIs) has primarily relied on weak supervision with Multiple Instance Learning (MIL). This approach leads to slide representations highly tailored to a specific clinical task. Self-supervised learning (SSL) has been successfully applied to train histopathology foundation models (FMs) for patch embedding generation. However, generating patient or slide level embeddings remains challenging. Existing approaches for slide representation learning extend the principles of SSL from patch level learning to entire slides by aligning different augmentations of the slide or by utilizing multimodal data. By integrating tile embeddings from multiple FMs, we propose a new single modality SSL method in feature space that generates useful slide representations. Our contrastive pretraining strategy, called COBRA, employs multiple FMs and an architecture based on Mamba-2. COBRA exceeds performance of state-of-the-art slide encoders on four different public Clinical Protemic Tumor Analysis Consortium (CPTAC) cohorts on average by at least +4.4% AUC, despite only being pretrained on 3048 WSIs from The Cancer Genome Atlas (TCGA). Additionally, COBRA is readily compatible at inference time with previously unseen feature extractors. Code available at https://github.com/KatherLab/COBRA

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义
- **研究动机**：计算病理学中，全切片图像（WSI）的表示学习主要依赖弱监督多实例学习（MIL），产生的切片表示高度特化于特定临床任务。自监督学习（SSL）虽已成功应用于训练组织病理学基础模型（FMs）生成块级嵌入，但生成患者/切片级嵌入仍具挑战。现有方法通过对齐切片不同增强或利用多模态数据将SSL扩展到整个切片，但前者难以产生多样性特征增强，后者受限于配对数据获取。
- **核心问题**：如何利用图像单模态数据，以一种任务无关的方式，无监督地学习出高质量、通用性强的切片级表示，使其能灵活适配多种下游任务和不同FMs。
- **整体含义**：提出一种新的特征空间自监督对比学习方法，整合来自多个已冻结的块级FMs的嵌入来训练切片编码器，从而无需人工标注即可生成强大的切片表示，并在极少量预训练数据下超越现有方法。

### 2. 论文提出的方法论
- **核心思想**：COntrastive Biomarker Representation Alignment (COBRA)。将多个不同FMs在不同放大倍率下提取的块嵌入作为特征空间中的“增强”，通过对比学习训练一个基于Mamba-2的切片编码器，迫使来自同一患者的不同“增强”（不同FM、不同放大倍率）在嵌入空间中接近。
- **关键技术细节**：
  - **预处理**：将WSI切割为224×224像素的块，用Canny边缘检测去背景。使用四种FMs（CTransPath、UNI、Virchow2、H-optimus-0）分别在0.5、1.14、2 MPP放大倍率下提取块嵌入。
  - **切片编码器架构**：
    - 嵌入模块 f_E：针对不同FM维度的线性映射至共享维度 d。
    - 状态空间对偶模块 f_S：两层Mamba-2（SSD）对嵌入序列建模。
    - 聚合模块 f_A：多头门控注意力机制，将序列聚合为单一特征向量。
  - **推理模式**：
    - 单FM模式：用原始块嵌入加权平均得到切片表示，权重由编码后的特征计算。
    - 多FM模式（†）：平均所有训练FMs的嵌入模块输出，输入到状态空间模块，再用指定FM的原始块嵌入进行加权聚合。
  - **损失函数**：采用MoCo-v3风格的动量对比学习（InfoNCE损失），查询编码器和键编码器通过动量更新保持一致性。
- **公式概览**（文字描述）：切片编码器输出 z = f_A(f_S(f_E(H)))，其中 H 为某FM的块嵌入集。对比损失中，同一WSI的不同“视图”作为正对，其他为负对。

### 3. 实验设计
- **数据集**：
  - **预训练**：TCGA中3048张WSI（2848患者），涉及BRCA、CRC、LUAD、LUSC、STAD五种组织类型。
  - **内部下游训练与验证**：TCGA中5折交叉验证。
  - **外部验证**：CPTAC中1604张WSI（444患者），涉及BRCA、COAD、LUAD、LUSC四种组织。
- **下游任务**（15个分类任务）：包括NSCLC亚型分型；LUAD中STK11、EGFR、TP53、KRAS突变预测；BRCA中ESR1、PGR、ERBB2表达及PIK3CA突变；COAD中MSI状态、BRAF、KRAS、PIK3CA突变、肿瘤位置（左/右半结肠）及淋巴结转移状态（N-Status）。报告AUC为主，补充F1、AUPRC、平衡准确率。
- **对比方法**：
  - 块均值基线：CTransPath、UNI、Virchow、CONCH、H-Optimus、GigaPath、Virchow2的均值池化。
  - 集成预测与拼接均值。
  - 现有切片编码器：GigaPath-SE、MADELEINE、CHIEF、PRISM。
- **消融实验**：
  - 不同FM的COBRA单FM模式（CTP、UNI、H0、V2）。
  - 多FM联合推理模式（†）及未见FM（GigaPath）适配。
  - 不同放大倍率（5×、9×、20×）效果。
  - 单放大倍率预训练 vs. 三放大倍率预训练对比。
  - 少量样本线性评估（k=5, 10, 25）的稳健性。

### 4. 资源与算力
- 预训练使用4块NVIDIA A100 GPU，批量大小1024，训练2000个epoch，耗时约40小时。参数总量15M（表1）。

### 5. 实验数量与充分性
- 进行了较为全面的评估：15个下游任务的MLP分类；6种对比方法加多种基线；针对不同FM、推理模式、放大倍率、多尺度预训练效应的多组消融；少样本学习实验；无监督热图可视化与UMAP嵌入可视化。
- 实验设计客观、公平：预训练数据与下游验证数据严格隔离（TCGA仅用于预训练，CPTAC全部分配外部验证），且所有FM均未在CPTAC上训练，防止数据泄露。
- 实验覆盖面从乳腺癌、肺癌到结直肠癌等多种组织，任务类型包括突变预测、亚型分类、淋巴结状态等，较为充分。

### 6. 论文的主要结论与发现
- COBRA在仅使用3048张WSI预训练的情况下，于15项CPTAC验证任务上的平均AUC超越现有最佳切片编码器PRISM至少+4.4%，超越Virchow2均值基线+1.5%。
- COBRA具有FM无关性，可显著提升小FM（如CTransPath）的性能，也能兼容未见FM（如GigaPath），使其超越均值基线。
- 低放大倍率（5×）下仍保持高精度，且多尺度预训练有助于提升低倍性能。
- 在少量样本条件下，COBRA比其他切片编码器更稳健。
- 模型注意权重能无监督地高亮肿瘤区域，嵌入空间可区分组织类型。

### 7. 优点
- **数据高效**：仅需3k张WSI，远少于对比方法（多为>10k甚至>100k），适合隐私敏感场景。
- **任务无关与FM无关**：可适配任意块级FM，并可产生通用切片表示用于多种下游任务。
- **设计优雅**：利用冻结的多FM多尺度嵌入直接做特征空间增强，避免图像增强的局限性。
- **推理灵活**：单FM或联合多FM模式，低倍率可大幅降低计算成本且性能损失小。
- **可解释性**：注意力权重提供直观的组织区域定位，无需额外监督。

### 8. 不足与局限
- **预训练范围有限**：仅在四种癌种（BRCA、CRC、LUAD、LUSC、STAD）上预训练，未覆盖更多组织类型或非癌样本，可能导致分布偏移。
- **依赖已有FM**：性能受限于使用的基座模型质量，若FM本身较差，COBRA虽有提升但仍有上限。
- **对比损失单一**：仅采用MoCo-v3，未探索其他SSL目标（如掩码建模）。
- **任务偏颇**：评估集中在突变和表达预测等分类任务，缺少回归任务（如生存分析）或分级任务。
- **解释性粗粒度**：注意力仅到块级，非像素级，精细定位受限。
- **计算开销**：需为每个WSI在不同FM和倍率下预提取嵌入，存储与预处理成本较高。

（完）
