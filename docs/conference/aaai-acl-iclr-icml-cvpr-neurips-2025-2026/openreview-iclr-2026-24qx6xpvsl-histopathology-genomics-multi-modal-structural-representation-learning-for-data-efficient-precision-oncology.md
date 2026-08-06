---
title: Histopathology-Genomics Multi-modal Structural Representation Learning for Data-Efficient Precision Oncology
title_zh: 组织病理学-基因组学多模态结构表示学习用于数据高效的精准肿瘤学
authors: "Kun Wu, Zhiguo Jiang, Xinyu Zhu, Jun Shi, Yushan Zheng"
date: 2026-01-26
pdf: "https://openreview.net/pdf?id=24QX6XpvSL"
tags: ["query:immuno-topo"]
score: 5.0
evidence: 融合组织病理学与基因组学的多模态结构表示学习用于精准肿瘤学
tldr: 该论文针对现实场景中基因组数据常缺失的问题，提出一种多模态结构表示学习框架MSRL。通过挖掘病例间的结构关系，并利用训练集中可获得的基因组数据，在测试时仅凭组织病理图像即可进行有效的肿瘤分析。该方法提升了数据稀缺情况下的精准肿瘤学预测性能。
source: ICLR-2026-Accepted
selection_source: conference_retrieval
motivation: 基因组数据缺失限制精准肿瘤学应用，现有方法仅利用单病例信息。
method: 提出MSRL框架，利用病例间关系融合组织病理与基因组数据。
result: 在基因组数据缺失情况下，模型仍能保持高性能。
conclusion: 结构表示学习为数据高效精准肿瘤学提供了有效策略。
---

## Abstract
Fusing histopathology images and genomics data with deep learning has significantly advanced precision oncology. However, genomics data is often missing due to its high acquisition cost and complexity in real-world clinical scenarios. Existing solutions aim to reconstruct genomics data from histopathology images. Nevertheless, these methods typically relied only on individual case and overlooked the potential relationships among cases. Additionally, they failed to take advantage of the authentic genomics data of diagnostically related cases that are accessible from training for inference. In this work, we propose a novel Multi-modal Structural Representation Learning (MSRL) framework for data-efficient precision oncology. We pre-train a histopathology-genomics multi-modal representation graph adopting Graph Structure Learning (GSL) to construct inter-case relevance based on the data inherently. During the fine-tuning stage, we dynamically capture structural relevance between the training cases and the acquired authentic cases for precise prediction. MSRL leverages prior inter-case associations and authentic genomics data from diagnosed cases based on the graph, which contributes to effective inference based on the single histopathology image modality. We evaluated MSRL on public TCGA datasets with 7,263 cases across various tasks, including survival prediction, cancer grading, and gene mutation prediction. The results demonstrate that MSRL significantly outperforms existing missing-genomics generation approaches with improvements of 1.44% to 3.12% in C-Index on survival prediction tasks and achieves comparable performance to multi-modal fusion methods. The code and data are available at https://github.com/WkEEn/MSRL.

---

## 论文详细总结（自动生成）

## 1. 论文的核心问题与整体含义

- **核心问题**：在精准肿瘤学中，融合组织病理图像与基因组数据可提升诊断性能，但基因组数据在实际临床中常因高成本与复杂性而缺失，导致多模态方法受限。
- **整体含义**：现有方法尝试从病理图像重建缺失的基因组数据，但仅利用单病例信息，忽略了病例间的关联，且未能有效复用已有诊断病例的真实基因组数据。该论文提出利用病例间结构关系，在测试时仅凭组织病理图像进行高效预测，以实现数据高效（data‑efficient）的肿瘤分析。

## 2. 论文提出的方法论

- **核心思想**：构建多模态结构表示学习框架（MSRL），通过图结构学习（Graph Structure Learning, GSL）预训练一个融合组织病理与基因组数据的多模态表示图，捕捉病例间内在相关性；在微调和推理阶段，动态利用训练病例与已知诊断病例的结构相似性，结合其真实基因组数据，提升仅基于病理图像的预测性能。
- **关键技术细节**：
  - **预训练阶段**：采用图结构学习方法，以病例为节点，联合组织病理与基因组特征构建多模态表示图，学习病例间结构关联。
  - **微调/推理阶段**：对测试病例，从图中捕获其与训练集中已拥有真实基因组数据的病例的结构关联，从而以结构化方式引入基因组信息，辅助仅依赖病理图像的预测。
  - **数据多模态融合策略**：不是简单的模态补齐或生成，而是通过图拓扑传播关联病例的真实基因组信息。
- **算法流程**（文字说明）：
  1. 利用全部训练病例的组织病理图像和基因组数据，通过GSL构造跨病例的关系图并学习节点表示。
  2. 针对下游任务（生存预测、分级、突变预测等），微调模型，在预测时对目标病例基于学到的图结构检索相关病例并整合其基因组信息。
  3. 测试时仅输入组织病理图像，利用图结构动态获取训练/已诊断病例的结构支持和真实基因组知识。

## 3. 实验设计

- **数据集**：公共TCGA数据集，覆盖7,263例病例。
- **任务场景**：生存预测、癌症分级、基因突变预测。
- **对比基准（Benchmark）**：
  - 现有缺失基因组生成方法（missing‑genomics generation approaches）。
  - 多模态融合方法（作为性能上界参考）。
- **评估指标**：生存预测任务主要使用C‑Index。

## 4. 资源与算力

- 根据提供的元数据和摘要，**未明确说明**训练所用的GPU型号、数量或训练时长。论文正文中可能包含具体细节，但本次分析仅基于摘要和元数据，无法给出相应结论。

## 5. 实验数量与充分性

- **实验规模**：从摘要可知，至少在三个不同任务（生存预测、癌症分级、基因突变预测）上进行了评估，并包含与多类方法的比较。
- **充分性**：
  - 使用大规模公开数据集（TCGA 7,263例）增强了统计效力。
  - 与缺失基因组生成方法及多模态融合方法对比，基准选择合理。
  - 摘要未提及消融实验或跨癌种/跨中心的详细分析，但从方法设计看，研究应包含必要的组件验证。
- **客观性与公平性**：采用公开数据集和标准指标（C‑Index等），与同类方法直接比较，具备一定的客观性。

## 6. 论文的主要结论与发现

- MSRL在基因组缺失场景下显著优于现有缺失基因组生成方法，在生存预测任务上C‑Index提升1.44%～3.12%。
- 该方法在仅使用病理图像测试时，能达到与多模态融合方法接近的性能，表现出数据高效的优势。
- 结构表示学习通过引入病例间关系并复用已诊断病例的真实基因组数据，为精准肿瘤学提供了一种有效且实用的方案。

## 7. 优点

- **方法创新**：首次将图结构学习用于组织病理‑基因组多模态融合，利用病例间关系而非单点生成，解决基因组缺失问题。
- **临床友好**：推理阶段仅需病理图像，无需额外基因组检测，降低了应用门槛。
- **性能突出**：在多个肿瘤分析任务上取得一致提升，且与完全多模态方法性能可比，验证了方法的有效性。
- **实验规模大**：基于TCGA 7,263例，结果具有较好的代表性和统计意义。

## 8. 不足与局限

- **实验覆盖**：摘要未提及是否在不同的独立外部队列、不同人群或不同扫描仪来源的数据上验证，其结果泛化性尚待进一步确认。
- **偏差风险**：TCGA数据集可能存在机构或人群偏差；基于图的方法对训练集中已诊断病例的代表性有一定依赖。
- **算力与效率**：未说明推理阶段图检索的计算成本，可能影响实时临床应用。
- **消融分析**：从摘要无法判断各组件（GSL、动态结构关联等）的具体贡献，缺乏深入的模块分析信息（正文中可能包含，但当前材料未提供）。
- **应用限制**：方法适用于具备大量已诊断病例且有组织病理图像的场景，对罕见癌症或小数据集的效果仍需验证。

（完）
