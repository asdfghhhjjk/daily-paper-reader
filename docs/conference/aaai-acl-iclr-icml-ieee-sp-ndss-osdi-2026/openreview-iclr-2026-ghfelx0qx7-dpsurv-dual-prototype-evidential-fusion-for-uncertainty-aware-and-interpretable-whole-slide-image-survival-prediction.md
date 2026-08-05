---
title: "DPsurv: Dual-Prototype Evidential Fusion for Uncertainty-Aware and Interpretable Whole Slide Image Survival Prediction"
title_zh: DPsurv：面向不确定性感知和可解释的全切片图像生存预测的双原型证据融合
authors: "Yucheng Xing, Ling Huang, Jingying Ma, Ruping Hong, Jiangdong Qiu, Pei Liu, Kai He, Huazhu Fu, Mengling Feng"
date: 2025-09-03
pdf: "https://openreview.net/pdf?id=gHFeLx0QX7"
tags: ["query:path-xai-sel"]
score: 9.0
evidence: 利用补丁原型分配图解释生存预测，突出显著补丁
tldr: 提出DPsurv网络，通过双原型证据融合实现全切片图像生存预测的不确定性感知和可解释性，利用补丁原型分配图识别重要区域并提供风险解读。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 现有全切片图像生存分析方法可解释性有限且忽略预测不确定性。
method: 提出双原型证据融合网络，通过补丁原型分配、组件原型和风险比实现解释。
result: 在病理全切片图像生存预测中提供可解释的区域识别和不确定性区间。
conclusion: 为全切片图像预后分析提供了可解释且可靠的工具。
---

## Abstract
Pathology whole-slide images (WSIs) are widely used for cancer survival analysis because of their comprehensive histopathological information at both cellular and tissue levels, enabling quantitative, large-scale, and prognostically rich tumor feature analysis. However, most existing methods in WSI survival analysis struggle with limited interpretability and often overlook predictive uncertainty in heterogeneous slide images. In this paper, we propose DPsurv, a dual-prototype whole-slide image evidential fusion network that outputs uncertainty-aware survival intervals, while enabling interpretation of predictions through patch prototype assignment maps, component prototypes, and component-wise relative risk aggregation. Experiments on five publicly available datasets achieve the highest mean concordance index and the lowest mean integrated Brier score, validating the effectiveness and reliability of DPsurv. The interpretation of prediction results provides transparency at the feature, reasoning, and decision levels, thereby enhancing the trustworthiness and interpretability of DPsurv.

---

## 论文详细总结（自动生成）

由于提供的论文文本受验证页面阻挡，无法获取全文，以下总结基于论文标题、摘要及元数据中的动机、方法、结果和结论字段展开，信息可能不够详尽。

## 1. 论文的核心问题与整体含义
- **研究背景**：病理全切片图像（WSI）在癌症生存分析中具有重要价值，能提供细胞与组织层面的综合预后信息。
- **核心问题**：现有WSI生存分析方法存在两大痛点：
  - 可解释性有限，难以揭示模型决策的依据。
  - 忽视预测的不确定性，尤其面对异质性组织图像时，缺乏对预测置信度的量化。
- **整体含义**：提出DPsurv，旨在同时解决不确定性感知和可解释性缺失的问题，为WSI生存预测提供更可信、透明的工具。

## 2. 方法论
- **核心思想**：构建双原型证据融合网络，通过补丁原型（patch prototype）分配和组件式风险聚合，实现可解释的生存预测，并输出不确定性感知的生存区间。
- **关键技术细节**：
  - **补丁原型分配**：将WSI中的图像补丁分配给不同的原型，生成补丁原型分配图，用于解释显著区域。
  - **组件原型与风险比**：利用组件原型和逐成分的相对风险聚合，实现决策级别的解释。
  - **证据融合**：采用证据理论（evidential fusion）输出生存预测的不确定性（可能以置信区间或分布的形式体现）。
- **流程**：端到端地输入WSI，通过双原型网络进行特征提取、原型匹配、风险聚合，最终输出生存预测及其不确定性，并同步提供多层级解释（特征级、推理级、决策级）。

## 3. 实验设计
- **数据集**：五个公开可用的WSI生存分析数据集（具体名称未在摘要和元数据中说明）。
- **Benchmark与对比方法**：摘要提到与现有方法对比，计算平均一致性指数（mean concordance index）和平均综合Brier评分（mean integrated Brier score），表明对比的是生存预测领域的常见指标。但具体对比方法未列出。
- **评价指标**：一致性指数（区分能力）和综合Brier评分（校准度与预测准确度）。

## 4. 资源与算力
- 未在现有信息中提及GPU型号、数量、训练时长等算力细节。因无法获取全文，此部分缺失。

## 5. 实验数量与充分性
- 已报告的结果包括：在五个公开数据集上取得最高平均一致性指数和最低平均综合Brier评分，表明进行了多数据集验证。
- 可能包含消融实验（如原型有效性、不确定性建模等），但摘要和元数据未提供细节。以现有信息判断，实验跨数据集，具备一定的客观性与充分性，但具体实验组数未知。

## 6. 主要结论与发现
- DPsurv在五个数据集上实现最优的生存预测性能（区分力与校准度）。
- 方法可同时提供补丁级重要性解释和不确定性量化，增强了模型的可信度与可解释性。
- 为病理WSI的预后分析提供了一个可解释且可靠的新工具。

## 7. 优点
- **双重能力**：将不确定性与可解释性统一到同一生存预测框架中，相较于现有方法更具综合性。
- **多层解释**：覆盖特征、推理和决策三个层级，使模型内部运作更透明。
- **强实证表现**：在多个公开数据集上取得领先的性能，兼具区分力与校准度优势。
- **临床友好**：通过突出显著补丁和风险归因，利于病理医生理解和信任模型输出。

## 8. 不足与局限
- **技术细节不明**：由于未获全文，双原型的具体定义、证据融合的数学细节、不确定性输出的形式（如分布假设）等关键信息缺失。
- **实验覆盖未知**：未说明是否与最新的可解释生存模型或不确定性感知模型进行对比；数据集特性（癌种、规模、比例）未披露，难以评估泛化性。
- **偏差风险**：若数据集来源单一或标注方式存在系统偏差，可能影响结论的普适性。
- **应用限制**：原型分配的解释依赖于原型质量，对WSI染色变异、扫描仪差异的稳健性未经验证；不确定性区间在临床决策中的实际效用未经外部验证。
- **算力未报告**：无法评估方法的资源需求和可复现性难度。

（完）
