---
title: MICRON learns outcome-associated representations of spatial immune microenvironments
title_zh: MICRON 学习空间免疫微环境的结局相关表征
authors: "Chen, C.-J., George, B., Dhawka, L., Evangelista, B., Stanley, N."
date: 2026-04-16
pdf: "https://www.biorxiv.org/content/10.64898/2026.04.14.718488v1.full.pdf"
tags: ["query:cellrep"]
score: 8.0
evidence: 用于空间免疫微环境结果关联表征的多实例学习
tldr: 本研究提出了MICRON，一种基于多实例学习的无分割自动化分析工具，用于从空间成像蛋白质组学数据中识别与疾病预后相关的免疫微环境。该方法无需细胞分割即可学习数据表示，从而提升预后与诊断预测的准确性，并在脑癌案例中揭示了影响生存的关键免疫结构。
source: biorxiv
selection_source: fresh_fetch
figures_json: "[{\"url\": \"assets/figures/biorxiv/biorxiv-10-64898-2026-04-14-718488-v1/fig-001.webp\", \"caption\": \"Fig. 1 MICRON learns outcome-associated spatial immune signatures and microenvironments. (a) Schematic of the multiple-instance learning framework used to train MICRON to predict outcomes from spatial imaging proteomics modalities. During training, square regions (instances) are cropped from the input image and processed by a fully convolutional network (FCN) to generate instance-level class predictions. The distribution of instance-level outcome probability predictions are summarized via a quantile-based featurization per each outcome class. The quantile vectors across classes are concatenated and input to a softmax function to predict an outcome probability for each sample. The model parameters, including both the FCN and quantile aggregation module, are optimized via the cross-entropy loss. (b) Sample representations are computed for new, unseen samples by using the trained MICRON model to generate embedding vectors for each image crop. (c) Crops across testing images are prioritized via SHAP values and identify both high-impact and outcomeassociated image crops, corresponding to key immune microenvironments. (d) For predicting sample outcomes, MICRON can specify two types of immune features, including (i) (multiple-instance (MI) features), obtained by pooling learned instance embedding dimensions across all cells and (ii) (frequency features), obtained by clustering instance embedding vectors and counting the proportion of instances assigned to each cluster per sample. Featurizations are used for downstream prediction tasks, such as, survival analysis. (e) Immune signatures obtained through MICRON were evaluated for their accuracy in predicting binary clinical outcomes on three publicly available clinical IMC datasets. The number of channels measured in the IMC experiments are denoted as well as the number of donors in each outcome class. (f) The prediction accuracy of MICRON is compared to related methods for predicting a binary clinical outcome across the three datasets (area under the ROC curve (AUROC)). (g) In the Karimi dataset, MICRON identified more frequent co-occurrences between astrocytes, NK cells, and M1-like MDMs in glioblastoma patients than was observed in patients with metastasized brain tumors. Bold green lines indicate the most frequently co-occurring cell-type pairs across topmost-informative image crops. Nodes circled in gold represent the set of cell-types that were most ubiquitously identified across immune microenvironments.\", \"page\": 17, \"index\": 1, \"width\": 738, \"height\": 857}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-64898-2026-04-14-718488-v1/fig-002.webp\", \"caption\": \"Fig. 2 Microenvironments uncovered with MICRON prioritized differential cell-cell communication mechanisms. (a) Representative brain metastasis (BrM) and glioblastoma (GBM) sample images colored according to expression of key markers for phenotyping macrophages (CD68), astrocytes (GFAP), and NK cells (CD94 and CD16). Superpixel importance scores show image regions prioritized by MICRON. Cells in high-scoring regions were segmented and phenotyped to reveal prominent microenvironments in the BrM and GBM classes. (b) Overview of how MICRON can be applied to perform survival analysis in patients from the Karimi study. For a set of held out patients, MICRON was used to identify the top 20 most outcome-associated superpixels in each image (denoted as V in superpixel map). (c) Image crops were clustered with k-means (K = 10) using MICRON-computed embeddings. The UMAP (top) shows cells colored according to the embedding clusters. Patients were stratified into high and low frequency groups for each cluster. The UMAP (bottom) colors cells based on the risk of death and identifies clusters 4 and 9 as being survival-associated and survival unassociated, respectively. (d) Cluster 4 was observed to be strongly associated with survival and highlights strong spatial co-occurrence between astrocytes, NK cells, and M1-like MDMs in glioblastoma. (e) Cell-cell communication patterns via ligand/receptor signaling were investigated in an independent cohort of glioblastoma patients profiled with single-cell RNA-seq (Ruiz-Moreno study [22]). Dotplots visualize top genes with enrichment patterns according to specificity rank (indicated by dot size and color) specifically between astrocytes, macrophages, and NK cells. (f)A graph was constructed between cells where the edges are weighted by the specificity rank between a pair of cell-types. The graph reveals prominent cross-talk between astrocytes and NK cells, supporting the spatial signature prioritized by MICRON in the Karimi study. (g) scGPT was used to featurize samples in the Ruiz-Moreno glioblastoma study based on genes prioritized by LIANA for mediating ligandreceptor mediated signaling between astrocytes, NK cells, and macrophages. Featurizations were used to predict the age of each donor under different pooling strategies (mean, sum, and median) in the implementation of scGPT. Prediction accuracy from scGPT features (pink) was compared to that obtained using featurizations obtained using random cells and genes (pink).\", \"page\": 18, \"index\": 2, \"width\": 737, \"height\": 732}]"
motivation: 由于空间成像数据中细胞形态复杂且样本异质性高，传统方法难以识别与疾病结局相关的免疫微环境。
method: 该研究采用无分割的多实例学习框架，从空间成像蛋白质组学数据中学习免疫微环境的特征表示。
result: MICRON显著提高了预后和诊断预测准确性，并揭示了脑癌中星形胶质细胞、NK细胞和巨噬细胞间的关键通讯模式。
conclusion: MICRON为疾病预后相关免疫微环境的自动识别提供了高效可靠的新途径。
---

## 摘要
空间成像蛋白质组学技术（如成像质谱流式细胞术）能够全面识别驱动疾病结局的免疫微环境。从这些数据中识别与结局相关的免疫微环境一直十分复杂，因为这需要对形态复杂的细胞进行分割，并在众多异质样本之间整合空间特征。我们提出了 MICRON，这是一种基于多实例学习的无分割、全自动工具，用于自动识别与结局相关的免疫微环境。MICRON 能够从空间成像蛋白质组学数据中学习样本表征，使其在预后和诊断预测方面优于现有方法。作为案例研究，我们展示了 MICRON 生成的综合重要性图谱，揭示了脑癌中与结局相关的关键免疫微环境，发现了星形胶质细胞、自然杀伤细胞和巨噬细胞之间与生存结局相关的协同细胞间通信。MICRON 作为开源软件提供，供临床医生和生物学家广泛使用，网址为：https://github.com/ChenCookie/micron。

## Abstract
Spatial imaging proteomics modalities, such as imaging mass cytometry, enable comprehensive identification of immune microenvironments driving disease outcomes. Identifying outcome-associated immune microenvironments from these data has proven to be complex, as it requires segmenting cells with complex shapes and reconciling spatial signatures across many heterogeneous samples. We present MICRON, a segmentation-free, fully automated multiple-instance learning based tool for automatic identification of outcome-linked immune microenvironments. MICRON learns representations of samples profiled with spatial imaging proteomics modalities, enabling more accurate prognostic and diagnostic prediction over existing approaches. As a case study, we show that MICRON generates a comprehensive importance map that reveals key outcome-associated immune microenvironments in brain cancer, uncovering coordinated cell-cell communication between astrocytes, NK cells, and macrophages linked to survival outcomes. MICRON is provided as open source software for broad use by clinicians and biologists at https://github.com/ChenCookie/micron.

---

## 论文详细总结（自动生成）

# MICRON 学习空间免疫微环境的结局相关表征 — 综合总结

---

## 一、研究核心问题与背景

- **研究动机**：  
  空间成像蛋白质组学（如成像质谱流式细胞术，IMC）可实现多通道、高维度的免疫组织映射，揭示驱动疾病结局的空间细胞微环境。  
  然而，现有计算方法普遍依赖**细胞分割**来提取特征，导致：
  - 对形态复杂（非球形）的细胞，如神经元和小胶质细胞，难以准确分割。  
  - 样本间异质性高、分割误差大，导致空间免疫特征整合困难。
  
- **核心问题**：如何在不依赖细胞分割的前提下，从空间成像蛋白质组学数据中自动学习与疾病结局相关的免疫微环境表示。

- **研究意义**：  
  提出一种自动化、可解释、可推广的分析工具，以协助疾病预后预测、患者分层及机制探索。

---

## 二、方法论：MICRON 框架

### 1. 核心思想
- **MICRON**（Microenvironment-aware Clinical Representation learning for Outcome prediction via multiple-instance learning）是一个**无分割的表示学习框架**。  
- 它基于**多实例学习（Multiple Instance Learning, MIL）**，将每个样本视为由多个“图像片段（instances）”组成的集合，通过聚合片段特征学习样本级表征，实现对临床结局的预测。

### 2. 技术细节
- **输入处理**：  
  利用 SLIC 算法将图像划分为约 100 个超像素（superpixels），每个超像素代表一个空间一致的免疫微环境。
- **筛选策略**：  
  选取形状不规则度最高的前 30 个超像素，认为这些区域信息更丰富。
- **多实例学习特征聚合**：  
  - 使用全卷积网络（FCN）对每个 crop 生成预测概率。  
  - 通过**分位数聚合函数（quantile aggregation）**汇总实例层级预测，得到样本级概率分布。  
  - 最终通过 softmax 输出样本结局预测。  
  - 优化目标：**交叉熵损失函数**。
- **可解释性分析**：  
  使用 SHAP (SHapley Additive exPlanations) 分析各 crop 对预测结果的贡献，形成“重要性图谱”，揭示关键免疫微环境关联。
- **输出**：  
  通过嵌入向量聚类与频率统计，生成样本级空间免疫特征，可进行后续生存分析或结果预测。

### 3. 公式核心逻辑（文字描述）
- 多实例集合 \(B_i = \{r_{mi}\}_{m=1}^{M}\) → 对每个实例 m 计算预测分布 \(P_{mi,k}\)；
- 对每个类别 k，计算分位数特征 \(V_{i,k} = \text{Quantile}(P_{i,k})\)；
- 将所有类别特征拼接为 \(V_i = [V_{i,1},...,V_{i,K}]\)，并经 softmax 得到样本级概率；
- 使用交叉熵损失优化模型；
- 最后通过 SHAP 分析得到每个 crop 的 SHAP 重要度 \(Importance_{i,c} = \sum_j |\phi_{i,c}^j|\)。

---

## 三、实验设计

### 1. 数据集
MICRON 在三个公开的 IMC 数据集上进行验证：
- **Diabetes（Damond et al., 2019）**：  
  人胰腺组织样本，区分非糖尿病与 1 型糖尿病患者（67 人）。
- **Breast Cancer（Jackson et al., 2020）**：  
  乳腺肿瘤组织，预测患者生存状态（376 样本）。  
- **Brain Tumors（Karimi et al., 2023）**：  
  比较原发性胶质母细胞瘤（GBM）与脑转移瘤（BrM）（139+46 患者）。

此外结合：
- **单细胞 RNA 测序数据（Ruiz-Moreno et al., 2022）**用于验证机制性信号（配体-受体通讯）。

### 2. 对比方法（Benchmark）
- **Segmentation-based**：CellPose 分割后提取细胞特征。  
- **Segmentation-free**：CANVAS（自监督表示学习法）。  
- **其他**：基于频率统计或 pooling 的特征表示（mean、median、max、sum）。

### 3. 实验指标
- **分类性能**：AUC （Area under ROC Curve）；
- **生存分析**：Kaplan-Meier 曲线及显著性检测；
- **机制验证**：配体-受体互作（LIANA）、基因表达特征（scGPT）。

---

## 四、资源与算力

- 文中未明确说明 GPU 规格、数量或训练耗时。
- 作为多实例学习框架，推测可在标准研究工作站上运行（论文提供开源实现 https://github.com/ChenCookie/micron），但**算力细节缺失**。

---

## 五、实验数量与充分性

- 涉及 **三个临床空间成像数据集 + 一个单细胞 RNA-seq 数据集**。
- 每个数据集进行独立二分类实验，并进行了：
  - **性能对比**（MICRON vs. CANVAS/CellPose 等）；  
  - **生存分析与机制联动验证**（通过 ligand–receptor 及 scGPT）。  
  - 多折交叉验证（200 fold）评估鲁棒性。
- 结果覆盖癌症、糖尿病等多病种，说明实验相对**丰富且跨领域**。
- 尚未看到消融实验或参数敏感性分析，属于轻度缺失。

---

## 六、主要结论与发现

- MICRON 无需细胞分割即可：
  - 在各数据集中实现高诊断/预后预测准确率（最高 AUC 达 1.0）。  
  - 自动识别与结局关联的**空间免疫微环境**。
- 在脑癌数据中：
  - 发现在生存较好的患者中，星形胶质细胞、NK 细胞和 M1样巨噬细胞之间空间共存的微环境更丰富。  
  - 单细胞数据验证了 NK-astrocyte 间通过 **XCL1–ADGVR1** 途径的配体受体通讯机制。
- 微环境特征可被用于其他表型预测，如年龄分层（scGPT提取基因embedding准确率达0.8）。

---

## 七、优点与创新性

- **技术创新**：
  - 首次在空间蛋白质组学中实现**多实例+分位数聚合**的无分割学习框架。
  - 可解释性增强（SHAP）→ 显式定位关键免疫微环境。  
- **生物学价值**：
  - 跨模态验证机制（空间蛋白质学 + 单细胞转录组）。
  - 发现新型免疫通信结构，与生存相关。
- **实用性**：
  - 开源实现，适合广泛临床与科研应用。
  - 适应不同细胞形态和异质组织。

---

## 八、不足与局限

- **算力与复现实验细节**：未给出硬件配置、时间消耗、超参数确定方式。  
- **缺乏消融分析**：未系统阐明各模块（如 SLIC、quantile 聚合、SHAP）的贡献比例。  
- **任务类型局限**：当前仅支持**二分类**结局预测，尚未支持连续或多类别结局。  
- **泛化性验证不足**：实验集中于三类病种，需未来扩展至更多组织与疾病类型。  
- **机制验证跨模态依赖性**：单细胞验证虽支持结论，但基因层机制解释仍需实验生物确认。

---

（完）
