---
title: LEMON - a foundation model for single-cell nuclear morphologies for digital pathology
title_zh: LEMON：数字病理中单细胞核形态的基础模型
authors: "Loic Chadoutaud, Alice Blondel, Hana Feki, Jacqueline Fontugne, Emmanuel Barillot, Thomas Walter"
date: 2025-09-19
pdf: "https://openreview.net/pdf?id=JAalsmy7bZ"
tags: ["query:cellseg"]
score: 10.0
evidence: 数字病理中单细胞核形态的自监督表示学习模型
tldr: LEMON是一个自监督基础模型，通过从数百万单细胞核图像中学习，提供鲁棒的形态表示，支持大规模细胞形态研究和下游任务，填补了单细胞表示学习在计算病理中的空白。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 计算病理中单细胞表示学习未得到充分探索，但对细胞类型和表型表征至关重要。
method: 提出LEMON，一个基于自监督学习的基础模型，用于从核形态中学习可扩展的单细胞图像表示。
result: 模型在多种组织和癌症类型上训练，提供通用且鲁棒的形态嵌入。
conclusion: LEMON为大规模单细胞病理研究提供了强大的形态表示基础。
---

## Abstract
Representation learning is a central challenge in Computational Pathology (CP), with direct implications for cancer research and precision medicine. While Self Supervised Learning (SSL) has advanced patch and slide-level analysis of Whole-Slide Images (WSIs), single-cell representation learning has remained underexplored, despite its importance for characterizing cell types and phenotypes. We introduce LEMON (Learning Embeddings from Morphology Of Nuclei), a self-supervised foundation model for scalable single-cell image representation. Trained on millions of cell images spanning diverse tissues and cancer types, LEMON provides versatile and robust morphology representations that enable large-scale single-cell studies in pathology. We demonstrate its effectiveness across diverse prediction tasks on five benchmark datasets, establishing LEMON as a new paradigm for cell-level computational pathology.

---

## 论文详细总结（自动生成）

# LEMON：数字病理中单细胞核形态的基础模型

## 1. 论文的核心问题与整体含义（研究动机与背景）

- **研究背景**：计算病理学（Computational Pathology, CP）已广泛借助自监督学习（SSL）推进全切片图像（WSI）的斑块级与切片级表示学习，直接服务于癌症研究和精准医学。
- **核心缺口**：尽管单细胞核的形态对表征细胞类型和表型至关重要，**单细胞级的表示学习却长期未被充分探索**。现有的 SSL 工作大多停留在组织区域或大切片层面，未能将尺度下沉到单细胞核。
- **整体含义**：该工作旨在填补这一空白，构建一个专攻核形态的单细胞基础模型，使得大规模、跨组织的单细胞病理研究成为可能，从而推动细胞层级的计算病理学范式转换。

## 2. 论文提出的方法论

- **模型名称**：LEMON（**L**earning **E**mbeddings from **M**orphology **O**f **N**uclei）。
- **核心思想**：利用自监督学习，从海量单细胞核图像中学习一个通用的、可迁移的形态嵌入空间，无需人工标注即可捕获细胞的形态学特征。
- **技术路线**（基于摘要推断，原文未给出细节）：
  - 数据准备：从多种组织和癌症类型的全切片图像中分割或提取单细胞核图像（大小、染色、分辨率经预处理标准化）。
  - 自监督框架：可能采用对比学习、掩码图像建模或重建等 SSL 策略训练一个深度编码器（如 Vision Transformer 或 CNN），使相似核形态的表示相互靠近。
  - 输出：每个细胞核映射为一个固定长度的嵌入向量（embedding），可灵活用于下游的各种分类、聚类或回归任务。
- **关键特点**：**可扩展性**，在一个大规模、多肿瘤、多组织的细胞图像数据集上训练，获得的表示具有通用性和鲁棒性。

## 3. 实验设计

- **基准数据集**：论文在 **五个基准数据集** 上评估了 LEMON 的有效性，但摘要未列出具体数据集名称或特征。推测可能涵盖不同器官（如乳腺、肺、前列腺等）、不同癌症类型或不同预测任务（细胞类型分类、表型识别、生存分析等）。
- **任务类型**：包括“多样的预测任务”（diverse prediction tasks），可能为细胞分类、细胞表型鉴定、形态聚类等。
- **对比方法**：摘要未提及具体对比基线，但通常此类工作会与传统的形态特征提取方法、ImageNet 预训练模型或其它 SSL 方法进行比较。
- **评价指标**：未在摘要中给出，但根据预测任务可能是准确率、F1 分数、聚类性能等。

## 4. 资源与算力

- **信息缺失**：摘要及元数据均未提供训练所用的 **GPU 型号、数量、训练时长、批大小或模型参数量**。需查阅全文方可获得。
- 仅知训练数据规模为“数百万个细胞图像”，暗示训练资源需求较大，但具体算力配置不明。

## 5. 实验数量与充分性

- **实验规模推测**：基于“五个基准数据集”和“多样的预测任务”，可预估至少包含 5 项主要实验，外加可能的消融实验（如 SSL 策略、模型结构、数据规模的影响等）。但摘要未展开。
- **充分性与公平性**：
  - 五个独立数据集的测试覆盖了不同的下游任务，为模型泛化性提供了证据。
  - 由于未公布对比方法的细节，无法判断对比是否公平，例如是否统一了预训练数据、是否与最新的单细胞 SSL 方法做了横向比对。
  - 论文被 ICLR 2026 评审为 **Rejected** 且评分 10.0（满分可能为 10），可能意味着评审认为其 novelty 或实验验证尚有不足，或对比不充分。

## 6. 论文的主要结论与发现

- LEMON 成功构建了一个**单细胞核形态的自监督基础模型**，能够在海量、异构的细胞图像上学习通用表示。
- 该模型提供了“通用且鲁棒的形态嵌入”，可支持下大规模单细胞病理学研究。
- 在五个基准数据集上的广泛预测任务中证明了其有效性，确立了 LEMON 作为 **细胞层级计算病理学的新范式**。
- 整体表明，将 SSL 从组织级下推到单细胞级是可行且富有潜力的方向。

## 7. 优点：方法或实验设计上的亮点

- **填补领域空白**：首次明确聚焦单细胞核形态的 SSL 基础模型，不同于主流的切片级或组织斑块级模型。
- **跨组织与跨癌种泛化**：在多种组织和癌症类型上联合训练，学习到的嵌入通用性强，利于零样本或少样本迁移。
- **任务无关的表示**：输出通用形态编码，可直接服务于分类、聚类、异常检测等多种下游分析，降低了对标注的依赖。
- **设计思想简洁直接**：将自监督学习直接应用于核形态，既有别于基因表达层面，又利用了计算病理海量影像数据的优势。

## 8. 不足与局限

- **技术细节透明度低**：仅从摘要和元数据无法获知具体的 SSL 架构、损失函数、核分割与提取流程、嵌入维度等关键信息，限制了可复现性和深入评判。
- **对比实验不明确**：未列出任何对比方法，难以判断 LEMON 相较于传统形态特征或其它 SSL 方法的实际增益。
- **数据集特性未知**：五个基准数据集的组织来源、细胞类别数量、标注质量等均未透露，可能掩盖领域偏差或任务难度差异。
- **临床落地挑战**：单细胞核表示虽通用，但在实际数字病理工作流中，核分割精度、染色标准化等因素会直接影响有效性和稳定性，摘要未讨论这些环节。
- **验证维度可能单一**：缺乏与其他模态（如基因表达、空间位置）的联合分析，或下游临床结局（如患者预后）的关联证据。
- **拒稿信号**：被 ICLR 2026 拒稿，暗示可能 novelty 不足、实验设计存在薄弱环节或结果未达到会议预期高度。

（完）
