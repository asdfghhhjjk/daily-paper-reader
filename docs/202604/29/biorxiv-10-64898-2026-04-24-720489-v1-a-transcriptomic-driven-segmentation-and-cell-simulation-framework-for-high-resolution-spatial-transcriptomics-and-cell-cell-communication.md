---
title: A transcriptomic-driven segmentation and cell simulation framework for high-resolution spatial transcriptomics and cell-cell communication
title_zh: 一种用于高分辨率空间转录组学与细胞间通信的基于转录组驱动的分割与细胞模拟框架
authors: "Wanchai, V., Bustamante-Gomez, N. C., Kurilung, A., Beenken, K. E., Cortes, S., Smeltzer, M. S., Leung, Y.-K., Xiong, J., Almeida, M., O'Brien, C. A., Nookaew, I."
date: 2026-04-28
pdf: "https://www.biorxiv.org/content/10.64898/2026.04.24.720489v1.full.pdf"
tags: ["query:pathseg"]
score: 7.5
evidence: 转录组驱动的分割和细胞模拟框架
tldr: 本研究开发了TENGU框架，以转录信号为主导实现高分辨率细胞分割与模拟，通过迭代优化校正空间误差，大幅提升高密度组织中的细胞识别和空间通讯分析精度，为复杂组织的分子解构提供新工具。
source: biorxiv
selection_source: fresh_fetch
motivation: 传统的空间转录组细胞分割高度依赖组织学图像，难以在高密度或病变组织中准确识别单细胞。
method: 研究提出以转录信号密度为核心并结合细胞模拟的分割算法，实现端到端空间转录组分析流程。
result: TENGU在小鼠脑和炎症骨组织等复杂环境中表现出更高的转录组区分度，并成功识别关键细胞通讯网络。
conclusion: TENGU克服传统方法对图像依赖的局限，提供稳健灵活的计算框架以准确解析组织微结构。
---

## 摘要
Visium HD 空间转录组学平台能够在接近单细胞分辨率下实现转录组范围的分析。然而，准确的细胞分割以定义空间边界高度依赖组织学图像。现有方法在组织细胞密度高、存在炎症或矿化的情况下难以界定单个细胞，导致转录信号穿透和聚类不准确。为此，我们开发了 TENGU（Transcript-signal Enrichment and Grouping Unit），一个综合的端到端生物信息学软件包。与现有工具不同，TENGU 采用基于转录信号优先的分割策略，将转录信号密度作为主要模态，仅在未解区域中使用组织学图像作为辅助。通过一种新的基于转录组的细胞模拟算法进一步优化初始边界。基于局部基因表达概率的迭代边界优化有效减少空间信号散射，同时保留生物学上不同的分子特征。该流程可无缝集成组织分割、高分辨率细胞类型注释以及基本的空间感知细胞间通信（CCC）分析。我们将 TENGU 在多种复杂微环境下与 10X Genomics 及 Bin2cell 流程进行细胞分割的严格对比。TENGU 在小鼠脑中表现出更高的转录组差异性，成功捕获了基质嵌入型骨细胞，并在小鼠骨髓炎模型中定位关键的骨免疫细胞通信网络（Tgfb 和 Il1a）。此外，TENGU 还在高度致密的人源结直肠癌异种移植模型中解析出物种特异性的促肿瘤信号枢纽（MDK-SDC4）。通过减少传统图像依赖分割的局限，TENGU 提供了一个高度可适应且稳健的计算框架，使研究者能够准确解码健康与病理组织中复杂的功能微观结构。

## Abstract
The Visium HD spatial transcriptomics platform enables transcriptome-wide profiling at near-single-cell resolution. However, accurate segmentation of cells to define spatial boundaries relies heavily on histological images. Previous approaches struggle to define cells when the tissues have high cell density, are inflamed, or are mineralized, leading to transcriptomic bleed-through and inaccurate clustering. To address this, we developed TENGU (Transcript-signal Enrichment and Grouping Unit), a comprehensive end-to-end bioinformatic software package. Unlike existing tools, TENGU employs a transcript-first segmentation approach, prioritizing transcript-signal density as the primary modality and utilizing histological images only as a secondary supplement in unresolved regions. These initial boundaries are further optimized through a novel transcriptomic-driven cell simulation algorithm. Iterative refinement of boundaries based on localized gene expression probabilities effectively minimizes spatial scattering and preserves biologically distinct molecular signatures. The pipeline seamlessly integrates tissue segmentation, high-resolution cell-type annotation, and basic spatially aware cell-cell communication (CCC) analysis. We rigorously benchmarked TENGU against the 10X Genomics and Bin2cell pipelines for cell segmentation across diverse and technically challenging microenvironments. TENGU demonstrated superior transcriptomic distinctness in the murine brain, successfully captured matrix-embedded osteocytes, and localized critical osteoimmune CCC networks (Tgfb and Il1a) in a murine model of osteomyelitis. TENGU also resolved species-specific, pro-tumorigenic signaling hubs (MDK-SDC4) within a highly compacted human colorectal cancer xenograft. By mitigating the constraints of traditional image-dependent segmentation, TENGU provides a highly adaptable and robust computational framework that empowers researchers to accurately decode the complex functional micro-anatomy of both healthy and pathological tissues.