---
title: "AnnotateAnyCell: Open-Source AI Framework for Efficient Annotation in Digital Pathology"
title_zh: AnnotateAnyCell：用于数字病理高效标注的开源人工智能框架
authors: "Verma, S., Malusare, A., Wang, M., Wang, L., Mahapatra, A., English, A. L., Cox, A. D., Broman, M., de Brot, S., Burcham, G., Knapp, D., Dhawan, D., Sola, M., Aggarwal, V., Grama, A., Lanman, N. A."
date: 2026-04-13
pdf: "https://www.biorxiv.org/content/10.1101/2025.11.02.686114v3.full.pdf"
tags: ["query:cellrep"]
score: 10.0
evidence: 利用对比学习和潜空间可视化进行细胞级标注与分类
tldr: 该研究提出了一个名为AnnotateAnyCell的开源半监督框架，通过结合对比学习与人机交互的标注反馈机制，提高数字病理切片中细胞的标注效率和分类精度，实现专家级准确度并显著减少标注时间。
source: biorxiv
selection_source: fresh_fetch
figures_json: "[{\"url\": \"assets/figures/biorxiv/biorxiv-10-1101-2025-11-02-686114-v3/fig-001.webp\", \"caption\": \"Figure 3: Left panel: Displays annotation summary statistics including counts for different morphological features along with distribution histograms. Center panel: Whole slide image view with cyan markers indicating the spatial locations of all annotated cells across the tissue sample, enabling pathologists to assess spatial distribution patterns and tissue architecture context. Right panel: Individual cell inspection tool showing detailed annotations for the selected cell (Tile 2791) with its specific morphological classifications. The interface includes data export functionality (Download CSV), version information, and the ability to filter and visualize cells based on specific morphological criteria. This output interface enables analysis of annotation results and supports research workflows requiring quantitative cellular phenotype data.\", \"page\": 6, \"index\": 1, \"width\": 968, \"height\": 523}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-1101-2025-11-02-686114-v3/fig-002.webp\", \"caption\": \"Figure 4: A. Sequential snapshots of the learned embedding space progression of annotations (green) within the unlabeled cellular population (blue). B. Classification evaluation of mitotic figures, nucleoli, and nuclear shape across training sizes using 5-fold cross-validation. C. Scaling behaviors highlight fundamental differences in data efficiency.\", \"page\": 7, \"index\": 2, \"width\": 951, \"height\": 952}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-1101-2025-11-02-686114-v3/fig-003.webp\", \"caption\": \"Figure 1: Pre-processing stage: Raw H&E-stained tissue images undergo segmentation using Cellpose models to generate nuclear masks. Each detected nucleus is extracted as three complementary representations: raw image patches, isolated nuclear regions, and semantic masks; Active Learning Loop: Expert pathologists (represented by colored figures) provide initial annotations for nuclear morphology features of neoplastic cells, including mitotic figures, vesicular chromatin, and prominent nucleoli. These labeled samples train a contrastive classifier that generates embeddings and pseudolabels for unlabeled data. A convolutional autoencoder processes the multi-modal inputs (raw, isolated, mask) to learn compact latent representations; Output Interface: The system produces annotated whole slide images with nuclei visualization, quantitative feature distributions, and prediction probabilities for downstream analysis. The iterative process refines the model’s understanding of cellular morphologies through expert feedback. Image Preparation: Left: Representative whole-slide image (WSI). Center: Nuclear segmentation results using pretrained Cellpose models. Right: Binary segmentation mask showing all detected valid cells. (Bottom row) Nine examples of 128×128 pixel cellular tiles illustrating morphological diversity across expert-defined annotation categories. Examples include bizarre mitotic figures showing irregular mitotic configurations, canonical mitotic figures demonstrating typical mitotic chromatin condensation patterns, nucleolar variations (single vs. multiple nucleoli) combined with nuclear shape classifications (circular, oval, irregular), and chromatin texture patterns (vesicular chromatin).\", \"page\": 3, \"index\": 3, \"width\": 968, \"height\": 819}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-1101-2025-11-02-686114-v3/fig-004.webp\", \"caption\": \"Figure 5: A. Illustrates labelling time with and without clustering, along with spatial distributions of agreement (green) and disagreement (brown) reveal localized cell-level ambiguities, with disagreement intensity encoded by saturation. B. Presents the annotation workflow metrics like agreement rates, reliability scores, consistency and spatial coverage scores across 11 annotators. C. Illustrates feature correlation demonstrating nuclear features are largely independent dimensions of morphology, and pairwise disagreement analyses showing some users might disagree more than others.\", \"page\": 8, \"index\": 4, \"width\": 964, \"height\": 539}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-1101-2025-11-02-686114-v3/fig-005.webp\", \"caption\": \"Figure 2: Left panel: Displays workflow guide for pathologists, nuclear size distribution histogram, and nuclear-to-cell ratio distribution with red indicators showing the currently selected cell’s measurements. Center panel: Interactive UMAP embedding visualization, where each point represents a cellular tile extracted from the whole slide image. Cells are color-coded based on annotation status (blue: unlabeled, green: labeled, orange: selected) and naturally cluster based on morphological similarities. Right panel: Shows a high-resolution preview of the selected cell tile (Tile 710) with morphological annotation options including mitotic figures, chromatin patterns, nucleoli characteristics, and nuclear shape classifications. The interface includes progress tracking (300/300 labeled points), version control, and model retraining capabilities (\\\"Update Clusters\\\" button).\", \"page\": 5, \"index\": 5, \"width\": 968, \"height\": 523}]"
motivation: 人工标注病理全景图像耗时较长，限制了计算病理与临床AI的应用。
method: 作者采用了结合Cellpose分割、UMAP可视化和对比学习的半监督流程，并引入伪标签传播与人机交互标注机制。
result: "该框架在减少约25%标注时间的同时，细胞分类准确率超过96%，显示出高效与准确兼具的性能。"
conclusion: 该框架显著降低了病理标注负担，为资源有限环境下的AI辅助诊断提供了可扩展解决方案。
---

## 摘要
对组织病理学全切片图像进行人工标注仍然是计算病理学和临床人工智能部署中的关键瓶颈，在大规模应用时需要耗费大量专家时间。本文提出一个开源的半监督框架，将主动对比学习与迭代式人机交互反馈相结合，以实现高效的细胞标注与分类。该流程集成了 Cellpose 分割、基于 UMAP 的潜空间可视化，以及结合伪标签传播的对比学习，并在五张犬侵袭性尿路上皮癌的全切片图像上进行了评估，涵盖低、中、高三个组织学分级（40x 放大倍率）。潜空间聚类引导的标注耗时 47 分钟，而顺序标注为 63 分钟，减少了 25%（95% 置信区间 18–32%）。在使用 1,075 个标注样本时，分裂像的分类准确率达到 96.3%（±1.2%），核仁的分类准确率为 98.3%（±1.4%）；仅使用 215 个样本时，核仁分类的准确率仍可达到 95.5%（±1.5%）。在染色质（κ = 1.00）和核仁（κ = 0.95）的标注中，标注者间一致性较高，而在分裂像（κ = 0.58）和细胞核形状（κ = 0.36）上则为中等，反映了这些类别在形态学上的固有模糊性。该框架显著降低了标注负担，同时在定义明确的形态学特征上实现了专家级准确度，为资源有限的病理学应用环境中实现人工智能辅助诊断提供了可扩展的途径。

## Abstract
AO_SCPLOWBSTRACTC_SCPLOWManual annotation of histopathological whole slide images remains a critical bottleneck for computational pathology and clinical AI deployment, requiring prohibitive expert time at scale. Here we present an open-source semi-supervised framework combining active contrastive learning with iterative human-in-the-loop feedback for efficient cellular annotation and classification. The pipeline integrates Cellpose segmentation, UMAP-based latent space visualization, and contrastive learning with pseudolabel propagation, evaluated on five whole slide images of canine invasive urothelial carcinoma across low, intermediate, and high histological grades at 40x magnification. Latent space clustering-guided annotation required 47 minutes compared to 63 minutes for sequential annotation, a 25% reduction (95% CI 18-32%). Classification accuracy reached 96.3% {+/-} 1.2% for mitotic figures and 98.3% {+/-} 1.4% for nucleoli using 1,075 labeled samples, with nucleoli classification achieving 95.5% {+/-} 1.5% accuracy from only 215 samples. Inter-annotator agreement was high for chromatin ({kappa} = 1.00) and nucleoli ({kappa} = 0.95) but moderate for mitotic figures ({kappa} = 0.58) and nuclear shape ({kappa} = 0.36), reflecting intrinsic morphological ambiguity in these categories. This framework substantially reduces annotation burden while achieving expert-level accuracy for well-defined morphological features, providing a scalable path toward AI-assisted diagnostics in resource-constrained pathology settings.

---

## 论文详细总结（自动生成）

# AnnotateAnyCell：用于数字病理高效标注的开源人工智能框架 — 深度中文总结

---

## 一、研究动机与背景

- **核心问题**：数字病理学中的全景组织切片（Whole Slide Images, WSI）包含数十万细胞，人工标注这些细胞形态（如分裂像、核仁、染色质等）极为耗时，成为临床与计算病理AI落地的主要瓶颈。  
- **背景现状**：
  - 当前主流方法多采用**完全监督学习**，需大量专家标注数据。
  - 数据在不同机构间存在“域偏移”（染色、扫描设备差异），导致模型泛化性弱。
  - 现有半监督或主动学习工具在**交互体验、标注反馈循环、算力需求**等方面仍不完善。  
- **研究目标**：设计一个**开源、跨平台、可交互**的AI标注框架，使病理专家能够在低标注成本下实现高质量的细胞形态识别和分类，推动临床AI模型部署。

---

## 二、方法论与技术细节

### 1. 整体框架结构
本文提出的 **AnnotateAnyCell** 是一个四阶段、半监督主动学习式标注与分类系统：
1. **细胞分割**：使用预训练的 Cellpose 模型从H&E染色切片中提取核与细胞区域；
2. **嵌入空间呈现**：利用 UMAP 对提取的细胞图块进行降维，在二维潜空间中根据形态聚类；
3. **对比学习与伪标签传播**：结合监督分类损失与 InfoNCE 对比损失，构建对比学习嵌入模型；
4. **多模态自编码器学习**：通过卷积式变分自编码器（VAE）整合原图、分割掩膜和核区域，学习细粒度形态特征与上下文。

### 2. 算法与公式描述

- **对比学习损失（InfoNCE）**：
  \[
  L_{InfoNCE} = -\log \frac{\exp(sim(q,k^+)/\tau)}{\sum_i \exp(sim(q,k_i)/\tau)}
  \]
  - 通过温度参数 τ 控制嵌入分布，拉近形态相似细胞的距离。

- **总优化目标**：
  \[
  L_{total} = \alpha L_{CE} + \beta L_{InfoNCE}
  \]
  - 在分类交叉熵损失与对比损失间平衡。

- **自编码器训练目标**：
  \[
  L_{total} = \alpha L_{recon} + \beta L_{feat}
  \]
  - 同时优化重建误差与形态特征预测误差，保持潜空间的结构与可解释性。

### 3. 人机交互机制
- 界面采用 **BokehJS** 构建，允许多用户实时标注、协作。
- 三栏界面结构：
  - 中心：UMAP潜空间散点图；
  - 左侧：统计和指导信息；
  - 右侧：高分辨细胞预览与标注界面。
- 用户可直接在嵌入图上选点、标注并触发“Update Clusters”更新模型，实现循环训练。

---

## 三、实验设计

- **数据来源**：
  - 犬侵袭性尿路上皮癌（Invasive Urothelial Carcinoma, IncUC）组织切片，来源于 Purdue 大学兽医学院。
  - 5 张高分辨率WSI（80,000 × 100,000 像素，40×放大）。
  - 包含低、中、高分级样本，反映形态多样性。
  
- **分类特征**：
  - 分裂像（mitotic figures），核仁特征（单/多/显著），染色质纹理（疏松 vs 致密），核形状（圆形、椭圆、不规则）。

- **对比方法**：
  - 与**顺序人工标注法**对比效率；
  - 比较3类特征分类精度（mitotic、nucleoli、shape）随样本量变化的学习曲线；
  - 评估多标注者间一致性（Cohen’s κ）。

- **评估指标**：
  - 分类准确率、标注耗时统计、标注一致率、空间分布分析。

---

## 四、资源与算力

- **算力配置**：论文未明确说明 GPU、CPU 或训练时间等算力细节。  
- **可推测**：由于框架包含卷积网络与UMAP降维，可推定使用常规单GPU环境即可运行（性能需求相对有限）。  
- **开源资源**：
  - 所有代码与数据计划开源于 GitHub 与 Zenodo（待正式论文接受后）。

---

## 五、实验数量与充分性

- **主要实验组**：
  - 标注效率对比：聚类引导 vs 顺序标注；
  - 模型性能评估：三类形态特征的学习曲线（不同样本数量）；
  - 多专家一致性分析（11位病理学专家）；
  - 特征间相关性和空间分布分析。

- **实验充分性与公平性**：
  - 涵盖效率、准确率、主观一致性三维度；
  - 采用5折交叉验证；
  - 标注任务由认证病理专家执行，结果具备权威性。
  - 数据样本虽仅限犬癌症切片，但为**人类膀胱癌的可靠动物模型**，合理具备转化价值。

---

## 六、主要结论与发现

- **效率提升**：潜空间聚类引导标注比顺序标注快约25%（47 vs 63分钟；每细胞9.4s vs 12.6s）。
- **精度表现**：
  - 核仁分类准确率达 98.3%，分裂像 96.3%，形状 59.5%。
  - 仅用 215 个样本即可实现核仁分类 95.5% 准确率。
- **一致性分析**：
  - 染色质和显著核仁标注一致率 100%、核仁 κ=0.95；
  - 分裂像 κ=0.58、形状 κ=0.36 存在主观差异。
- **特征独立性**：不同形态特征间相关性弱（|r| < 0.3），提示多维形态学空间可独立建模。
- **临床意义**：可实现专家级自动分类，适配低资源实验室，支持“人机混合诊断”。

---

## 七、优点与创新性

- **技术创新**：
  - 将主动学习与对比学习融合，实现半监督细胞级特征提取。
  - 使用多模态卷积自编码器融合原图、掩膜与区域特征。
- **实用价值**：
  - 交互式标注界面大幅减轻专家标注负担；
  - 可通过伪标签传播加速模型迭代。
- **科学贡献**：
  - 提供开放代码与标准化标注体系；
  - 案例验证跨专家一致性，支持未来临床拓展。

---

## 八、不足与局限

- **实验覆盖**：
  - 仅在犬膀胱癌切片上评估，缺乏跨组织或多物种测试；
  - 未涉及多中心或不同扫描设备的泛化验证。
- **主观标注偏差**：
  - 分裂像与核形状分类存在较高人为不确定性；
  - 需建立更强的噪声鲁棒算法或多专家共识机制。
- **算力与系统性能**：
  - 未提供详细算力信息，不利于复现可比性。
- **扩展性**：
  - 当前界面针对研究环境优化，尚未验证真实诊断工作流中的稳定性与易用性。

---

**（完）**
