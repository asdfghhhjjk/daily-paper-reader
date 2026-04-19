---
title: "AnnotateAnyCell: Open-Source AI Framework for Efficient Annotation in Digital Pathology"
title_zh: AnnotateAnyCell：面向数字病理学高效标注的开源人工智能框架
authors: "Verma, S., Malusare, A., Wang, M., Wang, L., Mahapatra, A., English, A. L., Cox, A. D., Broman, M., de Brot, S., Burcham, G., Knapp, D., Dhawan, D., Sola, M., Aggarwal, V., Grama, A., Lanman, N. A."
date: 2026-04-13
pdf: "https://www.biorxiv.org/content/10.1101/2025.11.02.686114v3.full.pdf"
tags: ["query:cellrep"]
score: 10.0
evidence: 利用潜空间可视化在数字病理中进行高效的细胞标注与分类
tldr: "本文提出AnnotateAnyCell，一个开源半监督框架，利用主动对比学习与人机交互迭代优化病理细胞标注效率。通过集成Cellpose分割、UMAP可视化和伪标签传播，该方法在减少约四分之一标注时间的同时，保持超过96%的分类准确率，为资源受限条件下的AI辅助病理诊断提供可行方案。"
source: biorxiv
selection_source: fresh_fetch
figures_json: "[{\"url\": \"assets/figures/biorxiv/biorxiv-10-1101-2025-11-02-686114-v3/fig-001.webp\", \"caption\": \"Figure 3: Left panel: Displays annotation summary statistics including counts for different morphological features along with distribution histograms. Center panel: Whole slide image view with cyan markers indicating the spatial locations of all annotated cells across the tissue sample, enabling pathologists to assess spatial distribution patterns and tissue architecture context. Right panel: Individual cell inspection tool showing detailed annotations for the selected cell (Tile 2791) with its specific morphological classifications. The interface includes data export functionality (Download CSV), version information, and the ability to filter and visualize cells based on specific morphological criteria. This output interface enables analysis of annotation results and supports research workflows requiring quantitative cellular phenotype data.\", \"page\": 6, \"index\": 1, \"width\": 968, \"height\": 523}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-1101-2025-11-02-686114-v3/fig-002.webp\", \"caption\": \"Figure 4: A. Sequential snapshots of the learned embedding space progression of annotations (green) within the unlabeled cellular population (blue). B. Classification evaluation of mitotic figures, nucleoli, and nuclear shape across training sizes using 5-fold cross-validation. C. Scaling behaviors highlight fundamental differences in data efficiency.\", \"page\": 7, \"index\": 2, \"width\": 951, \"height\": 952}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-1101-2025-11-02-686114-v3/fig-003.webp\", \"caption\": \"Figure 1: Pre-processing stage: Raw H&E-stained tissue images undergo segmentation using Cellpose models to generate nuclear masks. Each detected nucleus is extracted as three complementary representations: raw image patches, isolated nuclear regions, and semantic masks; Active Learning Loop: Expert pathologists (represented by colored figures) provide initial annotations for nuclear morphology features of neoplastic cells, including mitotic figures, vesicular chromatin, and prominent nucleoli. These labeled samples train a contrastive classifier that generates embeddings and pseudolabels for unlabeled data. A convolutional autoencoder processes the multi-modal inputs (raw, isolated, mask) to learn compact latent representations; Output Interface: The system produces annotated whole slide images with nuclei visualization, quantitative feature distributions, and prediction probabilities for downstream analysis. The iterative process refines the model’s understanding of cellular morphologies through expert feedback. Image Preparation: Left: Representative whole-slide image (WSI). Center: Nuclear segmentation results using pretrained Cellpose models. Right: Binary segmentation mask showing all detected valid cells. (Bottom row) Nine examples of 128×128 pixel cellular tiles illustrating morphological diversity across expert-defined annotation categories. Examples include bizarre mitotic figures showing irregular mitotic configurations, canonical mitotic figures demonstrating typical mitotic chromatin condensation patterns, nucleolar variations (single vs. multiple nucleoli) combined with nuclear shape classifications (circular, oval, irregular), and chromatin texture patterns (vesicular chromatin).\", \"page\": 3, \"index\": 3, \"width\": 968, \"height\": 819}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-1101-2025-11-02-686114-v3/fig-004.webp\", \"caption\": \"Figure 5: A. Illustrates labelling time with and without clustering, along with spatial distributions of agreement (green) and disagreement (brown) reveal localized cell-level ambiguities, with disagreement intensity encoded by saturation. B. Presents the annotation workflow metrics like agreement rates, reliability scores, consistency and spatial coverage scores across 11 annotators. C. Illustrates feature correlation demonstrating nuclear features are largely independent dimensions of morphology, and pairwise disagreement analyses showing some users might disagree more than others.\", \"page\": 8, \"index\": 4, \"width\": 964, \"height\": 539}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-1101-2025-11-02-686114-v3/fig-005.webp\", \"caption\": \"Figure 2: Left panel: Displays workflow guide for pathologists, nuclear size distribution histogram, and nuclear-to-cell ratio distribution with red indicators showing the currently selected cell’s measurements. Center panel: Interactive UMAP embedding visualization, where each point represents a cellular tile extracted from the whole slide image. Cells are color-coded based on annotation status (blue: unlabeled, green: labeled, orange: selected) and naturally cluster based on morphological similarities. Right panel: Shows a high-resolution preview of the selected cell tile (Tile 710) with morphological annotation options including mitotic figures, chromatin patterns, nucleoli characteristics, and nuclear shape classifications. The interface includes progress tracking (300/300 labeled points), version control, and model retraining capabilities (\\\"Update Clusters\\\" button).\", \"page\": 5, \"index\": 5, \"width\": 968, \"height\": 523}]"
motivation: 手工标注病理全切片图像耗时且限制计算病理学和AI临床应用的规模化落地。
method: 研究提出一个结合主动对比学习与人机交互反馈的开源半监督框架，集成Cellpose分割、UMAP可视化及伪标签传播。
result: "该方法将标注时间减少约25%，分类准确率最高达98%以上，且在多个形态特征上获得较高一致性。"
conclusion: 该框架有效降低病理图像标注负担，并在形态特征明确定义的类别中达到专家级准确率，展示了AI辅助病理诊断的可扩展潜力。
---

## 摘要
手工标注组织病理学全视野切片图像仍然是计算病理学和临床人工智能部署中的关键瓶颈，在大规模下需要专家投入大量时间。本文提出了一个开源的半监督框架，将主动对比学习与人机交互的迭代反馈相结合，用于实现高效的细胞标注与分类。该流程整合了 Cellpose 分割、基于 UMAP 的潜在空间可视化以及带有伪标签传播的对比学习，并在五张犬侵袭性尿路上皮癌全视野切片上进行了评估，涵盖低、中、高组织学分级，放大倍数为 40x。与顺序式标注相比，潜在空间聚类引导的标注仅需 47 分钟，而前者需要 63 分钟，减少了 25%（95% 置信区间 18–32%）。在使用 1,075 个标注样本的情况下，有丝分裂像分类准确率达到 96.3%（±1.2%），核仁分类准确率为 98.3%（±1.4%）；仅使用 215 个样本即可实现核仁分类 95.5%（±1.5%）的准确率。标注者间一致性在染色质（κ = 1.00）和核仁（κ = 0.95）方面较高，而在有丝分裂像（κ = 0.58）和核形状（κ = 0.36）方面为中等，反映了这些类别固有的形态学模糊性。该框架在显著降低标注负担的同时，对于定义明确的形态特征可实现专家级准确度，为资源受限的病理学环境中推进人工智能辅助诊断提供了一种可扩展的途径。

## Abstract
AO_SCPLOWBSTRACTC_SCPLOWManual annotation of histopathological whole slide images remains a critical bottleneck for computational pathology and clinical AI deployment, requiring prohibitive expert time at scale. Here we present an open-source semi-supervised framework combining active contrastive learning with iterative human-in-the-loop feedback for efficient cellular annotation and classification. The pipeline integrates Cellpose segmentation, UMAP-based latent space visualization, and contrastive learning with pseudolabel propagation, evaluated on five whole slide images of canine invasive urothelial carcinoma across low, intermediate, and high histological grades at 40x magnification. Latent space clustering-guided annotation required 47 minutes compared to 63 minutes for sequential annotation, a 25% reduction (95% CI 18-32%). Classification accuracy reached 96.3% {+/-} 1.2% for mitotic figures and 98.3% {+/-} 1.4% for nucleoli using 1,075 labeled samples, with nucleoli classification achieving 95.5% {+/-} 1.5% accuracy from only 215 samples. Inter-annotator agreement was high for chromatin ({kappa} = 1.00) and nucleoli ({kappa} = 0.95) but moderate for mitotic figures ({kappa} = 0.58) and nuclear shape ({kappa} = 0.36), reflecting intrinsic morphological ambiguity in these categories. This framework substantially reduces annotation burden while achieving expert-level accuracy for well-defined morphological features, providing a scalable path toward AI-assisted diagnostics in resource-constrained pathology settings.

---

## 论文详细总结（自动生成）

# AnnotateAnyCell：面向数字病理学高效标注的开源人工智能框架 — 中文深度总结

---

## 一、研究背景与核心问题

- **研究动机**：在计算病理学和临床人工智能应用中，组织病理学全视野切片（Whole Slide Image, WSI）的手工标注仍是关键瓶颈；标注工作需要高度专业知识且耗时，阻碍了大规模模型训练和落地应用。  
- **核心挑战**：  
  1. 标注过程高度依赖专家，时间成本高。  
  2. 病理细胞结构多样、形态复杂，导致类别定义的边界模糊。  
  3. 现有自动标注模型在细胞级别精确分类上存在性能与解释性不足。  
- **研究目标**：开发一个可开源、低成本、带人机交互的 AI 框架，在保证标注质量的同时显著降低标注时间，提升数字病理标注工作效率。

---

## 二、方法论与技术架构

### 2.1 核心思想
将**主动对比学习（Active Contrastive Learning）**与**人机迭代反馈机制（Human-in-the-loop）**相结合，通过半监督训练实现更少人工标注下的高精度细胞分类。

### 2.2 架构组成

1. **图像分割阶段**  
   - 使用预训练的 **Cellpose** 模型从 H&E 染色组织切片中分割细胞核。  
   - 生成多模态输入：  
     - 原始图像小块（raw patches）  
     - 分割后的独立核图像（isolated nucleus）  
     - 二值化掩膜（semantic mask）

2. **潜空间嵌入与对比学习**  
   - 使用卷积自编码器（Convolutional Autoencoder）提取潜空间特征。  
   - 利用对比损失（Contrastive Loss）在标注与未标注样本间拉近同类距离、拉远异类距离。  
   - 通过 UMAP 降维生成二维潜空间可视化；聚类中心辅助专家标注。

3. **主动学习与伪标签传播**  
   - 专家在 UMAP 可视化界面中标注部分样本。  
   - 系统根据已标注样本生成伪标签（pseudolabel），并用于指导模型再训练。  
   - 循环迭代：标注 → 模型更新 → 再可视化 → 新一轮标注。

4. **输出界面与结果分析**  
   - 标注结果通过交互式界面展示，包括分布直方图、标注一致性得分、空间位置图等。  
   - 支持 CSV 导出与版本管理，方便科研复现与统计分析。

---

## 三、实验设计

### 3.1 数据集与场景  
- **数据来源**：五张 **犬侵袭性尿路上皮癌（canine invasive urothelial carcinoma）** 全视野切片（WSI）。  
- **分级覆盖**：包括低、中、高三个组织学分级。  
- **放大倍率**：40x。  
- **标注任务类型**：  
  - 有丝分裂像分类（mitotic figures）  
  - 核仁形态（nucleoli）  
  - 核形状（nuclear shape）  
  - 染色质纹理（chromatin pattern）  

### 3.2 Benchmark 与对比方法  
- **对比对象**：传统逐点标注流程（sequential annotation）。  
- **评估指标**：标注时间、分类准确率、标注者间一致性（Cohen’s κ）。  
- **实验配置**：五折交叉验证（5-fold cross-validation）。

---

## 四、资源与算力

- 文中未提供具体算力信息（GPU 型号、数量或训练时长）。  
- 据推测实验基于标准深度学习环境（可能使用单 GPU），但论文未作详细说明。  
- 这一缺失限制了算法在算力资源消耗层面的可对比性分析。

---

## 五、实验数量与充分性

- **实验类型**：  
  1. 基于不同训练样本数量的分类性能评估。  
  2. 标注时间与效率对比实验。  
  3. 标注者间一致性分析（共 11 位专家）。  
  4. 潜空间聚类分布的可视化进展分析。  
- **充分性评估**：  
  - 覆盖了多种形态学特征，具有代表性。  
  - 采用多专家参与与交叉验证，保证一定公平性。  
  - 但样本量仍有限（5 张 WSI），外推性有待验证。

---

## 六、主要结论与发现

- **效率提升**：潜空间聚类引导标注仅需 47 分钟，相比传统 63 分钟减少约 25%（95% CI: 18–32%）。  
- **准确率表现**：  
  - 有丝分裂像：96.3% ± 1.2%  
  - 核仁：98.3% ± 1.4%  
  - 使用仅 215 个样本即可达核仁分类 95.5% ± 1.5%。  
- **一致性分析**：  
  - 染色质 κ = 1.00（完美一致）  
  - 核仁 κ = 0.95（高一致）  
  - 有丝分裂像 κ = 0.58、核形状 κ = 0.36（中等一致）  
- **总体结论**：框架有效减少专家标注负担，并在形态定义清晰的类别上达到专家级准确率。

---

## 七、优点与创新亮点

1. **人机协同模式**：主动学习结合交互界面，显著提升专家标注体验与速度。  
2. **半监督设计**：充分利用未标注数据，减少人工样本需求。  
3. **多模态集成**：同时考虑原始图像、核区域及掩膜，提高特征表达力。  
4. **潜空间可视化可解释性强**：UMAP 嵌入助于直观理解聚类与分类逻辑。  
5. **开源框架**：便于复用、拓展与社区改进。

---

## 八、不足与局限

- **数据规模有限**：仅使用五张犬类病理切片，缺乏对人类组织及更多癌种的验证。  
- **形态学类别不均衡**：部分特征存在标注歧义，有丝分裂像与核形状一致性偏低。  
- **算力与硬件信息缺失**：无法评估方法在不同硬件条件下的可扩展性。  
- **自动化程度有限**：人机迭代仍需专家参与，未完全实现脱离人工的自适应学习。  
- **泛化验证不足**：未给出跨机构、跨染色条件的验证结果。

---

**（完）**
