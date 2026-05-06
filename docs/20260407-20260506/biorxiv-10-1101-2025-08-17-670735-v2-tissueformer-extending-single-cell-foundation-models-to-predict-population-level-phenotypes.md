---
title: "TissueFormer: Extending single-cell foundation models to predict population-level phenotypes"
title_zh: TissueFormer：将单细胞基础模型扩展用于预测群体层面表型
authors: "Benjamin, A. S., Zador, A."
date: 2026-04-28
pdf: "https://www.biorxiv.org/content/10.1101/2025.08.17.670735v2.full.pdf"
tags: ["query:cellrep"]
score: 6.0
evidence: 基于Transformer的网络，从单细胞谱中推断群体级标签
tldr: 本文提出TissueFormer，一种基于Transformer的神经网络模型，用于从单细胞RNA测序群体中预测样本级表型。该模型结合单细胞分辨率与整体组织特征，在COVID-19严重程度预测和小鼠大脑皮层区域识别任务中均显著优于现有方法。
source: biorxiv
selection_source: fresh_fetch
motivation: 现有单细胞分析方法忽略了样本内细胞组成对组织或表型的影响。
method: 研究采用Transformer结构从多细胞RNA表达数据中学习样本级标签预测。
result: TissueFormer在疾病严重度预测和空间转录组脑区识别中表现优异，并揭示发育扰动对脑区大小的影响。
conclusion: TissueFormer实现了更高精度的群体表型预测，并促进组织级特征的自动化分析。
---

## 摘要
背景 单细胞RNA测序技术为理解基因表达提供了前所未有的洞察，并为诊断和组织注释开辟了新的途径。目前，大多数用于解释单细胞数据的计算方法都是基于单个细胞转录组特征来预测标签或属性。然而，这种方法忽视了样本中的细胞组成，而这种组成往往对推断组织身份或其他样本层面的表型至关重要。

结果 为了应对这一局限，我们提出了TissueFormer，这是一种基于Transformer的神经网络，它能够从多个单细胞RNA特征中推断总体层面的标签，同时保持单细胞分辨率。我们将TissueFormer应用于两个任务：根据血液样本的单细胞RNA测序数据预测COVID-19的严重程度，以及从小鼠大脑的空间转录组数据中预测皮层区域的身份。TissueFormer的表现优于单细胞基础模型以及应用于伪批数据和细胞类型组成的机器学习方法。

结论 TissueFormer的更高性能有望实现更精确的诊断，并能够直接基于空间转录组数据，在单个小鼠中自动构建高分辨率的大脑区域图谱。将其应用于视觉输入发育受扰的小鼠时，这些图谱揭示了预测的视觉皮层区域显著缩小，说明了如何定量化个体间神经解剖结构的差异。从更广泛的角度来看，TissueFormer为预测由细胞多样性和组织层次结构所影响的任何总体层面表型提供了一个框架。

## Abstract
BackgroundSingle-cell RNA sequencing technologies have enabled unprecedented insights into gene expression and opened new pathways for diagnostics and tissue annotation. At present, most computational approaches for interpreting single-cell data predict labels or properties based on isolated single-cell transcriptomic profiles. This approach overlooks the cellular composition within a sample, which is often critical for inferring tissue identity or other sample-level phenotypes.

ResultsTo address this limitation, we introduce TissueFormer, a Transformer-based neural network that infers population-level labels from groups of single-cell RNA profiles while retaining single-cell resolution. We applied TissueFormer to two tasks: predicting COVID-19 severity from single-cell RNA sequencing of blood samples, and predicting cortical area identity from spatial transcriptomic data in mouse brains. TissueFormer outperformed single-cell foundation models and machine learning methods applied to pseudobulk and cell type composition.

ConclusionsTissueFormers higher performance promises more accurate diagnostics and enables the automated construction of high-resolution brain region maps in individual mice directly from spatial transcriptomic data. Applied to mice with developmental perturbations to visual input, these maps revealed a significant reduction in predicted visual cortex area, illustrating how individual differences in neuroanatomy can be quantified. More broadly, TissueFormer provides a framework for predicting any population-level phenotypes which are influenced by cellular diversity and tissue-level organization.