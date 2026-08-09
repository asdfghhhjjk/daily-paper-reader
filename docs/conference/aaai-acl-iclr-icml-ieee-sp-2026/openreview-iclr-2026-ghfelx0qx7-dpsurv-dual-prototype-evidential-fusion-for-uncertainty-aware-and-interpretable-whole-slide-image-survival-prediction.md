---
title: "DPsurv: Dual-Prototype Evidential Fusion for Uncertainty-Aware and Interpretable Whole Slide Image Survival Prediction"
title_zh: DPsurv：面向不确定性感知与可解释全切片图像生存预测的双重原型证据融合
authors: "Yucheng Xing, Ling Huang, Jingying Ma, Ruping Hong, Jiangdong Qiu, Pei Liu, Kai He, Huazhu Fu, Mengling Feng"
date: 2025-09-03
pdf: "https://openreview.net/pdf?id=gHFeLx0QX7"
tags: ["query:path-xai-sel"]
score: 8.0
evidence: 通过补丁原型分配实现可区分的区域可解释WSI生存预测
tldr: 现有WSI生存分析方法可解释性差且忽略预测不确定性。DPsurv提出双原型证据融合网络，输出不确定性感知的生存区间，并通过补丁原型分配图、组件原型和组件相对风险实现预测解释，使临床决策更透明。实验表明该方法在生存预测准确性和可解释性间取得平衡。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: WSI生存分析缺乏可解释性和不确定性量化。
method: 双原型证据融合网络，输出不确定性感知生存区间。
result: 提供可解释的补丁原型图，平衡预测准确性与可解释性。
conclusion: DPsurv为临床决策提供透明、可靠的生存预测。
---

## Abstract
Pathology whole-slide images (WSIs) are widely used for cancer survival analysis because of their comprehensive histopathological information at both cellular and tissue levels, enabling quantitative, large-scale, and prognostically rich tumor feature analysis. However, most existing methods in WSI survival analysis struggle with limited interpretability and often overlook predictive uncertainty in heterogeneous slide images. In this paper, we propose DPsurv, a dual-prototype whole-slide image evidential fusion network that outputs uncertainty-aware survival intervals, while enabling interpretation of predictions through patch prototype assignment maps, component prototypes, and component-wise relative risk aggregation. Experiments on five publicly available datasets achieve the highest mean concordance index and the lowest mean integrated Brier score, validating the effectiveness and reliability of DPsurv. The interpretation of prediction results provides transparency at the feature, reasoning, and decision levels, thereby enhancing the trustworthiness and interpretability of DPsurv.

---

## 论文详细总结（自动生成）

好的，以下是基于提供的论文元数据和摘要生成的结构化中文总结。

---

## 1. 论文的核心问题与整体含义

- **核心问题**：在癌症生存分析领域，全切片图像（WSI）虽能提供细胞和组织层面的丰富预后信息，但现有的WSI生存分析方法存在两大瓶颈：**可解释性差**（模型决策过程不透明，难以被病理医生理解和信任）和**忽视预测不确定性**（对高度异质的WSI仅给出点估计，缺乏对预测置信度的可靠评估）。
- **整体含义**：为弥补上述不足，本文提出 **DPsurv（双重原型证据融合网络）**，旨在构建一种既能输出**不确定性感知的生存区间**、又能通过**可区分的补丁原型分配、组件原型和组件相对风险聚合**来提供多层级解释的生存预测模型，从而提升临床决策的透明度和可信度。

## 2. 论文提出的方法论

- **核心思想**：
  - 采用**双原型（dual-prototype）证据融合**机制，将WSI建模为多个局部补丁的原型表示，并利用证据理论（evidential theory）输出**生存时间的预测区间**，而非单一的点估计，以此量化模型对预测的确定性。
  - 通过**补丁原型分配图**、**组件原型**和**组件级相对风险聚合**三个层次实现预测的可解释性，使临床人员可以从特征、推理到决策层面理解模型的依据。
- **关键技术细节**：
  - **双原型结构**：从WSI中提取补丁特征后，通过两组原型（可能是实例级原型和组件级原型）进行编码与融合，以捕获多尺度的组织形态学模式。
  - **证据深度生存模型**：基于证据回归或类似框架，输出生存分布的参数化表示（如Weibull分布），同时给出**认知不确定性**和**偶然不确定性**，最终形成包含置信度的生存区间。
  - **可解释性设计**：补丁到原型的分配权重可视化生成**原型分配图**；**组件原型**代表可归纳的组织成分；通过对组件相对风险的聚合，展示各形态学模式对预后的正向或负向影响。
- **算法流程**（据摘要推断）：
  1. 补丁特征提取 → 2. 双原型映射与分配 → 3. 证据融合与生存分布预测 → 4. 输出生存区间 + 不确定性 → 5. 生成多级解释（原型图、组件贡献、相对风险）。

## 3. 实验设计

- **数据集**：在**五个公开可用的癌症病理WSI数据集**上进行了验证（具体名称未在摘要中列出，但通常可能包括TCGA等大型癌症基因组图谱相关的WSI生存数据集）。
- **基准指标**：
  - **一致性指数**：评价生存排序准确性，追求最高均值。
  - **综合Brier分数**：评价生存概率校准度，追求最低均值。
- **对比方法**：摘要未列出对比方法具体名称，但通常应包括当前主流的WSI生存分析模型，如基于MIL的方法（如DeepAttnMISL、CLAM）、基于图的方法（如Patch-GCN）、基于Transformer的方法以及可能的不确定性量化方法。

## 4. 资源与算力

- **文中未明确说明**GPU型号、数量、训练时长等具体算力信息。根据提供的文本，无法获得相关数据。

## 5. 实验数量与充分性

- **实验规模推断**：
  - 在**5个数据集**上进行了评估，范围较广，增强了结果的泛化性。
  - 必定包含与多个现有方法的对比实验（文中虽未列出方法数，但作为顶会投稿一般覆盖5~10种SOTA）。
  - 很可能包含**消融实验**（验证双原型、证据融合、可解释模块的必要性）以及不确定性质量评估。
- **实验充分性与公平性评价**：
  - 多数据集、多指标（一致性指数与综合Brier分数）的设计较为客观，从准确性和校准度两个维度进行了验证。
  - 从摘要看，“achieve the highest mean concordance index and the lowest mean integrated Brier score”表明在主要指标上达到最优，可认为实验有说服力。但未给出具体数值和标准差，无法判断显著性水平。

## 6. 论文的主要结论与发现

- **有效性**：DPsurv在五个公开数据集上取得了最高的平均一致性指数和最低的平均综合Brier分数，证明其在生存预测准确性和概率校准方面均优于现有方法。
- **可靠性**：输出的不确定性感知生存区间能够为临床提供更可靠的预测参考。
- **可解释性**：通过特征层（原型分配图）、推理层（组件原型）和决策层（相对风险聚合）三个级别的解释，做到全流程透明，有利于病理医生理解模型决策依据，增强信任。

## 7. 优点

- **多层级可解释性设计**：创新性地将原型学习与生存分析结合，提供从补丁到全局决策的透明推理链，这是对传统“黑箱”WSI生存模型的重要突破。
- **不确定性量化**：引入证据理论输出生存区间而非点估计，使模型对不可靠样本（如异质性很高、训练分布稀疏的区域）能够“自知其不知”，非常适合高风险医疗场景。
- **综合性评估**：同时考察辨别能力（C-index）和校准性能（IBS），且在多数据集上验证，结论较为稳健。

## 8. 不足与局限

- **算力与实现细节缺失**：摘要未报告计算资源需求，无法评估其实际部署的算力门槛和训练效率。
- **数据信息模糊**：未说明五个数据集的具体名称、样本量及癌种覆盖范围，可能夸大规模和泛化性；也未提供对比方法的详细列表和结果数值，无法独立评判其进步幅度与显著性。
- **方法论细节不详**：摘要未给出双原型的具体结构、证据融合的数学形式，难以评估方法的新颖性和复杂度。
- **可解释性评估主观性**：尽管提供了可解释输出，但摘要未描述是否有临床医生参与验证或使用标准可解释性评估指标（如医生评分、定位准确性），可信度的量化评价尚缺。
- **应用限制**：仅基于病理图像，未融合基因组学、临床指标等多模态数据，这可能限制了其在真实世界精准肿瘤学中的潜力。不确定性区间的临床实用性（如是否校准良好、区间的宽度是否可接受）需进一步验证。

（完）
