---
title: A Correspondence-Driven Framework for Un-paired Spatial Multi-Omics Integrative Analysis
title_zh: 一种基于对应关系驱动的无配对空间多组学整合分析框架
authors: "Cai, W., Li, W."
date: 2026-04-21
pdf: "https://www.biorxiv.org/content/10.1101/2025.09.14.676067v2.full.pdf"
tags: ["query:cellrep"]
score: 6.5
evidence: 多尺度细胞对应关系和空间异质性表征
tldr: 本研究提出SpatialFuser框架，通过多头协作图注意力自编码和迭代最优传输实现非配对空间多组学数据整合，在多种组学领域上显著提升空间异质性解析与跨模态融合能力。
source: biorxiv
selection_source: fresh_fetch
motivation: 现有空间多组学技术虽能解析组织微环境，但跨异质数据集的综合分析仍具挑战。
method: 采用多头协作图注意力自编码和几何预匹配结合迭代最优传输推断跨切片对应关系，实现多模态空间整合。
result: SpatialFuser在空间域识别、跨切片对齐和多组学整合等任务上表现优于现有方法。
conclusion: SpatialFuser可高精度复原分子模式，揭示发育动态并挖掘被掩盖的生物变异。
---

## 摘要
空间多组学技术的最新进展为解析组织微环境中的分子特征提供了前所未有的机遇，但在跨异质数据集的整合分析中仍面临挑战。在此，我们提出了 SpatialFuser——一个由对应关系驱动的深度学习框架，用于无配对空间表观基因组学、转录组学、蛋白质组学和代谢组学的整合分析。SpatialFuser 引入了多头协同图注意自编码器（Multi-head Collaborative Graph Attention auToEncoder，MCGATE），以推断多尺度的细胞对应关系，从而在超越预定义空间邻域的层面上进行空间异质性的精细化刻画。通过结合灵活的几何预匹配进行粗略初始化，并通过迭代优化传输推断自适应的跨切片对应关系，SpatialFuser 实现了对具有不同几何结构、空间分辨率、发育阶段和分子模态的异质数据集的稳健整合。基准测试表明，SpatialFuser 在空间域识别、跨切片配准和多组学整合方面均显著优于现有的最先进方法。实际数据集的应用显示，SpatialFuser 能够解析精确的分子模式，揭示发育动态，并恢复跨模态的互补信号。我们的方法还实现了对弱相关模态的跨分辨率整合，从而揭示出以往被掩盖的生物学变异。该框架具有通用性和灵活性，可支持定制化分析场景，并具备向新兴组学扩展的潜力。

亮点：
1. 一个统一的深度学习框架，用于空间多组学整合数据分析。
2. 在空间识别、配准和多组学整合方面的性能优于现有最先进方法。
3. 实现前所未有的跨模态分析场景，提供空间多组学的整体视角。
4. 框架设计全面，具有通用性与灵活性，可用于定制化场景与潜在扩展。

## Abstract
Recent advances in spatial multi-omics technologies provide unprecedented opportunities to interpret molecular features in tissue micro-environments but remain challenging in integrative analysis across heterogeneous datasets. Here we present SpatialFuser, a correspondence-driven deep learning framework for integrative analysis across un-paired spatial epigenomics, transcriptomics, proteomics, and metabolomics. SpatialFuser introduces a Multi-head Collaborative Graph Attention auToEncoder (MCGATE) to infer multi-scale cellular correspondences for fine-grained characterization of spatial heterogeneity beyond predefined spatial neighbourhoods. By incorporating flexible geometric pre-matching for coarse initialization and inferring adaptive cross-slice correspondences via iteratively refined optimal transport, SpatialFuser enables robust integration across heterogeneous datasets with varying geometries, spatial resolutions, developmental stages, and molecular modalities. Benchmarking demonstrates superior performance and reliability against existing state-of-the-art methods in spatial domain identification, cross-slice alignment, and multi-omics integration. Applications to real datasets demonstrate that SpatialFuser resolves precise molecular patterns, reveals developmental dynamics, and recovery of complementary signals across modalities. Cross-resolution integration of weakly correlated modalities by our method further uncovers previously obscured biological variation. Our framework is generalizable and versatile, enabling customized analytical scenarios and potential extension for emerging omics.

HighlightsO_LIA unified deep learning framework for spatial multi-omics integrative data analysis
C_LIO_LISuperior performance against state-of-the-art methods in spatial identification, alignment, and multi-omics integration
C_LIO_LIUnprecedented cross-modality analysis scenarios to offer a holistic view of spatial multi-omics
C_LIO_LIComprehensive framework design with generalizability and versatility for customized scenarios and potential extension
C_LI