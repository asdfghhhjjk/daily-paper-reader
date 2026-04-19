---
title: Adaptive Integration of Heterogeneous Foundation Models to Find Histologically Predictable Genes in Breast Cancer
title_zh: 异质基础模型的自适应整合以发现乳腺癌中可由组织学预测的基因
authors: "Nguyen, H., Li, C., Peng, C., Simpson, P., Ye, N., Nguyen, Q."
date: 2026-04-08
pdf: "https://www.biorxiv.org/content/10.64898/2026.04.05.716435v1.full.pdf"
tags: ["query:cellrep"]
score: 9.0
evidence: 计算病理学基础模型提取丰富的生物学和形态学表征
tldr: 本文提出一种自适应整合异质性基础模型的框架，用于在乳腺癌组织病理图像中预测基因表达。通过将各模型嵌入映射到基因层预测并用加权网络融合输出，该方法在空间转录组数据上显著提升了临床相关基因及PAM50亚型标志物的预测准确率，同时增强了模型的可解释性。
source: biorxiv
selection_source: fresh_fetch
figures_json: "[{\"url\": \"assets/figures/biorxiv/biorxiv-10-64898-2026-04-05-716435-v1/fig-001.webp\", \"caption\": \"Fig. 2: Per-gene PCC distribution across nine FMs and our adaptive ensemble on the BRCA-Xenium dataset. Mean ± standard deviation is reported above each box (for the top 50 highly variable genes of the IDC dataset and all xenium v1 genes panel of the BRCA-Xenium dataset). The dashed blue line marks the average PCC of single encoders. Best is bold, second best is underlined.\", \"page\": 6, \"index\": 1, \"width\": 723, \"height\": 304}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-64898-2026-04-05-716435-v1/fig-002.webp\", \"caption\": \"Fig. 1: Overview of the proposed framework. ST data on WSI are split into pairs of image tiles and gene expression labels. The model integrates multiple FM embeddings and predicts gene expression at each spatial location by a gating function that computes spot- and gene-aware weighting.\", \"page\": 2, \"index\": 2, \"width\": 646, \"height\": 235}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-64898-2026-04-05-716435-v1/fig-003.webp\", \"caption\": \"Fig. 3: Percentage improvement in PCC over the ResNet50 baseline for clinically relevant gene markers across FMs and our ensemble, on the BRCA-Xenium dataset (A) and IDC dataset (B). Subtypes (Luminal, Basal, Proliferation, HER2 and clinical markers) are indicated by the colored legend beneath the heatmap, and black vertical lines denote boundaries between subtype groups. Colour intensity follows a log scale. Improvements are computed relative to ResNet50: positive values indicate performance gains, negative values indicate regression.\", \"page\": 7, \"index\": 3, \"width\": 650, \"height\": 265}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-64898-2026-04-05-716435-v1/fig-004.webp\", \"caption\": \"Table 1: FMs evaluated in this study. All models are frozen encoders pre-trained on histopathology images using self-supervised learning.\", \"page\": 3, \"index\": 4, \"width\": 725, \"height\": 189}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-64898-2026-04-05-716435-v1/fig-005.webp\", \"caption\": \"Fig. 4: Spatial gene expression prediction maps for ERBB2 (BRCA-Xenium, a single cell ST dataset) and ESR1 (IDC, a lower resolution dataset). From left to right: H&E tissue, ground truth, and predictions from Virchow2, GPFM, h0_mini, and our ensemble.\", \"page\": 8, \"index\": 5, \"width\": 652, \"height\": 256}]"
motivation: 不同基础模型在组织病理学任务中的性能差异需要有效融合策略以实现稳健分析。
method: 利用各基础模型的特征通过专属预测头映射至基因层，并用轻量加权网络自适应融合输出。
result: 在多组空间转录组数据中，该方法在基因预测准确率及模型解释性上均优于单模型和传统集成方法。
conclusion: 该研究提供了一个高效框架，可整合多种基础模型以增强组织病理学图像的基因分析和可解释性。
---

## 摘要
用于计算病理学的基础模型迅速成为从组织病理学图像中提取丰富生物学与形态学表征的强大工具。然而，模型架构、预训练数据和优化目标的差异常常导致任务相关而非普适的泛化性能。因此，开发有效的方法以整合这些模型的互补优势，对于充分发挥基础模型在稳健组织病理分析中的潜能至关重要。与此同时，空间转录组学等近期突破为整合同一患者样本的基因和组织病理信息提供了前所未有的机遇，从而最大化分子与解剖病理学洞察。具体而言，每个模型的嵌入首先通过专用预测头映射至基因层面的预测，以实现模型特定特征的利用。然后，一个轻量级加权网络自适应地聚合这些预测，生成在基因和空间位置层面统一且稳健的输出。在多个空间转录组学数据集上，我们的方法稳定地优于单一基础模型和传统集成方法。以乳腺癌为重点，我们观察到在临床相关的 PAM50 亚型标志物和药物靶基因预测准确率上显著提升。此外，该框架提升了可解释性，揭示了模型在基因层面的特定贡献与专长。总体而言，我们的工作提出了一种有效的解决方案，用以整合多种基础模型，从而增强组织病理图像的基因分析能力。

## Abstract
Foundation models for computational pathology have rapidly emerged as powerful tools for extracting rich biological and morphological representations from histopathology images. However, variations in model architecture, pre-training data, and optimization objectives often lead to task-dependent performance, rather than universal generalization. As a result, effective strategies for integrating their complementary strengths are essential to fully realize the potential of foundation models for robust histopathology analysis. Meanwhile, recent breakthroughs such as spatial transcriptomics provide an unprecedented opportunity to integrate genetic and histopathology information from the same patient sample, thereby maximizing both molecular and anatomical pathology insights. Specifically, each models embedding is first mapped to gene-level predictions via a dedicated prediction head, enabling model-specific feature utilization. A lightweight weighting network then adaptively aggregates these predictions to produce a unified and robust output at gene and spatial location levels. Across multiple spatial transcriptomics datasets, our approach consistently outperforms both individual foundation models and classical ensembling methods. Focusing on breast cancer, we observe substantial gains in prediction accuracy for clinically relevant PAM50 subtype markers and drug-target genes. Moreover, the proposed framework improves interpretability by revealing model-specific contributions and specialization at the gene level. Overall, our work presents an effective solution to integrating multiple foundation models for enhancing the genetic analyses of histopathology images.

---

## 论文详细总结（自动生成）

# 异质基础模型的自适应整合以发现乳腺癌中可由组织学预测的基因 — 论文总结

---

## 一、核心问题与研究背景

- **研究动机**：  
  计算病理学中的**基础模型（Foundation Models, FMs）**能够从组织病理图像中提取丰富的形态学与生物学特征。然而，不同模型在结构设计、预训练数据和优化目标上存在显著差异，导致在特定任务中表现不一致，难以实现通用泛化。
- **问题定义**：  
  当前多数方法仅依赖单个基础模型来预测基因表达，但不同模型往往捕获互补的信息。单模型方法忽略了这种异质性，使得预测性能有限。
- **研究目标**：  
  提出一种**自适应整合框架**，在空间转录组学（Spatial Transcriptomics，ST）场景中融合多个病理基础模型，提升从组织病理图像预测基因表达的精度与稳健性，重点聚焦乳腺癌相关基因和临床分型。

---

## 二、方法论：核心思想与技术细节

### 1. 总体框架
- 论文提出了一个**基于自适应加权的模型融合框架**，旨在将多个异质病理基础模型整合，用于**空间基因表达预测任务**。
- 方法包含两个关键组件：
  1. **模型专属预测头（Prediction Head）**：每个基础模型的嵌入通过独立的轻量 MLP 映射到基因预测空间；
  2. **自适应加权网络（Gating Network）**：根据每个空间位置及基因类别，动态计算各模型的贡献权重。

### 2. 算法流程（概念化说明）
- **输入**：H&E 组织切片，与其对应的 ST 空间坐标及基因表达矩阵。  
- **过程**：
  1. 从每个空间位置提取 224×224 像素的组织图像块；
  2. 通过 9 个预训练基础模型分别提取嵌入向量；
  3. 对每个模型嵌入输入至自身的 MLP 预测头，生成基因预测值；
  4. 将所有模型的嵌入拼接，通过两层 MLP 输出一个 **spot-及 gene-aware 权重矩阵**；
  5. 按权重融合各模型预测，得到最终的基因表达预测。
- **训练目标**：
  使用均方误差 (MSE) 损失在样本层面优化预测结果，训练参数包括所有预测头和 gating 网络。  
  优化器为 **AdamW**，学习率 1×10⁻⁴，批次大小 512，训练 300 轮。

---

## 三、实验设计

### 1. 数据集与场景
- **BRCA-Xenium**：空间转录组单细胞级乳腺癌样本（5 个样本）。  
- **IDC**：HEST 数据集的侵袭性导管癌（Invasive Ductal Carcinoma）子集（4 个样本）。
- 均为乳腺癌病理图像，任务为**预测各空间位置上基因表达矩阵**。

### 2. Benchmark 协议
- 采用 HEST-Bench 评估流程：
  1. 多模型特征提取；
  2. PCA 降维至 256；
  3. Ridge 回归预测基因；
  4. k-fold 交叉验证计算平均与标准差。
- 主评价指标为 **Pearson 相关系数（PCC）**。

### 3. 对比方法
- 单模型基线：ResNet50、UNI、CONCH、GigaPath、Virchow2、CHIEF、GPFM、Hibou-L、h0-mini。
- 集成基线：交叉注意力（Cross-Att）、门控注意力（Gate-Att）、简单拼接（Concat）、统一投影（Unified-Proj）。

---

## 四、资源与算力

- 论文仅提到训练使用 **GPU、batch size = 512**；未具体说明 GPU 型号和数量。
- 训练周期为 **300 epochs**。
- 未报告总算力、显存占用或训练时间。

---

## 五、实验数量与充分性

- **主要实验**：两个独立数据集（BRCA-Xenium 与 IDC）；
- **定量分析**：每基因 PCC 分布、全局平均对比；
- **特定分析**：PAM50 分型基因与免疫治疗靶点的细致评估；
- **额外实验**：4 种融合策略消融测试。
- **充分性评价**：
  - 实验覆盖多个模型和多种融合方案，验证了框架的通用性；
  - 数据样本仍有限（共 9 个乳腺癌样本），但基因维度较高，结论具有一定统计可靠性；
  - 对随机性与参数敏感性未有深入讨论。

---

## 六、主要结论与发现

- 自适应整合方法在两个数据集上均显著提升：
  - BRCA-Xenium：平均 PCC **0.567 ± 0.193**（优于 Virchow2 的 0.552 ± 0.198）；
  - IDC：平均 PCC **0.615 ± 0.176**（较 ResNet50 提升约 22.2%）。
- 在乳腺癌临床相关基因方面显著改善：
  - Luminal 标志物（如 SFRP1）提升 70%–150%；
  - Basal 类型基因（EGFR、KRT5、KRT14）提升最高达 774%；
  - 免疫标志物（CD274、PDCD1）均有正向改进。
- 自适应权重机制揭示了各模型在不同基因上的专长，增强了**模型可解释性与生物学关联性**。

---

## 七、优点与亮点

- **创新性集成设计**：首次在空间转录组预测中实现模型级自适应选择（spot & gene aware gating）。
- **细粒度可解释性**：可观察各基础模型在不同基因的特定贡献，有助于揭示形态与分子关系。
- **性能稳健**：在多个数据集、不同分型基因上均显著超越传统平均或注意力集成。
- **轻量实现**：预测头和加权网络参数规模小，对现有基础模型兼容度高。

---

## 八、不足与局限

- **数据覆盖有限**：仅使用乳腺癌两类数据集，缺乏跨癌种验证。
- **算力细节缺失**：未报告 GPU 型号、总训练时间，难以评估资源效率。
- **样本规模偏小**：空间转录组样本数量较少，泛化能力需更多验证。
- **模型冻结假设**：所有基础模型均冻结，仅优化预测层，可能限制更深的特征适配。
- **缺乏输出不确定性分析**：未探讨预测的置信度和生物学噪声对结果影响。

---

（完）
