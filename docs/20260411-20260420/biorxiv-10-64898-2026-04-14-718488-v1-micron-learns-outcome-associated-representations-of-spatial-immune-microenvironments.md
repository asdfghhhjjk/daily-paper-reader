---
title: MICRON learns outcome-associated representations of spatial immune microenvironments
title_zh: MICRON 学习与结果相关的空间免疫微环境表征
authors: "Chen, C.-J., George, B., Dhawka, L., Evangelista, B., Stanley, N."
date: 2026-04-16
pdf: "https://www.biorxiv.org/content/10.64898/2026.04.14.718488v1.full.pdf"
tags: ["query:cellrep"]
score: 9.0
evidence: 用于结果相关免疫微环境的无分割多实例学习
tldr: 本研究提出MICRON，一种无需细胞分割的多实例学习工具，可从空间成像蛋白质组数据中自动识别与临床结局相关的免疫微环境，显著提升预后预测准确性，并在脑癌研究中揭示关键细胞互作机制。
source: biorxiv
selection_source: fresh_fetch
figures_json: "[{\"url\": \"assets/figures/biorxiv/biorxiv-10-64898-2026-04-14-718488-v1/fig-001.webp\", \"caption\": \"Fig. 1 MICRON learns outcome-associated spatial immune signatures and microenvironments. (a) Schematic of the multiple-instance learning framework used to train MICRON to predict outcomes from spatial imaging proteomics modalities. During training, square regions (instances) are cropped from the input image and processed by a fully convolutional network (FCN) to generate instance-level class predictions. The distribution of instance-level outcome probability predictions are summarized via a quantile-based featurization per each outcome class. The quantile vectors across classes are concatenated and input to a softmax function to predict an outcome probability for each sample. The model parameters, including both the FCN and quantile aggregation module, are optimized via the cross-entropy loss. (b) Sample representations are computed for new, unseen samples by using the trained MICRON model to generate embedding vectors for each image crop. (c) Crops across testing images are prioritized via SHAP values and identify both high-impact and outcomeassociated image crops, corresponding to key immune microenvironments. (d) For predicting sample outcomes, MICRON can specify two types of immune features, including (i) (multiple-instance (MI) features), obtained by pooling learned instance embedding dimensions across all cells and (ii) (frequency features), obtained by clustering instance embedding vectors and counting the proportion of instances assigned to each cluster per sample. Featurizations are used for downstream prediction tasks, such as, survival analysis. (e) Immune signatures obtained through MICRON were evaluated for their accuracy in predicting binary clinical outcomes on three publicly available clinical IMC datasets. The number of channels measured in the IMC experiments are denoted as well as the number of donors in each outcome class. (f) The prediction accuracy of MICRON is compared to related methods for predicting a binary clinical outcome across the three datasets (area under the ROC curve (AUROC)). (g) In the Karimi dataset, MICRON identified more frequent co-occurrences between astrocytes, NK cells, and M1-like MDMs in glioblastoma patients than was observed in patients with metastasized brain tumors. Bold green lines indicate the most frequently co-occurring cell-type pairs across topmost-informative image crops. Nodes circled in gold represent the set of cell-types that were most ubiquitously identified across immune microenvironments.\", \"page\": 17, \"index\": 1, \"width\": 738, \"height\": 857}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-64898-2026-04-14-718488-v1/fig-002.webp\", \"caption\": \"Fig. 2 Microenvironments uncovered with MICRON prioritized differential cell-cell communication mechanisms. (a) Representative brain metastasis (BrM) and glioblastoma (GBM) sample images colored according to expression of key markers for phenotyping macrophages (CD68), astrocytes (GFAP), and NK cells (CD94 and CD16). Superpixel importance scores show image regions prioritized by MICRON. Cells in high-scoring regions were segmented and phenotyped to reveal prominent microenvironments in the BrM and GBM classes. (b) Overview of how MICRON can be applied to perform survival analysis in patients from the Karimi study. For a set of held out patients, MICRON was used to identify the top 20 most outcome-associated superpixels in each image (denoted as V in superpixel map). (c) Image crops were clustered with k-means (K = 10) using MICRON-computed embeddings. The UMAP (top) shows cells colored according to the embedding clusters. Patients were stratified into high and low frequency groups for each cluster. The UMAP (bottom) colors cells based on the risk of death and identifies clusters 4 and 9 as being survival-associated and survival unassociated, respectively. (d) Cluster 4 was observed to be strongly associated with survival and highlights strong spatial co-occurrence between astrocytes, NK cells, and M1-like MDMs in glioblastoma. (e) Cell-cell communication patterns via ligand/receptor signaling were investigated in an independent cohort of glioblastoma patients profiled with single-cell RNA-seq (Ruiz-Moreno study [22]). Dotplots visualize top genes with enrichment patterns according to specificity rank (indicated by dot size and color) specifically between astrocytes, macrophages, and NK cells. (f)A graph was constructed between cells where the edges are weighted by the specificity rank between a pair of cell-types. The graph reveals prominent cross-talk between astrocytes and NK cells, supporting the spatial signature prioritized by MICRON in the Karimi study. (g) scGPT was used to featurize samples in the Ruiz-Moreno glioblastoma study based on genes prioritized by LIANA for mediating ligandreceptor mediated signaling between astrocytes, NK cells, and macrophages. Featurizations were used to predict the age of each donor under different pooling strategies (mean, sum, and median) in the implementation of scGPT. Prediction accuracy from scGPT features (pink) was compared to that obtained using featurizations obtained using random cells and genes (pink).\", \"page\": 18, \"index\": 2, \"width\": 737, \"height\": 732}]"
motivation: 现有空间成像蛋白质组数据难以准确识别与疾病结局相关的免疫微环境，需要一种自动化且高效的分析方法。
method: 采用基于多实例学习的表示学习框架，并跳过细胞分割步骤，实现自动识别结局相关的空间免疫结构。
result: MICRON在脑癌数据中揭示了与生存结局相关的免疫微环境结构及细胞间通讯。
conclusion: MICRON为临床和生物学研究提供了强有力的空间免疫微环境分析新方法。
---

## 摘要
空间成像蛋白质组学技术（如成像质谱流式细胞术）能够全面识别驱动疾病结果的免疫微环境。从这些数据中识别与结果相关的免疫微环境非常复杂，因为这需要对具有复杂形状的细胞进行分割，并在众多异质样本之间协调空间特征。我们提出了 MICRON，这是一种无分割、全自动的多实例学习工具，用于自动识别与结果相关的免疫微环境。MICRON 能够学习利用空间成像蛋白质组学技术分析的样本表示，相较于现有方法，能实现更准确的预后和诊断预测。作为一个案例研究，我们展示了 MICRON 能够生成全面的重要性图，揭示脑癌中与结果相关的关键免疫微环境，发现星形胶质细胞、自然杀伤细胞与巨噬细胞之间的协调细胞间通信与生存结果相关。MICRON 作为开源软件提供，供临床医生和生物学家广泛使用，网址为 https://github.com/ChenCookie/micron。

## Abstract
Spatial imaging proteomics modalities, such as imaging mass cytometry, enable comprehensive identification of immune microenvironments driving disease outcomes. Identifying outcome-associated immune microenvironments from these data has proven to be complex, as it requires segmenting cells with complex shapes and reconciling spatial signatures across many heterogeneous samples. We present MICRON, a segmentation-free, fully automated multiple-instance learning based tool for automatic identification of outcome-linked immune microenvironments. MICRON learns representations of samples profiled with spatial imaging proteomics modalities, enabling more accurate prognostic and diagnostic prediction over existing approaches. As a case study, we show that MICRON generates a comprehensive importance map that reveals key outcome-associated immune microenvironments in brain cancer, uncovering coordinated cell-cell communication between astrocytes, NK cells, and macrophages linked to survival outcomes. MICRON is provided as open source software for broad use by clinicians and biologists at https://github.com/ChenCookie/micron.

---

## 论文详细总结（自动生成）

# 《MICRON 学习与结果相关的空间免疫微环境表征》论文总结

---

## 1. 核心问题与研究背景

- **研究问题**：如何从空间成像蛋白质组学（Spatial Imaging Proteomics）数据中识别与临床结果（如生存、疾病状态等）相关的免疫微环境。  
- **问题难点**：  
  - 现有分析方法依赖**单细胞分割**，但许多细胞（如神经元、星形胶质细胞、微胶质细胞）形态复杂，分割误差大。  
  - 不同样本间空间异质性强，使得特征对齐困难。  
- **研究动机**：迫切需要一种**无需细胞分割**、能自动学习空间特征并与临床结果关联的算法，提高预后预测和免疫微环境识别的准确性。  
- **核心意义**：MICRON 提供一种端到端的表示学习框架，不仅提升诊断预测性能，还能解释性地揭示关键免疫微环境。

---

## 2. 方法论与技术框架

### 2.1 核心思想

- 提出 **MICRON（Microenvironment-aware Clinical Representation learning via multiple-instance learning）**：  
  一种**分割无关（segmentation-free）**的多实例学习（Multiple-Instance Learning, MIL）框架，用于自动学习与疾病结果关联的空间组织特征。

### 2.2 模型结构与流程

1. **输入处理与区域划分**  
   - 原始成像样本通过 **SLIC 超像素算法**划分为多个**一致性区域（superpixels）**；  
   - 每个区域代表一个“实例”（instance）输入模型。  
   - 按照区域形状不规则性排序，选取最具信息的前 30 个区域作为训练样本。  

2. **多实例学习框架**  
   - 各图像块经 **全卷积网络（FCN）**提取表征；  
   - 对每个实例输出的结果分布进行**分位数（quantile）聚合**，生成样本级特征；  
   - 分位数聚合公式（简化描述）：
     \[
     V_{i,k} = Quantile(P_{i,k})
     \]
     其中 \(P_{i,k}\) 为样本 \(i\) 对于类别 \(k\) 的所有实例预测概率集；
   - 聚合后的特征输入 **Softmax + 交叉熵损失**，完成样本级结果预测。

3. **解释性分析（Explainable component）**  
   - 使用 **SHAP（SHapley Additive exPlanations）** 计算每个图像区域的重要性；
   - 通过高 SHAP 值的区域生成“重要性地图”，可定位与结果相关的免疫微环境。

4. **特征表达输出**  
   - 输出两类特征：
     - **聚合特征（MI features）**：编码整体图像空间信息；
     - **频率特征（Frequency features）**：基于聚类统计各类超像素的分布频率。

---

## 3. 实验设计

### 3.1 数据集与场景

论文共使用四个公开数据集：
| 数据集 | 类型 | 样本规模 | 任务 | 来源 |
|--------|------|-----------|------|------|
| **Damond et al. (2019)** | 胰腺 IMC | 67 人（T1D vs 非糖尿病） | 分类 | [20] |
| **Jackson et al. (2020)** | 乳腺肿瘤 IMC | 376 样本 | 生存预测 | [6] |
| **Karimi et al. (2023)** | 脑肿瘤 IMC | 139+46 患者区域 | 区分原发 GBM vs 转移 BrM | [21] |
| **Ruiz-Moreno et al. (2022)** | 单细胞 RNA-seq (scRNA-seq) | 240 患者 | 机制验证与年龄二分类 | [22] |

### 3.2 对照方法（benchmarks）

MICRON 与以下方法进行了比较：
- **CANVAS (segmentation-free self-supervised)** — 与 MICRON 类型最接近；
- **Cellpose、QUICHE、LEAPH、SpatialLDA 等 segmentation-based 方法**；
- **统计特征与聚类频率法** 等非学习基线。

### 3.3 评估指标

- **分类任务**：AUC (Area Under ROC Curve)；
- **生存分析**：Kaplan-Meier 曲线及 log-rank 检验；
- **模型解释性**：SHAP 显著性区域与空间共现分析。

---

## 4. 资源与算力

- 论文中**未明确给出硬件配置**、GPU 型号或训练时长。  
- 可推测由于使用全卷积网络与多实例聚合，计算资源至少需要 GPU 级别硬件，但尚无公开的算力统计数据。

---

## 5. 实验数量与充分性

- **实验数量**：
  - 3 个独立 IMC 临床数据集；
  - 1 个独立 scRNA-seq 数据集用于机制验证；
  - 约 3 种以上特征池化或频率聚合方案；
  - 与 5 种基线方法进行对比。  
- **评估充分性**：  
  - 覆盖不同疾病类型（代谢病、乳腺癌、脑癌）；  
  - 通过多随机折叠交叉验证（200 folds）提升稳健性；  
  - 生存分析与独立组学验证表明结果具独立可复现性。  
- 整体而言，实验设计**全面且客观**，但缺少消融实验（如去除 SHAP 或量化不同超像素数量的影响）。

---

## 6. 主要结果与发现

- **性能提升**：
  - 在乳腺癌生存分类中 AUC 从 0.56（CANVAS）提高至 **0.63**；
  - 在脑肿瘤分类（GBM vs BrM）中达到 **AUC = 0.88**；
  - 在糖尿病分类中与 CANVAS 持平（AUC = 1.0）。  

- **关键生物学发现**：
  - 在脑癌样本中识别到与生存延长显著相关的“星形胶质细胞–NK 细胞–M1 型巨噬细胞”协作微环境；
  - 通过独立 scRNA-seq 数据集验证该三细胞互作可通过 **XCL1–ADGRV1** 配体-受体通路介导；
  - 基于 scGPT 表征进一步证实该基因通路对患者年龄分层具有显著预测力（准确率 0.8）。

---

## 7. 方法与实验优点

- **创新性**：
  - 首个将多实例学习（MIL）与分位数聚合（quantile aggregation）结合的空间免疫表征框架；
  - 首次在**分割无关（segmentation-free）**模式下实现样本级预后预测。  
- **解释性强**：
  - 结合 SHAP 提供**空间可视化的重要性地图**，揭示免疫微环境级别机制；
  - 与单细胞组学（scRNA-seq）验证互补，支持生物学合理性。  
- **实用性与可拓展性**：
  - 适用于形态复杂的细胞类型（如神经组织）；
  - 可与多组学数据融合，用于未来临床预后分析。

---

## 8. 不足与局限

- **算力与实施细节不透明**：缺乏硬件和复杂度说明，难以评估算法可复现性。  
- **生物学解释精度有限**：虽然验证了个别信号通路，但机制推断仍需实验验证。  
- **消融与泛化分析不足**：未系统评估超参数选择（如超像素数量、聚类 K 值）对结果的影响。  
- **任务局限**：目前仅验证二分类任务（如二元生存、疾病状态），未扩展至连续变量预测或时间序列。  
- **评估依赖公开数据**：还需在真实临床前瞻性数据中进一步测试稳定性。

---

**（完）**
