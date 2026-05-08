---
title: "Spartan: activation-aware framework for spatial domain and variable gene discovery"
title_zh: Spartan：一种用于空间域与可变基因发现的激活感知框架
authors: "Faiz, M. F. I., Jokl, E., Jennings, R., Piper Hanley, K., Sharrocks, A., Iqbal, M., Baker, S. M."
date: 2026-04-30
pdf: "https://www.biorxiv.org/content/10.64898/2026.02.18.706570v2.full.pdf"
tags: ["query:cellrep"]
score: 6.5
evidence: 单细胞水平分辨率下的高分辨率区域发现
tldr: 本文提出Spartan，一个融合空间拓扑与局部空间激活信号的多重图框架，用于高分辨率识别空间转录组数据中的组织域和变量基因，有效改善现有方法在边界与过渡区识别中的不足，实现稳定、可扩展的空间系统级分析。
source: biorxiv
selection_source: fresh_fetch
motivation: 现有空间转录组分析方法难以准确识别连续组织梯度中的空间结构与微区。
method: Spartan通过构建整合空间拓扑与局部空间激活（LSA）的多重图模型联合建模区域内凝聚与异质结构。
result: Spartan在多种空间转录组技术上实现了高精度解剖对齐分区和变量基因识别，并具备近线性扩展性。
conclusion: Spartan为空间组学提供了可扩展、稳定且可解释的高分辨率域和变量基因发现新框架。
---

## 摘要
空间转录组学正快速发展到单细胞级分辨率，揭示了沿连续解剖梯度组织的复杂组织结构。然而，空间域的精确识别仍然是一个核心的计算挑战，因为许多现有的聚类方法会模糊解剖边界、合并过渡区域或无法解析局部微结构。本文介绍了 Spartan，这是一种用于高分辨率域发现的激活感知多路图框架。Spartan 整合了空间拓扑与局部空间激活（Local Spatial Activation, LSA）信号，这是一种邻域偏差信号，用于捕获基于相似性聚类中常被削弱的局部转录异质性。通过联合建模域内凝聚性与局部激活结构，Spartan 在包括 Visium HD、MERFISH、Stereo-seq 和 STARmap 等空间分辨转录组技术中，能够恢复与解剖结构一致的分区。我们进一步在发育中人类食管和胃的高分辨率 Visium HD 切片中展示了其应用价值，其中激活感知的图整合能够精确划定复杂的过渡区域（如胃食管交界处），并支持在无需精细超参数调优的情况下实现稳定的多尺度域恢复。除域识别外，Spartan 还利用激活感知结构检测与局部组织重塑相关的空间可变基因。Spartan 的计算规模几乎与数据集大小呈线性增长，为空间系统级分析提供了一个稳健且可解释的框架。

## Abstract
Spatial transcriptomics is rapidly advancing toward single-cell-level resolution, revealing complex tissue architectures organized across continuous anatomical gradients. However, accurate identification of spatial domains remains a central computational challenge, as many existing clustering approaches blur anatomical boundaries, merge transitional zones, or fail to resolve localized microstructures. Here we introduce Spartan, an activation-aware multiplex graph framework for high-resolution domain discovery. Spartan integrates spatial topology and Local Spatial Activation (LSA), a neighborhood deviation signal that captures localized transcriptional heterogeneity often attenuated by similarity-based clustering. By jointly modeling cohesion within domains and localized activation structure, Spartan recovers anatomically aligned partitions across spatially resolved transcriptomics technologies including Visium HD, MERFISH, Stereo-seq, and STARmap. We further demonstrate its utility in a high-resolution Visium HD section of developing human esophagus and stomach, where activation-aware graph integration enables precise delineation of complex transitional regions such as the gastroesophageal junction and supports stable multi-scale domain recovery without fragile hyperparameter tuning. Beyond domain identification, Spartan leverages activation-aware structure to detect spatially variable genes associated with localized tissue remodeling. Spartan scales near-linearly with dataset size, providing a robust and interpretable framework for spatial systems-level analysis.