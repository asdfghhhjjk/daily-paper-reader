---
title: Foundation cell segmentation models performance on live microscopy and spatial-omics data
title_zh: 基础细胞分割模型在活体显微镜与空间组学数据上的性能
authors: "Miao, Y., Surguladze, N., Lerner, J., Poysungnoen, K., Ariano, K., Li, Y., Zhu, Y., Van Batavia, K., Jepson, J., Van De Klashorst, J., Ni, B. Y. X., Armstrong, A., Rahman, R., Horstmeyer, R., Hickey, J. W."
date: 2026-04-21
pdf: "https://www.biorxiv.org/content/10.64898/2026.04.18.719315v1.full.pdf"
tags: ["query:sam"]
score: 9.0
evidence: 评估基于SAM的模型在显微镜和空间组学中的细胞分割性能
tldr: 该研究系统比较了多种通用深度学习细胞分割模型在不同显微成像任务上的性能，发现模型表现依赖于数据类型，其中Cellpose-SAM在相差图像中效果最佳，但不同模型在多重荧光组织图像中各有优劣，提示需按数据特征选择分割模型。
source: biorxiv
selection_source: fresh_fetch
motivation: 目前缺乏针对通用细胞分割模型在生物学下游分析层面的系统比较。
method: 本文系统评估了多种通用细胞分割模型在不同显微成像数据上的表现。
result: Cellpose-SAM在相差图像中表现最佳，SAM类模型在荧光细胞培养数据中稳定，而在CODEX数据上无单一模型全面优胜。
conclusion: 研究表明应根据数据特性和分析目标选择分割模型，而非依赖单一通用方案。
---

## 摘要
准确的细胞分割是生物影像数据定量分析的关键步骤。近年来，深度学习的进展促成了通用分割模型的发展，这些模型在多种成像模态中均表现出稳健的性能，包括无标记相差成像、荧光细胞培养成像以及多重荧光组织成像。然而，对这些模型在下游生物学分析层面的系统性比较仍然有限。为填补这一空白，我们评估了多个近期的分割模型，包括 Cellpose cyto3、Cellpose-SAM、{micro}SAM 和 CellSAM，在相差和荧光细胞培养图像上的表现。此外，我们还将 Mesmer 和 InstanSeg 纳入基准测试，用于评估通过 CO-Detection by IndEXing（CODEX）生成的多重荧光组织图像。我们发现，Cellpose-SAM 在相差图像上表现出色，而基于 SAM 的模型在荧光细胞培养数据上均表现稳健。相比之下，没有单一模型在 CODEX 数据集上始终优于其他模型。不同模型各自展现出独特的优势与局限，导致下游分析（包括聚类和细胞类型识别）结果存在差异。总体而言，我们的研究强调应根据数据集特征和分析目标选择分割模型，而非依赖单一的通用方案。

## Abstract
Accurate cell segmentation is an essential step for quantitative analysis of biological imaging data. Recent advances in deep learning have led to the development of generalist segmentation models that perform robustly across multiple imaging modalities, including label-free phase contrast, fluorescence cell culture, and multiplexed fluorescence tissue imaging. However, systematic comparisons of these models at the level of downstream biological analysis remain limited. To address this gap, we evaluated several recent segmentation models, including Cellpose cyto3, Cellpose-SAM, {micro}SAM, and CellSAM, on phase contrast and fluorescence cell culture images. In addition, Mesmer and InstanSeg were included for benchmarking on multiplexed fluorescence tissue images generated using CO-Detection by IndEXing (CODEX). We found that Cellpose-SAM achieved strong performance on phase contrast images, while SAM-based models consistently performed well on fluorescence cell culture data. In contrast, no single model consistently outperformed others on CODEX datasets. Instead, each model exhibited distinct strengths and limitations, which led to differences in downstream analyses, including clustering and cell type identification. Together, our study emphasizes the importance of selecting segmentation models based on dataset characteristics and analytical goals, rather than relying on a single universal approach.

---

## 论文详细总结（自动生成）

# 基础细胞分割模型在活体显微镜与空间组学数据上的性能 — 深度总结

---

## 一、研究核心问题与背景

- **核心问题**：细胞分割是定量生物影像分析的前提和关键步骤，决定下游如形态测量、特征提取和细胞类型识别的准确性。  
- **现有挑战**：  
  - 不同成像模态（如相差显微镜、荧光细胞培养、空间组学组织成像）间存在显著差异，导致模型难以跨模态泛化。  
  - 当前的对比研究主要停留在“掩膜级别指标”（IoU、AP、F1），未能系统评估分割差异对生物学分析的影响。  
- **研究动机**：弥补分割模型比较研究的不足，建立涵盖多成像模态且关注下游生物学解释的综合评价框架。  
- **研究目标**：比较多种近期主流的深度学习细胞分割模型在活体显微镜与空间组学场景的性能表现与生物意义。

---

## 二、方法论与技术框架

### 1. 核心思想

- 建立一个**双重评价框架**：既评估模型的分割性能（掩膜级别指标），又考察分割差异对**下游生物学分析（聚类、细胞类型识别）**的影响。
- 将**基于 Segment Anything Model (SAM)** 的新型分割模型与传统通用模型（如 Cellpose）进行系统比较。

### 2. 使用模型与体系结构

- **通用模型**：Cellpose cyto3  
- **SAM系列模型**：
  - Cellpose-SAM：融合 SAM 的视觉特征与 Cellpose 的流场重建策略。  
  - μSAM（micro-SAM）：自动生成提示（prompts），基于 ViT-L 架构。  
  - CellSAM：完全基于 SAM 提示编码和掩膜解码策略。  
- **组织专用模型**：
  - Mesmer：在空间荧光组织成像中表现良好。  
  - InstanSeg：强调计算效率与可移植性。

### 3. 评估指标与算法流程

- **掩膜级别指标**：
  - IoU（交并比）；
  - Average Precision（AP）；
  - Segmentation Accuracy（SEG）；
  - F1 Score。
- **下游生物学分析流程**：
  1. 从分割掩膜中提取每个细胞的多通道荧光强度；
  2. 进行 z-score 标准化；
  3. Leiden 聚类；
  4. 手动或半自动注释为细胞类型；
  5. 对比混合聚类比例、纯簇数等指标。

---

## 三、实验设计与数据集

- **数据类型**：
  1. *相差显微镜图像*：活体鼠黑色素瘤细胞（B16-F10）及人肺癌细胞（A549）。  
  2. *荧光细胞培养图像*：固定的 A549 细胞，双通道（核+细胞膜标记）。  
  3. *空间组学组织图像*：来自 HuBMAP 的人类大、小肠 CODEX 数据（8个样本、40+蛋白标记）。  

- **对比模型**：Cellpose cyto3、Cellpose-SAM、μSAM、CellSAM、Mesmer、InstanSeg，共六种。

- **Benchmark与参考**：与 HuBMAP 官方 Cytokit 分割结果以及人类专家注释进行对照。

- **评估维度**：
  - 掩膜数量与平均面积；
  - 基于真实标注的准确度指标；
  - 分割掩膜间一致性（模型间互匹配 IoU）；
  - 下游聚类纯度与数据污染度。

---

## 四、资源与算力

- **计算设备**：单张 NVIDIA RTX 4080 GPU。  
- **运行时间对比**：
  - CellSAM：约 8 小时（每个组织区域约 60 分钟），耗时最长；
  - μSAM：约 33 分钟（4 分钟/区域）；
  - Mesmer：约 25 分钟（3 分钟/区域）；
  - Cellpose-SAM：约 16 分钟（2 分钟/区域）；
  - InstanSeg、Cellpose cyto3：约 6 分钟（每区域 < 1 分钟）。  
- **训练信息**：
  - 仅 Cellpose-SAM 执行了数据集特定的微调（fine-tuning），采用人机交互标注；其他模型使用预训练权重。  
- **结论**：训练和推理资源消耗明确报告，符合可复现性要求。

---

## 五、实验数量与充分性

- **阶段性实验设计**：
  1. 相差显微镜分割性能验证（含微调实验）；  
  2. 荧光细胞培养对比；  
  3. CODEX 空间组学全组织分割与下游聚类分析。  
- **消融与稳健性测试**：
  - 高低信噪比验证、模糊信号鲁棒性、弱核信号敏感性等多维分析。  
  - 对模型间掩膜一致性与下游混合聚类比例进行定量评估。  
- **充分性**：实验覆盖三种典型成像模态，评估指标多样，结果较为全面和客观；报告了模型参数及运行条件，公正性较高。

---

## 六、主要结论与发现

- **相差显微镜图像**：Cellpose-SAM 分割最准确，可通过少量微调进一步优化。  
- **荧光细胞培养图像**：所有 SAM 系列模型与人工分割精度相当，具较强抗噪能力。  
- **CODEX 多重组织图像**：  
  - 无单一模型全面胜出；  
  - SAM 系列（Cellpose-SAM、μSAM、CellSAM）预测结果最相似；  
  - μSAM 与 CellSAM 在弱信号组织区域检测更全面；  
  - InstanSeg 和 Cellpose cyto3计算最快，但部分细胞检测缺失；  
  - 分割掩膜差异直接影响下游细胞类型分辨率与混合比例。  
- **生物学分析层面**：分割差异可改变特定细胞比例（如上皮胞系、免疫亚群），从而影响结论的生物学解释。

---

## 七、优点与亮点

- **方法学创新**：
  - 首次提出同时考察“分割质量”与“下游分析影响”的评价框架。  
  - 融合 SAM 架构与细胞流场特征生成的优化方案。  
- **实验设计全面**：覆盖多模态成像和多级分析（视觉质检 + 生物学验证）。  
- **可复现性强**：数据、代码、标注及预训练模型均公开。  
- **实用指导性**：为研究者提供按数据类型选择分割模型的明确建议。

---

## 八、不足与局限

- **数据范围**：仅测试三种成像模态（细胞培养与肠组织），尚未覆盖更广的组织类型。  
- **评估指标局限**：虽扩展至下游分析，但未系统考察时序动态或三维成像。  
- **模型偏差风险**：部分模型的预训练数据分布与实验数据相差较大，可能影响泛化性。  
- **计算成本高**：CellSAM 虽精度高，但运行时间长，难以应用于大规模数据。  
- **人工注释依赖**：下游聚类纯度分析仍依靠人工确认，存在主观性。

---

**（完）**
