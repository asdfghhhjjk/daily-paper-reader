---
title: "DPsurv: Dual-Prototype Evidential Fusion for Uncertainty-Aware and Interpretable Whole Slide Image Survival Prediction"
title_zh: DPsurv：面向全切片图像生存预测的双原型证据融合网络
authors: "Yucheng Xing, Ling Huang, Jingying Ma, Ruping Hong, Jiangdong Qiu, Pei Liu, Kai He, Huazhu Fu, Mengling Feng"
date: 2026-04-30
pdf: "https://openreview.net/pdf/f7ff576288af888c2a3bba3875bf2bf56b896168.pdf"
tags: ["query:cell-path"]
score: 7.0
evidence: 基于全切片图像的生存预测，融合细胞与组织水平信息，具有不确定性和可解释性
tldr: 针对现有WSI生存分析方法可解释性差且忽略预测不确定性的问题，本文提出DPsurv，一种双原型全切片图像证据融合网络。该方法通过补丁原型分布分配、组件原型证据推理输出不确定性感知的生存区间。实验表明，DPsurv提高了生存预测的准确性和可解释性，为细胞与组织水平的预后分析提供了新工具。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 现有WSI生存分析缺乏可解释性且忽视预测不确定性。
method: 提出双原型证据融合网络，利用补丁原型分配和组件证据推理输出生存区间。
result: 方法在生存预测中提供了不确定性区间和可解释的组件贡献。
conclusion: DPsurv为WSI预后分析提供了可解释且不确定性感知的解决方案。
---

## Abstract
Whole-slide images (WSIs) are widely used for cancer survival analysis because of their comprehensive histopathological information at both cellular and tissue levels, enabling quantitative, large-scale, and prognostically rich tumor feature analysis. However, most existing WSI survival analysis methods struggle with limited interpretability and often overlook predictive uncertainty in heterogeneous slide images. In this paper, we propose DPsurv, a dual-prototype whole-slide image evidential fusion network that outputs uncertainty-aware survival intervals, and enables interpretable survival results through patch prototype distribution assignment, component prototype evidence reasoning, and component-wise relative risk aggregation. Experiments on five publicly available datasets demonstrate strong discriminative performance and well-calibrated predictions, validating its effectiveness and reliability. The interpretation of survival results provides transparency at the feature, reasoning, and decision levels, thereby enhancing the trustworthiness and interpretability of DPsurv.

---

## 论文详细总结（自动生成）

> 说明：以下总结仅基于提供的标题、摘要及元数据；PDF 正文因访问验证未实际获取，因此部分细节无法从现有信息中确认。

## 1. 论文的核心问题与整体含义

- **研究背景**：全切片图像（WSI）被广泛用于癌症生存分析，因其包含细胞水平与组织水平的丰富病理信息，可用于定量、大规模且具有预后价值的肿瘤特征分析。
- **核心问题**：
  - 现有多数 WSI 生存分析方法可解释性有限。
  - 在异质性较强的切片图像中，预测不确定性常被忽略。
- **整体含义**：论文提出 **DPsurv**，目标是构建一个既能输出**不确定性感知生存区间**，又能提供**可解释生存结果**的 WSI 生存预测模型，从而提升临床预后分析的可信度与透明性。

## 2. 论文提出的方法论

- **核心思想**：通过“双原型证据融合”同时利用细胞级与组织级信息，将证据推理引入生存预测，输出不确定性感知的风险估计。
- **关键技术组成**（来自摘要与元数据）：
  - **补丁原型分布分配（patch prototype distribution assignment）**：将 WSI 中的局部补丁映射到原型分布，用来表征切片中的细胞/组织模式。
  - **组件原型证据推理（component prototype evidence reasoning）**：基于证据机制对组件原型进行推理，得到带有不确定性的预测证据。
  - **组件相对风险聚合（component-wise relative risk aggregation）**：将组件级相对风险聚合为患者级生存风险。
- **输出形式**：
  - 不确定性感知的生存区间。
  - 多层级的可解释结果：特征级、推理级、决策级。
- **公式 / 算法流程说明**：
  - 当前提供的材料中未给出具体数学公式。
  - 可概括流程为：WSI 输入 → 补丁特征提取 → 补丁原型分布分配 → 组件原型证据推理 → 组件相对风险聚合 → 输出生存区间与解释信息。

## 3. 实验设计

- **数据集**：
  - 使用了 **5 个公开数据集**进行验证。
  - 具体数据集名称在当前提供内容中未列出。
- **实验场景**：
  - 癌症生存分析 / 预后预测。
- **Benchmark 与评估指标**：
  - 摘要提到“strong discriminative performance”和“well-calibrated predictions”，说明主要关注：
    - 判别性能（如生存预测区分能力）。
    - 预测校准性（不确定性估计是否合理）。
  - 未给出具体指标名称（如 C-index、IBS、D-calibration 等）。
- **对比方法**：
  - 当前提供内容未列出具体对比方法。

## 4. 资源与算力

- **未明确说明**。
- 当前提供的标题、摘要与元数据中，未提及：
  - GPU 型号。
  - GPU 数量。
  - 训练时长。
  - 模型参数量或推理开销。
- 因此无法评估其算力需求或训练成本。

## 5. 实验数量与充分性

- **实验规模概况**：
  - 至少覆盖 **5 个公开数据集**。
  - 涉及性能验证、校准性验证和可解释性验证。
- **充分性评价**：
  - 从数据集数量看，多数据集验证有利于展示一定泛化能力。
  - 但由于缺少方法对比、消融实验、统计检验等细节，当前信息不足以判断实验是否完全充分、客观、公平。
- **潜在缺失项**：
  - 未看到消融实验的具体设计。
  - 未看到与 SOTA 方法的定量对比表。
  - 未看到外部验证或多中心验证信息。

## 6. 论文的主要结论与发现

- DPsurv 在 5 个公开数据集上表现出：
  - 较强的判别性能。
  - 良好的预测校准性。
- 方法能输出不确定性感知的生存区间。
- 生存结果可从特征、推理和决策三个层面进行解释。
- 整体结论：DPsurv 为 WSI 预后分析提供了一种**可解释、不确定性感知**的解决方案，同时增强了可信度和透明性。

## 7. 优点

- **不确定性建模**：输出生存区间而非单一风险值，有助于反映预测可靠性，更适合临床风险沟通。
- **多级可解释性**：从补丁/组件到最终决策均有解释路径，比黑箱模型更透明。
- **信息融合**：双原型设计意图同时利用细胞级与组织级病理信息，可能更全面地捕获肿瘤微环境与组织结构。
- **多公开数据集验证**：在 5 个数据集上验证，展示一定泛化潜力。
- **校准性关注**：不仅优化判别性能，还关注预测概率/区间是否校准，这在实际临床决策中很重要。

## 8. 不足与局限

- **信息不完整**：
  - PDF 正文未能获取，许多关键细节缺失。
  - 数据集名称、对比方法、评测指标、统计显著性均未提供。
- **可复现性受限**：
  - 未给出具体公式、双原型定义、组件证据推理实现细节。
  - 未报告代码、模型配置或训练设置。
- **实验评估不透明**：
  - 无法判断对比是否公平，是否包含足够消融实验。
  - 未说明是否在独立外部队列上验证。
- **潜在偏差风险**：
  - 5 个公开数据集可能存在人群、染色、扫描仪等偏差。
  - 生存区间在临床中的可用性需要进一步临床验证。
- **应用限制**：
  - WSI 计算成本较高，但本文缺少算力与效率分析。
  - 可解释性虽然被强调，但未提供定量或人工评估证据。

（完）
