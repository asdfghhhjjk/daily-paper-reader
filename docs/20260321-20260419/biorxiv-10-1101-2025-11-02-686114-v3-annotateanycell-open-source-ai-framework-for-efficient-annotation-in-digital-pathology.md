---
title: "AnnotateAnyCell: Open-Source AI Framework for Efficient Annotation in Digital Pathology"
title_zh: AnnotateAnyCell：用于数字病理高效标注的开源人工智能框架
authors: "Verma, S., Malusare, A., Wang, M., Wang, L., Mahapatra, A., English, A. L., Cox, A. D., Broman, M., de Brot, S., Burcham, G., Knapp, D., Dhawan, D., Sola, M., Aggarwal, V., Grama, A., Lanman, N. A."
date: 2026-04-13
pdf: "https://www.biorxiv.org/content/10.1101/2025.11.02.686114v3.full.pdf"
tags: ["query:pathseg"]
score: 10.0
evidence: 数字病理中细胞标注与分割的AI框架
tldr: "该研究提出了AnnotateAnyCell开源半监督框架，通过结合主动对比学习与人机反馈，提高数字病理图像中的细胞标注与分类效率，在犬尿路上皮癌样本实验中实现准确率近98%，标注时间减少四分之一，为病理AI诊断提供高效解决方案。"
source: biorxiv
selection_source: fresh_fetch
figures_json: "[{\"url\": \"assets/figures/biorxiv/biorxiv-10-1101-2025-11-02-686114-v3/fig-001.webp\", \"caption\": \"Figure 3: Left panel: Displays annotation summary statistics including counts for different morphological features along with distribution histograms. Center panel: Whole slide image view with cyan markers indicating the spatial locations of all annotated cells across the tissue sample, enabling pathologists to assess spatial distribution patterns and tissue architecture context. Right panel: Individual cell inspection tool showing detailed annotations for the selected cell (Tile 2791) with its specific morphological classifications. The interface includes data export functionality (Download CSV), version information, and the ability to filter and visualize cells based on specific morphological criteria. This output interface enables analysis of annotation results and supports research workflows requiring quantitative cellular phenotype data.\", \"page\": 6, \"index\": 1, \"width\": 968, \"height\": 523}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-1101-2025-11-02-686114-v3/fig-002.webp\", \"caption\": \"Figure 4: A. Sequential snapshots of the learned embedding space progression of annotations (green) within the unlabeled cellular population (blue). B. Classification evaluation of mitotic figures, nucleoli, and nuclear shape across training sizes using 5-fold cross-validation. C. Scaling behaviors highlight fundamental differences in data efficiency.\", \"page\": 7, \"index\": 2, \"width\": 951, \"height\": 952}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-1101-2025-11-02-686114-v3/fig-003.webp\", \"caption\": \"Figure 1: Pre-processing stage: Raw H&E-stained tissue images undergo segmentation using Cellpose models to generate nuclear masks. Each detected nucleus is extracted as three complementary representations: raw image patches, isolated nuclear regions, and semantic masks; Active Learning Loop: Expert pathologists (represented by colored figures) provide initial annotations for nuclear morphology features of neoplastic cells, including mitotic figures, vesicular chromatin, and prominent nucleoli. These labeled samples train a contrastive classifier that generates embeddings and pseudolabels for unlabeled data. A convolutional autoencoder processes the multi-modal inputs (raw, isolated, mask) to learn compact latent representations; Output Interface: The system produces annotated whole slide images with nuclei visualization, quantitative feature distributions, and prediction probabilities for downstream analysis. The iterative process refines the model’s understanding of cellular morphologies through expert feedback. Image Preparation: Left: Representative whole-slide image (WSI). Center: Nuclear segmentation results using pretrained Cellpose models. Right: Binary segmentation mask showing all detected valid cells. (Bottom row) Nine examples of 128×128 pixel cellular tiles illustrating morphological diversity across expert-defined annotation categories. Examples include bizarre mitotic figures showing irregular mitotic configurations, canonical mitotic figures demonstrating typical mitotic chromatin condensation patterns, nucleolar variations (single vs. multiple nucleoli) combined with nuclear shape classifications (circular, oval, irregular), and chromatin texture patterns (vesicular chromatin).\", \"page\": 3, \"index\": 3, \"width\": 968, \"height\": 819}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-1101-2025-11-02-686114-v3/fig-004.webp\", \"caption\": \"Figure 5: A. Illustrates labelling time with and without clustering, along with spatial distributions of agreement (green) and disagreement (brown) reveal localized cell-level ambiguities, with disagreement intensity encoded by saturation. B. Presents the annotation workflow metrics like agreement rates, reliability scores, consistency and spatial coverage scores across 11 annotators. C. Illustrates feature correlation demonstrating nuclear features are largely independent dimensions of morphology, and pairwise disagreement analyses showing some users might disagree more than others.\", \"page\": 8, \"index\": 4, \"width\": 964, \"height\": 539}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-1101-2025-11-02-686114-v3/fig-005.webp\", \"caption\": \"Figure 2: Left panel: Displays workflow guide for pathologists, nuclear size distribution histogram, and nuclear-to-cell ratio distribution with red indicators showing the currently selected cell’s measurements. Center panel: Interactive UMAP embedding visualization, where each point represents a cellular tile extracted from the whole slide image. Cells are color-coded based on annotation status (blue: unlabeled, green: labeled, orange: selected) and naturally cluster based on morphological similarities. Right panel: Shows a high-resolution preview of the selected cell tile (Tile 710) with morphological annotation options including mitotic figures, chromatin patterns, nucleoli characteristics, and nuclear shape classifications. The interface includes progress tracking (300/300 labeled points), version control, and model retraining capabilities (\\\"Update Clusters\\\" button).\", \"page\": 5, \"index\": 5, \"width\": 968, \"height\": 523}]"
motivation: 当前病理全切片图像的人工标注耗时巨大，成为计算病理和临床AI应用的瓶颈。
method: 采用融合Cellpose分割、UMAP可视化和对比学习的半监督人机交互流程。
result: "在犬尿路上皮癌样本上，标注时间减少25%，分类准确率最高达98.3%，一致性良好。"
conclusion: 该框架显著降低了病理图像标注的工作量，并在细胞分类上达到了专家级精度，为资源有限环境下的AI辅助诊断提供了可扩展方案。
---

## 摘要
在计算病理学和临床人工智能部署中，对组织病理学全切片图像进行人工标注仍然是关键瓶颈，规模化标注需要耗费专家大量时间。在此，我们提出了一个开源的半监督框架，结合主动对比学习与人类参与的迭代反馈，实现高效的细胞标注与分类。该流程整合了 Cellpose 分割、基于 UMAP 的潜空间可视化以及基于伪标签传播的对比学习，并在五张犬侵袭性尿路上皮癌全切片图像上进行评估，涵盖低、中、高三个组织学分级、40 倍显微放大。基于潜空间聚类的标注耗时为 47 分钟，而顺序标注耗时为 63 分钟，减少了 25%（95% 置信区间：18–32%）。在 1075 个标注样本上，分裂象分类准确率达到 96.3% ± 1.2%，核仁分类准确率达到 98.3% ± 1.4%；仅使用 215 个样本时，核仁分类准确率仍达到 95.5% ± 1.5%。在染色质（κ = 1.00）和核仁（κ = 0.95）的评注者一致性较高，而在分裂象（κ = 0.58）和核形状（κ = 0.36）上则为中等，反映出这些类别的内在形态模糊性。该框架显著降低了标注负担，同时在明确的形态特征上实现了专家级的准确度，为资源受限的病理环境中迈向人工智能辅助诊断提供了可扩展的路径。

## 速览
**TLDR**：该研究提出了一个开源的半监督框架AnnotateAnyCell，通过结合主动对比学习和人机交互反馈实现数字病理图像中细胞的高效注释与分类，在降低专家标注负担的同时保持高准确率。 \
**Motivation**：手工标注病理全幻灯片图像耗时且限制计算病理和临床AI的规模化应用。 \
**Method**：采用Cellpose分割、UMAP潜在空间可视化以及对比学习结合伪标签传播，并利用人机互动的迭代标注流程。 \
**Result**：框架在犬侵袭性尿路上皮癌全幻灯片图像上验证，注释时间减少25%，细胞分类准确率超过96%。 \
**Conclusion**：该框架能显著减少病理图像标注时间并保持专家级准确性，为资源受限环境下的AI辅助诊断提供可行方案。

---

## Abstract
AO_SCPLOWBSTRACTC_SCPLOWManual annotation of histopathological whole slide images remains a critical bottleneck for computational pathology and clinical AI deployment, requiring prohibitive expert time at scale. Here we present an open-source semi-supervised framework combining active contrastive learning with iterative human-in-the-loop feedback for efficient cellular annotation and classification. The pipeline integrates Cellpose segmentation, UMAP-based latent space visualization, and contrastive learning with pseudolabel propagation, evaluated on five whole slide images of canine invasive urothelial carcinoma across low, intermediate, and high histological grades at 40x magnification. Latent space clustering-guided annotation required 47 minutes compared to 63 minutes for sequential annotation, a 25% reduction (95% CI 18-32%). Classification accuracy reached 96.3% {+/-} 1.2% for mitotic figures and 98.3% {+/-} 1.4% for nucleoli using 1,075 labeled samples, with nucleoli classification achieving 95.5% {+/-} 1.5% accuracy from only 215 samples. Inter-annotator agreement was high for chromatin ({kappa} = 1.00) and nucleoli ({kappa} = 0.95) but moderate for mitotic figures ({kappa} = 0.58) and nuclear shape ({kappa} = 0.36), reflecting intrinsic morphological ambiguity in these categories. This framework substantially reduces annotation burden while achieving expert-level accuracy for well-defined morphological features, providing a scalable path toward AI-assisted diagnostics in resource-constrained pathology settings.

---

## 论文详细总结（自动生成）

# AnnotateAnyCell：用于数字病理高效标注的开源AI框架 — 论文总结

---

## 一、研究问题与总体意义

- **核心问题**：在数字病理领域，病理学家仍需手工标注全切片图像（Whole Slide Images, WSI），这是计算病理学与临床AI模型部署的主要瓶颈。全切片图像通常包含数十万细胞、数GB容量，使得人工标注极度耗时。  
- **研究动机**：降低专家标注成本、提高标注效率，同时维持高准确度和临床信任度。  
- **目标**：开发一种支持 **半监督学习** 与 **主动学习（active learning）** 的开源框架，让病理学家在交互嵌入空间中快速进行细胞标注，实现人机协作的高效工作流，帮助病理AI在真实临床中落地。

---

## 二、方法论与技术体系

### 1. 框架总体思路  
提出一个名为 **AnnotateAnyCell** 的开源半监督主动学习框架，包括四个核心阶段：

1. **细胞级预处理与分割**：利用预训练的 **Cellpose3 / cyto3** 模型，对H&E切片执行细胞/核分割。
2. **UMAP空间可视化**：将提取的128×128细胞图块映射到二维嵌入空间，使形态相似的细胞自动聚类。
3. **对比学习与伪标签生成**：
   - 使用对比学习（InfoNCE损失）结合分类损失进行联合优化；
   - 生成高置信度伪标签并平衡各类别样本。
4. **迭代人机环路**：病理专家在UMAP空间中标注代表样本，模型利用伪标签和主动采样机制更新嵌入表示，持续优化分类性能。

### 2. 关键技术细节  

- **对比学习目标**：
  \[
  L_{\text{InfoNCE}} = -\log \frac{\exp(sim(q,k^+)/\tau)}{\sum_i \exp(sim(q,k_i)/\tau)}
  \]
  其中 sim 表示余弦相似度，τ为温度参数。

- **联合损失函数**：
  \[
  L_{\text{total}} = \alpha L_{CE} + \beta L_{\text{InfoNCE}}
  \]

- **伪标签生成**：按类别选择最高置信度 Top-N 样本（如 N=20），确保类别平衡。

- **多模态自编码器（VAE）**：同时编码原始图像、核区块和语义掩膜，生成256维潜表示，用于UMAP可视化与聚类。

- **主动学习循环**：基于不确定性采样与多样性促进策略选出最具信息量样本，再交由专家确认，提高数据利用效率。

---

## 三、实验设计

- **数据来源**：犬侵袭性尿路上皮癌（canine invasive urothelial carcinoma, IncUC）样本，来自普渡大学兽医教学医院。  
  - 每张切片尺寸约80,000×100,000像素，40×物镜（0.25 μm/pixel）。  
  - 选取5张代表性病理切片，包含不同分级、核特征与形态多样性。  
- **标注类别**：包括分裂象、核仁数量/显著性、染色质类型与核形状等四类细胞形态学特征。
- **参与专家**：11位病理学家及住院医师参与标注实验，每人标注300个细胞。
- **对照条件**：
  - 对比「顺序标注」与「基于潜空间聚类的标注」两种工作流效率。
  - 评估模型性能与人工标注一致性（Cohen’s κ 系数）。

---

## 四、资源与计算成本

- 论文**未明确指出GPU型号、批量大小或训练时长**等算力参数。  
- 根据框架描述，系统需执行：
  - Cellpose分割（基于GPU）；
  - 卷积分类器与自编码器训练；
  - UMAP降维与交互式可视化；
  推测使用中等规模计算资源即可运行（实验未专注于大规模训练，而强调前端交互效率）。

---

## 五、实验数量与充分性

- **实验层次**：
  1. 性能评估（分类准确率随样本量变化、5折交叉验证）；
  2. 时间效率比较（顺序 vs. 聚类标注）；
  3. 特征间相关分析；
  4. 多专家一致性评估；
  5. 框架在人机循环下的迭代可视化表现。  
- **充分性**：
  - 覆盖了算法性能、人工效率和一致性验证三个维度；
  - 虽然数据集仅5张WSI，但分析细致、指标完备；
  - 缺少跨机构或多肿瘤类型的泛化实验。

---

## 六、主要结果与结论

- **标注效率**：
  - 潜空间聚类标注平均耗时47分钟/300细胞；
  - 顺序标注耗时63分钟，节省25%（95% CI: 18–32%）。  
- **分类性能（1075样本）**：
  - 核仁分类准确率 98.3% ± 1.4%；  
  - 分裂象 96.3% ± 1.2%；  
  - 核形状 59.5% ± 2.1%。  
- **小样本性能**：
  - 核仁在仅215样本下已达 95.5% ± 1.5%。  
- **一致性分析**：
  - 染色质与核仁分类一致性极高（κ = 1.00, 0.95）；  
  - 分裂象与核形状中等一致(κ = 0.58, 0.36)；
  - 表明部分形态特征存在主观模糊性。  
- **总体结论**：
  该框架在保持专家级准确度的同时，显著降低了标注时间和人工负担，为资源受限机构提供可扩展的AI标注解决方案。

---

## 七、主要优点

- **方法创新**：首次将对比学习、伪标签传播与UMAP交互式可视化融合于单一框架。  
- **高效率**：主动学习策略有效减少约1/4的标注时间。  
- **开源开放**：完整工具链（Cellpose→UMAP→Web界面）将公开访问。  
- **人机结合**：真正实现迭代“human-in-the-loop”，增强医疗信任。  
- **小样本高精度**：少量标注即可获得高准确率，适合数据稀缺的病理场景。

---

## 八、局限与不足

- **数据范围有限**：仅在犬尿路上皮癌上验证，缺乏跨组织或人类数据测试。  
- **算力与可复现性信息缺失**：未说明训练硬件、时长和消融细节。  
- **形状分类表现较低**：核形状定义主观性强，算法难以达成高一致性。  
- **泛化能力待测**：尚未评估在不同实验室、扫描仪或染色条件下的鲁棒性。  
- **未比较其他主动学习框架（如 Quick Annotator / PatchSorter）的系统对照实验**。  

---

（完）
