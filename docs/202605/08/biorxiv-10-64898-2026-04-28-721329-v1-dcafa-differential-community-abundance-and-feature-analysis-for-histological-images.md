---
title: "DCAFA: Differential Community Abundance and Feature Analysis for Histological Images"
title_zh: DCAFA：用于组织学图像的差异群体丰度与特征分析
authors: "Wright, G., Keller, P., Muter, J., Brosens, J., Tejpar, S., Minhas, F."
date: 2026-04-30
pdf: "https://www.biorxiv.org/content/10.64898/2026.04.28.721329v1.full.pdf"
tags: ["query:cellrep"]
score: 8.0
evidence: 对组织学图像中相似实例组进行建模以关联临床结果
tldr: 本文提出DCAFA框架，用于组织学影像的群体组成与特征归因分析。通过聚类得到潜在社区并使用广义线性和混合效应模型进行差异分析，DCAFA能揭示组织结构组成变化与临床结果的关联，在多个医学数据集上验证了有效性。
source: biorxiv
selection_source: fresh_fetch
motivation: 当前分析多关注单一特征，而临床相关信号常源自组织结构组成的变化，亟需对群体层次特征建模。
method: 该方法通过聚类形成潜在社区，分别进行社区组成分析和特征归因分析，结合广义线性及混合效应模型。
result: DCAFA在多种生物医学数据上发现了可解释的组成变化和特定社区内的特征关联，优于传统特征分析。
conclusion: DCAFA为生物医学影像提供了一个统一的统计框架，使组织组成与临床或分子结果的关联分析更加可解释和实用。
---

## 摘要
组织学图像由细胞、腺体或组织片段等多种局部结构组成，这些结构的组织方式和相对丰度反映了潜在的生物学过程。虽然大多数计算方法专注于分析单个特征，但许多与临床相关的信号源于这些结构组成的变化，而非孤立的测量结果。这促使我们需要明确地建模相似实例的群体在不同样本中的变化及其与结果的关系。我们提出了 DCAFA（Differential Community Abundance and Feature Attribution Analysis，差异群体丰度与特征归因分析），这是一个基于回归的框架，用于从组成和特征层面分析分层生物医学数据。DCAFA 将实例分组为潜在社区，代表重复出现的形态学或表型模式，并执行两种互补分析：（i）社区组成分析，用于识别在不同结果中富集或耗竭的群体；（ii）特征归因分析，用于量化实例级特征如何直接或在特定社区内与结果相关。这两种分析均采用广义线性模型和混合效应模型，支持协变量调整，并通过效应量、置信区间和错误发现率控制进行推断。我们在多个生物医学场景中展示了 DCAFA 的实用性，包括子宫内膜组织病理学、空间转录组学、多重免疫荧光成像以及结直肠癌中的预定义细胞类型分析。这些示例揭示了可解释的组成变化和特定背景下的特征关联，而这些通常未能被传统基于特征的方法捕获。通过在单一统计框架中统一差异丰度检验和特征归因，DCAFA 提供了一个开放的工具箱，为生物医学成像数据中组织组成与临床或分子结果之间的关联提供了实用且可解释的分析手段。

代码地址：https://github.com/wgrgwrght/DCAFA

## Abstract
Histological images are composed of diverse local structures such as cells, glands, or tissue patches, whose organisation and relative abundance reflect underlying biological processes. While most computational approaches focus on analysing individual features, many clinically relevant signals arise from changes in the composition of these structures rather than isolated measurements. This motivates the need for explicitly modelling how groups of similar instances vary across samples and relate to outcomes. We present DCAFA (Differential Community Abundance and Feature Attribution Analysis), a regression-based framework for analysing hierarchical biomedical data through both compositional and feature-level perspectives. DCAFA groups instances into latent communities representing recurring morphological or phenotypic patterns, and then performs two complementary analyses: (i) community composition analysis, which identifies groups that are enriched or depleted across outcomes, and (ii) feature attribution analysis, which quantifies how instance-level features relate to outcomes directly or within specific communities. Both use generalised linear and mixed-effects models, enabling covariate adjustment and inference through effect sizes, confidence intervals, and false discovery rate control. We demonstrate the utility of DCAFA across multiple biomedical settings, including endometrial histopathology, spatial transcriptomics, multiplex immunofluorescence imaging, and predefined cell-type analyses in colorectal cancer. These examples identify interpretable compositional shifts and context-specific feature associations that are not captured by conventional feature-based approaches. By unifying differential abundance testing and feature attribution within a single statistical framework, DCAFA serves as an openly available toolbox that provides a practical and interpretable means of linking tissue composition with clinical or molecular outcomes in biomedical imaging data.

Code available at: https://github.com/wgrgwrght/DCAFA

---

## 论文详细总结（自动生成）

# DCAFA：用于组织学图像的差异群体丰度与特征分析 — 中文详细总结

---

## 一、研究背景与核心问题

- **背景与动机**  
  组织学图像由复杂的细胞、腺体和组织结构组成，这些局部结构的空间组织与相对丰度反映了生理和病理状态。  
  当前大多数计算病理学与生物影像分析方法聚焦于**单个特征**（如像素强度或局部嵌入），忽略了结构组成的变化。  
  临床上许多关键信号源自**群体组成的改变**而非单独特征的变化，如免疫浸润、腺体异化或间质比例改变。  
  因此，需要一种能够**显式建模群体结构组成**并定量分析其与临床或分子结果之间关联的框架。  

- **核心问题**  
  如何在高维、层级化的影像数据中——实例（细胞、片段）嵌套在样本（图像或病人）内——系统地量化群体组成与特征在不同条件下的差异性，并进行统计推断。

---

## 二、方法论：DCAFA 框架

### 1. 核心思想
- 提出 **DCAFA（Differential Community Abundance and Feature Attribution Analysis）** ——一种统一的统计框架；
- 将图像中的实例按形态或表型特征分成“**潜在社区（community）**”，再分两步进行：
  1. **社区丰度分析**：识别丰度在不同条件中富集或耗竭的社区；
  2. **特征归因分析**：评估实例特征与结果或社区之间的关联。

### 2. 技术模型
- 建立在 **广义线性模型（GLM）** 与 **广义线性混合效应模型（GLMM）** 之上；
- 支持协变量调整、嵌套结构、误差控制与效应量估计；
- 四类模型设置：
  - 图像级（bag-level）社区丰度分析；
  - 实例级社区分析；
  - 图像级特征归因；
  - 实例级特征回归。

### 3. 关键公式与算法流程
- **社区构建**：  
  实例特征 \(x_p \in \mathbb{R}^d\)，聚类为 K 个社区，得到成员关系 \(m_{pk}\)（可硬或软）。
- **丰度统计**：  
  \[
  c_{ik} = \sum_{p:s(p)=i} m_{pk}, \quad n_i = \sum_{k} c_{ik}
  \]
  表示第 i 张图像在第 k 社区中的实例数量。
- **图像级丰度模型（负二项回归）**：  
  \[
  c_{ik} \sim NB(\mu_{ik}, \alpha_k),\quad \log \mu_{ik} = \beta_{0k} + \beta_k y_i + v_i^T \delta_k + \log n_i
  \]
  其中 \( \beta_k \) 表征社区随结果 \(y_i\) 变化的倍数效应。
- **实例级特征模型（GLMM）**：  
  \[
  g(E[t_{p,r}]) = \alpha_r + \sum_{k} \gamma_{k,r} m_{pk} + v_{s(p)}^T \eta_r + u_{s(p),r}
  \]
  随机项处理同一图像中实例非独立性。
- **算法流程**（Algorithm 1）概述：
  1. 读取图像并提取实例特征；  
  2. 聚类形成社区并计算各社区丰度；  
  3. 拟合回归模型进行丰度与特征分析；  
  4. 输出效应系数与置信区间。

### 4. 可视化与推断
- 使用 **Wald 检验**进行显著性检测；
- 采用 **Benjamini–Hochberg 调整**控制 FDR；
- 可视化包括森林图与热图，直观展示效应大小与显著性。

---

## 三、实验设计与数据场景

### 1. 多个应用场景
论文共在四类生物医学场景中验证 DCAFA：
1. **子宫内膜组织病理学**：检测腺体和核群体组成与基因表达的关系；
2. **结直肠癌空间转录组学**：将空间转录组签名（STS）与局部核形态群体相关联；
3. **多重免疫荧光影像（Orion cohort）**：利用表达谱预测复发；
4. **结直肠癌预定义细胞类型丰度分析**（Valentino cohort）。

### 2. 具体数据统计
- 子宫内膜数据：624 张 WSIs、约 2.3×10^8 个核及 5.3×10^5 个腺体对象；
- 降维后采用 UMAP + k-means 得到 7 个核和腺体社区；
- 分析目标：13 个基因表达及其比值；
- 结直肠癌空间数据：16 张 H&E，全景配准 20 个空间转录组签名（STS），600,000 个核实例；
- 聚类 K=10，关联 INSIGHT 模型的风险区域输出。

### 3. 对比与基线
- 与传统的单一特征平均分析做对比；
- 参考了差异丰度算法 **MILO** 等统计方法；
- 展示了 DCAFA 与 “平均特征回归” 的性能差别：DCAFA 发现了更强的生物学一致性。

---

## 四、资源与算力说明

- 文中未明确说明硬件设备、GPU型号、训练时长或算力使用情况；
- 由于方法以统计建模为主、未涉及深度学习训练，可推测其计算成本主要集中在特征提取与聚类阶段；
- 若使用外部模型（如 ASTER、Cerberus），这些模型的算力需求在本工作中并未详细描述。

---

## 五、实验数量与充分性

- 主体研究包含至少 **两大完整实验（子宫内膜 + 结直肠癌）**，并在附录中提供 **三项补充分析**：治疗响应、复发预测、突变相关形态分析；
- 每一主实验内部含：
  - 多基因、多社区、多特征的统计检验；
  - 热图和森林图展示的回归结果；
- 统计推断控制 FDR，方法公开且参数透明；
- 整体实验设计 **充分且分层覆盖多场景**，但缺少与广泛已有影像分析方法（如深度表征模型）的直接量化对比。

---

## 六、主要发现与结论

1. **群体组成分析**：DCAFA 能检测出与基因表达或疾病状态相关的社区丰度变化；
   - 子宫内膜：揭示特定腺体群体与成熟标志基因（如 *SLC15A2*, *DPP4*, *CXCL14*）的强关联；
   - 核群体（Cluster 6）与免疫细胞标志基因（*IL2RB*, *ITGAD*）显著相关。
2. **特征归因结果**：在空间转录组数据中，转录组签名与不同核形态群体显著对应；
   - 高风险 STS 对应小而圆的紧凑核形态。
3. **统一框架**：可同时在社区丰度与实例特征层面执行统计推断，解释多层次的组织学变化。
4. **开源代码**：提供 Python 工具箱，支持直接在研究者自定义数据上运行。

---

## 七、方法与实验亮点

- 将**差异丰度检测**与**特征归因分析**统一至单一统计框架；
- 支持复杂度高的层级数据（实例—图像—病人）；
- 灵活的社区定义（聚类、软分配、重叠邻域）；
- 使用 GLMM 对同图像实例的相关性建模，保证统计严谨；
- 可直接输出可解释的效应量（如倍数变化、置信区间）；
- 框架通用，可用于多模态数据：病理图像、空间组学、免疫影像等；
- 可视化清晰，结果具强生物学解释性。

---

## 八、不足与局限

- **依赖聚类质量**：社区划分受特征提取与聚类算法影响，若聚类不稳可能导致解释偏差；
- **计算复杂性**：大规模实例聚类计算成本高；
- **极端不平衡数据**（如稀有社区）可能影响模型拟合；
- **仅为关联分析**：结果为统计相关，不具因果解释；需实验验证；
- **对比实验有限**：未与深度学习端到端方法或图结构模型进行系统性能比较；
- **算力信息缺失**：论文未报告硬件环境及效率指标，复现成本不确定。

---

（完）
