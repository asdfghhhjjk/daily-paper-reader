---
title: Transitive Representation Learning Enhances Histopathology Annotation
title_zh: 传递表示学习提升组织病理学注释
authors: "Moritz Schaefer, Zoe Piran, Nils Philipp Walter, Animesh Awasthi, Christoph Bock, Jure Leskovec, Zinaida Good"
date: 2026-04-30
pdf: "https://openreview.net/pdf/5633e8d66627583698d6fffa502376d7f9347d92.pdf"
tags: ["query:cell-path"]
score: 9.0
evidence: 从组织病理图像实现零样本细胞类型注释，直接相关于肿瘤微环境中细胞类型分类
tldr: 该论文针对组织病理学AI中粗粒度注释缺乏细胞身份信息的问题，提出SpatialWhisperer，一种三模态对比学习模型。该模型将组织病理图像、基因表达谱和自然语言描述关联起来，利用共享的基因表达模态建立图像与文本注释之间的传递关系。实验表明该方法能够实现零样本细胞类型注释，无需额外训练即可在组织图像中识别细胞类型。这项工作为细胞类型分类提供了高效且可扩展的解决方案。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 现有组织病理学AI受限于粗粒度注释，缺乏细胞身份信息。
method: 提出SpatialWhisperer，一种三模态对比学习模型，利用基因表达和自然语言描述桥接组织图像与文本注释。
result: 实现零样本细胞类型注释，无需额外训练即可识别细胞类型。
conclusion: 为组织病理学提供了精确的细胞级注释能力。
---

## Abstract
The characterization of histopathology with AI promises to assist clinical decision-making, but it is currently limited due to coarse-grained annotations that miss cellular identities. To overcome this gap, we bridge histopathological images, gene expression profiles, and natural-language descriptions using *SpatialWhisperer*, a trimodal contrastive learning model. Our training integrates community-scale datasets comprising spatially resolved gene expression profiles paired with histopathology images, as well as single-cell gene expression profiles with detailed annotations. The shared gene expression modality implies a transitive relationship between images and textual annotations, which our method leverages to enable accurate zero-shot cell type annotation directly from H&E images. *SpatialWhisperer* outperforms published baselines, achieving relative AUROC gains of up to 15.9% across three benchmarks spanning 19 tissues and 20 cell types. When training with data from all three modality pairs, we observe performance gains in low-data regimes. We formalize our approach and present a sufficient condition under which this transitive alignment is induced. Our work establishes *transitive representation learning* for fine-grained interpretation of histopathology images.

---

## 论文详细总结（自动生成）

说明：以下总结基于提供的论文元数据与摘要；原始 PDF 提取内容仅显示 OpenReview 验证页面，未获得完整正文，因此部分细节（如资源算力、具体数据集/基线名称、消融设计）缺失。

## 1. 论文的核心问题与整体含义

- **研究背景**：组织病理学 AI 有望辅助临床决策，但现有方法通常依赖粗粒度注释，缺少细胞身份信息，限制了对肿瘤微环境和组织结构的细粒度解读。
- **核心问题**：如何从常规 H&E 组织图像中实现细粒度、细胞类型级别的注释，尤其是在图像与文本注释缺乏直接配对数据的情况下。
- **整体含义**：论文提出“传递表示学习”思想，利用基因表达谱作为共享中间模态，将组织病理图像与自然语言描述间接对齐，从而赋予模型零样本细胞类型注释能力。

## 2. 论文提出的方法论

- **模型名称**：SpatialWhisperer，一种三模态对比学习模型。
- **核心思想**：
  - 同时建模三种模态：组织病理图像、基因表达谱、自然语言描述。
  - 利用“共享的基因表达模态”建立图像与文本之间的传递关系：图像—基因表达、基因表达—文本。
  - 即使没有直接的图像—文本配对标注，也能通过传递性诱导图像与文本在隐空间对齐。
- **关键技术与流程**：
  - 训练数据整合两类社区规模数据集：
    - 空间分辨基因表达谱 + 配对的组织病理图像；
    - 单细胞基因表达谱 + 详细文本注释。
  - 使用对比学习对齐跨模态嵌入：最大化配对样本的跨模态相似度，最小化非配对样本相似度。
  - 由于基因表达模态被图像和文本两侧共享，模型可隐式学习图像与文本注释之间的传递对齐。
  - 推理时，仅输入 H&E 图像，将图像映射到共享表示空间，与细胞类型文本描述匹配，实现零样本注释。
- **理论贡献**：
  - 对方法进行了形式化；
  - 提出并给出了“传递对齐被诱导”的充分条件。

## 3. 实验设计

- **数据集与场景**：
  - 三个基准测试，覆盖 19 种组织和 20 种细胞类型。
  - 涉及空间转录组 + 组织病理图像配对数据，以及单细胞基因表达谱 + 文本注释数据。
  - 具体数据集名称、样本量、组织来源等在所提供材料中未列出。
- **评价指标**：主要以 AUROC 衡量细胞类型注释性能。
- **对比方法**：
  - 与已发表基线进行比较，但具体基线名称未在提供材料中给出。
- **实验场景**：
  - 零样本细胞类型注释：直接从 H&E 图像识别细胞类型，无需额外训练。
  - 低数据机制训练：当使用三种模态对的数据进行训练时，观察低数据情况下的性能提升。

## 4. 资源与算力

- **提供材料中未明确说明 GPU 型号、GPU 数量、训练时长、显存占用或训练成本。**
- 因此无法评估该方法的计算开销、可复现性或实际部署成本；需参考论文原文中的附录或实验设置部分。

## 5. 实验数量与充分性

- **实验覆盖**：
  - 至少覆盖 3 个基准、19 种组织、20 种细胞类型；
  - 包含与已发表基线的对比；
  - 包含低数据机制下的性能分析；
  - 包含理论充分条件的提出与形式化。
- **充分性**：
  - 从摘要看，多基准、多组织、多细胞类型以及低数据场景的评估覆盖面较好；
  - 但消融实验、误差线、统计显著性检验、数据划分方式、跨中心泛化等细节未在提供材料中体现，难以判断实验的完整充分性。
- **客观性与公平性**：
  - 提供了相对 AUROC 提升数据，最高达 15.9%，结果可量化；
  - 但基线选择、超参数调优、统一数据预处理、是否公平比较等无法从现有信息验证。

## 6. 论文的主要结论与发现

- SpatialWhisperer 在三个基准上优于已发表基线，相对 AUROC 最高提升 15.9%。
- 通过共享基因表达模态，可以诱导图像与文本注释之间的传递对齐，实现零样本细胞类型注释。
- 在低数据场景下，使用所有三种模态对进行训练可带来性能提升。
- 论文形式化给出了传递对齐被诱导的充分条件。
- 总体结论：SpatialWhisperer 确立了“传递表示学习”用于组织病理图像细粒度解释的有效性。

## 7. 优点

- **创新性强**：用基因表达作为桥梁，规避了图像—文本直接配对标注稀缺的问题。
- **零样本能力**：无需额外训练即可从 H&E 图像中识别细胞类型，具有良好可扩展性。
- **多模态整合**：融合空间组学、单细胞转录组和病理图像，充分利用社区规模数据。
- **理论支撑**：不仅给出方法，还提供传递对齐的充分条件，理论形式化较清晰。
- **评估广度**：多个基准、多种组织、多种细胞类型的验证，结果具有跨组织参考价值。

## 8. 不足与局限

- **资源与算力信息缺失**：无法评估训练成本、可复现性和实际落地难度。
- **具体实验细节缺失**：所提供材料未列出数据集、基线名称、消融设计、误差线和统计检验等信息，限制了外部可验证性。
- **潜在偏差风险**：
  - 依赖基因表达模态质量和注释准确性；
  - 传递对齐的充分条件在非理想数据、批次效应或跨中心数据下是否仍然成立尚需验证。
- **应用限制**：
  - 零样本效果可能受组织类型、细胞类型粒度、图像质量、染色差异等因素影响；
  - 未讨论临床工作流集成、病理医生接受度或监管层面的可行性。
- **模态覆盖有限**：从摘要看主要针对 H&E 图像，其他染色方式或非转录组桥接模态未提及。

（完）
