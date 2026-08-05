---
title: Efficient Patch Search in Whole Slide Images via Morphological Momentum Prototype Learning
title_zh: 基于形态学动量原型学习的全切片图像高效patch搜索
authors: "Sihyeon Park, Jungwoo Park, Hyunjae Kim, Jaewoo Kang, Bumsoo Kim"
date: 2025-09-20
pdf: "https://openreview.net/pdf?id=rYbYbgeaEv"
tags: ["query:path-xai-sel"]
score: 9.0
evidence: 利用形态学原型在WSI中选择信息性patch以实现高效搜索
tldr: 针对全切片图像处理中计算复杂度高的问题，提出基于形态学动量原型学习的patch高效搜索方法，通过原型匹配快速定位具有判别信息的区域，提升大图分析的效率与可解释性。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 解决高分辨率WSI中全量patch分析的计算负担。
method: 提出形态学动量原型学习实现patch的快速筛选。
result: 在大幅减少计算量的同时保持了诊断性能。
conclusion: 为WSI分析提供了一种高效且可解释的patch选择策略。
---

## Abstract
Digital histopathology images play a crucial role in cancer diagnosis, therapeutic response prediction, and identification of clinically relevant morphological features. However, processing Whole Slide Images (WSI) with gigapixel resolution introduces significant challenges in computer vision, exceeding the memory capacity of standard vision encoders. To address this, recent methods employ a multi-stage pipeline: dissecting the image into small patches, extracting patch-level features, and aggregating these features using global pooling through Multi-Instance Learning (MIL) to form a final slide-level representation. Despite achieving clinical-grade performance, this approach becomes increasingly complex with higher magnification due to the quadratic increase in patch numbers and the generation of numerous irrelevant or redundant patches. This complexity burdens the global pooling network, resulting in long inference times and excessive computational resources, while redundant patches introduce noise during the MIL process, limiting the model’s ability to utilize high-magnification features fully. To overcome these challenges, we propose Momentum Morphological Prototype Learning (MMPL), an efficient method that redefines WSI diagnosis as a searching process of relevant patch-level representations with a learned set of global prototypes. MMPL trains a fixed set of prototypes to retrieve the most informative patches, computing the diagnostic score using only the retrieved patches. Evaluated on WSI classification benchmarks, MMPL achieves state-of-the-art performance across various pathology tasks, including metastasis detection, tumor grading, and tumor subtyping.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义
- **核心问题**：处理全切片图像（WSI）时，随着放大倍数的增加，图像切割产生的patch数量呈二次增长，其中包含大量无关或冗余的patch。这导致全局池化网络（MIL聚合器）的推理计算量巨大，同时冗余patch引入噪声，限制了模型充分利用高倍率特征的能力。
- **整体含义**：提出一种将WSI诊断重新定义为“基于全局原型搜索相关patch表征”的范式，旨在通过选择最具有信息量的少量patch，替代传统的全量patch特征聚合，从而大幅降低计算复杂度并提升效率与可解释性。

### 2. 论文提出的方法论
- **核心思想**：训练一组固定的全局原型（prototypes），在WSI的patch级特征中快速 **搜索/检索** 信息量最大的patch，并仅使用这些被检索到的patch来计算最终的诊断分数。
- **关键技术细节**：
    - **形态学动量原型学习（MMPL）**：学习一组可代表关键形态学特征的全局原型，以某种动量机制（文中未详述）更新，确保原型稳定且具有代表性。
    - **搜索与检索机制**：将WSI的每个patch特征与这组原型进行匹配（如相似度计算），筛选出最相关的少量patch参与后续诊断决策，丢弃大量无关patch。
    - **端到端训练**：原型被训练为能够检索出对下游分类任务最具判别力的patch，使整个流程可以进行联合优化。
- **算法流程（文字描述）**：
    1. 将WSI切割为大量patch，使用视觉编码器提取每个patch的嵌入向量。
    2. 维护一组可学习的全局原型向量，并利用动量更新策略保持其稳定。
    3. 对于每个WSI，计算所有patch与每个原型的匹配得分，根据得分检索出最相关的top-k个patch。
    4. 将检索到的patch特征进行聚合（如注意力池化），得到幻灯片级表示，并输出分类分数。
    5. 模型训练时，损失函数同时优化分类准确性和原型检索质量。

### 3. 实验设计
- **数据集/场景**：摘要中提及在WSI分类基准上进行评估，涵盖多种病理任务——**转移检测、肿瘤分级、肿瘤亚型分型**。但具体数据集名称（如CAMELYON16、TCGA等）原文未提供。
- **对比方法**：摘要仅指出“MMPL achieves state-of-the-art performance”，未列出具体的对比方法名称，但可以推测应与当前主流的MIL方法（如ABMIL、CLAM、TransMIL、DSMIL等）进行了比较。
- **基准**：以WSI分类准确率/性能为基准，同时可能评估了计算效率（如推理速度、使用的patch数量）。

### 4. 资源与算力
- 用户提供的摘要和元数据中 **未明确说明** 所使用的GPU型号、数量、训练时长或整体算力消耗。这些细节需从论文全文中获取。

### 5. 实验数量与充分性
- **实验组数推测**：摘要提到涵盖了多个任务（转移检测、肿瘤分级、亚型分型），因此至少在三个不同的临床分类任务上进行了实验。通常还需要包括消融实验（如验证原型数量、检索patch数量、动量机制等）、可视化分析以及效率对比实验。
- **充分性与公平性**：从现有信息无法判断实验是否充分客观。仅凭摘要声称“达到最先进性能”，需要查看原文中的具体数字、统计显著性检验、多数据集交叉验证以及对比方法的复现情况才能给出客观评价。

### 6. 论文的主要结论与发现
- MMPL能够通过 **仅使用检索到的少量高信息量patch**，高效地完成WSI诊断，其性能在多个病理任务上达到同期最优（state-of-the-art）。
- 该方法成功将WSI诊断重构为patch搜索问题，有效缓解了高放大倍数下因patch激增带来的计算爆炸和噪声问题，在保持临床级诊断精度的同时显著提升了计算效率。

### 7. 优点（亮点）
- **计算高效**：通过原型检索抛弃大量冗余patch，极大降低了MIL聚合阶段的输入规模，缩短推理时间。
- **可解释性强**：检索到的patch可直观展示模型关注的形态学区域，为诊断提供依据。
- **范式创新**：将WSI分析从传统的“特征提取→全局池化”转为“基于原型的主动搜索”，为高分辨率医学图像处理提供了新思路。
- **性能优异**：在多个任务上取得SOTA，证明了信息筛选的有效性。

### 8. 不足与局限
- **实验细节缺失**：基于当前提供的内容，无法评估具体的实验覆盖范围（如跨中心泛化性）、原型数量的敏感性、动量策略对超参数的依赖、对不同染色协议的鲁棒性等。
- **偏差风险**：仅检索少量patch可能丢失全局上下文中的长程关联或稀有病理性特征，对于一些需要综合全片模式判别的任务可能存在风险。
- **应用限制**：方法高度依赖原型学习的质量，若训练数据未能覆盖某些重要形态亚型，原型库可能存在遗漏，导致漏检。
- **对比不透明**：未列出具体对比方法及公平性设置，难以判断“SOTA”的含金量。

（完）
