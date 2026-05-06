---
title: "TissueFormer: Extending single-cell foundation models to predict population-level phenotypes"
title_zh: TissueFormer：扩展单细胞基础模型以预测群体层级表型
authors: "Benjamin, A. S., Zador, A."
date: 2026-04-28
pdf: "https://www.biorxiv.org/content/10.1101/2025.08.17.670735v2.full.pdf"
tags: ["query:cellrep"]
score: 8.0
evidence: 从单细胞谱组中推断群体级标签
tldr: 本文提出Transformer模型TissueFormer，可从单细胞RNA测序数据推断群体级表型。它解决了传统方法未考虑样本细胞组成的问题，在预测COVID-19严重程度及小鼠脑区域识别任务中表现优异，为高分辨率组织分析和疾病诊断提供新思路。
source: biorxiv
selection_source: fresh_fetch
motivation: 现有单细胞分析忽视了样本内细胞组成对群体表型预测的重要性。
method: 研究提出基于Transformer的神经网络TissueFormer，从单细胞RNA群体中推断组织级标签。
result: TissueFormer在预测COVID-19严重程度和小鼠脑皮层区域身份的任务上超越现有模型。
conclusion: TissueFormer为利用单细胞数据预测群体表型提供了强大框架，可应用于诊断和高分辨率组织映射。
---

## 摘要
背景 单细胞RNA测序技术使我们能够以前所未有的方式深入了解基因表达，并为诊断及组织注释开辟了新的途径。目前，大多数用于解释单细胞数据的计算方法都是基于独立的单细胞转录组谱来预测标签或性质。这种方法忽略了样本中的细胞组成，而细胞组成往往对于推断组织身份或其他样本层面的表型至关重要。

结果 为了克服这一局限，我们提出了TissueFormer，这是一种基于Transformer的神经网络，能够从单细胞RNA谱的群体中推断群体层级的标签，同时保持单细胞分辨率。我们将TissueFormer应用于两个任务：通过血液样本的单细胞RNA测序来预测COVID-19的严重程度，以及通过小鼠大脑的空间转录组数据来预测皮层区域的身份。TissueFormer的表现超越了单细胞基础模型和应用于伪总体数据及细胞类型组成的机器学习方法。

结论 TissueFormer性能的提升有望实现更精确的诊断，并使得能够从空间转录组数据中自动构建单个小鼠的高分辨率脑区图谱。当应用于具有视觉输入发育扰动的小鼠时，这些图谱揭示了预测的视觉皮层面积显著减少，说明了如何量化神经解剖学的个体差异。更广泛来看，TissueFormer提供了一个预测任何受细胞多样性和组织层级组织影响的群体层级表型的框架。

## Abstract
BackgroundSingle-cell RNA sequencing technologies have enabled unprecedented insights into gene expression and opened new pathways for diagnostics and tissue annotation. At present, most computational approaches for interpreting single-cell data predict labels or properties based on isolated single-cell transcriptomic profiles. This approach overlooks the cellular composition within a sample, which is often critical for inferring tissue identity or other sample-level phenotypes.

ResultsTo address this limitation, we introduce TissueFormer, a Transformer-based neural network that infers population-level labels from groups of single-cell RNA profiles while retaining single-cell resolution. We applied TissueFormer to two tasks: predicting COVID-19 severity from single-cell RNA sequencing of blood samples, and predicting cortical area identity from spatial transcriptomic data in mouse brains. TissueFormer outperformed single-cell foundation models and machine learning methods applied to pseudobulk and cell type composition.

ConclusionsTissueFormers higher performance promises more accurate diagnostics and enables the automated construction of high-resolution brain region maps in individual mice directly from spatial transcriptomic data. Applied to mice with developmental perturbations to visual input, these maps revealed a significant reduction in predicted visual cortex area, illustrating how individual differences in neuroanatomy can be quantified. More broadly, TissueFormer provides a framework for predicting any population-level phenotypes which are influenced by cellular diversity and tissue-level organization.