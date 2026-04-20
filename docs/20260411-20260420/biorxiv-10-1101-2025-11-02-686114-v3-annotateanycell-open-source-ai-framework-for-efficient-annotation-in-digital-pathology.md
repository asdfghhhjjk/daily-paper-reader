---
title: "AnnotateAnyCell: Open-Source AI Framework for Efficient Annotation in Digital Pathology"
title_zh: AnnotateAnyCell：用于数字病理高效标注的开源人工智能框架
authors: "Verma, S., Malusare, A., Wang, M., Wang, L., Mahapatra, A., English, A. L., Cox, A. D., Broman, M., de Brot, S., Burcham, G., Knapp, D., Dhawan, D., Sola, M., Aggarwal, V., Grama, A., Lanman, N. A."
date: 2026-04-13
pdf: "https://www.biorxiv.org/content/10.1101/2025.11.02.686114v3.full.pdf"
tags: ["query:cellrep"]
score: 10.0
evidence: 利用对比学习和嵌入进行细胞标注与分类的半监督框架
tldr: 本文提出名为AnnotateAnyCell的开源半监督标注框架，通过对病理切片的主动对比学习与人机交互反馈结合，利用Cellpose分割、UMAP可视化和伪标签传播，大幅提高细胞标注效率并维持专家级分类准确度。
source: biorxiv
selection_source: fresh_fetch
figures_json: "[{\"url\": \"assets/figures/biorxiv/biorxiv-10-1101-2025-11-02-686114-v3/fig-001.webp\", \"caption\": \"Figure 3: Left panel: Displays annotation summary statistics including counts for different morphological features along with distribution histograms. Center panel: Whole slide image view with cyan markers indicating the spatial locations of all annotated cells across the tissue sample, enabling pathologists to assess spatial distribution patterns and tissue architecture context. Right panel: Individual cell inspection tool showing detailed annotations for the selected cell (Tile 2791) with its specific morphological classifications. The interface includes data export functionality (Download CSV), version information, and the ability to filter and visualize cells based on specific morphological criteria. This output interface enables analysis of annotation results and supports research workflows requiring quantitative cellular phenotype data.\", \"page\": 6, \"index\": 1, \"width\": 968, \"height\": 523}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-1101-2025-11-02-686114-v3/fig-002.webp\", \"caption\": \"Figure 4: A. Sequential snapshots of the learned embedding space progression of annotations (green) within the unlabeled cellular population (blue). B. Classification evaluation of mitotic figures, nucleoli, and nuclear shape across training sizes using 5-fold cross-validation. C. Scaling behaviors highlight fundamental differences in data efficiency.\", \"page\": 7, \"index\": 2, \"width\": 951, \"height\": 952}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-1101-2025-11-02-686114-v3/fig-003.webp\", \"caption\": \"Figure 1: Pre-processing stage: Raw H&E-stained tissue images undergo segmentation using Cellpose models to generate nuclear masks. Each detected nucleus is extracted as three complementary representations: raw image patches, isolated nuclear regions, and semantic masks; Active Learning Loop: Expert pathologists (represented by colored figures) provide initial annotations for nuclear morphology features of neoplastic cells, including mitotic figures, vesicular chromatin, and prominent nucleoli. These labeled samples train a contrastive classifier that generates embeddings and pseudolabels for unlabeled data. A convolutional autoencoder processes the multi-modal inputs (raw, isolated, mask) to learn compact latent representations; Output Interface: The system produces annotated whole slide images with nuclei visualization, quantitative feature distributions, and prediction probabilities for downstream analysis. The iterative process refines the model’s understanding of cellular morphologies through expert feedback. Image Preparation: Left: Representative whole-slide image (WSI). Center: Nuclear segmentation results using pretrained Cellpose models. Right: Binary segmentation mask showing all detected valid cells. (Bottom row) Nine examples of 128×128 pixel cellular tiles illustrating morphological diversity across expert-defined annotation categories. Examples include bizarre mitotic figures showing irregular mitotic configurations, canonical mitotic figures demonstrating typical mitotic chromatin condensation patterns, nucleolar variations (single vs. multiple nucleoli) combined with nuclear shape classifications (circular, oval, irregular), and chromatin texture patterns (vesicular chromatin).\", \"page\": 3, \"index\": 3, \"width\": 968, \"height\": 819}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-1101-2025-11-02-686114-v3/fig-004.webp\", \"caption\": \"Figure 5: A. Illustrates labelling time with and without clustering, along with spatial distributions of agreement (green) and disagreement (brown) reveal localized cell-level ambiguities, with disagreement intensity encoded by saturation. B. Presents the annotation workflow metrics like agreement rates, reliability scores, consistency and spatial coverage scores across 11 annotators. C. Illustrates feature correlation demonstrating nuclear features are largely independent dimensions of morphology, and pairwise disagreement analyses showing some users might disagree more than others.\", \"page\": 8, \"index\": 4, \"width\": 964, \"height\": 539}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-1101-2025-11-02-686114-v3/fig-005.webp\", \"caption\": \"Figure 2: Left panel: Displays workflow guide for pathologists, nuclear size distribution histogram, and nuclear-to-cell ratio distribution with red indicators showing the currently selected cell’s measurements. Center panel: Interactive UMAP embedding visualization, where each point represents a cellular tile extracted from the whole slide image. Cells are color-coded based on annotation status (blue: unlabeled, green: labeled, orange: selected) and naturally cluster based on morphological similarities. Right panel: Shows a high-resolution preview of the selected cell tile (Tile 710) with morphological annotation options including mitotic figures, chromatin patterns, nucleoli characteristics, and nuclear shape classifications. The interface includes progress tracking (300/300 labeled points), version control, and model retraining capabilities (\\\"Update Clusters\\\" button).\", \"page\": 5, \"index\": 5, \"width\": 968, \"height\": 523}]"
motivation: 数字病理图像的人工作标注耗时耗力，成为计算病理和AI在临床应用中的瓶颈。
method: 采用主动对比学习与人机交互式迭代流程，结合Cellpose分割和UMAP潜空间聚类实现高效标注与分类。
result: "该方法将标注时间减少约25%，并在多个细胞特征分类中达到约96%-98%的高准确率。"
conclusion: 该框架显著降低标注负担，实现高精度自动分类，为资源有限的病理诊断提供可扩展的AI解决方案。
---

## 摘要
手动标注组织病理学全视野切片图像仍然是计算病理学与临床人工智能应用的关键瓶颈，需要耗费大量专家时间。本研究提出了一个开源的半监督框架，将主动对比学习与人类参与的迭代反馈相结合，实现高效的细胞标注与分类。该流程整合了 Cellpose 分割、基于 UMAP 的潜空间可视化以及带有伪标签传播的对比学习，并在犬侵袭性尿路上皮癌的五张全视野切片（涵盖低级、中级和高级组织学分级、40×放大倍数）上进行了评估。基于潜空间聚类引导的标注耗时 47 分钟，而顺序标注耗时 63 分钟，时间减少 25%（95% 置信区间 18–32%）。利用 1075 个标注样本，分裂相分类准确率达到 96.3% ± 1.2%，核仁分类准确率达到 98.3% ± 1.4%；仅使用 215 个样本，核仁分类仍可达到 95.5% ± 1.5% 的准确率。染色质（κ = 1.00）和核仁（κ = 0.95）的标注者间一致性较高，而分裂相（κ = 0.58）和核形（κ = 0.36）仅为中等一致性，反映出这些类别在形态学上的固有模糊性。该框架在保持专家级准确度的同时显著减轻了标注负担，为资源受限条件下的病理诊断提供了可扩展的人工智能辅助方案。

## Abstract
AO_SCPLOWBSTRACTC_SCPLOWManual annotation of histopathological whole slide images remains a critical bottleneck for computational pathology and clinical AI deployment, requiring prohibitive expert time at scale. Here we present an open-source semi-supervised framework combining active contrastive learning with iterative human-in-the-loop feedback for efficient cellular annotation and classification. The pipeline integrates Cellpose segmentation, UMAP-based latent space visualization, and contrastive learning with pseudolabel propagation, evaluated on five whole slide images of canine invasive urothelial carcinoma across low, intermediate, and high histological grades at 40x magnification. Latent space clustering-guided annotation required 47 minutes compared to 63 minutes for sequential annotation, a 25% reduction (95% CI 18-32%). Classification accuracy reached 96.3% {+/-} 1.2% for mitotic figures and 98.3% {+/-} 1.4% for nucleoli using 1,075 labeled samples, with nucleoli classification achieving 95.5% {+/-} 1.5% accuracy from only 215 samples. Inter-annotator agreement was high for chromatin ({kappa} = 1.00) and nucleoli ({kappa} = 0.95) but moderate for mitotic figures ({kappa} = 0.58) and nuclear shape ({kappa} = 0.36), reflecting intrinsic morphological ambiguity in these categories. This framework substantially reduces annotation burden while achieving expert-level accuracy for well-defined morphological features, providing a scalable path toward AI-assisted diagnostics in resource-constrained pathology settings.

---

## 论文详细总结（自动生成）

# AnnotateAnyCell：用于数字病理高效标注的开源人工智能框架 — 深度总结

---

## 一、研究动机与核心问题

- **研究背景**：数字病理（Digital Pathology）产生的全视野切片图像（Whole Slide Images, WSI）尺寸巨大，含有数十万细胞，人工手动标注极为耗时。  
- **核心问题**：深度学习在病理领域的推广受限于对大规模人工标注数据的需求；不同医院的扫描仪和染色差异导致模型泛化性差，需大量重复标注。  
- **研究目标**：在不牺牲标注精度的前提下，显著降低专家标注负担；建立一个**开源、半监督、可交互的人机协同标注框架**。

---

## 二、方法论概述

### 1. 核心思想
论文提出 **AnnotateAnyCell**，一个面向数字病理的半监督人机交互标注系统。  
该系统将 **主动学习（Active Learning）** 与 **对比学习（Contrastive Learning）** 相结合，让病理专家在可视化的潜空间中进行高效标注和模型更新。

### 2. 系统结构
整个流程包括四个阶段（循环迭代）：

1. **影像预处理与细胞分割**  
   - 使用 **Cellpose**（cyto3 模型）进行核分割，生成掩膜。  
   - 每个检测到的细胞以三种形式保存：  
     - 原图像块（raw patch）  
     - 分割后的核区域（isolated region）  
     - 语义掩膜（semantic mask）  
   - 由此构建包含细胞结构信息的多模态输入。

2. **嵌入与可视化标注**  
   - 利用 **UMAP** 对细胞特征进行降维，创建二维潜空间。  
   - 病理学家可在可视化界面中操作：点击聚类点、查看对应图像、直接赋予标注。  
   - 图像统计（核面积、核浆比）动态展示，便于诊断类比。

3. **对比学习与伪标签传播**  
   - 网络结构：CNN 特征提取器 + 投影头 + 分类头。  
   - 损失函数：
     - 分类损失 \(L_{CE}\)
     - 对比损失 \(L_{InfoNCE}\)：  
       \[
       L_{InfoNCE}=-\log{\frac{e^{sim(q,k^+)/\tau}}{\sum_i e^{sim(q,k_i)/\tau}}}
       \]
     - 总损失： \(L_{total} = \alpha L_{CE} + \beta L_{InfoNCE}\)
   - 模型通过高置信度选取机制生成伪标签（top-N per class），保证类均衡、防止主导类偏置。

4. **多模态自编码器（VAE）训练**
   - 输入三种模态（原图、核区域、掩膜）；采用并行编码器+跳跃连接。  
   - 潜变量维度为 256，用变分自编码器（VAE）重建输入并预测特征。  
   - 损失函数：
     \[
     L_{total} = \alpha L_{recon} + \beta L_{feat}
     \]
   - 输出经 UMAP 降维，形成可解释的潜空间，可用于专家迭代反馈。

---

## 三、实验设计

### 1. 数据来源
- **物种与病种**：犬类侵袭性尿路上皮癌（canine invasive urothelial carcinoma, IncUC），一种与人类肌层浸润性膀胱癌相似的动物模型。  
- **数据量**：5 张符合诊断质量标准的全视野切片（80,000×100,000 px，40×放大）。  
- **样本多样性**：从低、中、高分级病例中选择，包含多种核形与分裂特征。  

### 2. 标注策略
- **参与者**：11 名经认证的兽医病理学专家；每人标注 300 个细胞。  
- **标注特征**：
  - 分裂像（mitotic figures）
  - 核仁状态（单个、多重、显著）
  - 染色质类型（泡状/高染）
  - 核形态（圆、椭圆、不规则）

### 3. 评估指标与基准
- **分类准确率（Accuracy）**  
  - 分裂像：96.3% ± 1.2%  
  - 核仁：98.3% ± 1.4%  
  - 核形：59.5% ± 2.1%  
- **一致性系数（Cohen’s κ）**
  - 染色质：1.00  
  - 核仁：0.95  
  - 分裂像：0.58  
  - 核形：0.36  
- **标注效率对比**  
  - 聚类辅助 vs. 顺序标注：  
    - 47 分钟 vs. 63 分钟 → 时间减少 25%。

### 4. 对比与消融
- 与传统顺序标注方法（Sequential Annotation）对比效率。  
- 在使用 215、800、1075 样本的分级训练中分析数据效率和性能饱和度。  
- 不同特征学习曲线比较（形态复杂度显著不同）。

---

## 四、资源与算力

- 原文未明确说明 GPU 型号、显存或训练时长；  
- 提到使用 Cellpose 预训练模型与 CNN/VAE 网络在迭代式 pipeline 中进行重训练；  
- 可推测训练过程在标准研究级 GPU 环境下完成，但无具体算力披露。

---

## 五、实验数量与充分性

- **实验数量**：  
  - 主实验涵盖 5 张全视野切片、共计数千细胞。  
  - 包含标注效率对比、分类性能曲线、互标者一致性分析、特征间相关性等多维度研究。  
- **充分性判断**：  
  - 实验覆盖多位专家和多层次形态特征，具有较好代表性。  
  - 数据量在数字病理背景下偏小（仅犬种单一病种），未来可扩展。  
  - 未见到跨机构验证或外部 benchmark 对比。

---

## 六、主要结论与发现

- 半监督主动学习框架可将标注时间缩短约 **25%**。  
- 利用少量标注（约 215 样本）即可达接近专家的一致性（95%+）。  
- 不同形态特征的可学习性差异明显：
  - 核仁稳定、染色质高一致；
  - 分裂像和核形态因主观性较强间歇性不稳定。  
- 多模态自编码器和 InfoNCE 对比学习能增强潜空间可分性。  
- 框架支持“逐步自适应”机构化标注，可在资源有限场景下推广。

---

## 七、优点与创新点

- **创新融合**：首次集成 **Cellpose 分割 + 对比学习 + 主动伪标签传播 + UMAP 可视化标注**。  
- **人机互促**：提供交互式嵌入空间界面，使专家能高效浏览高维特征。  
- **高样本效率**：极少样本即可逼近饱和值，体现数据利用率高。  
- **可解释性强**：潜空间聚类直观显示细胞形态分布，有助于医学解释。  
- **开源与可复用性**：代码与数据计划开放，利于学界复现与扩展。

---

## 八、局限与不足

- **数据单一性**：仅使用犬尿路上皮癌样本，未验证跨物种或跨组织泛化。  
- **模型可扩展性未知**：未测试在多种扫描仪、染色协议下性能稳定性。  
- **算力不透明**：缺乏训练资源、硬件配置与时间信息，不利于完全复现。  
- **形态主观性风险**：分裂像与核形分类主观性强，伪标签传播可能放大误差。  
- **临床验证缺乏**：尚未进行前瞻性临床应用或与商业平台（如 HALO、Visiopharm）的对比。

---

**（完）**
