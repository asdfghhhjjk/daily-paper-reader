---
title: Adaptive Integration of Heterogeneous Foundation Models to Find Histologically Predictable Genes in Breast Cancer
title_zh: 异质基础模型的自适应整合以发现乳腺癌中可通过组织学预测的基因
authors: "Nguyen, H., Li, C., Peng, C., Simpson, P., Ye, N., Nguyen, Q."
date: 2026-04-08
pdf: "https://www.biorxiv.org/content/10.64898/2026.04.05.716435v1.full.pdf"
tags: ["query:cellrep"]
score: 9.0
evidence: 整合基础模型以获取组织病理学中的形态学表征
tldr: 本研究提出一种自适应整合异质基座模型的方法，用于从乳腺癌组织病理图像中预测可由组织学解释的基因。通过结合不同基座模型的特征并利用空间转录组数据，该方法显著提升基因预测的准确性与可解释性。
source: biorxiv
selection_source: fresh_fetch
figures_json: "[{\"url\": \"assets/figures/biorxiv/biorxiv-10-64898-2026-04-05-716435-v1/fig-001.webp\", \"caption\": \"Fig. 2: Per-gene PCC distribution across nine FMs and our adaptive ensemble on the BRCA-Xenium dataset. Mean ± standard deviation is reported above each box (for the top 50 highly variable genes of the IDC dataset and all xenium v1 genes panel of the BRCA-Xenium dataset). The dashed blue line marks the average PCC of single encoders. Best is bold, second best is underlined.\", \"page\": 6, \"index\": 1, \"width\": 723, \"height\": 304}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-64898-2026-04-05-716435-v1/fig-002.webp\", \"caption\": \"Fig. 1: Overview of the proposed framework. ST data on WSI are split into pairs of image tiles and gene expression labels. The model integrates multiple FM embeddings and predicts gene expression at each spatial location by a gating function that computes spot- and gene-aware weighting.\", \"page\": 2, \"index\": 2, \"width\": 646, \"height\": 235}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-64898-2026-04-05-716435-v1/fig-003.webp\", \"caption\": \"Fig. 3: Percentage improvement in PCC over the ResNet50 baseline for clinically relevant gene markers across FMs and our ensemble, on the BRCA-Xenium dataset (A) and IDC dataset (B). Subtypes (Luminal, Basal, Proliferation, HER2 and clinical markers) are indicated by the colored legend beneath the heatmap, and black vertical lines denote boundaries between subtype groups. Colour intensity follows a log scale. Improvements are computed relative to ResNet50: positive values indicate performance gains, negative values indicate regression.\", \"page\": 7, \"index\": 3, \"width\": 650, \"height\": 265}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-64898-2026-04-05-716435-v1/fig-004.webp\", \"caption\": \"Table 1: FMs evaluated in this study. All models are frozen encoders pre-trained on histopathology images using self-supervised learning.\", \"page\": 3, \"index\": 4, \"width\": 725, \"height\": 189}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-64898-2026-04-05-716435-v1/fig-005.webp\", \"caption\": \"Fig. 4: Spatial gene expression prediction maps for ERBB2 (BRCA-Xenium, a single cell ST dataset) and ESR1 (IDC, a lower resolution dataset). From left to right: H&E tissue, ground truth, and predictions from Virchow2, GPFM, h0_mini, and our ensemble.\", \"page\": 8, \"index\": 5, \"width\": 652, \"height\": 256}]"
motivation: 不同基座模型在病理图像任务中表现差异显著，迫切需要整合互补优势以提高模型的泛化性。
method: 将多种基座模型的嵌入映射为基因预测，并通过轻量加权网络自适应聚合结果获得统一输出。
result: 在多组空间转录组数据中，该方法在预测乳腺癌相关基因方面超越单一模型和传统集成方法。
conclusion: 该框架为多基座模型的融合提供了有效途径，能提升乳腺癌病理图像的基因预测性能与解释能力。
---

## 摘要
计算病理学的基础模型已迅速成为从组织病理学图像中提取丰富生物学和形态学表征的强大工具。然而，模型架构、预训练数据和优化目标的差异往往导致性能依赖于具体任务，而非具有普遍的泛化能力。因此，开发有效的策略以整合这些模型的互补优势，对于充分发挥基础模型在稳健组织病理分析中的潜力至关重要。同时，空间转录组学等最新突破为从同一患者样本中整合遗传信息与组织病理信息提供了前所未有的机会，从而最大化分子病理学与解剖病理学的洞察力。具体而言，每个模型的嵌入首先通过专用的预测头映射到基因层面的预测，从而实现模型特征的专属利用。接着，一个轻量级的加权网络自适应地汇聚这些预测，生成在基因及空间位置层面上统一且稳健的输出。在多个空间转录组数据集上，我们的方法在性能上始终优于单个基础模型和传统集成方法。在乳腺癌研究中，我们观察到针对临床相关的 PAM50 亚型标志物及药物靶基因的预测准确性显著提升。此外，所提出的框架通过揭示模型在基因层面的特定贡献与专长性，增强了可解释性。总体而言，我们的工作提出了一种有效的多基础模型整合方案，用于提升组织病理图像的遗传分析能力。

## Abstract
Foundation models for computational pathology have rapidly emerged as powerful tools for extracting rich biological and morphological representations from histopathology images. However, variations in model architecture, pre-training data, and optimization objectives often lead to task-dependent performance, rather than universal generalization. As a result, effective strategies for integrating their complementary strengths are essential to fully realize the potential of foundation models for robust histopathology analysis. Meanwhile, recent breakthroughs such as spatial transcriptomics provide an unprecedented opportunity to integrate genetic and histopathology information from the same patient sample, thereby maximizing both molecular and anatomical pathology insights. Specifically, each models embedding is first mapped to gene-level predictions via a dedicated prediction head, enabling model-specific feature utilization. A lightweight weighting network then adaptively aggregates these predictions to produce a unified and robust output at gene and spatial location levels. Across multiple spatial transcriptomics datasets, our approach consistently outperforms both individual foundation models and classical ensembling methods. Focusing on breast cancer, we observe substantial gains in prediction accuracy for clinically relevant PAM50 subtype markers and drug-target genes. Moreover, the proposed framework improves interpretability by revealing model-specific contributions and specialization at the gene level. Overall, our work presents an effective solution to integrating multiple foundation models for enhancing the genetic analyses of histopathology images.

---

## 论文详细总结（自动生成）

# 论文总结：异质基础模型的自适应整合以发现乳腺癌中可通过组织学预测的基因

---

## 一、核心问题与研究背景

- **研究动机**：  
  近年来，计算病理学（Computational Pathology, CPath）中的基础模型（Foundation Models, FMs）快速发展，能从组织切片图像中提取丰富的形态学特征。然而，不同模型在架构、预训练数据、优化策略上存在差异，导致其在特定任务上的表现差异显著，缺乏**普适性的泛化能力**。

- **核心问题**：  
  - 单一基础模型对复杂病理任务（如空间基因表达预测）的适应性有限。  
  - 不同模型可能捕获到**互补的生物学信号**，但尚缺乏有效整合它们的机制。  
  - 传统集成方法只采用**全局融合表示（global fusion）**，不能针对**基因特异性与空间异质性**进行自适应优化。

- **研究目标**：  
  作者提出一种新的**自适应多模型融合框架**，以整合多种异质的病理基础模型，并针对不同基因与空间位置动态选择模型贡献，从而提升乳腺癌组织学图像的基因表达预测精度与可解释性。

---

## 二、方法论：核心思想与关键技术机制

### 2.1 总体思路

- 将9个预训练的病理基础模型的嵌入特征输入同一任务框架；
- 由**各自的预测头（prediction head）**映射到基因层面的表达预测；
- 通过一个**轻量级自适应加权网络（gating network）**，在不同基因与空间位置尺度上动态聚合模型输出，从而实现**按基因和空间位置自适应集成**。

### 2.2 关键结构模块

- **输入与特征提取**：  
  每个空间转录组（ST）位置（spot）提取一个 224×224 的 H&E 图像块，并经 9 个预训练 FM（包括 ResNet、ViT 等结构）编码为特征嵌入。

- **模型级预测头（per-model prediction head）**：  
  每个模型的嵌入 Ei ∈ RN×di 输入一个3层MLP映射到 G 个基因预测向量：  
  \[
  \hat{Y_i} = \omega_i(E_i)
  \]

- **自适应加权融合（Adaptive Gating Ensemble）**：  
  将所有模型嵌入拼接后经两层MLP形成加权矩阵 W (维度 N×G×M)：  
  \[
  \tilde{W}_{n,g,i} = \frac{\exp(W_{logits,n,g,i})}{\sum_{j=1}^M \exp(W_{logits,n,g,j})}
  \]  
  最终预测为：
  \[
  \hat{Y}_{ens,n,g} = \sum_i \tilde{W}_{n,g,i} \hat{Y}_{i,n,g}
  \]
  即，在每个空间点、每个基因上，动态选择最优模型加权。

- **训练目标**：  
  使用均方误差（MSE）损失函数：
  \[
  L_{mse} = \frac{1}{NG} \| \hat{Y}_{ens} - Y \|_F^2
  \]
  采用 AdamW 优化器、学习率 1e-4、512 批次大小、训练300个epoch。

---

## 三、实验设计

### 3.1 数据集与任务场景

- **主要数据集**：
  - **BRCA-Xenium dataset**（乳腺癌单细胞空间转录组数据，5个样本）
  - **HEST-IDC dataset**（乳腺导管癌空间转录组数据子集，4个样本）
- 每个数据集包含配准的 **H&E 图像** 与 **空间基因表达矩阵**，实现图像到基因表达的回归预测。

### 3.2 模型对比与基线

- 对比的 9 个基础模型（见 Table 1）：
  - ResNet50、UNI、CONCH、GigaPath、Virchow2、CHIEF、GPFM、H0_mini、Hibou-L  
- **传统集成与融合方法**：
  - 特征拼接（Concatenation）  
  - 统一降维投影（Unified Projection）  
  - 交叉注意力（Cross-Attention）  
  - 门控注意力（Gate-Attention）

- **评价指标**：  
  - 皮尔森相关系数（PCC）按基因计算；
  - 采用 HEST-Bench 协议（特征提取、PCA降维、线性回归预测、k折交叉验证）。

---

## 四、资源与算力

- 文中提及训练使用**GPU 加速**、批量大小512，但**未明确说明GPU型号或数量**。  
- 未给出训练总时长，仅说明训练300个epoch。  
- 可推测实验在主流研究级GPU（如A100/V100）上进行，但原文未明示。

---

## 五、实验数量与充分性

- **实验覆盖面广**：
  - 两个独立数据集（BRCA-Xenium与IDC）
  - 覆盖9个基础模型与5种融合策略比较
  - 针对临床标志基因（PAM50亚型基因、免疫治疗靶点）做细粒度分析
  - 消融实验：比较自适应加权与多种经典融合方法

- **实验公平性**：
  - 所有单模型使用冻结编码器，避免因训练差异造成偏差；
  - 统一数据预处理与评估流程，遵循公共 benchmark（HEST-Bench）；
  - 表明结果具有较高可复现性与可比性。

---

## 六、主要结论与发现

- 自适应集成方法在全部实验中均显著**优于单一基础模型和传统集成策略**。  
- **总体性能提升**：
  - BRCA-Xenium 数据集：PCC 从 Virchow2 的 0.552 提高到 0.567。  
  - IDC 数据集：PCC 从 0.597 提高到 0.615。  
  - 相比 ResNet50 基线提升约 22%。  
- **临床相关基因显著受益**：
  - Luminal 基因 SFRP1 改进 70%~150%。  
  - Basal 基因 EGFR 提升达 774%。  
  - 免疫基因 CD274 / PDCD1 预测显著改善。
- **解释性结果**：  
  - 加权网络显示不同模型在不同基因上具特异优势，揭示可能的**形态-分子关联机制**。

---

## 七、方法优点与创新亮点

- **动态自适应加权机制**：打破单一全局融合假设，实现基因与空间位置级的动态组合。  
- **轻量框架结构**：可在冻结多模型编码器下训练少量参数，计算开销相对可控。  
- **强解释性**：可追溯各模型在特定基因预测中的贡献比例。  
- **高泛化性**：在两个来源不同的乳腺癌空间转录组数据上均表现优越。  
- **严格基准配置**：使用公认 benchmark（HEST-Bench）保证结果可复现性。

---

## 八、不足与局限

- **算力细节缺失**：论文未披露GPU配置与训练时间，难以评估计算成本。  
- **数据类型局限**：仅限于乳腺癌；对其他肿瘤类型或非癌组织的泛化能力尚未验证。  
- **模型解释尚属定性**：虽可观察权重，但缺乏定量因果分析。  
- **缺乏不确定性评估**：未来计划中提到可结合不确定性权重选择以增强稳健性。  
- **部分性能提升幅度有限**：在部分基因上增益较小，说明仍存在模型协同不充分的问题。

---

**（完）**
