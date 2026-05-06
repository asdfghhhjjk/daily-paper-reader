---
title: "Interpreting and Validating a Deep Learning Model Predictive of Spatial Morphologic-Molecular Patterns in Lung Adenocarcinoma, Using Ground Truth Immunohistochemistry"
title_zh: 利用真实免疫组化结果解释和验证可预测肺腺癌空间形态—分子模式的深度学习模型
authors: "Rao, V. R., Workman, A. A., Palisoul, S. M., Limoge, C. J., Vaickus, L. J., Zanazzi, G. J., Lu, L., Liu, X., Sukhadia, S. S."
date: 2026-04-23
pdf: "https://www.biorxiv.org/content/10.64898/2026.04.20.719723v1.full.pdf"
tags: ["query:pathseg"]
score: 7.0
evidence: "用于H&E全切片图像空间形态模式的深度学习模型"
tldr: 本研究针对肺腺癌复杂的形态与分子异质性，提出了可解释的深度学习模型XpressO-Lung，可利用常规HE染色全切片图像预测多个基因的空间表达模式，并通过免疫组化实验验证模型预测结果的可靠性，为肿瘤空间分子特征研究和精准诊疗提供新途径。
source: biorxiv
selection_source: fresh_fetch
motivation: 肺腺癌具有显著的组织学和分子异质性，传统基因组学和空间转录组学方法受限于成本和操作复杂性。
method: 研究团队基于200例TCGA肺腺癌样本构建并训练XpressO-Lung模型，从病理切片学习形态—转录组关联并预测基因空间表达模式。
result: 模型对多个关键基因的空间表达模式预测AUC范围为0.64至0.92，并在独立免疫组化验证中表现出较高一致性。
conclusion: XpressO-Lung有效连接了组织病理学与转录组学，实现了可解释的空间形态分子分析，助力肺腺癌的生物标志物发现和精准治疗。
---

## 摘要
肺腺癌（LUAD）是非小细胞肺癌中最常见的亚型，具有显著的组织学和分子异质性。尽管基因组分析已识别出关键的致癌驱动因子和免疫特征，但其应用受到成本、技术要求及组织样本可得性的限制。此外，空间转录组学能够提供分子层面的空间信息，但其操作仍具挑战性且耗时。为弥补这一空缺，我们开发了 XpressO-Lung，这是一种可解释的深度学习模型，可通过学习组织形态与相应整体转录组数据之间的关联，在基于苏木精-伊红（H&E）染色的诊断用全切片图像（Dx-WSIs）上空间预测肿瘤及其微环境中的基因表达异质性。利用来自癌症基因组图谱（The Cancer Genome Atlas）的 200 例 LUAD 病例，XpressO-Lung 能够在 Dx-WSIs 上预测 NAPSA、TP53I3、CD8A、TTF1、KRT7、CDKN2A、FOXO1、KEAP1、RB1 和 TP53 的空间表达模式，其 AUC 范围为 0.64 至 0.92。所预测的空间基因表达模式与已知的肿瘤及其微环境的形态学相互作用一致，能够直接在 Dx-WSIs 上捕捉生物学事件。这些空间－形态－分子关联进一步通过达特茅斯健康中心的临床样本免疫组化验证，显示出模型预测的空间模式与观察到的组织形态特征具有一致性。通过将预测性能与 Dx-WSIs 上基因表达的空间可解释性相结合，XpressO-Lung 模型在组织病理学与整体转录组学之间建立了桥梁，为 LUAD 的生物标志物发现、治疗分层及精准肿瘤学研究提供了可解释的空间－形态－基因组分析方法。

## Abstract
Lung adenocarcinoma (LUAD), the most common subtype of non-small cell lung cancer, exhibits profound histological and molecular heterogeneity. While genomic profiling has identified key oncogenic drivers and immune signatures, its use is limited by cost, technical demands and tissue availability. In addition, spatial transcriptomics provides spatially resolved molecular insights but remains challenging and time-consuming. To address this gap, we developed XpressO-Lung, an explanatory deep learning model that predicts gene expression heterogeneity spatially in tumor and its microenvironment on hematoxylin and eosin based diagnostic (Dx) whole-slide images (WSIs) by learning associations between tissue morphology and the corresponding bulk-transcriptomic data. Utilizing 200 LUAD cases from The Cancer Genome Atlas, XpressO-Lung predicted spatial expression patterns of NAPSA, TP53I3, CD8A, TTF1, KRT7, CDKN2A, FOXO1, KEAP1, RB1 and TP53 on Dx-WSIs with AUCs ranging from 0.64 to 0.92. The predicted spatial gene expression patterns aligned with the known morphologic interactions of the tumor and its microenvironment, capturing biological events directly on Dx-WSIs. These spatio-morpho-molecular associations were further validated using immunohistochemistry on an external set of clinical samples at Dartmouth Health, demonstrating concordance between model-predicted spatial patterns and observed histomorphologic features. By coupling predictive performance with spatial interpretability of gene expression on Dx-WSIs, the XpressO-Lung model bridges histopathology and bulk-transcriptomics, enabling explainable spatio-morpho-genomic analyses to advance biomarker discovery, therapeutic stratification and precision oncology in LUAD.