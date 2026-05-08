---
title: "SubCellSpace: Automated characterization of subcellular mRNA localization patterns in spatial transcriptomics"
title_zh: SubCellSpace：空间转录组学中亚细胞mRNA定位模式的自动化表征
authors: "Wouters, D., Alvira Larizgoitia, J. I., Tilkema, N., Van Minsel, P., Alar, C., Seeuws, N., Koulalis, I. T., Lee, M., Vandermeulen, N., Adivarahan, S., Da Cruz, S., Vandereyken, K., Moor, A., Thienpont, B., Voet, T., Sifrim, A."
date: 2026-04-30
pdf: "https://www.biorxiv.org/content/10.64898/2026.04.28.720613v1.full.pdf"
tags: ["query:cellrep"]
score: 7.0
evidence: 将观察到的单细胞亚细胞定位模式嵌入到可解释空间
tldr: 本文提出SubCellSpace，一个用于自动解析空间转录组数据中mRNA亚细胞定位模式的计算框架。它通过学习单细胞定位模式的潜在表示，实现了亚细胞模式的检测、定量和基因共定位分析，并通过实验证实其在识别已知极性基因及探索细胞空间异质性方面的有效性。
source: biorxiv
selection_source: fresh_fetch
motivation: 目前缺乏系统化、自动化的方法来大规模分析细胞内mRNA定位及其功能意义。
method: 通过将单细胞mRNA定位模式嵌入可解释的潜在空间，SubCellSpace实现模式检测、统计推断和异质性分析。
result: SubCellSpace在合成和真实数据中准确识别小肠上皮细胞的极性基因，并展示了其可用于无监督模式探索。
conclusion: SubCellSpace为揭示和定量分析细胞内RNA定位规律提供了高效自动化工具，助力空间转录组学研究。
---

## 摘要
转录本的局部翻译是各类生物领域中普遍存在的现象。许多亚细胞RNA定位及其功能重要性的实例已被描述。然而，这些实例仍然是零散的，需要进行更系统的、覆盖基因组和细胞类型的分析。当前的空间转录组技术能够以亚细胞分辨率表征数百至数千种转录本物种，从而实现对亚细胞mRNA定位的大规模研究。本文提出了SubCellSpace，一种用于学习mRNA定位模式通用表征的计算框架。通过将单细胞的亚细胞定位模式（SLPs）嵌入可解释的潜在空间，SubCellSpace能够检测并统计推断SLPs的存在，发现共定位的基因对，并刻画不同细胞在模式呈现上的异质性。我们在合成数据和真实数据中对SubCellSpace进行了基准测试，结果表明它能够正确检测出先前在小鼠小肠肠上皮细胞中已报道的顶端/基底极化基因，并能够编码肠上皮细胞的取向。此外，我们提供了一个定制的空间转录组验证数据集，用于基于先前在HEK293T细胞中报告的富集于亚细胞结构附近的转录本来评估SLP识别。我们提出了一种实用且计算效率高的分类工作流程，能够自动检测局部转录本物种并量化其模式化程度，同时控制假阳性率。最后，我们展示了SubCellSpace在监督和无监督环境下的应用，可用于分类预定义的SLPs，或在不预设模式类型的情况下探索空间模式化。像SubCellSpace这样的自动化AI模型及其与空间转录组分析流程的整合，将有助于揭示先前未知的亚细胞RNA定位现象，为研究转录后调控机制提供新的见解。

## Abstract
The localized translation of transcripts is a universal phenomenon across biological domains. Many examples of subcellular RNA localization and their functional importance have been described. However, these examples remain anecdotal, and a more systematic genome and cell-type-wide analysis is needed. Current spatial transcriptomic techniques can characterize hundreds to thousands of transcript species at subcellular resolutions, enabling the large-scale investigation of subcellular mRNA localization. Here we describe SubCellSpace, a computational framework to learn general representations of mRNA localization patterns. By embedding observed single-cell subcellular localization patterns (SLPs) to an interpretable latent space, SubCellSpace can detect and statistically infer the presence of SLPs, uncover colocalizing gene-pairs and characterize cellular heterogeneity for pattern-presentation. We benchmark SubCellSpace in both synthetic and real data, showing it can correctly detect previously described apical/basal polarized genes in the enterocytes of mouse small-intestine, as well as encode the enterocytes orientation. Additionally, we provide a tailored spatial transcriptomics validation dataset for benchmarking SLP identification based on transcripts previously described to be enriched near subcellular structures in HEK293T cells. We propose a practical and computationally-efficient classification workflow that automatically detects localized transcript species and quantifies their degree of patterning, while controlling false positive rates. Finally, we showcase SubCellSpace in both supervised and unsupervised settings, to either classify pre-determined SLPs or to explore spatial patterning without specifying pattern types a priori. Automated AI models such as SubCellSpace and their integration in spatial transcriptomics analysis workflows will help characterize previously undiscovered subcellular RNA localization phenomena, providing novel insights into post-transcriptional regulation mechanisms.