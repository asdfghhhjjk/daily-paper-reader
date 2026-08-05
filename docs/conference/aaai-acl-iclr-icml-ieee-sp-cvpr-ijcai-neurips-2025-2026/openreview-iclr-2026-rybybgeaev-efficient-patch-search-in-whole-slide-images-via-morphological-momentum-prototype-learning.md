---
title: Efficient Patch Search in Whole Slide Images via Morphological Momentum Prototype Learning
title_zh: 基于形态动量原型学习的高效全切片图像补丁搜索
authors: "Sihyeon Park, Jungwoo Park, Hyunjae Kim, Jaewoo Kang, Bumsoo Kim"
date: 2025-09-20
pdf: "https://openreview.net/pdf?id=rYbYbgeaEv"
tags: ["query:path-xai-sel"]
score: 9.0
evidence: 通过形态动量原型学习在WSI中高效搜索诊断相关补丁
tldr: 针对病理全切片图像放大率增加导致计算复杂度激增的问题，提出形态动量原型学习方法，动态选择具有判别力的补丁进行学习，并利用多实例学习聚合特征，实现高效且高精度的全切片分类。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 高放大率全切片图像处理面临计算复杂度过高、冗余补丁多的问题。
method: 提出形态动量原型学习，利用形态特征筛选关键补丁，并采用多实例学习进行聚合。
result: 在病理图像分类任务上，该方法在保证高精度的同时显著降低了计算开销。
conclusion: 形态动量原型学习为计算病理学中高效利用全切片信息提供了新策略，兼顾效率与性能。
---

## Abstract
Digital histopathology images play a crucial role in cancer diagnosis, therapeutic response prediction, and identification of clinically relevant morphological features. However, processing Whole Slide Images (WSI) with gigapixel resolution introduces significant challenges in computer vision, exceeding the memory capacity of standard vision encoders. To address this, recent methods employ a multi-stage pipeline: dissecting the image into small patches, extracting patch-level features, and aggregating these features using global pooling through Multi-Instance Learning (MIL) to form a final slide-level representation. Despite achieving clinical-grade performance, this approach becomes increasingly complex with higher magnification due to the quadratic increase in patch numbers and the generation of numerous irrelevant or redundant patches. This complexity burdens the global pooling network, resulting in long inference times and excessive computational resources, while redundant patches introduce noise during the MIL process, limiting the model’s ability to utilize high-magnification features fully. To overcome these challenges, we propose Momentum Morphological Prototype Learning (MMPL), an efficient method that redefines WSI diagnosis as a searching process of relevant patch-level representations with a learned set of global prototypes. MMPL trains a fixed set of prototypes to retrieve the most informative patches, computing the diagnostic score using only the retrieved patches. Evaluated on WSI classification benchmarks, MMPL achieves state-of-the-art performance across various pathology tasks, including metastasis detection, tumor grading, and tumor subtyping.

---

## 论文详细总结（自动生成）

# 论文总结：《基于形态动量原型学习的高效全切片图像补丁搜索》

## 1. 论文的核心问题与整体含义

- **研究背景：** 全切片图像（Whole Slide Images, WSIs）具有亿级像素分辨率，在癌症诊断、治疗反应预测及临床形态特征识别中至关重要。
- **核心挑战：** 传统多阶段处理流程需将WSI切割为大量小补丁（patches），再通过多实例学习（MIL）聚合特征。随着放大倍数增加，补丁数量呈二次方增长，大量冗余、无关补丁加重了全局池化网络的计算负担，导致推理时间长、资源消耗大，且引入噪声，限制了高倍率形态特征的充分利用。
- **问题定义：** 如何在高放大率WSI中高效筛选出最具诊断价值的少量补丁，以支撑准确、低耗时的切片级分类。

## 2. 方法论

### 核心思想
- 将WSI诊断重新定义为**相关补丁表征的搜索过程**，通过一组可学习的全局原型（prototypes）动态检索信息量最大的补丁，仅基于检索到的补丁计算诊断分数。

### 关键技术细节
- **形态动量原型学习（Momentum Morphological Prototype Learning, MMPL）：**
  - 固定数量的一组**可训练原型向量**，代表不同诊断相关的形态模式。
  - 训练过程中，每个原型在 WSI 的特征库中检索与其最相似的补丁表征，动量更新维持原型稳定性。
  - 通过**动量更新机制**使原型保持判别性，同时缓解训练过程的不稳定。
- **流程：**
  1. 图像切分为补丁，提取补丁级特征；
  2. 原型与补丁特征计算相似度，筛选 Top-K 个最具信息量的补丁；
  3. 仅将筛选出的补丁特征送入 MIL 聚合器，生成切片级表征；
  4. 基于切片级表征输出分类结果。
- **优化目标：** 最小化分类损失的同时，隐式引导原型聚焦于有诊断价值的形态区域。

## 3. 实验设计

### 数据集与场景
- 覆盖多种病理任务的标准WSI分类基准：
  - 转移检测（metastasis detection）
  - 肿瘤分级（tumor grading）
  - 肿瘤亚型分型（tumor subtyping）
- 具体数据集名称在摘要中未列出，但强调了在多个公开基准上评估。

### Benchmark与对比方法
- **对比方法：** 与现有WSI分类方法比较（摘要未列出具体方法名），包含传统多实例学习流程。
- **评价指标：** 推测为分类准确率、AUC、推理时间、计算资源开销等。

## 4. 资源与算力

- **论文摘要未提供** GPU 型号、数量或训练时长等具体算力信息。
- 由于提取文本仅为验证页，无法判断正文是否包含此类细节。基于提供内容，**算力信息缺失**。

## 5. 实验数量与充分性

- **实验数量：** 至少涉及3类不同病理任务，每个任务可能有多个数据集或场景。摘要提到“在各种病理任务上评估”，表明具有多组实验。
- **充分性：** 若任务覆盖转移检测、分级、分型，则实验层面较为全面，涵盖了病理诊断的关键类别，可验证方法的通用性。
- **客观性与公平性：** 与现有方法对比且达到SOTA，说明对比公平性有基础。但摘要未说明是否进行消融实验（如原型数目、动量机制的作用），故无法进一步判断内部验证充分性。

## 6. 主要结论与发现

- MMPL通过原型学习动态关注关键补丁，**在多个病理分类任务上取得最先进性能**。
- 方法在保持高精度的同时，显著降低了计算开销和推理时间，解决了高倍率WSI计算的效率瓶颈。
- 证明了将诊断任务构建为“相关补丁搜索”这一新策略的有效性。

## 7. 优点

- **创新视角：** 首次将WSI分类建模为基于原型的补丁检索任务，从“全部聚合”转变为“选择性检索”。
- **效率提升明显：** 仅使用部分补丁参与聚合，大幅减少计算量，使高倍率特征得以实际应用。
- **动量更新机制：** 增强了原型学习的稳定性和判别性。
- **多任务验证：** 覆盖转移、分级、分型三类关键病理任务，展现算法泛化能力。

## 8. 不足与局限

- **算力细节缺失：** 基于现有信息无法评估其实际资源消耗与可复现性。
- **消融分析未知：** 未提及原型数量、检索比例、动量系数等关键超参数的影响，内部有效性有待商榷。
- **数据集名称未披露：** 无法确认实验数据集的具体来源与代表性，可能存在特定数据偏差。
- **临床应用限制：** 原型在高异质性组织中的覆盖能力、罕见形态模式的捕获能力未讨论。
- **对比方法不明确：** 仅声明“现有方法”，缺乏具体对比方法清单，影响结果的客观评判。

（完）
