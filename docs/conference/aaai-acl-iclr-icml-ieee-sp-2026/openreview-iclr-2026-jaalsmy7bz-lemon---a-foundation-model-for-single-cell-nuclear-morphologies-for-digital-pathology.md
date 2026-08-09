---
title: LEMON - a foundation model for single-cell nuclear morphologies for digital pathology
title_zh: LEMON：面向数字病理学的单细胞核形态基础模型
authors: "Loic Chadoutaud, Alice Blondel, Hana Feki, Jacqueline Fontugne, Emmanuel Barillot, Thomas Walter"
date: 2025-09-19
pdf: "https://openreview.net/pdf?id=JAalsmy7bZ"
tags: ["query:cellseg"]
score: 9.0
evidence: 针对数字病理学中单细胞核形态的基础模型，支持下游细胞级任务。
tldr: 当前计算病理学在单细胞表示学习方面尚未充分挖掘，限制了细胞类型和表型的精细表征。LEMON提出一种基于核形态的自监督基础模型，在数百万跨组织和癌症类型的细胞图像上训练，获得可扩展的单细胞图像表示。实验表明，该模型能够稳健地捕获核形态特征，支持大规模单细胞研究，为下游任务提供通用特征。该工作打通了从HE切片细胞分割到高级表型分析的桥梁。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 现有SSL方法聚焦于patch和slide级别，单细胞表示学习被忽视，制约了细胞类型精细表征。
method: 在数百万细胞图像上自监督训练一个基于核形态的通用表示模型，提供可扩展的单细胞特征。
result: 模型在多组织和癌症类型上学习到鲁棒的形态表示，支持大规模单细胞研究。
conclusion: LEMON为数字病理学提供了单细胞级的基础模型，打通从分割到下游分析的通道。
---

## Abstract
Representation learning is a central challenge in Computational Pathology (CP), with direct implications for cancer research and precision medicine. While Self Supervised Learning (SSL) has advanced patch and slide-level analysis of Whole-Slide Images (WSIs), single-cell representation learning has remained underexplored, despite its importance for characterizing cell types and phenotypes. We introduce LEMON (Learning Embeddings from Morphology Of Nuclei), a self-supervised foundation model for scalable single-cell image representation. Trained on millions of cell images spanning diverse tissues and cancer types, LEMON provides versatile and robust morphology representations that enable large-scale single-cell studies in pathology. We demonstrate its effectiveness across diverse prediction tasks on five benchmark datasets, establishing LEMON as a new paradigm for cell-level computational pathology.

---

## 论文详细总结（自动生成）

# 论文总结：LEMON - 面向数字病理学的单细胞核形态基础模型

## 1. 论文的核心问题与整体含义

- **核心问题**：当前计算病理学中的表示学习主要聚焦于整张全切片图像（WSI）的小块（patch）或切片（slide）级别，单细胞级别的表示学习长期被忽视。然而，精细表征细胞类型与表型对癌症研究和精准医学至关重要。
- **整体含义**：论文旨在填补这一空白，提出一个专门针对单细胞图像的通用基础模型，用于从细胞核形态中学习可迁移的表示，从而打通从细胞分割到高级表型分析的桥梁，为大规模单细胞病理研究提供新范式。

## 2. 论文提出的方法论

- **核心思想**：利用自监督学习（SSL）在海量细胞图像上预训练一个表示模型，以捕获细胞核的形态特征，形成通用的“细胞形态嵌入”。
- **关键设计**：
  - 模型名称：LEMON（**L**earning **E**mbeddings from **M**orphology **O**f **N**uclei）。
  - 训练数据：跨越多种组织类型和癌症种类的数百万细胞图像。
  - 预训练策略：采用自监督方法，未明确指定具体框架（如对比学习或掩码自编码器），但目的在于生成鲁棒、可扩展的形态表示。
- **算法流程（推断）**：
  1. 从WSI中分割出单个细胞核图像。
  2. 构建自监督预训练任务（可能基于形态不变性、对比学习等）。
  3. 在千万级细胞图像上训练一个主干网络（如ResNet或ViT），得到细胞图像编码器。
  4. 为下游任务提供冻结或微调的特征表示，支持细胞分类、聚类等分析。

## 3. 实验设计

- **基准数据集**：在5个公开或标准基准数据集上进行评估，具体名称未披露。
- **任务类型**：覆盖多种预测任务，可能包括细胞类型分类、表型预测、癌细胞识别等。
- **对比方法**：未详细列出，但应与当前主流的自监督学习方法（如SimCLR、MoCo等面向patch或slide的模型）以及有监督基线进行对比，以证明单细胞专用模型的有效性。
- **评估指标**：应包含与细胞分类相关的准确率、F1值等，需参考原文。

## 4. 资源与算力

- 论文提供的摘要及元数据中**未明确说明**所使用的GPU型号、数量、训练时长或总计算量。
- 考虑到模型在数百万细胞图像上训练，且需处理高分辨率病理图像，预估需要多卡高性能GPU（如A100）集群，训练时间可能以小时或天计，但确切信息应从原文获取。

## 5. 实验数量与充分性

- **实验组数量**：基于摘要中提及“5个基准数据集”和“多种预测任务”，可推断至少包含5组主要实验，并可能附加消融实验（如不同预训练数据量、模型结构的影响）。但元数据中未提供消融实验细节。
- **充分性与公平性**：
  - 覆盖多个组织及癌症类型，提升了泛化性验证的充分性。
  - 与现有patch/slide级方法对比，能体现单细胞建模的必要性。
  - 由于缺乏方法细节和完整的消融研究描述，难以判断实验是否完全公平，例如不同方法的算力/数据量是否对齐未知。

## 6. 论文的主要结论与发现

- LEMON能够从大规模、跨组织的细胞核图像中学习到稳健而通用的形态学表示。
- 该模型为单细胞数字病理学提供了一个可扩展的基础模型，显著支持下游的大规模单细胞研究。
- 在多个基准任务上验证了有效性，证明了细胞级别自监督表示学习是一种构建病理学基础模型的可行新范式。
- 打通了从HE切片细胞分割到高级表型分析的流程，推动了计算病理学向更细粒度的方向发展。

## 7. 优点

- **研究缺口抓取精准**：明确指出了单细胞表示学习被忽视的现状，具有明确的创新动机。
- **规模庞大**：基于数百万细胞、多种组织/癌症类型训练，增强了模型的通用性和鲁棒性。
- **范式创新**：将基础模型的概念下沉到细胞核形态层面，是对当前patch/slide级基础模型的重要补充。
- **即插即用潜力**：作为通用细胞特征提取器，能便捷地接入多种下游任务，降低单细胞分析的门槛。

## 8. 不足与局限

- **信息缺失严重**：提供的内容仅为摘要和简短元数据，方法论细节（自监督具体策略、网络结构）、实验完整设置、对比方法、算力开销等均不明确，导致评估深度受限。
- **数据多样性的潜在风险**：虽声称覆盖“多种组织和癌症类型”，但未说明数据来源是否足够多元（种族、扫描仪、制备流程），可能存在领域偏移风险。
- **分割依赖**：模型性能严重依赖于前序细胞核分割算法的精度，分割错误会直接传导至特征质量，文中未讨论该影响的敏感度。
- **下游任务覆盖面**：5个基准数据集虽具代表性，但可能未充分覆盖罕见癌症、免疫微环境分析等复杂场景，泛化边界尚需更多验证。
- **可解释性空白**：未说明是否对学习到的形态特征进行了解释性分析（如哪些核形态起关键作用），可能影响临床信任度。

（完）
