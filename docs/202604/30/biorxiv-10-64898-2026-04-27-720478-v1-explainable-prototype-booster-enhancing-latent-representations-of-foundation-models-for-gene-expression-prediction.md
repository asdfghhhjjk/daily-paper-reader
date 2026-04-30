---
title: "Explainable Prototype Booster: Enhancing Latent Representations of Foundation Models for Gene Expression Prediction"
title_zh: 可解释原型增强器：提升基础模型的潜在表示以改进基因表达预测
authors: "Li, C., Nguyen, Q."
date: 2026-04-29
pdf: "https://www.biorxiv.org/content/10.64898/2026.04.27.720478v1.full.pdf"
tags: ["query:pathseg"]
score: 8.5
evidence: "利用基础模型嵌入从H&E染色组织图像中预测基因标记"
tldr: "本文针对基础模型在从H&E染色组织图像预测基因表达中的不足，提出Explainable Prototype Booster方法，利用生物先验知识构建可解释原型优化图像嵌入，在多癌症数据和空间转录组平台上实现更优预测性能与可解释性。"
source: biorxiv
selection_source: fresh_fetch
motivation: 现有基础模型的图像表示虽强大，但缺乏针对基因表达预测的任务特异性和可解释性。
method: 研究提出Explainable Prototype Booster，通过引入生物先验知识构建和训练可学习原型来优化嵌入表示。
result: 在多个数据集、癌症类型和空间转录组平台上，EP-Booster在预测性能和生物学可解释性方面均优于现有方法。
conclusion: EP-Booster显著增强了基础模型在基因表达预测中的表现，并提供可解释的生物学洞察。
---

## 摘要
空间转录组学（Spatial Transcriptomics，ST）是一项前沿技术，能够在保留空间背景的同时测量基因表达，并生成病理级别的组织图像。尽管ST已促成众多发现，并在病理诊断与预后评估中展现出巨大的应用潜力，但该技术仍然耗时且昂贵。能够从苏木精-伊红（H&E）染色的组织图像中预测癌症的基因标志，将有助于克服这些技术障碍，为精准与个体化病理学开辟新前景。近年来，基础模型（foundation models）在生成H&E图像的通用嵌入表示方面取得了显著进展。然而，这些改进的表示在基因表达预测任务上并未得到优化，且缺乏任务特定的适应能力。为解决这一问题，我们提出了具有可解释性的原型增强器（Explainable Prototype Booster，EP-Booster），它通过引入生物学先验知识，引导可学习原型的构建与训练，以改进嵌入表示，从而提升基因表达预测性能。值得注意的是，该模型的预测结果可通过与原型相关的通路级归因实现内在可解释性。我们在多个数据集、癌症类型及空间转录组学平台上进行了大量实验，结果表明EP-Booster在各项指标上均优于现有方法。此外，EP-Booster可与多种基础模型结合，以增强任务特定的表示，从而在癌症生物标志物预测、生存分析及药物反应预测等临床相关应用中，提高预测性能与生物学可解释性。

## Abstract
Spatial transcriptomics (ST) is a cutting-edge technology that measures gene expression while preserving spatial context and generating pathology-grade tissue images. Although ST has enabled numerous discoveries and demonstrated a huge application potential in pathological diagnosis and prognosis, the technology remains time-consuming and costly. The ability to predict gene markers of cancer from histological H&E-stained tissue images can overcome these technological barriers to open new horizons for precision and personalised pathology. Recently, foundation models have demonstrated improvements in generating general-purpose embeddings of H&E-images. However, these improved representations are not optimized for gene expression prediction and lack task-specific adaptability. To address this limitation, we propose the Explainable Prototype Booster (EP-Booster), which incorporates biological prior knowledge to guide the construction and training of learnable prototypes for embedding refinement, thereby improving gene expression prediction. Importantly, model predictions are inherently interpretable through pathway-level attributions associated with the prototypes. Extensive experiments across multiple datasets, cancer types, and spatial transcriptomics platforms demonstrate that EP-Booster consistently outperforms existing methods. Moreover, EP-Booster can be integrated with diverse foundation models to enhance task-specific representations, thereby improving predictive performance and biological interpretability in clinically relevant applications, including cancer biomarker prediction, survival analysis, and drug response prediction.