---
title: Translating Histopathology Foundation Model Embeddings into Cellular and Molecular Features for Clinical Studies
title_zh: 将组织病理学基础模型嵌入转换为用于临床研究的细胞和分子特征
authors: "Cui, S., Sui, Z., Li, Z., Matkowskyj, K. A., Yu, M., Grady, W. M., Sun, W."
date: 2026-03-23
pdf: "https://www.biorxiv.org/content/10.64898/2026.03.17.711896v2.full.pdf"
tags: ["query:pathseg"]
score: 9.0
evidence: 将病理基础模型嵌入转化为细胞类型组成
tldr: 本研究针对现有病理学基础模型嵌入不可解释的问题，提出STpath框架，将影像嵌入与空间转录组数据结合，通过癌种特异性的XGBoost模型推断细胞组成与基因表达，在结直肠癌和乳腺癌数据上验证了其实用性，并显示可用于临床结局分析。
source: biorxiv
selection_source: fresh_fetch
figures_json: "[{\"url\": \"assets/figures/biorxiv/biorxiv-10-64898-2026-03-17-711896-v2/fig-001.webp\", \"caption\": \"Figure 6. STpath predictions enable spatial distance metrics and clinical associations in TCGACOAD. (A) Cell type prediction and tile classification. Top row: Predicted cell type proportions (normalized) for tumor cell, stromal cell, T-cells, and pan-APCs in a representative TCGA-COAD sample Bottom row: Tile classification based on proportion thresholds (tumor cell>30%, stromal cell >40%, Tcells >10%, pan-APCs >30%). (B). Minimum directional distance calculation. Schematic illustrating calculation of weighted minimum distance from a tumor tile to stromal tiles, where distance is weighted by the source tile's cell proportion. Bottom row: Spatial distribution of minimum directional distances from tumor-to-stromal cell, T-cells, and pan-APCs. (C) Kaplan-Meier curves for progression-free interval (PFI). Left: PFI stratified by median minimum directional distance groups (low vs. high) for tumor-topan-APCs, stratified by AJCC tumor stages. N=232 TCGA-COAD patients. P-values from log-rank test.\", \"page\": 25, \"index\": 1, \"width\": 976, \"height\": 976}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-64898-2026-03-17-711896-v2/fig-002.webp\", \"caption\": \"Figure 7. Cross-validated performance for breast cancer, feature importance comparison between breast colorectal cell and breast tumor cell prediction. (A). LOIO cross-validation performance. Model performance across five pathology foundation AI models, a reference model, and a combined model for eight major cell-type categories. Left: MAE. Right: Pearson correlation. Each point represents an individual sample. Boxes show interquartile ranges with median lines. (B) Feature importance comparison between colorectal and breast tumor cell prediction models. Scatter plots comparing XGBoost feature importance for tumor cell prediction between BRCA and COAD. Left: UNI2h (N features = 1536). Right: Virchow2 (N features = 2560).\", \"page\": 26, \"index\": 2, \"width\": 976, \"height\": 1074}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-64898-2026-03-17-711896-v2/fig-003.webp\", \"caption\": \"Figure 2. Cell type deconvolution and validation. (A) UMAP visualization of double-confirmed colorectal cancer single-cell RNA-seq data showing 20 annotated cell subtypes, including tumor subtypes (ASC: Absorptive stem-like cancer cells, CSC: Carcinoma-specific epithelial cells, SSC: Serrated-lesion– derived cells), normal epithelial subtypes (CT: Crypt-top colonocytes, EE: Enteroendocrine cells, TUF: Tuft cells, ABS: Absorptive colonocytes), stromal subtypes (FIB: Fibroblasts, END: Endothelial cells), T cell subtypes (CD4+T, CD8+T) and pan-APC subsets (PLA: Plasma, MYE: Myeloid, MAS: Mast cells, B cells). (B) Heatmap of scaled log-normalized marker genes expression across cell subtypes, confirming distinct transcriptional profiles. (C) Deconvoluted cell type proportions at the tissue region level, shown for ungrouped subtypes (top) and aggregated into five major categories (bottom). (D) Correlation analysis between deconvoluted cell type proportions and marker gene expression–based relative expression. Representative examples show positive Spearman correlations across all five major categories, supporting the validity of deconvolution results. (E) Representative H&E-stained image with corresponding spatial hexagonal binned heatmaps of deconvoluted tumor cell proportions and relative marker genes expression (GE).\", \"page\": 21, \"index\": 3, \"width\": 962, \"height\": 962}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-64898-2026-03-17-711896-v2/fig-004.webp\", \"caption\": \"Figure 3. Feature representation, predicting models’ comparison, efficiency, and complementarity across pathology foundation models. (A) UMAP visualization of extracted features from 5 pathology foundation models and ResNet50 as a reference model. For each model, both the full features set, and the top 10 features selected by XGBoost were visualized, with embeddings colored by dataset cohorts (top) and deconvoluted cancer cell proportions (bottom). (B) Contribution analysis of foundation models to the combined XGBoost prediction performance for tumor and stromal cells. Both absolute contributions (blue and normalized per-feature contributions (orange) are shown, highlighting complementary strengths of different models. (C) Comparison of predictive performance and computational efficiency across multiple machine learning methods, including MLP, Lasso, Random Forest, and XGBoost. Models were evaluated using leave-one-out training. (D) Pairwise complementarity analysis of foundation model features using ridge regression. The heatmap shows scores between predicted and target models, with lower values indicating higher complementarity.\", \"page\": 22, \"index\": 4, \"width\": 976, \"height\": 990}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-64898-2026-03-17-711896-v2/fig-005.webp\", \"caption\": \"Figure 4. Cross-validated performance, gene expression, and spatial agreement of STpath predictions for colorectal cancer. (A) Leave-one-individual-out (LOIO) performance across 5 pathology foundation AI models, reference model and the combined model for 5 major cell-type categories. Left: Mean Absolute Error (MAE). Right: Pearson correlation. Each point represents an individual. Boxes show interquartile ranges with medians. (B) Representative whole-slide results for Tumor, Stromal, and T-cell enrichment. Columns show the original H&E WSI, deconvoluted proportions from spatial transcriptomics, LOIO model-predicted proportions, and spot-wise scatter plots comparing predictions with deconvoluted values. (C) Gene expression prediction comparison. Left: Pearson correlations between predicted and true gene expression across 5 marker gene sets (30 genes each) and 30 HVGs. For each gene, Pearson correlation was computed under the LOIO strategy and the median across individuals was taken. Each point represents one gene. Right: Scatter plot comparing ResNet50 and Virchow2, with each dot representing a single gene.\", \"page\": 23, \"index\": 5, \"width\": 976, \"height\": 985}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-64898-2026-03-17-711896-v2/fig-006.webp\", \"caption\": \"Table 1. Cox proportional hazards regression models of median distance features for progressionfree survival in TCGA-COAD. Hazard ratios with 95% confidence intervals and p-values are reported from the Cox proportional hazards model (either unadjusted or adjusted) with progression-free survival as the outcome. Significant associations ( 0.05) are shown in bold.\", \"page\": 27, \"index\": 6, \"width\": 989, \"height\": 523}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-64898-2026-03-17-711896-v2/fig-007.webp\", \"caption\": \"Table 2. Adjusted log-linear regression model of median distance features for mutation burden in TCGA-COAD. Multiplicative effects with 95% confidence intervals and p-values are reported from the joint model with log-transformed somatic mutation burden as the outcome. Predictors include AJCC tumor stage status, age, gender, and each of the spatial distance medians. Significant associations ( 0.05) are shown in bold.\", \"page\": 27, \"index\": 7, \"width\": 971, \"height\": 475}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-64898-2026-03-17-711896-v2/fig-008.webp\", \"caption\": \"Figure 5. Robustness of overall cell type proportion estimates to patch-grid resolution.\", \"page\": 24, \"index\": 8, \"width\": 976, \"height\": 979}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-64898-2026-03-17-711896-v2/fig-009.webp\", \"caption\": \"Figure 1. Overview of the STpath. (A) Whole-slide H&E images were aligned with spatial transcriptomics spot coordinates and partitioned into tissue tiles. (B) scRNA-seq data were processed to curate reference cell type signatures, followed by cell type deconvolution of ST data and validation of inferred cell type proportions with marker gene expression. Annotated tiles were generated by linking deconvolution results to matched image regions. (C) Annotated tissue tiles were used to extract embeddings from multiple pre-trained pathology foundation AI models. These embeddings were input into ML models to predict cell type proportions, with training and leave-one-individual-out validation. (D Trained models were applied to external colorectal and breast cancer WSIs, enabling downstream clinical applications including overall tumor grading, quantitative soft tissue segmentation, and association with genomic and clinical outcomes.\", \"page\": 20, \"index\": 9, \"width\": 976, \"height\": 979}]"
motivation: 病理影像嵌入缺乏生物和临床可解释性，限制了其在临床分析中的应用。
method: 作者开发了STpath框架，利用癌种特异性的XGBoost模型将病理影像嵌入与空间转录组数据整合。
result: STpath能准确预测细胞类型组成与部分基因表达，并通过多模型嵌入进一步提升性能。
conclusion: STpath桥接了病理学基础模型与分子层面特征之间的差距，为临床研究提供了可解释的生物信息。
---

## 摘要
由人工智能驱动的病理学基础模型通过将病理图像切片编码为数值嵌入向量，提供了针对组织病理图像的通用表示。然而，这些嵌入在生物学或临床层面上并不具有直接可解释性，必须将其转化为生物学上有意义的特征，如细胞类型组成或基因表达，以支持下游的临床应用。为弥合这一差距，我们开发了 STpath 框架，该框架将来自现有病理学基础模型的组织病理图像嵌入与匹配的空间分辨转录组数据进行整合。STpath 由癌种特异性的 XGBoost 模型组成，这些模型经过训练，可从组织病理图像切片中推断细胞类型组成和基因表达。我们在结直肠癌和乳腺癌数据集中评估了 STpath，结果显示该方法能够准确估计主要细胞类型的组成以及部分基因的表达水平，并且通过结合多个基础模型的嵌入可以进一步提升性能。最后，我们证明了 STpath 所推断的特征可用于下游研究，以评估其与临床结局之间的关联。

## 速览
**TLDR**：本研究提出STpath框架，将病理影像基础模型的嵌入与空间转录组数据结合，利用癌种特异的XGBoost模型预测细胞组成和基因表达，验证于结直肠癌与乳腺癌数据集，结果显示预测精度高并可用于临床结局研究。 \
**Motivation**：病理影像基础模型生成的嵌入难以直接生物学解释，需建立能关联到细胞与分子特征的桥梁。 \
**Method**：研究构建了基于病理图像嵌入和空间转录组的XGBoost预测模型。 \
**Result**：在结直肠癌和乳腺癌数据上验证，STpath能准确预测主要细胞类型组成和部分基因表达，并在结合多种基础模型嵌入后性能进一步提升。 \
**Conclusion**：STpath能将影像嵌入转化为可解释的生物分子特征，为病理AI在临床研究中的应用提供新途径。

---

## Abstract
AI-powered pathology foundation models provide general-purpose representations of histopathological images by encoding image tiles into numerical embeddings. However, these embeddings are not directly interpretable in biological or clinical terms and must be translated into biologically meaningful features, such as cell-type composition or gene expression, to enable downstream clinical applications. To bridge this gap, we developed STpath, a framework that integrates histopathology image embeddings derived from existing pathology foundation models with matched, spatially resolved transcriptomics data. STpath consists of cancer-specific XGBoost models trained to infer cell-type compositions and gene expression from histopathology image tiles. We evaluated STpath in colorectal and breast cancer datasets and showed that it provides accurate estimates of the composition of major cell types and the expression of a subset of genes, with further performance gains achieved by combining embeddings from multiple foundation models. Finally, we demonstrated that STpath inferred features that can be used in downstream studies to evaluate their associations with clinical outcomes.

---

## 论文详细总结（自动生成）

# 《将组织病理学基础模型嵌入转换为用于临床研究的细胞和分子特征》论文总结

---

## 一、研究问题与背景

- **研究动机**：  
  近年来，基于人工智能的病理学基础模型（Foundation Models）通过在大规模 H&E 图像上预训练，可生成通用的图像嵌入表示。然而，这些高维嵌入缺乏生物学与临床可解释性，难以直接用于疾病机理研究或临床决策。
- **核心问题**：  
  如何将这些抽象的病理影像嵌入转化为生物学上有意义的特征（如细胞类型组成、基因表达谱），以便：
  - 支撑肿瘤微环境（TME）的定量研究；
  - 促进临床预后分析；
  - 弥合人工智能模型与可解释临床特征之间的 gap。

---

## 二、方法论：STpath 框架

### 1. 核心思想

- 提出 **STpath（Spatial Transcriptomics-guided Pathology translation）** 框架：
  - 利用已有病理基础模型生成的嵌入向量；
  - 结合空间转录组（SRT）数据建立映射关系；
  - 通过癌种特异性的监督学习模型，将嵌入转换为细胞类型比例或基因表达预测结果。

### 2. 关键技术流程

1. **数据配对与预处理**：
   - 将 H&E 全视野图像（WSI）分割为标准尺寸的图像小块（tiles，约 256×256 像素）。
   - 对应每个 tile 的空间转录组信号，通过匹配坐标与组织区域实现空间对齐。
2. **细胞类型标注与验证**：
   - 使用单细胞转录组（scRNA-seq）数据构建参考表达矩阵；
   - 采用 **CARD** 算法进行细胞类型去卷积；
   - 验证每种细胞类型的估计值与标志基因表达之间的相关性（Spearman 相关）。
3. **特征提取**：
   - 从多个基础模型提取数值嵌入（例：Virchow、UNI2-h、Prov-Gigapath、Conch、Virchow2、ResNet50）。
   - 各模型的嵌入维度介于 512–2560 之间。
4. **监督学习建模**：
   - 将嵌入作为输入特征，细胞类型比例或基因表达作为输出标签；
   - 采用 **XGBoost 回归** 建立模型；
   - 使用留一患者交叉验证（LOIO）评估泛化能力；
   - 通过特征重要度筛选去除批效应（Batch Effect）。
5. **模型集成**：
   - 将来自多个基础模型的最重要特征拼接形成**组合模型（Combined Model）**；
   - 分析不同模型间的特征互补性（利用岭回归评估特征可预测性）。
6. **预测基因表达与空间分析**：
   - 面向 180 个目标基因建立基因表达预测；
   - 使用偏相关分析控制细胞组成效应；
   - 进一步计算细胞类型间的**最小方向距离**（Directional Distance），用于关联突变负荷与生存率。

---

## 三、实验设计

### 1. 数据来源与规模

| 癌种 | H&E 图像数 | 图像小块数 | 来源 |
|------|-------------|-------------|------|
| 结直肠癌 (CRC) | 63 张 | >120,000 个 tiles | Colon Molecular Atlas、HEST-1K、Fred Hutch 自建 |
| 乳腺癌 (BRCA) | 11 张 | >43,000 个 tiles | 10x Genomics、Liu 等、Wu 等公开数据集 |
| 临床验证集 | TCGA-COAD、TCGA-BRCA | 外部独立样本 | 用于预后与突变负荷分析 |

### 2. 对比模型

- **主要对比基线**：ResNet50（ImageNet 预训练）。  
- **病理基础模型**：
  - Conch、Prov-GigaPath、UNI2-h、Virchow、Virchow2。
- **算法对比**：
  - XGBoost、随机森林、前馈神经网络（MLP）、Lasso 回归。

### 3. 评估指标

- **回归性能**:
  - Mean Absolute Error (MAE)；
  - Pearson 相关系数；
- **空间一致性**:
  - 多分辨率稳定性（不同 segmentation grid 尺寸下的变异度 ≤8%）；
- **临床相关性**:
  - Cox 回归 (Progression-Free Interval)；
  - 线性回归（Mutation Burden）。

---

## 四、算力与资源

- **硬件环境**：
  - Apple MacBook Pro（M3 Max，14 核 CPU，30 核 GPU，64 GB 内存）；
  - 支持 MPS、CUDA 及 CPU-only 模式。
- **计算开销**：
  - 每个基础模型提取约 33 万张 tile 特征需时 4–6 小时；
  - 全部模型训练与验证约 240 GPU 小时；
  - 峰值显存需求 4–16 GB（取决于模型维度与组合模型大小）。

---

## 五、实验数量与充分性

- 主要实验类别：
  1. **不同基础模型的比较（6 种模型）**；
  2. **不同机器学习方法比较（4 种算法）**；
  3. **多模型组合与互补性分析**；
  4. **跨癌种泛化（CRC vs. BRCA）**；
  5. **空间尺度鲁棒性测试**；
  6. **外部临床验证（TCGA-COAD/BRCA）**；
  7. **基因层面预测与偏相关分析**。
- **充分性评估**：
  - 覆盖不同任务（细胞组成 / 基因表达 / 生存分析），设计较完整；
  - 使用严格的 LOIO 策略避免数据泄漏；
  - 对比基线合理且包含非领域模型；
  - 实验数量充足且基于不同来源数据集，验证较客观。

---

## 六、主要结论与发现

1. **STpath 成功将病理嵌入映射为细胞构成与基因表达特征**；
2. **监督学习有效缓解批效应**，XGBoost 在准确性与计算效率上表现最佳；
3. **多模型嵌入集成优于单一基础模型**，体现多源信息互补；
4. **预测结果具备较好泛化性**（LOIO 评估下肿瘤/基质细胞预测相关 >0.7）；
5. **推断特征具有临床相关性**：
   - 肿瘤与抗原呈递细胞或 T 细胞的短距离分布与良好预后相关；
   - 同样距离特征与突变负荷呈负相关；
6. **癌种特异性明显**：
   - 同一模型在不同癌种间特征权重显著不同；
   - STpath 需为不同癌种单独训练。

---

## 七、优点与创新

- **创新模型架构**：首个将多病理基础模型嵌入与空间转录组结合的可解释学习框架；
- **严谨的验证机制**：使用 LOIO 避免过拟合误导；
- **可解释性增强**：基于特征重要度进行批效应校正；
- **多模型融合策略**：通过特征互补性分析实现最佳性能；
- **良好的临床外推性**：可用于外部数据集的预后分析；
- **开源与复现性高**：提供公开代码与示例数据。

---

## 八、不足与局限

- **数据依赖性强**：STpath 需空间转录组数据进行监督训练，目前此类数据有限；
- **癌种特异性限制泛用性**：模型需针对不同癌种独立训练；
- **基因表达预测仍不稳定**：部分基因相关性 <0.1；
- **批效应来源复杂**：虽然可缓解，但未完全消除；
- **样本数量仍偏少**（尤其乳腺癌，仅 11 张 WSIs）；
- **仅限五大主要细胞类型**，对 stromal 细胞亚型区分不足；
- **临床应用仍需进一步验证**，尚未进入真实诊断流程。

---

**（完）**
