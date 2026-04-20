---
title: "AnnotateAnyCell: Open-Source AI Framework for Efficient Annotation in Digital Pathology"
title_zh: AnnotateAnyCell：一种用于数字病理高效标注的开源人工智能框架
authors: "Verma, S., Malusare, A., Wang, M., Wang, L., Mahapatra, A., English, A. L., Cox, A. D., Broman, M., de Brot, S., Burcham, G., Knapp, D., Dhawan, D., Sola, M., Aggarwal, V., Grama, A., Lanman, N. A."
date: 2026-04-13
pdf: "https://www.biorxiv.org/content/10.1101/2025.11.02.686114v3.full.pdf"
tags: ["query:cellrep"]
score: 10.0
evidence: 数字病理中利用潜空间可视化和对比学习进行细胞标注与分类的半监督框架
tldr: "本文提出一种开源半监督AI框架AnnotateAnyCell，通过结合主动对比学习、人机交互反馈与伪标签传播，提高病理全切片图像的细胞注释效率与分类准确度。评估结果显示注释时间减少25%，分类精度超过96%，显著减轻专家标注负担。"
source: biorxiv
selection_source: fresh_fetch
figures_json: "[{\"url\": \"assets/figures/biorxiv/biorxiv-10-1101-2025-11-02-686114-v3/fig-001.webp\", \"caption\": \"Figure 3: Left panel: Displays annotation summary statistics including counts for different morphological features along with distribution histograms. Center panel: Whole slide image view with cyan markers indicating the spatial locations of all annotated cells across the tissue sample, enabling pathologists to assess spatial distribution patterns and tissue architecture context. Right panel: Individual cell inspection tool showing detailed annotations for the selected cell (Tile 2791) with its specific morphological classifications. The interface includes data export functionality (Download CSV), version information, and the ability to filter and visualize cells based on specific morphological criteria. This output interface enables analysis of annotation results and supports research workflows requiring quantitative cellular phenotype data.\", \"page\": 6, \"index\": 1, \"width\": 968, \"height\": 523}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-1101-2025-11-02-686114-v3/fig-002.webp\", \"caption\": \"Figure 4: A. Sequential snapshots of the learned embedding space progression of annotations (green) within the unlabeled cellular population (blue). B. Classification evaluation of mitotic figures, nucleoli, and nuclear shape across training sizes using 5-fold cross-validation. C. Scaling behaviors highlight fundamental differences in data efficiency.\", \"page\": 7, \"index\": 2, \"width\": 951, \"height\": 952}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-1101-2025-11-02-686114-v3/fig-003.webp\", \"caption\": \"Figure 1: Pre-processing stage: Raw H&E-stained tissue images undergo segmentation using Cellpose models to generate nuclear masks. Each detected nucleus is extracted as three complementary representations: raw image patches, isolated nuclear regions, and semantic masks; Active Learning Loop: Expert pathologists (represented by colored figures) provide initial annotations for nuclear morphology features of neoplastic cells, including mitotic figures, vesicular chromatin, and prominent nucleoli. These labeled samples train a contrastive classifier that generates embeddings and pseudolabels for unlabeled data. A convolutional autoencoder processes the multi-modal inputs (raw, isolated, mask) to learn compact latent representations; Output Interface: The system produces annotated whole slide images with nuclei visualization, quantitative feature distributions, and prediction probabilities for downstream analysis. The iterative process refines the model’s understanding of cellular morphologies through expert feedback. Image Preparation: Left: Representative whole-slide image (WSI). Center: Nuclear segmentation results using pretrained Cellpose models. Right: Binary segmentation mask showing all detected valid cells. (Bottom row) Nine examples of 128×128 pixel cellular tiles illustrating morphological diversity across expert-defined annotation categories. Examples include bizarre mitotic figures showing irregular mitotic configurations, canonical mitotic figures demonstrating typical mitotic chromatin condensation patterns, nucleolar variations (single vs. multiple nucleoli) combined with nuclear shape classifications (circular, oval, irregular), and chromatin texture patterns (vesicular chromatin).\", \"page\": 3, \"index\": 3, \"width\": 968, \"height\": 819}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-1101-2025-11-02-686114-v3/fig-004.webp\", \"caption\": \"Figure 5: A. Illustrates labelling time with and without clustering, along with spatial distributions of agreement (green) and disagreement (brown) reveal localized cell-level ambiguities, with disagreement intensity encoded by saturation. B. Presents the annotation workflow metrics like agreement rates, reliability scores, consistency and spatial coverage scores across 11 annotators. C. Illustrates feature correlation demonstrating nuclear features are largely independent dimensions of morphology, and pairwise disagreement analyses showing some users might disagree more than others.\", \"page\": 8, \"index\": 4, \"width\": 964, \"height\": 539}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-1101-2025-11-02-686114-v3/fig-005.webp\", \"caption\": \"Figure 2: Left panel: Displays workflow guide for pathologists, nuclear size distribution histogram, and nuclear-to-cell ratio distribution with red indicators showing the currently selected cell’s measurements. Center panel: Interactive UMAP embedding visualization, where each point represents a cellular tile extracted from the whole slide image. Cells are color-coded based on annotation status (blue: unlabeled, green: labeled, orange: selected) and naturally cluster based on morphological similarities. Right panel: Shows a high-resolution preview of the selected cell tile (Tile 710) with morphological annotation options including mitotic figures, chromatin patterns, nucleoli characteristics, and nuclear shape classifications. The interface includes progress tracking (300/300 labeled points), version control, and model retraining capabilities (\\\"Update Clusters\\\" button).\", \"page\": 5, \"index\": 5, \"width\": 968, \"height\": 523}]"
motivation: 传统组织病理图像的人工注释耗时且昂贵，限制了计算病理和临床AI的广泛应用。
method: 提出结合主动对比学习和人机迭代反馈的半监督开源框架，整合Cellpose分割、UMAP可视化及伪标签传播。
result: "注释时间减少25%，分类精度在不同细胞特征上最高达98.3%，一致性在明确特征上表现良好。"
conclusion: 该框架显著减少了细胞注释的人工开销，并在形态明确特征上实现专家级精度，为资源受限环境中的AI诊断提供可扩展方案。
---

## 摘要
全视野组织病理学图像的人工标注仍然是计算病理学和临床人工智能应用部署的关键瓶颈，因其在大规模下需要专家投入大量时间。本文提出了一个开源的半监督框架，将主动对比学习与人机交互的迭代式反馈相结合，以实现高效的细胞标注与分类。该流程整合了 Cellpose 分割、基于 UMAP 的潜空间可视化，以及结合伪标签传播的对比学习。我们在五张来源于犬浸润性尿路上皮癌的全视野图像上进行了评估，涵盖低级别、中级别及高级别的组织学分级，放大倍数为 40x。在潜空间聚类引导的标注下，所需时间为 47 分钟，而顺序标注为 63 分钟，实现了 25%（95% 置信区间 18–32%）的时间缩减。对于有丝分裂象的分类准确率达到 96.3% ± 1.2%，核仁的分类准确率为 98.3% ± 1.4%，使用了 1,075 个标注样本；此外，仅使用 215 个样本，核仁分类仍可达到 95.5% ± 1.5% 的准确率。在不同标注者之间，染色质（κ = 1.00）与核仁（κ = 0.95）的一致性较高，而有丝分裂象（κ = 0.58）与核形态（κ = 0.36）中等一致性，反映了这些类别在形态学上的内在模糊性。该框架在实现专家级准确度的同时显著降低了标注负担，为资源受限的病理学环境中实现人工智能辅助诊断提供了可扩展路径。

## Abstract
AO_SCPLOWBSTRACTC_SCPLOWManual annotation of histopathological whole slide images remains a critical bottleneck for computational pathology and clinical AI deployment, requiring prohibitive expert time at scale. Here we present an open-source semi-supervised framework combining active contrastive learning with iterative human-in-the-loop feedback for efficient cellular annotation and classification. The pipeline integrates Cellpose segmentation, UMAP-based latent space visualization, and contrastive learning with pseudolabel propagation, evaluated on five whole slide images of canine invasive urothelial carcinoma across low, intermediate, and high histological grades at 40x magnification. Latent space clustering-guided annotation required 47 minutes compared to 63 minutes for sequential annotation, a 25% reduction (95% CI 18-32%). Classification accuracy reached 96.3% {+/-} 1.2% for mitotic figures and 98.3% {+/-} 1.4% for nucleoli using 1,075 labeled samples, with nucleoli classification achieving 95.5% {+/-} 1.5% accuracy from only 215 samples. Inter-annotator agreement was high for chromatin ({kappa} = 1.00) and nucleoli ({kappa} = 0.95) but moderate for mitotic figures ({kappa} = 0.58) and nuclear shape ({kappa} = 0.36), reflecting intrinsic morphological ambiguity in these categories. This framework substantially reduces annotation burden while achieving expert-level accuracy for well-defined morphological features, providing a scalable path toward AI-assisted diagnostics in resource-constrained pathology settings.

---

## 论文详细总结（自动生成）

# AnnotateAnyCell：用于数字病理高效标注的开源AI框架 —— 中文结构化总结

## 1. 研究动机与核心问题

- **研究背景**：  
  在数字病理学中，组织全视野图像（Whole Slide Image, WSI）通常包含数十万细胞，数据量巨大且特征复杂。传统人工方式要求病理专家逐一标注细胞核形态（如有丝分裂象、核仁、染色质形态等），这不仅耗时巨大、成本高昂，还成为临床AI模型训练和部署的瓶颈。

- **核心问题**：  
  现有全监督模型严重依赖大规模标注数据，跨机构泛化能力差，且缺乏可被病理学家交互验证的直观工具。  
  作者希望降低专家标注负担，通过“**半监督学习 + 主动学习 + 可交互潜空间嵌入**”的方式，让模型在有限标注条件下快速学习、自动化聚类，并保留专家控制权。

- **研究目标**：  
  实现一个**开源、可解释且节省专家时间的人机协同标注平台**，推动 AI 在资源受限的病理环境中的落地。

---

## 2. 方法论与技术框架

### 2.1 核心思想
提出 **AnnotateAnyCell** —— 一个结合半监督学习、主动对比学习（Active Contrastive Learning）与人机迭代反馈的人机协同标注系统。  
通过学习到的潜空间（embedding）将形态相似的细胞聚类展示，专家可以直接在二维可视化界面中标注相似群体并进行快速修正。

### 2.2 技术组成

1. **Cellpose 分割**  
   - 使用预训练的 *Cellpose cyto3 模型* 对 H&E 染色的切片进行核与细胞级分割。  
   - 输出三类图像：原始切片、语义掩膜、以及提取的单细胞区域。

2. **UMAP 潜空间嵌入与交互界面**  
   - 对 128×128 像素的细胞 patch 提取嵌入特征并使用 **UMAP** 进行降维。  
   - 界面由三部分组成：  
     - 中央面板：UMAP 散点图，展示所有细胞的聚类情况。  
     - 左侧面板：统计分布与进度条。  
     - 右侧面板：高分辨细胞预览和标注选项。

3. **对比学习与伪标签传播**  
   - 核心算法：对比学习 + 交叉熵联合损失。  
     \[
     L_{total} = αL_{CE} + βL_{InfoNCE}
     \]
     其中 InfoNCE 用于增强特征区分性，CE 用于监督分类。
   - 模型采用**类均衡的伪标签选择策略**，优先选取每类中最高置信度的样本进行扩展标注。
   - 同时采用不确定性采样（uncertainty sampling）与多样性促进，避免过拟合于主导类。

4. **多模态自编码器（VAE）**
   - 三输入通道：原始图像、核区域图、语义掩膜。
   - 通过并行编码器和变分瓶颈（VAE reparameterization trick）学习 256 维潜向量。
   - 总体损失：
     \[
     L_{total} = αL_{recon} + βL_{feat}
     \]
     结合重构误差与特征分类损失，以捕获高层次形态特征。

5. **主动学习迭代循环**
   - 专家标注 → 模型更新 → 伪标签生成 → 样本再选择。  
   - 在每轮迭代中 UMAP 聚类动态更新，实现逐步精化的潜空间结构。

---

## 3. 实验设计

- **数据来源**：  
  使用犬的浸润性尿路上皮癌（Invasive Urothelial Carcinoma, IncUC）样本（五张组织切片，40×放大率）。  
  - 来源：普渡大学兽医医院临床病例。  
  - 每张图像分辨率达 80,000×100,000 像素，总体含有数十万细胞核。  
  - 细胞特征类别：有丝分裂象、染色质质地、核仁数量/显著性、核形态。

- **标注者与实验规模**：  
  - 参与者包括 11 位经认证的兽医病理学家。  
  - 每位专家标注约 300 个细胞，累计超过 3,000+ 标注样本。  
  - 实验对象包含三类任务：  
    - 有丝分裂象分类  
    - 核仁特征分类  
    - 核形态识别  

- **对比方式**：  
  - **顺序人工标注 vs 聚类引导标注** → 时间效率对比。  
  - **半监督算法 vs 全监督基线** → 精度和样本效率。  
  - **不同标注者间一致性分析（Cohen’s κ）**。

- **评测指标**：  
  分类准确率、效率增益、Cohen’s κ 一致性、特征间相关性 (|r|)。

---

## 4. 资源与算力

- 论文未明确报告 GPU 型号、数量及训练时间。  
- 从方法规模和模型复杂度推测，计算需求较为中等（CNN + VAE + UMAP），可在单机 GPU（如 NVIDIA RTX 3090/4090）条件下运行。  
- 作者声明平台将开源，支持本地化低资源部署。

---

## 5. 实验数量与充分性

- **主要实验类型**：
  1. 标注效率对比实验（时间/速度）  
  2. 模型分类精度随样本数量变化曲线（学习曲线）  
  3. 聚类质量与潜空间可视化（UMAP 散点图）  
  4. 多标注者一致性与相关性分析  
  5. 特征间独立性与形态学相关性研究  

- **实验量化数据**：
  - 约 5 套切片 × 数千细胞样本 × 11 位专家标注。  
  - 精度分析采用五折交叉验证（5-fold CV）。  

- **充分性评价**：
  - 实验覆盖到注释效率、精度、标注一致性和可解释性多个维度，设计完整。  
  - 然而仅基于一个肿瘤类型（犬尿路上皮癌），跨组织泛化验证尚缺乏。

---

## 6. 主要结论与发现

- **效率提升**：  
  比传统逐点标注节省 25%（47 分钟 vs 63 分钟），单细胞标注耗时下降约 3 秒。

- **精度表现**：  
  - 核仁分类：98.3% ± 1.4%  
  - 有丝分裂象：96.3% ± 1.2%  
  - 核形态：59.5% ± 2.1%（识别难度较高）  
  - 仅用 215 个标注样本，核仁分类即可达 95.5% 精度。

- **一致性分析**：  
  - 染色质与核仁 κ ≥ 0.95（高一致性）  
  - 有丝分裂象 κ = 0.58、形态 κ = 0.36（中等或较低一致性）

- **多特征独立性**：  
  各形态学维度弱相关 (|r| < 0.3)，暗示核特征是多维互补的诊断参数。

- **临床应用潜力**：  
  高置信度预测可用于自动化筛查，低置信样本由专家复核，实现**半自动诊断流程**。

---

## 7. 方法优点与创新点

- **开放源代码与通用框架**：  
  完全开源、模块化、支持人机交互与再训练。

- **创新的交互式潜空间标注**：  
  通过 UMAP+对比学习 embedding，使专家以空间聚类方式标注而非逐点操作。

- **高效伪标签传播算法**：  
  融合类均衡与置信度筛选，减少伪标签噪音。

- **多模态自编码器**：  
  同时利用原始图像、核特征、语义掩膜三种模态，捕获细胞上下文信息。

- **实证充分性强**：  
  覆盖不同专家、不同特征、不同标注阶段的多视角评估。

---

## 8. 不足与局限

- **数据范围有限**：  
  仅分析一种犬肿瘤组织，跨物种或多组织泛化能力未验证。

- **缺乏算力与性能细节**：  
  未说明训练设备、时间与参数；可复现性信息略显不足。

- **特征主观性问题**：  
  像“核形态”类连续表型分类仍具主观模糊，导致模型上限受限。

- **临床验证不足**：  
  仅为离线实验评估，尚未在实际诊断场景中进行前瞻性验证。

- **噪声与偏差控制**：  
  对标注噪声的鲁棒性未作深入实验，未来需加入噪声建模或贝叶斯不确定性推理。

---

**（完）**
