---
title: Do Multiple Instance Learning Models Transfer?
title_zh: 多实例学习模型是否具备迁移能力？
authors: "Daniel Shao, Richard J. Chen, Andrew H. Song, Joel Runevic, Ming Y. Lu, Tong Ding, Faisal Mahmood"
date: 2025-05-01
pdf: "https://openreview.net/pdf?id=hfLqdquVt3"
tags: ["query:cell-path"]
score: 5.0
evidence: 计算病理学全切片图像嵌入与临床结局预测的多实例学习
tldr: 该研究针对计算病理学中多实例学习模型迁移性未知的问题，系统评估了11个预训练MIL模型在19个病理任务上的迁移能力，涵盖组织分型、癌症分级和分子亚型预测。实验揭示了不同预训练任务对下游性能的影响模式，为小样本临床数据集下的模型选择提供了指导。该工作填补了计算病理学中MIL迁移学习的空白，有助于提升弱监督全切片图像分析的实用性。
source: ICML-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-icml-2025-hflqdquvt3/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 846, \"height\": 758}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-hflqdquvt3/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 836, \"height\": 811}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-hflqdquvt3/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 832, \"height\": 595}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-hflqdquvt3/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 846, \"height\": 544}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-hflqdquvt3/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 821, \"height\": 529}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-hflqdquvt3/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 808, \"height\": 599}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-hflqdquvt3/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1775, \"height\": 1937}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-hflqdquvt3/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1714, \"height\": 1709}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-icml-2025-hflqdquvt3/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1778, \"height\": 667}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-hflqdquvt3/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1690, \"height\": 633}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-hflqdquvt3/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 861, \"height\": 606}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-hflqdquvt3/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 892, \"height\": 252}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-hflqdquvt3/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 848, \"height\": 369}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-hflqdquvt3/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1665, \"height\": 480}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-hflqdquvt3/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1548, \"height\": 391}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-hflqdquvt3/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1122, \"height\": 412}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-hflqdquvt3/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1229, \"height\": 1957}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-hflqdquvt3/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 564, \"height\": 608}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-hflqdquvt3/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1821, \"height\": 1120}]"
motivation: 计算病理学中MIL模型受限于小样本临床数据，其迁移学习能力尚未被探索。
method: 系统评估11个预训练MIL模型在19个病理任务上的迁移性能，涵盖组织分型、分级和分子亚型预测。
result: 揭示了预训练MIL模型在不同病理任务上的迁移效果差异，提供了选择依据。
conclusion: 预训练MIL模型可以作为计算病理学数据稀缺场景下的有效迁移起点。
---

## Abstract
Multiple Instance Learning (MIL) is a cornerstone approach in computational pathology for distilling embeddings from gigapixel tissue images into patient-level representations to predict clinical outcomes. However, MIL is frequently challenged by the constraints of working with small, weakly-supervised clinical datasets. Unlike fields such as natural language processing and computer vision, which effectively use transfer learning to improve model quality in data-scarce environments, the transferability of MIL models remains largely unexplored. We conduct the first comprehensive investigation into transfer learning capabilities of pretrained MIL models, evaluating 11 MIL models across 19 pretraining tasks spanning tissue subtyping, cancer grading, and molecular subtype prediction. We observe a substantial performance boost with finetuning pretrained models over training from randomly initialized weights, even with domain differences between pretraining and target tasks. Pretraining on pan-cancer datasets enables consistent generalization across organs and task types compared to single-disease pretraining. Remarkably, this pan-cancer pretraining leads to better transfer than that of a state-of-the-art slide-level foundation model, while using only 6.5\% of the training data. These findings indicate that MIL architectures exhibit robust adaptability, offering insights into the benefits of leveraging pretrained models to enhance performance in computational pathology.

---

## 论文详细总结（自动生成）

# 论文总结：多实例学习模型是否具备迁移能力？

## 1. 论文的核心问题与整体含义

- **研究背景**：多实例学习（Multiple Instance Learning, MIL）是计算病理学中的核心方法，常用于从千兆像素级全切片图像中提取嵌入，并聚合为患者级表示以预测临床结局。
- **核心问题**：MIL 模型通常在小规模、弱监督的临床数据集上训练，数据稀缺限制了模型质量。在自然语言处理和计算机视觉中，迁移学习已被广泛用于缓解数据不足，但 **MIL 模型的迁移能力尚未被系统探索**。
- **整体含义**：该工作填补了计算病理学中 MIL 迁移学习研究的空白，旨在回答“预训练 MIL 模型能否作为小样本临床任务的有效起点”，从而提升弱监督全切片图像分析的实用性。

## 2. 论文提出的方法论

- **核心思想**：论文并非提出新的 MIL 架构，而是进行一项**系统性的迁移学习评估研究**，考察预训练 MIL 模型在不同病理任务上的迁移表现。
- **关键流程**（文字描述）：
  1. 选取 11 个 MIL 模型作为评估对象。
  2. 在 19 个预训练任务上进行预训练，任务涵盖组织分型、癌症分级和分子亚型预测。
  3. 将预训练模型迁移到下游目标任务，并通过微调（finetuning）与从头训练（随机初始化权重）进行对比。
  4. 分析预训练任务与目标任务之间的域差异、单病种预训练与泛癌预训练的差异，以及与其他基础模型的数据效率对比。
- **关键变量**：预训练任务类型、目标域与预训练域的差异性、是否使用泛癌数据、训练数据量比例。

## 3. 实验设计

- **数据集 / 场景**：
  - 涉及 19 个病理相关任务/数据集，覆盖组织分型、癌症分级、分子亚型预测三类任务。
  - 包含单病种数据集与泛癌（pan-cancer）数据集。
- **Benchmark**：
  - 从随机初始化权重训练作为基线。
  - 比较单病种预训练与泛癌预训练的迁移效果。
  - 对比先进的 slide-level foundation model（切片级基础模型）在迁移性能和数据效率上的表现。
- **对比方法**：
  - 随机初始化 + 微调。
  - 单病种预训练 + 微调。
  - 泛癌预训练 + 微调。
  - 现有 SOTA 切片级基础模型作为参考基准。

## 4. 资源与算力

- **未明确说明**：所提供的摘要与元数据中**没有提及 GPU 型号、GPU 数量、训练时长或具体算力开销**。
- 无法从现有信息判断实验的算力规模和可复现性；若需评估资源需求，需要查阅论文全文中的实验配置或附录。

## 5. 实验数量与充分性

- **实验规模**：涉及 **11 个 MIL 模型 × 19 个病理预训练任务**，并跨多类下游任务进行评估；从论文配图（8 张图）和表格（9 张表）数量来看，实验体系较为丰富。
- **充分性**：在摘要层面看，实验覆盖了不同任务类型、不同预训练数据域、不同初始化和不同模型对比，能够支撑关于迁移能力的一般性结论。
- **客观性与公平性**：
  - 设立了随机初始化基线，比较公平。
  - 对比了单病种与泛癌预训练，控制数据域差异变量。
  - 与 SOTA 基础模型比较时引入了数据量比例（6.5%）作为效率指标，避免单纯比较精度。
- **局限**：由于仅提供摘要，无法确认是否有更多消融实验（如不同 MIL 聚合器、不同嵌入器、不同微调策略）、统计显著性检验或跨中心外部验证。

## 6. 论文的主要结论与发现

- **微调预训练模型显著优于随机初始化训练**，即使预训练任务与目标任务之间存在域差异。
- **泛癌预训练比单病种预训练具有更强的一致泛化能力**，能够跨器官和任务类型稳定迁移。
- **泛癌预训练在迁移效果上超越了先进的切片级基础模型**，且仅使用后者 6.5% 的训练数据。
- 总体表明 **MIL 架构具有稳健的适应性**，预训练 MIL 模型可以作为数据稀缺场景下计算病理学任务的有效起点。

## 7. 优点

- **填补研究空白**：首次系统研究 MIL 模型的迁移学习能力，具有领域开创性。
- **实验设计系统性强**：覆盖多模型、多任务、多域差异，结论具有较好的普适性。
- **实际应用价值高**：为小样本临床数据集下的模型选择提供了直接指导。
- **数据效率洞察**：发现泛癌预训练在极低数据比例下仍能超越大型基础模型，对资源受限场景有重要意义。
- **兼顾域差异分析**：没有回避预训练与目标域不同的现实情况，增强了结论的实用性。

## 8. 不足与局限

- **细节信息缺失**：当前可获得的摘要未提供模型架构细节、具体数据集名称、下游任务数量、超参数设置和统计检验结果，难以完整评估方法严谨性。
- **算力与可复现性未知**：缺少 GPU 型号、训练时长等资源信息，无法判断实验成本和复现难度。
- **任务覆盖范围有限**：主要围绕组织分型、癌症分级和分子亚型预测，是否适用于其他病理任务（如预后预测、治疗响应预测）仍不明确。
- **模型和预训练数据代表性**：仅评估 11 个 MIL 模型，可能未覆盖所有主流 MIL 变体；泛癌数据集的构成也可能影响结论的外推性。
- **潜在偏差风险**：预训练与下游任务若共享同一来源或高度相似数据，可能高估迁移效果；需要外部独立验证进一步确认。
- **未提供失败案例分析**：尚未看到对迁移失败或负迁移情况的系统讨论。

（完）
