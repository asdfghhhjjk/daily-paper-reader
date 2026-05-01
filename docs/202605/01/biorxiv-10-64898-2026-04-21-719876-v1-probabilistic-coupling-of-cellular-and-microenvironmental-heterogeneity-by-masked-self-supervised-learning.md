---
title: Probabilistic coupling of cellular and microenvironmental heterogeneity by masked self-supervised learning
title_zh: 通过掩码自监督学习实现细胞与微环境异质性的概率耦合
authors: "Kojima, Y., Tanaka, Y., Hirose, H., Chiwaki, F., Nishimura, K., Hayashi, S., Itahashi, K., Ishikawa, M., Shimamura, T., Mano, H."
date: 2026-04-24
pdf: "https://www.biorxiv.org/content/10.64898/2026.04.21.719876v1.full.pdf"
tags: ["query:cellrep"]
score: 9.5
evidence: 基于Transformer的微环境和细胞嵌入学习框架
tldr: 本文提出了Mievformer，一种基于Transformer的掩码自监督学习模型，用于在空间组学数据中学习微环境嵌入，通过整合邻近细胞状态和空间关系来推断细胞与微环境异质性的概率耦合。该方法在模拟和真实数据中显著优于现有算法，能够实现微环境聚类、细胞亚群识别及相关基因表达模式发现。
source: biorxiv
selection_source: fresh_fetch
motivation: 空间组学的出现需要在单细胞尺度上准确解析微环境状态与细胞异质性之间的耦合关系。
method: 采用基于Transformer的掩码自监督学习和InfoNCE优化来学习细胞空间分布的条件概率嵌入。
result: Mievformer在模拟和多平台真实空间组学数据的微环境聚类任务中超过现有方法并展现出更高的生物学解释力。
conclusion: Mievformer为空间组学数据中表征细胞与微环境关系提供了高效且生物学意义丰富的解决方案。
---

## 摘要
空间组学技术已发展到单细胞分辨率，使得能够系统地分析组织微环境以及细胞状态的异质性。然而，在单细胞分辨率下以计算方式定义微环境状态，并识别对生物学发现最具信息性的表示，仍然是主要挑战。本文提出了 Mievformer，这是一种基于 Transformer 的掩码自监督框架，通过编码邻近细胞状态及其相对空间结构，学习微环境嵌入，以参数化在中心空间位置的连续细胞状态的条件分布。通过 InfoNCE 优化，Mievformer 学习的表示能够捕获细胞状态在不同微环境中的相对富集情况，并将其形式化为条件密度比，从而支持微环境与细胞异质性之间耦合的概率推断。Mievformer 在模拟空间转录组数据的生态位聚类中优于现有方法，并在跨越三种空间转录组平台的五个真实数据集中获得最高平均性能，其评估指标为 DREC——一种无真实标签的度量，在模拟中与真实标签性能的相关性最强。除常规聚类之外，Mievformer 还可基于微环境分布识别细胞亚群体，并检测与特定细胞群体共定位相关的基因表达特征。这些结果共同确立了 Mievformer 作为一种定量稳健且具有生物学信息量的空间组学微环境表示学习框架。

## Abstract
AO_SCPLOWBSTRACTC_SCPLOWSpatial omics technologies have advanced to single-cell resolution, enabling systematic analysis of tissue microenvironments alongside cellular-state heterogeneity. However, computationally defining microenvironmental states at single-cell resolution and identifying representations most informative for biological discovery remain major challenges. Here we present Mievformer, a Transformer-based masked self-supervised framework that learns microenvironmental embeddings by encoding neighboring cellular states and relative spatial configurations to parameterize the conditional distribution of continuous cell states at central spatial positions. Through InfoNCE optimization, Mievformer learns representations that capture the relative enrichment of cell states across microenvironments, formalized as a conditional density ratio, thereby enabling probabilistic inference of the coupling between microenvironmental and cellular heterogeneity. Mievformer outperformed existing methods in niche clustering on simulated spatial transcriptomics data and achieved the highest average performance across five real datasets spanning three spatial transcriptomics platforms when evaluated using DREC, a ground-truth-free metric that most strongly correlated with ground-truth performance in simulations. Beyond conventional clustering, Mievformer enables identification of cellular subpopulations based on their microenvironmental distribution and detection of gene-expression signatures associated with colocalization of specific cell populations. Together, these results establish Mievformer as a quantitatively robust and biologically informative framework for learning microenvironment representations in spatial omics.

---

## 论文详细总结（自动生成）

# 论文总结：通过掩码自监督学习实现细胞与微环境异质性的概率耦合  

---

## 1. 研究背景与核心问题  

- **研究动机**：  
  随着空间组学技术发展到单细胞分辨率，研究者可以在细胞层面同时获取空间位置和基因表达信息。这使得探索细胞状态的异质性及其所在的微环境成为可能。  
- **核心难题**：  
  传统空间转录组学方法难以在单细胞层面上准确定义“微环境状态”，原因在于：  
  - 微环境通常由多种不同细胞类型组成；  
  - 以邻域平均或局部聚合为基础的传统算法会损失空间分辨率；  
  - 没有统一的标准指标来度量“微环境表示”是否保留生物学意义。  
- **研究目标**：  
  作者旨在建立一种能够同时捕获细胞与其邻近微环境之间**概率耦合关系**的模型，使其能从空间组学数据中学习具有高解释力的微环境嵌入。

---

## 2. 方法论：Mievformer 框架  

### 2.1 核心思想  
Mievformer 是一种 **基于 Transformer 的掩码自监督学习系统**，利用邻近细胞状态及空间位置信息推断目标位置的条件细胞状态分布。

### 2.2 模型结构与流程  
- **输入**：  
  每个细胞的基因表达向量（经 PCA 降维）、空间坐标。  
- **掩码机制**：  
  在训练时，将中心细胞的状态掩码，仅提供其邻域信息。  
- **Transformer 编码器（NicheEncoder）**：  
  - 输入序列包括中心掩码 token及邻居细胞的嵌入向量+位置编码（sin/cos 相对坐标编码）。  
  - 经多层自注意力网络处理后，输出一个微环境表征向量 `e_i`。  
- **分布推断（Distributor 模块）**：  
  通过得分函数  
  \[
  s_\theta(e_i, z_j) = w_e(e_i)^T w_z(z_j) + b_z(z_j)
  \]  
  计算任意细胞状态 `z_j` 在微环境 `e_i` 中出现的概率，采用 Softmax 归一化：  
  \[
  P_{ij} = \frac{e^{s_\theta(e_i, z_j)}}{\sum_{j'} e^{s_\theta(e_i, z_{j'})}}
  \]  
  并利用 **InfoNCE 损失**最大化真实配对概率 \( P_{ii} \)。  
- **训练目标**：最大化中心细胞与其微环境表征间的互信息，使得模型学习到的 `e_i` 参数化条件密度比 \( p(z|e)/p(z) \)。  
- **推理阶段**：  
  - 可计算细胞对微环境的**后验分布** \( p(e|z)/p(e) \)。  
  - 推导细胞群体在特定微环境中的**存在密度**；  
  - 实现下游任务：微环境聚类、细胞亚群识别、共定位相关基因分析。

---

## 3. 实验设计  

### 3.1 模拟数据  
- 构建了多层环状结构的仿真实验（inner/boundary/outer 三层），模拟典型组织结构如滤泡或管状组织。  
- 对比方法包括：  
  - **NicheCompass**, **CellCharter**, **Banksy**, **GraphST**, **STAGATE**, **COVET**, 及简单基线（PCA / raw 坐标）。  
- 通过 **Adjusted Rand Index (ARI)** 衡量聚类准确度。  

### 3.2 真实数据  
- 共使用五个真实空间转录组数据集：  
  - Xenium 平台（胰腺癌、肺癌、胶质母细胞瘤）  
  - Stereo-seq 小鼠脑  
  - Visium HD 小鼠脑  
- 主要评估指标：**DREC（Dual Recovery）**。此指标与仿真中真实标注的相关性最高。  
- 额外提出 CAS、SCAS、NEA 三种自定义度量，并与 NicheCompass 原有四项指标对比验证其相关性。  

---

## 4. 资源与算力  

- 论文中提及模型实现基于 **PyTorch / PyTorch Lightning** 框架，采用 **AdamW 优化器**、学习率 1e-3，训练 1000 epoch，早停耐心 20。  
- 文中未具体说明 GPU 型号或数量、训练用时或算力配置，因此算力资源**未明确披露**。  

---

## 5. 实验数量与充分性  

- **模拟实验**：测试不同参数（边界厚度、微环境模式数量）下的性能稳健性，共计多组仿真。  
- **真实数据**：横跨三大平台、五个数据集，涵盖不同组织与疾病类型。  
- **度量验证**：在仿真中系统比较 8 种指标与真实性能的相关性，确保评价方法科学公正。  
- 整体来看，实验设计覆盖广泛且系统，结果具有较高的统计与生物学可信度。

---

## 6. 主要结论与发现  

- Mievformer 能有效学习微环境的条件概率表示，在模拟数据中 **ARI 最高**，真实数据中 **平均 DREC 第一**。  
- 模型可在单细胞分辨率下推断：  
  - 各细胞类型在不同微环境中的分布概率；  
  - 微环境特异性细胞亚群；  
  - 基因表达与细胞共定位模式的相关性。  
- 案例包括：  
  - 肺癌数据中区分纤维母细胞和肿瘤微环境的细粒度分层；  
  - 胰腺癌数据中发现肿瘤细胞与成纤维细胞共定位时 **MYC** 表达显著升高，与免疫组化验证一致。

---

## 7. 方法亮点与优点  

- **创新性算法**：首次将条件密度比 \( p(z|e)/p(z) \) 的概率建模引入空间组学微环境学习。  
- **高分辨率保持**：不依赖邻域平均，保留单细胞尺度空间信息。  
- **双向推断能力**：同时支持从微环境到细胞状态、以及反向从细胞到微环境的推理。  
- **度量创新**：提出 DREC 作为无标签性能评估的新指标，验证中与真实标签高度相关。  
- **生物学解释力强**：通过概率建模衍生出可解释的细胞群密度、分布和共定位基因关系。

---

## 8. 不足与局限  

- **结构层次限制**：当前版本只能捕获局部连续微环境，难以描述层级或跨尺度的复杂空间结构。  
- **多样本整合能力有限**：目前聚焦单组织样本分析，未引入批次校正或跨样本共享嵌入机制。  
- **算力与效率信息不详**：论文未报告训练硬件与时长，模型复杂度或资源需求无法评估。  
- **高阶生物学验证有限**：虽有免疫组化验证，但尚未在大规模临床样本中实证其广泛有效性。  

---

**（完）**
