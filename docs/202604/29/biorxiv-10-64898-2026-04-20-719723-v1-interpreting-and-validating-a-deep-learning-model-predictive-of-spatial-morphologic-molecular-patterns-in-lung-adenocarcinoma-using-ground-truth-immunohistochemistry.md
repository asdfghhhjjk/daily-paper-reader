---
title: "Interpreting and Validating a Deep Learning Model Predictive of Spatial Morphologic-Molecular Patterns in Lung Adenocarcinoma, Using Ground Truth Immunohistochemistry"
title_zh: 利用免疫组织化学真实验证解释和验证深度学习模型在肺腺癌中预测空间形态-分子模式的能力
authors: "Rao, V. R., Workman, A. A., Palisoul, S. M., Limoge, C. J., Vaickus, L. J., Zanazzi, G. J., Lu, L., Liu, X., Sukhadia, S. S."
date: 2026-04-23
pdf: "https://www.biorxiv.org/content/10.64898/2026.04.20.719723v1.full.pdf"
tags: ["query:pathseg"]
score: 8.5
evidence: "在H&E全切片图像上预测基因表达异质性"
tldr: "研究针对肺腺癌的组织与分子异质性问题，开发了XpressO-Lung深度学习模型，该模型利用H&E诊断切片预测并解释基因空间表达模式，并通过免疫组化验证了模型预测的可靠性与生物学意义，实现了组织病理形态与转录组信息的可解释性融合。"
source: biorxiv
selection_source: fresh_fetch
motivation: 肺腺癌具有显著分子与形态异质性，现有分子检测受制于成本和技术限制，因此需要一种从常规病理切片中推断分子特征的新方法。
method: "研究开发了XpressO-Lung深度学习模型，通过学习H&E切片形态与转录组数据关联来预测空间基因表达。"
result: 模型预测LUAD组织切片上多个基因的空间表达模式，AUC在0.64至0.92之间，且与免疫组化结果一致。
conclusion: 该研究展示了可解释的形态-分子预测模型在肿瘤精准诊断与分层治疗中的应用潜力。
---

## 摘要
肺腺癌（LUAD）是非小细胞肺癌中最常见的亚型，呈现显著的组织学和分子异质性。虽然基因组分析已识别出关键致癌驱动因子和免疫特征，但其应用受限于成本、技术要求和组织获取。空间转录组学虽然能提供空间分辨的分子洞察，但仍然存在挑战且耗时。为弥补这一空白，我们开发了 XpressO-Lung，一个可解释的深度学习模型，可在以苏木精-伊红染色为基础的诊断（Dx）全切片图像（WSI）上，通过学习组织形态与相应的整体转录组数据之间的关联，预测肿瘤及其微环境中基因表达的空间异质性。利用癌症基因组图谱（TCGA）中的 200 例 LUAD 病例，XpressO-Lung 在 Dx-WSIs 上预测了 NAPSA、TP53I3、CD8A、TTF1、KRT7、CDKN2A、FOXO1、KEAP1、RB1 和 TP53 的空间表达模式，其 AUC 值范围为 0.64 至 0.92。预测的空间基因表达模式与已知的肿瘤及其微环境的形态学相互作用一致，能够在 Dx-WSIs 上直接反映生物学事件。这些空间-形态-分子关联进一步在达特茅斯健康中心的临床样本上通过免疫组织化学得到验证，模型预测的空间模式与观察到的组织形态特征高度一致。通过将预测性能与 Dx-WSIs 上基因表达的空间可解释性相结合，XpressO-Lung 模型连接了组织病理学与整体转录组学，为可解释的空间-形态-基因组分析提供了可能，从而推动 LUAD 的生物标志物发现、治疗分层与精准肿瘤学的发展。

## Abstract
Lung adenocarcinoma (LUAD), the most common subtype of non-small cell lung cancer, exhibits profound histological and molecular heterogeneity. While genomic profiling has identified key oncogenic drivers and immune signatures, its use is limited by cost, technical demands and tissue availability. In addition, spatial transcriptomics provides spatially resolved molecular insights but remains challenging and time-consuming. To address this gap, we developed XpressO-Lung, an explanatory deep learning model that predicts gene expression heterogeneity spatially in tumor and its microenvironment on hematoxylin and eosin based diagnostic (Dx) whole-slide images (WSIs) by learning associations between tissue morphology and the corresponding bulk-transcriptomic data. Utilizing 200 LUAD cases from The Cancer Genome Atlas, XpressO-Lung predicted spatial expression patterns of NAPSA, TP53I3, CD8A, TTF1, KRT7, CDKN2A, FOXO1, KEAP1, RB1 and TP53 on Dx-WSIs with AUCs ranging from 0.64 to 0.92. The predicted spatial gene expression patterns aligned with the known morphologic interactions of the tumor and its microenvironment, capturing biological events directly on Dx-WSIs. These spatio-morpho-molecular associations were further validated using immunohistochemistry on an external set of clinical samples at Dartmouth Health, demonstrating concordance between model-predicted spatial patterns and observed histomorphologic features. By coupling predictive performance with spatial interpretability of gene expression on Dx-WSIs, the XpressO-Lung model bridges histopathology and bulk-transcriptomics, enabling explainable spatio-morpho-genomic analyses to advance biomarker discovery, therapeutic stratification and precision oncology in LUAD.