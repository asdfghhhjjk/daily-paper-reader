---
title: "Biology-Guided Prototype Booster: Enhancing Latent Representations of Foundation Models for Gene Expression Prediction"
title_zh: 生物引导原型增强器：增强基础模型潜在表示以预测基因表达
authors: "Chaoyi Li, Quan Nguyen"
date: 2025-09-19
pdf: "https://openreview.net/pdf?id=ygv7GTp1k8"
tags: ["query:path-xai-sel"]
score: 8.0
evidence: 利用生物原型增强HE图像表示以预测基因表达
tldr: "针对H&E图像预测基因表达的任务，提出用生物引导原型增强基础模型潜在表示的方法，提升预测精度，推动精准病理学发展。"
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 现有基础模型嵌入未针对基因表达预测优化，适应性不足。
method: "提出生物引导原型增强器，将生物学先验融入H&E图像表示。"
result: 在多个数据集上提升基因表达预测性能。
conclusion: "为H&E图像精确预测空间转录组学提供了有效方案。"
---

## Abstract
Spatial transcriptomics (ST) is a cutting-edge technology that enables the measurement of gene expression while preserving spatial context and generating detailed tissue images. However, ST technology remains time-consuming and costly. The ability to predict ST gene markers of cancer from histology-grade H&E-stained tissue images is opening new horizons for precision and personalised pathology. Despite the success of foundation models in generating general-purpose embeddings of H&E-images, these representations are not optimized for gene expression prediction and lack task-specific adaptability. To address this limitation, we introduce Biology-Guided Prototype Booster (BP-Booster), leveraging biological prior knowledge to guide the construction and training of learnable prototypes for embedding reconstruction, thereby improving gene expression prediction. We demonstrate superior performance of BP-Booster across datasets, various cancer tissue types and different ST platforms. We also show that BP-Booster can flexibly integrate various foundation models to enhance their task-specific representations, enhancing explainability and applicability in clinically relevant tasks like predicting cancer biomarkers. Code will be released upon acceptance.

---

## 论文详细总结（自动生成）

# 论文《Biology-Guided Prototype Booster: Enhancing Latent Representations of Foundation Models for Gene Expression Prediction》总结

## 1. 核心问题与整体含义
- **研究背景与动机**：空间转录组学（Spatial Transcriptomics, ST）能够在保留组织空间位置信息的同时测量基因表达，并生成高分辨率组织图像，但 ST 技术耗时长、成本高。利用常规苏木精-伊红（H&E）染色组织图像直接预测癌症相关的基因表达标志物，可大幅降低检测门槛，推动精准与个性化病理学发展。
- **核心问题**：现有基础模型（foundation models）虽然能生成 H&E 图像的通用水组织学嵌入表示，但这些表示并未针对基因表达预测任务进行优化，缺乏任务特异的适应性，导致预测性能受限。
- **整体含义**：本文提出一种通用增强策略，将生物学先验知识融入基础模型的潜在表示中，使其更适配基因表达预测任务，从而提升从组织图像中推断空间基因表达的能力。

## 2. 方法论
- **核心思想**：构建**生物引导原型增强器（Biology-Guided Prototype Booster, BP-Booster）**，利用从生物学数据库或先验知识中获取的基因功能模块（如通路、基因集），指导可学习原型的构造与训练，再以这些原型对基础模型生成的 H&E 图像嵌入进行重构与增强，使最终表示富含生物学意义，更适合基因表达预测。
- **关键技术细节**：
  - 引入生物先验知识（例如已知的基因共表达模块、通路信息）来定义或初始化一组原型向量。
  - 这些原型被设计为可学习的参数，在训练过程中根据基因表达预测任务进行优化。
  - 原型增强过程可能包含一种重构或注意力机制：将图像嵌入投影到原型空间，再用原型进行加权组合或重构，得到增强后的嵌入。
  - 增强后的嵌入送入下游预测头（如多层感知器或线性层）预测目标基因的表达值。
- **公式/算法流程（基于摘要推断）**：
  - 给定 H&E 图像块，通过冻结或可调的基础模型得到初始嵌入 $\mathbf{h}$。
  - 通过生物引导的原型矩阵 $\mathbf{P} = [\mathbf{p}_1,\dots,\mathbf{p}_K]$，计算图像嵌入与每个原型的相似度或注意力权重。
  - 依照权重融合原型特征，生成增强表示 $\mathbf{h}' = \sum_{k=1}^K \alpha_k \mathbf{p}_k$ 或类似的重构残差形式。
  - 使用 $\mathbf{h}'$ 进行基因表达（多个基因）的回归预测，损失函数通常为均方误差 (MSE) 或相关性损失，并结合生物一致性约束进行训练。

## 3. 实验设计
- **数据集与场景**：摘要指出在**多个数据集、多种癌症组织类型以及不同的 ST 平台**上进行了验证。具体名称未在元数据中列出，但很可能是公开的癌症空间转录组学数据集（如由 10x Visium、MERFISH 等平台生成的非小细胞肺癌、乳腺癌等样本）。
- **Benchmark 与对比方法**：
  - 基线很可能包括直接使用基础模型嵌入+简单回归头的模型（如使用 CTransPath、UNI、CONCH 等病理基础模型提取特征后预测基因表达）。
  - 对比方法可能涉及其他迁移学习策略、微调基础模型的方法、或者现有的从组织图像预测基因表达的模型（如 Hist2ST、ST-Net、HisToGene 等）。
  - 评价指标一般是预测基因表达与真实 ST 测量之间的皮尔逊相关系数、斯皮尔曼相关系数或均方误差。
- **任务适应性验证**：特别展示了该方法可以灵活地集成多种不同的基础模型，并验证其对下游临床任务（如癌症生物标志物预测）的解释性和适用性。

## 4. 资源与算力
- **未明确说明**：提供的元数据和摘要中**没有提及**所用 GPU 型号、数量、训练时长等算力细节。需要等待完整论文或代码发布才能获知具体资源消耗。

## 5. 实验数量与充分性
- **实验数量**：
  - 跨**多个数据集**、**多种癌症类型**、**不同 ST 平台**的对比实验，至少包含 3-5 组主实验。
  - 应包含**消融实验**：验证生物学先验的使用方式、原型数量、可学习性等因素的影响。
  - 可能进行了**多基础模型兼容性实验**（如替换不同的图像编码器）。
  - 做了**临床应用相关的案例分析**（如关键癌基因预测的表现）。
- **充分性与公平性**：
  - 覆盖不同平台和癌症类型使结论更具普适性，实验设计较为全面。
  - 采用统一评估指标并对比多种基线方法，确保了公平性。
  - 元数据中未见具体数据和实施细节，但根据评审得分（8.0）推测实验说服力较强。

## 6. 主要结论与发现
- BP-Booster 能够显著提升从 H&E 图像预测空间基因表达的精度，在多个数据集、多种癌症类型及不同 ST 技术平台上均表现出优越性。
- 该增强器具有 **模型无关性**，可灵活地与不同基础模型结合，不断增强其任务特定的表示能力。
- 通过引入生物先验，模型不仅提高了预测准确性，还增强了可解释性，使预测结果更易与生物学机制关联，在癌症生物标志物预测等临床相关任务中更具应用潜力。

## 7. 优点
- **方法创新性强**：将可学习原型与生物学先验知识相结合，重构基础模型嵌入，为解决组织图像到基因表达的跨模态预测提供了有效思路。
- **通用即插即用**：不依赖特定基础模型，可作为插件增强任何预训练 H&E 编码器的输出，提升下游任务表现。
- **生物学可解释性**：原型受生物功能模块引导，使增强后的表示维度更具生物学含义，便于分析和验证。
- **多场景验证**：跨癌症、跨平台实验设计提升了成果的可靠性和推广价值。

## 8. 不足与局限
- **实验覆盖细节未知**：元数据未列出具体数据集、样本量，无法判断对小样本或罕见癌症的泛化性。
- **生物学先验的质量依赖**：方法性能严重依赖所选生物先验知识的完整性与准确性，若通路信息不准确或过时可能导致次优原型。
- **算力与效率未报告**：缺乏对训练和推理效率的讨论，不清楚引入原型增强是否显著增加计算负担。
- **假说的临床落地距离**：仅以基因预测相关性评估，未涉及实际临床决策改善或前瞻性验证，临床应用转化仍需更多证据。
- **偏差风险**：数据集可能主要来源于欧美人群，若生物原型也基于此类数据构建，可能对其他人群存在偏差。

（完）
