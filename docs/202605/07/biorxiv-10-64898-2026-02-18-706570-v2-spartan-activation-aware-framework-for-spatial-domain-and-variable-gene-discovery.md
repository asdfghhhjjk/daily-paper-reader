---
title: "Spartan: activation-aware framework for spatial domain and variable gene discovery"
title_zh: Spartan：一种用于空间域与可变基因发现的激活感知框架
authors: "Faiz, M. F. I., Jokl, E., Jennings, R., Piper Hanley, K., Sharrocks, A., Iqbal, M., Baker, S. M."
date: 2026-04-30
pdf: "https://www.biorxiv.org/content/10.64898/2026.02.18.706570v2.full.pdf"
tags: ["query:cellrep"]
score: 6.0
evidence: 空间转录组学中单细胞水平的高分辨率区域发现
tldr: 本文提出Spartan框架，该方法融合空间拓扑与局部空间激活信号，实现高分辨率的空间域识别与可变基因发现，在多种空间转录组数据中表现出优异的结构保持与鲁棒性。
source: biorxiv
selection_source: fresh_fetch
motivation: 当前空间转录组学在精确识别空间域时存在边界模糊和过度聚合的问题。
method: 提出Spartan框架，将空间拓扑与局部空间激活信号(LSA)结合，构建激活感知的多重图模型。
result: Spartan在多种空间转录组技术中实现高分辨率的组织域划分，并准确识别复杂过渡区域。
conclusion: Spartan为高精度空间域识别和系统级空间分析提供了一种可扩展且解释性强的计算框架。
---

## 摘要
空间转录组学正在迅速发展，朝着单细胞级分辨率迈进，揭示了跨越连续解剖梯度的复杂组织结构。然而，空间域的准确识别仍然是一个核心计算挑战，因为许多现有的聚类方法会模糊解剖边界、混合过渡区域，或无法解析局部的微结构。在此，我们提出了 Spartan——一种基于激活感知的多路图框架，用于高分辨率的空间域发现。Spartan 整合了空间拓扑信息和局部空间激活（Local Spatial Activation, LSA），后者是一种邻域偏差信号，能够捕捉基于相似性聚类常常削弱的局部转录异质性。通过联合建模域内的凝聚性与局部激活结构，Spartan 能在包括 Visium HD、MERFISH、Stereo-seq 和 STARmap 等空间分辨转录组技术中，恢复与解剖结构一致的分区。我们进一步展示了其在发育中人类食管和胃的高分辨率 Visium HD 切片中的应用，其中基于激活感知的图整合能够精确描绘如胃食管交界等复杂的过渡区域，并支持在无需脆弱超参数调整的情况下实现稳定的多尺度域恢复。除域识别外，Spartan 还利用激活感知结构来检测与局部组织重塑相关的空间可变基因。Spartan 的计算复杂度随数据集规模近乎线性增长，为空间系统级分析提供了一个稳健且可解释的框架。

## Abstract
Spatial transcriptomics is rapidly advancing toward single-cell-level resolution, revealing complex tissue architectures organized across continuous anatomical gradients. However, accurate identification of spatial domains remains a central computational challenge, as many existing clustering approaches blur anatomical boundaries, merge transitional zones, or fail to resolve localized microstructures. Here we introduce Spartan, an activation-aware multiplex graph framework for high-resolution domain discovery. Spartan integrates spatial topology and Local Spatial Activation (LSA), a neighborhood deviation signal that captures localized transcriptional heterogeneity often attenuated by similarity-based clustering. By jointly modeling cohesion within domains and localized activation structure, Spartan recovers anatomically aligned partitions across spatially resolved transcriptomics technologies including Visium HD, MERFISH, Stereo-seq, and STARmap. We further demonstrate its utility in a high-resolution Visium HD section of developing human esophagus and stomach, where activation-aware graph integration enables precise delineation of complex transitional regions such as the gastroesophageal junction and supports stable multi-scale domain recovery without fragile hyperparameter tuning. Beyond domain identification, Spartan leverages activation-aware structure to detect spatially variable genes associated with localized tissue remodeling. Spartan scales near-linearly with dataset size, providing a robust and interpretable framework for spatial systems-level analysis.