---
title: "Fusing Pixels and Genes: Spatially-Aware Learning in Computational Pathology"
title_zh: 融合像素与基因：计算病理学中的空间感知学习
authors: "Minghao Han, Dingkang Yang, Linhao Qu, Zizhi Chen, Gang Li, Han Wang, Jiacong Wang, Lihua Zhang"
date: 2026-01-26
pdf: "https://openreview.net/pdf?id=uVXO6gzVzj"
tags: ["query:path-xai-sel"]
score: 9.0
evidence: 将空间转录组学与病理图像整合，实现分子引导的联合嵌入，推动计算病理学发展
tldr: STAMP提出空间转录组学增强的多模态病理表征学习框架，将空间解析的基因表达谱与病理图像整合，克服纯视觉-语言模态缺乏分子特异性的瓶颈。通过自监督、基因引导训练，该框架学习到鲁棒的病理图像表征，并在多个下游任务上验证有效，为计算病理学提供了新的分子感知学习范式。
source: ICLR-2026-Accepted
selection_source: conference_retrieval
motivation: 现有病理多模态模型依赖视觉-语言，缺少分子特异性，导致表征瓶颈。
method: 提出STAMP框架，将空间转录组学数据与病理图像进行自监督联合训练。
result: 学到的表征在多项病理下游任务上取得领先性能。
conclusion: 分子引导的空间感知学习为计算病理提供强大通用的表征，连接图像与分子信息。
---

## Abstract
Recent years have witnessed remarkable progress in multimodal learning within computational pathology. Existing models primarily rely on vision and language modalities; however, language alone lacks molecular specificity and offers limited pathological supervision, leading to representational bottlenecks. In this paper, we propose STAMP, a Spatial Transcriptomics-Augmented Multimodal Pathology representation learning framework that integrates spatially-resolved gene expression profiles to enable molecule-guided joint embedding of pathology images and transcriptomic data. Our study shows that self-supervised, gene-guided training provides a robust and task-agnostic signal for learning pathology image representations. Incorporating spatial context and multi-scale information further enhances model performance and generalizability. To support this, we constructed SpaVis-6M, the largest Visium-based spatial transcriptomics dataset to date, and trained a spatially-aware gene encoder on this resource. Leveraging hierarchical multi-scale contrastive alignment and cross-scale patch localization mechanisms, STAMP effectively aligns spatial transcriptomics with pathology images, capturing spatial structure and molecular variation. We validate STAMP across six datasets and four downstream tasks, where it consistently achieves strong performance. These results highlight the value and necessity of integrating spatially resolved molecular supervision for advancing multimodal learning in computational pathology. The code is included in the supplementary materials. The pretrained weights and SpaVis-6M are available at: https://github.com/Hanminghao/STAMP.

---

## 论文详细总结（自动生成）

## 1. 论文的核心问题与整体含义
- **研究背景**：计算病理学中的多模态学习近年来发展迅速，但现有模型主要依赖视觉（病理图像）与语言（病理报告文本）两种模态。
- **核心瓶颈**：单纯的语言模态缺乏分子层面的特异性，提供的病理监督信息有限，导致图像表征学习陷入性能瓶颈。
- **研究意图**：引入空间转录组学（spatially-resolved transcriptomics），将空间解析的基因表达谱与病理图像进行联合建模，用分子信号直接引导图像表征的学习，突破纯“图像-语言”范式的天花板。
- **整体意义**：提出一种从“融合像素与基因”出发的空间感知学习范式，使病理图像表征具备分子感知能力，为精准诊断、预后评估等下游任务提供更本质的生物信号。

## 2. 论文提出的方法论
- **总体框架**：STAMP（Spatial Transcriptomics-Augmented Multimodal Pathology），一个空间转录组学增强的多模态病理表征学习框架。
- **核心思想**：通过自监督的基因引导训练，将空间转录组数据中的基因表达作为监督信号，与病理图像进行对齐，从而学到鲁棒且任务无关的图像表征。
- **关键技术细节**：
  - 构建大规模 Visium 空间转录组数据集 **SpaVis-6M**，以此训练一个空间感知的基因编码器（spatially-aware gene encoder）。
  - 提出 **层次化多尺度对比对齐**（hierarchical multi-scale contrastive alignment）机制，在多个空间尺度上将图像块特征与基因表达特征对齐。
  - 设计 **跨尺度斑块定位**（cross-scale patch localization）机制，捕捉不同粒度下的空间结构与分子变异。
  - 显式融入空间上下文（spatial context）与多尺度信息，进一步提升表征泛化能力。
- **训练方式**：自监督联合训练，无需下游任务标签即可学习通用表征。

## 3. 实验设计
- **数据集与场景**：
  - 自建数据集 **SpaVis-6M**（最大的 Visium 空间转录组数据集）用于预训练。
  - 在 **6 个数据集** 上进行下游验证，覆盖多种组织类型与疾病场景。
- **评测基准（benchmark）**：围绕 **4 类下游任务** 评估表征质量（具体任务类型摘要中未详列，推测为分类、检测、分割或预测等）。
- **对比方法**：文中应与纯视觉模型、视觉-语言模型等基线方法对比（摘要未列出具体名称，如 CLIP 变体、病理专用 VLM 等），以体现分子引导的优势。

## 4. 资源与算力
- 提供的摘要文本 **未明确提及** 所用 GPU 型号、数量或训练时长等计算资源信息。该部分内容需查阅论文全文方可获知。

## 5. 实验数量与充分性
- 摘要显示实验覆盖 **6 个数据集 × 4 个下游任务**，形成较为丰富的评估矩阵。
- 预计包含对关键模块（多尺度机制、空间上下文、对齐策略等）的消融实验，但摘要未披露具体设计数量。
- 从中观层面看，实验设计具备一定的广度（多数据、多任务），且明确宣称“一致性取得强大性能”，在公平性与客观性上应符合社区发展水平；但消融实验的深度与统计分析充分性需结合全文判断。

## 6. 论文的主要结论与发现
- 利用自监督、基因引导的方式，可为病理图像学习提供稳健、任务无关的强表示。
- 明确纳入空间上下文和多尺度信息，能够显著提升模型的性能与可推广性。
- STAMP 在多项下游任务上达到领先水平，证明分子引导的空间感知学习是推动计算病理学发展的有效且必要的方向。
- 该方法成功在图像空间与基因表达空间之间建立有意义的跨模态链接。

## 7. 优点
- **创新性强**：首次将空间转录组学大规模引入病理图像表征学习，从“看像素”跃迁到“读分子”。
- **数据贡献**：构建了迄今最大的 Visium 空间转录组数据集 SpaVis-6M，推动领域数据基础。
- **方法论扎实**：提出层次多尺度对比对齐和跨尺度定位，建模空间结构与分子变异，设计精细。
- **验证广泛**：横跨 6 个数据集和 4 类任务，结果有说服力。
- **开源开放**：代码、预训练权重及数据集均已计划公开，利于复现与拓展。

## 8. 不足与局限
- **数据依赖性**：方法依赖空间转录组数据，获取成本高、通量有限，限制大规模推广。
- **技术平台局限**：预训练与对齐基于 Visium 技术（分辨率约 55 μm/spot），未扩展到单细胞级空间组学（如 MERFISH、Xenium 等），可能丢失亚细胞空间精度。
- **任务通用性未完全验证**：摘要未披露 4 类下游任务的具体性质，是否包含生存分析、治疗反应预测等临床高价值任务有待确认。
- **对比基线不明**：摘要未列出具体对比方法，难以判断其相对最新视觉‑语言模型（如 CONCH、Prov-GigaPath 等）的增益幅度。
- **算力需求未量化**：无 GPU 和时间信息，实际落地成本未知。

（完）
