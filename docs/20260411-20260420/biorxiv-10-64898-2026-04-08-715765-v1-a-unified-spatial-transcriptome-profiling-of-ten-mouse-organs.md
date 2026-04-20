---
title: A unified spatial transcriptome profiling of ten mouse organs
title_zh: 十种小鼠器官的统一空间转录组谱图
authors: "Ren, X., Lv, T., Liu, N., Shi, C., Fang, J., Zhao, N., Kang, Q., Wang, D."
date: 2026-04-11
pdf: "https://www.biorxiv.org/content/10.64898/2026.04.08.715765v1.full.pdf"
tags: ["query:pathseg"]
score: 7.0
evidence: "具有匹配H&E染色图像和细胞标注的空间转录组数据集"
tldr: 本研究构建了一个涵盖10种小鼠器官的统一空间转录组数据集，使用Stereo-seq平台生成高分辨率表达矩阵及匹配染色图像，并验证了标注准确性，为空间转录组模型开发和多模态分析提供标准化资源。
source: biorxiv
selection_source: fresh_fetch
figures_json: "[{\"url\": \"assets/figures/biorxiv/biorxiv-10-64898-2026-04-08-715765-v1/fig-001.webp\", \"caption\": \"Table 1. Overview of 10 mouse organ dataset.\", \"page\": 5, \"index\": 1, \"width\": 808, \"height\": 756}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-64898-2026-04-08-715765-v1/fig-002.webp\", \"caption\": \"Table 2. Statistics of genes captured at different squarebin sizes. Squarebin Size indicates the number of DNBs combined into a single analysis unit. Mean Gene Types and Median Gene Types represent the average and median number of gene types captured per bin, respectively. Mean UMI Counts and Median UMI Counts denote the average and median unique molecular identifier (UMI) counts per bin, reflecting the levels of gene expression. The table summarizes the statistics for slice 1 of each tissue.\", \"page\": 6, \"index\": 2, \"width\": 1054, \"height\": 1063}]"
motivation: 为空间转录组学中深度学习模型的训练提供统一、高质量的数据资源。
method: 利用Stereo-seq平台生成包含10种小鼠器官的空间转录组数据集。
result: 获得23个组织切片和21个芯片的单细胞或25微米分辨率表达矩阵，并验证了细胞类型标注的可靠性。
conclusion: 该数据集显著促进了空间转录组方法的研发、性能评测及跨模态研究。
---

## 摘要
空间转录组学的进步促使该领域出现了众多深度学习模型，而训练这些模型需要大量高质量数据，尤其是与组织学图像配对的表达矩阵。在此，我们基于 Stereo-seq 平台，构建了一个统一的空间转录组数据集，涵盖了 10 种小鼠器官——包括脑、肾、肺、胸腺、大肠、皮肤、脾、卵巢、睾丸和子宫——共包含来自 21 个芯片的 23 张组织切片，每张切片均匹配有 ssDNA 或 H&E 染色图像。该数据集为每个样本提供了单细胞分辨率（cell-bin）或方形 bin-50（25 微米 × 25 微米）表达矩阵，并附有相应的细胞类型注释。注释的可靠性进一步通过同一组织不同切片间的一致性以及与典型标志基因表达模式的吻合得到验证。最后，我们比较了 cell-bin 与 bin-50 表达矩阵的特征，展示了 cell-bin 分辨率在细胞注释方面的优势。该数据集为空间转录组学方法的开发、性能评估和多模态分析提供了标准化资源。

## Abstract
Spatial transcriptomics has enabled numerous deep learning models in this area, and training them requires large amounts of high-quality data, especially expression matrices paired with histological images. Here, we present a unified spatial transcriptomic dataset generated using the Stereo-seq platform, covering 10 mouse organs--including brain, kidney, lung, thymus, large intestine, skin, spleen, ovary, testis, and uterus--encompassing 23 tissue sections generated from 21 chips, each with matched ssDNA or H&E staining images. The dataset comprises single-cell-resolution (cell-bin) or square bin-50 (25 {micro}m x 25 {micro}m) expression matrices for each sample, accompanied by corresponding cell type annotations. Annotation robustness was further supported by concordance across different sections of the same tissue and corroboration with canonical marker gene expression patterns. Finally, we compared the characteristics of the cell-bin and bin-50 expression matrices and demonstrated the advantages of cell-bin resolution for cell annotation. This dataset provides a standardized resource for spatial transcriptomics method development, benchmarking, and multimodal analysis.