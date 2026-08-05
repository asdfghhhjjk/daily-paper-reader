---
title: "Fusing Pixels and Genes: Spatially-Aware Learning in Computational Pathology"
title_zh: 像素与基因的融合：计算病理学中的空间感知学习
authors: "Minghao Han, Dingkang Yang, Linhao Qu, Zizhi Chen, Gang Li, Han Wang, Jiacong Wang, Lihua Zhang"
date: 2026-01-26
pdf: "https://openreview.net/pdf?id=uVXO6gzVzj"
tags: ["query:path-xai-sel"]
score: 8.0
evidence: 提出融合空间转录组学的多模态病理表征学习框架，提升组织表示能力。
tldr: STAMP利用空间基因表达作为自监督信号，指导病理图像与转录组数据的联合嵌入，获得任务无关的鲁棒表征。
source: ICLR-2026-Accepted
selection_source: conference_retrieval
motivation: 现有模型主要依赖视觉和语言模态，缺乏分子特异性，存在表征瓶颈。
method: 设计空间转录组增强的多模态病理表征学习框架，实现分子引导的联合嵌入。
result: 自监督训练提供了鲁棒的任务无关信号，提升了病理图像表征能力。
conclusion: 基因引导的训练为计算病理学提供了更有效的多模态表征。
---

## Abstract
Recent years have witnessed remarkable progress in multimodal learning within computational pathology. Existing models primarily rely on vision and language modalities; however, language alone lacks molecular specificity and offers limited pathological supervision, leading to representational bottlenecks. In this paper, we propose STAMP, a Spatial Transcriptomics-Augmented Multimodal Pathology representation learning framework that integrates spatially-resolved gene expression profiles to enable molecule-guided joint embedding of pathology images and transcriptomic data. Our study shows that self-supervised, gene-guided training provides a robust and task-agnostic signal for learning pathology image representations. Incorporating spatial context and multi-scale information further enhances model performance and generalizability. To support this, we constructed SpaVis-6M, the largest Visium-based spatial transcriptomics dataset to date, and trained a spatially-aware gene encoder on this resource. Leveraging hierarchical multi-scale contrastive alignment and cross-scale patch localization mechanisms, STAMP effectively aligns spatial transcriptomics with pathology images, capturing spatial structure and molecular variation. We validate STAMP across six datasets and four downstream tasks, where it consistently achieves strong performance. These results highlight the value and necessity of integrating spatially resolved molecular supervision for advancing multimodal learning in computational pathology. The code is included in the supplementary materials. The pretrained weights and SpaVis-6M are available at: https://github.com/Hanminghao/STAMP.

---

## 论文详细总结（自动生成）

## 1. 论文的核心问题与整体含义
- **研究背景**：计算病理学中多模态学习虽已取得显著进展，但现有模型主要依赖视觉和语言两种模态。语言缺乏分子特异性，提供的病理监督信号有限，导致表征学习面临瓶颈。
- **核心问题**：如何突破视觉 – 语言范式的限制，将更本质的分子层面信息引入病理图像表征学习，从而提升模型的判别力与泛化性。
- **整体含义**：论文提出将“像素”与“基因”相融合，利用空间转录组学作为额外的监督源，为病理图像学习提供任务无关的、分子引导的强健信号，开辟了空间感知的多模态病理表征新范式。

## 2. 论文提出的方法论
- **核心思想**：以空间分辨的基因表达谱为教师信号，通过自监督方式指导病理图像与转录组数据进入同一联合嵌入空间，使视觉特征天然带有分子层面的空间结构信息。
- **关键技术组件**：
  - **STAMP 框架**：空间转录组增强的多模态病理表征学习框架。
  - **SpaVis-6M 数据集**：构建了迄今最大的基于 Visium 的空间转录组数据集，用于训练空间感知的基因编码器。
  - **层次多尺度对比对齐**：在不同分辨率下将图像补丁与对应的基因表达区域对齐，捕捉多尺度空间模式。
  - **跨尺度补丁定位机制**：实现图像局部区域与转录组测序点的精确匹配，保留空间组织结构和分子变异。
  - **空间感知基因编码器**：从空间基因表达中学习嵌入表示，为病理图像提供分子级监督。
- **算法流程**（文字概括）：  
  1. 利用 SpaVis-6M 大规模空间转录组数据预训练基因编码器，使其能够编码空间分布的基因表达。  
  2. 将病理图像切分为多尺度补丁，基因表达按空间坐标组织为对应的区域。  
  3. 通过层次化对比损失，最大化匹配的图文（图像补丁与基因表达区域）相似性，同时推开不匹配对。  
  4. 引入跨尺度定位约束，保证细粒度空间一致性。  
  5. 最终获得图像编码器，其输出特征可用于多种下游任务。

## 3. 实验设计
- **数据集与场景**：
  - **预训练数据集**：自建的 **SpaVis-6M**，是目前最大的 Visium 空间转录组数据集。
  - **下游评估数据集**：使用了 **6 个数据集**、覆盖 **4 种下游任务**（具体任务名称未在摘要中详列，但暗示包括组织分类、预后预测等典型病理任务）。
- **基准对比**：摘要指出 STAMP 在这些数据集和任务上始终取得了强劲性能，表明其与现有方法（未列出具体名称）相比具备优势，但未详述对比方法名称。
- **评价指标**：未明示，但可合理推断为下游任务相关的标准指标（如 AUC、准确率等）。

## 4. 资源与算力
- 摘要及提供的文本中 **未明确说明** 所用 GPU 型号、数量、训练时长等算力细节。  
- 仅提及代码、预训练权重和 SpaVis-6M 数据集将开源，可以间接推断训练规模较大，但具体资源消耗无从得知。

## 5. 实验数量与充分性
- **实验组数**：至少覆盖 6 个数据集 × 4 种下游任务的评估，加上预训练阶段和可能存在的消融研究（如多尺度、空间上下文等模块的有效性验证）。总体实验矩阵较为丰富。
- **充分性判断**：从已报告的结果看，跨数据集、跨任务的广泛验证初步说明实验设计较为充分，能够检验模型的泛化能力和鲁棒性。  
- **客观与公平性**：摘要未提及与具体对比方法详细比较时的公平性控制（如统一预训练数据规模、计算预算等），但数据集规模和任务多样性在一定程度上减少了偏向性风险。

## 6. 论文的主要结论与发现
- 自监督、基因引导的训练能够为病理图像表征学习提供 **鲁棒且任务无关** 的信号，显著提升表征质量。
- 融入 **空间上下文和多尺度信息** 对于增强模型性能和泛化性至关重要。
- STAMP 成功实现了空间转录组学与病理图像的有效对齐，能够同时捕获 **组织空间结构和分子变异**。
- 在所有验证任务上的一致性强势表现，证明了 **整合空间解析分子监督** 对推进计算病理多模态学习的价值与必要性。

## 7. 优点
- **创新性模态融合**：首次将空间转录组学引入病理图像表征学习，弥补了语言模态分子特异性不足的缺陷。
- **大规模数据构建**：SpaVis-6M 为空间转录组与病理图像联合建模提供了宝贵资源，具有社区推动价值。
- **精细的对齐机制**：层次多尺度对比和跨尺度补丁定位设计巧妙，既能捕获宏观结构又能保留微观分子差异。
- **任务无关的通用性**：自监督目标不依赖特定下游任务标签，学到的特征可直接迁移到多个任务，泛化能力突出。

## 8. 不足与局限
- **实验对比细节缺失**：摘要未列出具体对比方法，无法判断与最新视觉 – 语言模型（如 CONCH、UNI 等）的直接优劣。
- **算力信息缺失**：未提及训练成本，难以评估方法在大规模应用中的可行性及资源需求。
- **潜在数据依赖性**：方法高度依赖空间转录组数据（尤其是 Visium 技术），这类数据获取成本高、通量有限，可能限制在真实临床场景的推广。
- **局限讨论不足**：摘要未涉及模型在罕见肿瘤类型、跨平台转录组数据、图像质量波动等情况下的表现，稳健性有待进一步检验。
- **评估任务可能与现有基准重合度不足**：未明确列出任务，难以判断其与社区标准 benchmark 的对齐程度。

（完）
