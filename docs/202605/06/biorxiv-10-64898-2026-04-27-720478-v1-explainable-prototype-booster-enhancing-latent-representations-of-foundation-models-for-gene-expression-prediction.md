---
title: "Explainable Prototype Booster: Enhancing Latent Representations of Foundation Models for Gene Expression Prediction"
title_zh: 可解释原型增强器：提升基础模型潜在表示以改进基因表达预测
authors: "Li, C., Nguyen, Q."
date: 2026-04-29
pdf: "https://www.biorxiv.org/content/10.64898/2026.04.27.720478v1.full.pdf"
tags: ["query:cellrep"]
score: 8.5
evidence: "增强基础模型的潜表征以从H&E图像预测基因表达"
tldr: 本文针对基础模型在基因表达预测中的局限，提出可解释原型增强器EP-Booster，利用生物学先验构建可学习原型优化图像嵌入，使模型预测结果具有通路层可解释性。实验显示，该方法在多癌种空间转录组数据上显著提升预测表现与生物学解释度。
source: biorxiv
selection_source: fresh_fetch
motivation: 现有基础模型虽能生成通用组织图像嵌入，但未针对基因表达预测任务优化，缺乏任务特异性与可解释性。
method: 论文提出Explainable Prototype Booster，通过引入生物学先验知识和可学习原型来优化基础模型的嵌入表示。
result: 在多个数据集和癌症类型上，EP-Booster性能优于现有方法，且提升了临床相关预测的可靠性与解释性。
conclusion: EP-Booster显著提升了基础模型的任务适应性和可解释性，为癌症分子诊断和精准医疗提供了新的途径。
---

## 摘要
空间转录组学（Spatial transcriptomics, ST）是一项前沿技术，能够在保留空间背景信息的同时测量基因表达，并生成病理级别的组织图像。虽然ST技术已促进了许多重要发现，并在病理诊断与预后中展现出巨大应用潜力，但其仍存在耗时和成本高的问题。通过组织学H&E染色组织图像预测癌症的基因标志物，有望克服这些技术瓶颈，为精准与个体化病理学开辟新方向。近年来，基础模型（foundation models）在生成H&E图像的一般用途嵌入方面表现出改进。然而，这些改进后的表征并未针对基因表达预测进行优化，缺乏任务特定的适应性。为了解决这一问题，我们提出了Explainable Prototype Booster（EP-Booster），一种通过引入生物学先验知识来指导可学习原型的构建和训练，从而优化嵌入表示并提升基因表达预测性能的方法。值得注意的是，该模型的预测结果通过与原型相关的通路级（pathway-level）归因具有内在可解释性。在多个数据集、不同癌症类型及空间转录组平台上的大量实验表明，EP-Booster在性能上始终优于现有方法。此外，EP-Booster可以与多种基础模型相结合，以增强任务特定表征，从而在包括癌症生物标志物预测、生存分析和药物反应预测等临床相关应用中提升预测性能和生物学可解释性。

## Abstract
Spatial transcriptomics (ST) is a cutting-edge technology that measures gene expression while preserving spatial context and generating pathology-grade tissue images. Although ST has enabled numerous discoveries and demonstrated a huge application potential in pathological diagnosis and prognosis, the technology remains time-consuming and costly. The ability to predict gene markers of cancer from histological H&E-stained tissue images can overcome these technological barriers to open new horizons for precision and personalised pathology. Recently, foundation models have demonstrated improvements in generating general-purpose embeddings of H&E-images. However, these improved representations are not optimized for gene expression prediction and lack task-specific adaptability. To address this limitation, we propose the Explainable Prototype Booster (EP-Booster), which incorporates biological prior knowledge to guide the construction and training of learnable prototypes for embedding refinement, thereby improving gene expression prediction. Importantly, model predictions are inherently interpretable through pathway-level attributions associated with the prototypes. Extensive experiments across multiple datasets, cancer types, and spatial transcriptomics platforms demonstrate that EP-Booster consistently outperforms existing methods. Moreover, EP-Booster can be integrated with diverse foundation models to enhance task-specific representations, thereby improving predictive performance and biological interpretability in clinically relevant applications, including cancer biomarker prediction, survival analysis, and drug response prediction.