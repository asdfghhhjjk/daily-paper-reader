---
title: "AnnotateAnyCell: Open-Source AI Framework for Efficient Annotation in Digital Pathology"
title_zh: AnnotateAnyCell：用于数字病理学高效标注的开源人工智能框架
authors: "Verma, S., Malusare, A., Wang, M., Wang, L., Mahapatra, A., English, A. L., Cox, A. D., Broman, M., de Brot, S., Burcham, G., Knapp, D., Dhawan, D., Sola, M., Aggarwal, V., Grama, A., Lanman, N. A."
date: 2026-04-13
pdf: "https://www.biorxiv.org/content/10.1101/2025.11.02.686114v3.full.pdf"
tags: ["query:pathseg"]
score: 10.0
evidence: 组织病理学WSI中高效的细胞标注与分类
tldr: "本文提出一个开源半监督框架AnnotateAnyCell，用于数字病理图像的高效细胞标注，结合主动对比学习与人机交互反馈，实现了标注时间减少约25%和专家水平的分类准确率，为资源有限的病理AI诊断提供了可扩展方案。"
source: biorxiv
selection_source: fresh_fetch
figures_json: "[{\"url\": \"assets/figures/biorxiv/biorxiv-10-1101-2025-11-02-686114-v3/fig-001.webp\", \"caption\": \"Figure 3: Left panel: Displays annotation summary statistics including counts for different morphological features along with distribution histograms. Center panel: Whole slide image view with cyan markers indicating the spatial locations of all annotated cells across the tissue sample, enabling pathologists to assess spatial distribution patterns and tissue architecture context. Right panel: Individual cell inspection tool showing detailed annotations for the selected cell (Tile 2791) with its specific morphological classifications. The interface includes data export functionality (Download CSV), version information, and the ability to filter and visualize cells based on specific morphological criteria. This output interface enables analysis of annotation results and supports research workflows requiring quantitative cellular phenotype data.\", \"page\": 6, \"index\": 1, \"width\": 968, \"height\": 523}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-1101-2025-11-02-686114-v3/fig-002.webp\", \"caption\": \"Figure 4: A. Sequential snapshots of the learned embedding space progression of annotations (green) within the unlabeled cellular population (blue). B. Classification evaluation of mitotic figures, nucleoli, and nuclear shape across training sizes using 5-fold cross-validation. C. Scaling behaviors highlight fundamental differences in data efficiency.\", \"page\": 7, \"index\": 2, \"width\": 951, \"height\": 952}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-1101-2025-11-02-686114-v3/fig-003.webp\", \"caption\": \"Figure 1: Pre-processing stage: Raw H&E-stained tissue images undergo segmentation using Cellpose models to generate nuclear masks. Each detected nucleus is extracted as three complementary representations: raw image patches, isolated nuclear regions, and semantic masks; Active Learning Loop: Expert pathologists (represented by colored figures) provide initial annotations for nuclear morphology features of neoplastic cells, including mitotic figures, vesicular chromatin, and prominent nucleoli. These labeled samples train a contrastive classifier that generates embeddings and pseudolabels for unlabeled data. A convolutional autoencoder processes the multi-modal inputs (raw, isolated, mask) to learn compact latent representations; Output Interface: The system produces annotated whole slide images with nuclei visualization, quantitative feature distributions, and prediction probabilities for downstream analysis. The iterative process refines the model’s understanding of cellular morphologies through expert feedback. Image Preparation: Left: Representative whole-slide image (WSI). Center: Nuclear segmentation results using pretrained Cellpose models. Right: Binary segmentation mask showing all detected valid cells. (Bottom row) Nine examples of 128×128 pixel cellular tiles illustrating morphological diversity across expert-defined annotation categories. Examples include bizarre mitotic figures showing irregular mitotic configurations, canonical mitotic figures demonstrating typical mitotic chromatin condensation patterns, nucleolar variations (single vs. multiple nucleoli) combined with nuclear shape classifications (circular, oval, irregular), and chromatin texture patterns (vesicular chromatin).\", \"page\": 3, \"index\": 3, \"width\": 968, \"height\": 819}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-1101-2025-11-02-686114-v3/fig-004.webp\", \"caption\": \"Figure 5: A. Illustrates labelling time with and without clustering, along with spatial distributions of agreement (green) and disagreement (brown) reveal localized cell-level ambiguities, with disagreement intensity encoded by saturation. B. Presents the annotation workflow metrics like agreement rates, reliability scores, consistency and spatial coverage scores across 11 annotators. C. Illustrates feature correlation demonstrating nuclear features are largely independent dimensions of morphology, and pairwise disagreement analyses showing some users might disagree more than others.\", \"page\": 8, \"index\": 4, \"width\": 964, \"height\": 539}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-1101-2025-11-02-686114-v3/fig-005.webp\", \"caption\": \"Figure 2: Left panel: Displays workflow guide for pathologists, nuclear size distribution histogram, and nuclear-to-cell ratio distribution with red indicators showing the currently selected cell’s measurements. Center panel: Interactive UMAP embedding visualization, where each point represents a cellular tile extracted from the whole slide image. Cells are color-coded based on annotation status (blue: unlabeled, green: labeled, orange: selected) and naturally cluster based on morphological similarities. Right panel: Shows a high-resolution preview of the selected cell tile (Tile 710) with morphological annotation options including mitotic figures, chromatin patterns, nucleoli characteristics, and nuclear shape classifications. The interface includes progress tracking (300/300 labeled points), version control, and model retraining capabilities (\\\"Update Clusters\\\" button).\", \"page\": 5, \"index\": 5, \"width\": 968, \"height\": 523}]"
motivation: 手工标注病理切片费时且限制了AI在病理诊断中的大规模应用。
method: 采用Cellpose分割、UMAP可视化及对比学习与伪标签传播的半监督流程实现细胞标注。
result: "该框架在犬侵袭性尿路上皮癌的全切片图像上实现了较高分类准确率，且标注时间减少约25%。"
conclusion: 该研究证明了结合主动学习与人机交互的开源标注框架能有效降低人工标注负担并保持高精度。
---

## 摘要
对组织病理学全视野切片图像进行人工标注仍然是计算病理学和临床人工智能部署的关键瓶颈，因为在大规模下需要消耗专家大量时间。我们提出了一个开源的半监督框架，该框架结合主动对比学习与迭代的人机交互反馈，用于高效的细胞标注和分类。整个流程集成了 Cellpose 分割、基于 UMAP 的潜空间可视化，以及采用伪标签传播的对比学习，并在 5 张犬侵袭性尿路上皮癌的全视野切片图像上进行了评估，这些样本涵盖了低级、中级和高级组织学分级，放大倍数为 40×。与连续标注相比，潜空间聚类引导的标注耗时 47 分钟，而连续标注耗时 63 分钟，减少了 25%（95% 置信区间 18–32%）。在 1,075 个已标注样本中，有丝分裂体分类准确率为 96.3% ± 1.2%，核仁分类准确率为 98.3% ± 1.4%；而仅使用 215 个样本时，核仁分类仍达到 95.5% ± 1.5% 的准确率。不同标注者之间对染色质（κ = 1.00）和核仁（κ = 0.95）的标注一致性较高，但对有丝分裂体（κ = 0.58）和核形态（κ = 0.36）的一致性中等，反映了这些类别中固有的形态学不确定性。该框架在保持专家级精度的同时显著降低了标注负担，为资源受限的病理环境中的人工智能辅助诊断提供了一条可扩展的路径。

## Abstract
AO_SCPLOWBSTRACTC_SCPLOWManual annotation of histopathological whole slide images remains a critical bottleneck for computational pathology and clinical AI deployment, requiring prohibitive expert time at scale. Here we present an open-source semi-supervised framework combining active contrastive learning with iterative human-in-the-loop feedback for efficient cellular annotation and classification. The pipeline integrates Cellpose segmentation, UMAP-based latent space visualization, and contrastive learning with pseudolabel propagation, evaluated on five whole slide images of canine invasive urothelial carcinoma across low, intermediate, and high histological grades at 40x magnification. Latent space clustering-guided annotation required 47 minutes compared to 63 minutes for sequential annotation, a 25% reduction (95% CI 18-32%). Classification accuracy reached 96.3% {+/-} 1.2% for mitotic figures and 98.3% {+/-} 1.4% for nucleoli using 1,075 labeled samples, with nucleoli classification achieving 95.5% {+/-} 1.5% accuracy from only 215 samples. Inter-annotator agreement was high for chromatin ({kappa} = 1.00) and nucleoli ({kappa} = 0.95) but moderate for mitotic figures ({kappa} = 0.58) and nuclear shape ({kappa} = 0.36), reflecting intrinsic morphological ambiguity in these categories. This framework substantially reduces annotation burden while achieving expert-level accuracy for well-defined morphological features, providing a scalable path toward AI-assisted diagnostics in resource-constrained pathology settings.

---

## 论文详细总结（自动生成）

# AnnotateAnyCell：用于数字病理学高效标注的开源人工智能框架 — 总结分析

---

## 一、研究动机与核心问题

- **研究背景**：在数字病理学中，全视野组织切片（Whole Slide Images, WSI）往往包含数十万个细胞，文件体积巨大（可达数 GB）。现有深度学习模型虽能进行自动化细胞识别与分类，但**临床部署的瓶颈在于人工标注成本**过高，需要病理专家耗费大量时间逐细描绘细胞边界及形态学类别。  
- **核心问题**：如何在保证专家级准确率的前提下，显著减少标注工作量和时间，从而实现高效、可扩展的人工智能辅助病理诊断。  
- **研究目标**：提出一种开源的“半监督 + 主动学习 + 人机交互”框架，使病理专家可在学习到的潜空间中快速标注相似细胞，实现高效数据构建与可靠分类。

---

## 二、方法论与技术体系

### 1. 核心思想
- 将**对比学习（Contrastive Learning）**与**主动学习（Active Learning）**融合，形成一个**半监督循环标注流程**。  
- 结合**人机交互式界面**，使病理专家能直接在由 UMAP 投影的嵌入空间中进行标注，而非传统的空间坐标基础。

### 2. 流程组成（四个主要阶段）

1. **Cellpose 分割阶段**  
   - 使用预训练的 Cellpose 模型（cyto3）对 H&E 染色切片进行核分割。  
   - 提取每个细胞的三种视图：原始图块、孤立核区、语义分割掩膜。  

2. **潜空间可视化与专家标注**  
   - 以 UMAP 降维生成二维嵌入空间，形态相似的细胞聚集。  
   - 专家在界面中浏览聚类分布，选择代表性样本进行标注。  

3. **对比学习与伪标签生成**  
   - 采用 InfoNCE 损失进行嵌入优化：  
     \[
     L_{InfoNCE} = -\log\frac{\exp(sim(q,k^+)/\tau)}{\sum_{i=1}^{K}\exp(sim(q,k_i)/\tau)}
     \]
   - 总损失为监督交叉熵与对比损失加权求和：  
     \[
     L_{total} = \alpha L_{CE} + \beta L_{InfoNCE}
     \]
   - 高置信度样本生成“伪标签”（pseudolabels），确保类别平衡。  

4. **多模态卷积变分自编码器（VAE）**  
   - 输入三种模态（原图、核区、掩膜），通过并行编码器提取特征再融合。  
   - 生成 256 维潜向量，经 UMAP 投影形成更新聚类空间。  
   - 损失函数结合重建误差与特征预测交叉熵。  

5. **迭代人机反馈**
   - 专家在新嵌入空间中验证或修正伪标签，迭代更新模型，逐步提升分类性能与聚类结构。

---

## 三、实验设计

### 1. 数据来源
- **物种与疾病**：犬类侵袭性尿路上皮癌（Canine Invasive Urothelial Carcinoma, IncUC），该动物模型与人类肌层浸润性膀胱癌在生物学上高度相似。  
- **数据量与制备**：  
  - 5 张全切片图像（80,000×100,000 像素，40× 放大）。  
  - 每张切片经病理专家挑选，确保染色均一、细胞形态完整。  
- **标注类别**：有丝分裂体、核仁特征（单/多/显著）、染色质纹理、核形态（圆形、椭圆、非规则）。

### 2. 对比与性能评估
- 未与外部商业平台直接对比，但参考了包括 QuPath、Orbit、HALO、Quick Annotator 等已有工具。  
- 内部对比方式：**聚类引导标注 vs. 顺序标注**。  

### 3. 实验指标
- **效率指标**：标注时间、细胞标注速率（秒/细胞）。  
- **准确度指标**：分类准确率、Cohen’s κ一致性系数。  
- **泛化指标**：使用 5 折交叉验证评估特征分类稳定性。

---

## 四、资源与算力

- 文中**未明确说明**所使用的 GPU 型号、数量及训练时间。  
- 可推测主要执行单机或研究级 GPU（如 NVIDIA RTX/3090 级别）即可完成，因为涉及 Cellpose 分割与中等规模网络。  
- 论文仅指出模型可通过 BokehJS 实时交互、MongoDB 数据管理、异步更新。

---

## 五、实验数量与充分性

- 样本规模：五张 WSI，共计上千细胞实例（约 1,075 个已标注样本）。  
- 参与者：11 位认证病理学家与住院医师构成标注者群。  
- 实验内容：
  - 主动学习迭代实验（不同标注数下的准确率变化）。  
  - 时间效率对比实验（聚类引导 vs. 顺序）。  
  - 一致性与相关性分析（多专家 κ 系数、特征相关矩阵）。  
- 实验较为充分，覆盖了效率、准确率、一致性三大维度，**但缺乏不同病种或跨机构验证**。

---

## 六、主要结论与发现

- **效率提升**：聚类引导标注平均节省 25% 时间（47 分钟 vs 63 分钟）。  
- **学习效果**：  
  - 核仁分类准确率最高（98.3% ± 1.4%）。  
  - 有丝分裂体次之（96.3% ± 1.2%）。  
  - 核形态分类较低（59.5% ± 2.1%）。  
- **数据效率**：仅 215 个样本即可达到核仁分类 95.5% 的准确率。  
- **一致性分析**：染色质与核仁特征标注 κ ≥ 0.95，一致性高；形态与有丝分裂体标注中等一致性。  
- **临床潜力**：可在有限标注条件下建立机构特定模型，用于初筛或辅助诊断。

---

## 七、优点与创新亮点

- ✅ **半监督与主动学习结合**：在病理领域中少见的多模态人机迭代框架。  
- ✅ **交互式嵌入空间标注**：将 UMAP 嵌入应用于专家真实操作界面。  
- ✅ **数据效率极高**：能在极少标注样本中达到接近专家的分类准确率。  
- ✅ **开源平台**：基于 Python + BokehJS + MongoDB，支持多用户协作。  
- ✅ **明确可解释性**：潜空间聚类可视化提供结构化反馈，提高用户信任。

---

## 八、不足与局限

- ⚠ **算力与训练细节未公开**：影响复现性评估。  
- ⚠ **疾病单一性**：仅验证在犬尿路上皮癌，缺乏跨病种泛化。  
- ⚠ **低一致性特征（如核形状）处理仍薄弱**，需进一步引入不确定性建模或多专家共识机制。  
- ⚠ **无与商业平台或标准化基准测试明确对比**，难以量化相对优势。  
- ⚠ **临床验证阶段缺失**：尚未进行前瞻性或多机构临床试用。

---

**（完）**
