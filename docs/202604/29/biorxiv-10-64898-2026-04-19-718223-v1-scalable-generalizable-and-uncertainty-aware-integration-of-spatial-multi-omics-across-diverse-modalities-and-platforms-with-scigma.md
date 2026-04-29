---
title: "Scalable, Generalizable, and Uncertainty-Aware Integration of Spatial Multi-Omics Across Diverse Modalities and Platforms with SCIGMA"
title_zh: 具备可扩展性、可泛化性与不确定性感知的跨多模态与平台空间多组学整合方法：SCIGMA
authors: "Chang, S., Fleischmann, A., Ma, Y."
date: 2026-04-22
pdf: "https://www.biorxiv.org/content/10.64898/2026.04.19.718223v1.full.pdf"
tags: ["query:cellrep"]
score: 6.5
evidence: 用于空间多组学集成（包括影像数据）的深度学习框架
tldr: 本研究提出SCIGMA，这是一种具备可扩展性和不确定性感知能力的空间多组学整合框架，通过结合对比学习和多视角图神经网络，有效融合高分辨率下的多模态组学数据，显著提升了整合准确性、可解释性与通用性。
source: biorxiv
selection_source: fresh_fetch
motivation: 空间多组学技术的快速发展产生了多模态大规模数据，迫切需要高效、可扩展的整合方法。
method: 提出了SCIGMA深度学习框架，结合不确定性感知对比学习与多视角图神经网络实现空间多组学数据整合。
result: SCIGMA在19个跨多组织和平台的数据集中优于现有方法，提升了空间域检测、特征重建与可重复性。
conclusion: SCIGMA为空间多组学数据整合提供了灵活、通用且面向未来的解决方案。
---

## 摘要
空间组学技术的最新进展使得在高空间分辨率下同时获取转录组学、蛋白质组学、表观基因组学、代谢组学和成像数据成为可能，为解析组织复杂性提供了前所未有的机会。然而，整合这些多样且大规模的空间多模态数据集仍然是一项主要的计算挑战。我们提出了 SCIGMA，这是一种可扩展且可泛化的用于空间多组学整合的深度学习框架。SCIGMA 引入了一种新颖的具备不确定性感知的对比学习目标以及多视图图神经网络，以在学习具有生物学意义的联合表示时保留模态特异性信号。与现有方法不同，SCIGMA 提供了空间分辨的不确定性估计，从而提高了解释性，并能识别具有生物学或技术异质性的区域。SCIGMA 是首个能够支持多达五种模态整合的空间多组学方法——在 Spatial-Mux-Seq 数据上得到了验证——其模块化框架还可扩展至未来具有更多模态的技术。它还可扩展至超过一百万个空间位置，从而能够分析如 VisiumHD 和 Xenium Prime 等超高分辨率数据集。我们在涵盖 8 种模态、10 种组织和 9 个平台的 19 个数据集上对 SCIGMA 进行了评估。在可对比的基准数据集上，SCIGMA 在空间域检测、模态保持、特征重建和可重复性方面均优于现有方法。在不同应用中，SCIGMA 揭示了具有生物学意义的结构，精细划分了空间域，并识别了模态特异性的调控程序；同时，其不确定性估计揭示了可能存在生物学或技术变化的组织区域。总体而言，SCIGMA 提供了一种稳健、灵活且面向未来的解决方案，用于可扩展的空间多模态整合。

## Abstract
Recent advances in spatial omics technologies have enabled simultaneous profiling of transcriptomic, proteomic, epigenomic, metabolomic, and imaging data at high spatial resolution, offering unprecedented opportunities to dissect tissue complexity. However, integrating these diverse and large-scale spatial multi-modal datasets remains a major computational challenge. We present SCIGMA, a scalable and generalizable deep learning framework for spatial multiomics integration. SCIGMA introduces a novel uncertainty-aware contrastive learning objective and multi-view graph neural networks to preserve modality-specific signals while learning biologically meaningful joint representations. Unlike existing methods, SCIGMA provides spatially resolved uncertainty estimates, improving interpretability and identifying regions of biological or technical heterogeneity. SCIGMA is the first spatial multi-omics method to support integration of up to five modalities--as demonstrated on Spatial-Mux-Seq data--and its modular framework is extensible to future technologies with even more modalities. It also scales to over one million spatial locations, enabling analysis of ultra-high-resolution datasets such as VisiumHD and Xenium Prime. We evaluated SCIGMA across 19 datasets spanning 8 modalities, 10 tissues, and 9 platforms. On benchmarkable datasets, SCIGMA outperformed existing methods in spatial domain detection, modality preservation, feature reconstruction, and reproducibility. Across applications, it uncovered biologically meaningful structures, refined spatial domains, and modality-specific regulatory programs, while its uncertainty estimates revealed tissue regions with potential biological or technical variation. Together, SCIGMA provides a robust, flexible, and future-ready solution for scalable spatial multi-modal integration.