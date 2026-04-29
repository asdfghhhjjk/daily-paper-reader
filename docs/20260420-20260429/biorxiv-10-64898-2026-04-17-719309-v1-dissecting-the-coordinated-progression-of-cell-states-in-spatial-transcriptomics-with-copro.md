---
title: Dissecting the coordinated progression of cell states in spatial transcriptomics with CoPro
title_zh: 利用 CoPro 剖析空间转录组学中细胞状态的协调进程
authors: "Miao, Z., Qu, Y., Huang, S., Laux, L., Peters, S., Aristel, A., Zhang, Z., Niedernhofer, L. J., McMahon, A., Kim, J., Zhang, N."
date: 2026-04-21
pdf: "https://www.biorxiv.org/content/10.64898/2026.04.17.719309v1.full.pdf"
tags: ["query:cellrep"]
score: 7.5
evidence: 空间转录组学和组织学中细胞状态演变的计算框架
tldr: 本研究针对空间转录组学中细胞状态空间协调难题，提出了计算框架CoPro，支持监督与无监督模式下识别细胞间协同的基因表达程序，并成功在多种组织中揭示解剖结构与疾病信号的复杂空间关系。
source: biorxiv
selection_source: fresh_fetch
motivation: 空间转录组学需要识别在组织中连续变化且跨细胞类型协调的基因表达程序。
method: 提出了一个计算框架CoPro，用于检测细胞状态在空间上的协同演进。
result: CoPro在多种组织数据中成功解析了重叠的空间模式和细胞状态，如结肠、脑、肝脏及肾脏。
conclusion: CoPro能有效解析复杂组织中空间协同的基因表达过程，助力揭示组织功能与疾病机制。
---

## 摘要
空间转录组学使研究者能够探究细胞在组织内如何协调其分子状态，从而为理解正常功能与疾病过程提供洞见。一个关键挑战是识别在空间上连续变化并在细胞类型间协调的基因表达程序。我们提出了 CoPro，这是一种用于检测细胞状态空间协调进程的计算框架。CoPro 可以在监督和非监督模式下运行，以识别在细胞内或细胞间协同变化的基因程序，并解析多个重叠的空间模式。CoPro 可应用于单细胞水平的空间转录组学数据集，包括 MERFISH、SeqFISH+、Xenium 以及基于组织学推测的转录组数据。我们在结肠、大脑、肝脏和肾脏组织的数据中展示了 CoPro 的实用性。在结肠中，CoPro 将沿隐窝轴的上皮分化与空间局部化的炎症信号区分开来。在衰老肝脏中，它识别出多个叠加于解剖分区之上的与衰老相关的细胞程序。在大脑中，灵活的核设计使其能够解耦沿背腹和内外侧轴的基因表达梯度。在肾脏中，CoPro 识别出对肾单位功能至关重要的小管与血管之间的协调。这些结果展示了 CoPro 在分析复杂组织中基因表达空间协调及解析重叠生物过程（如解剖结构与疾病相关变异）方面的实用价值。

## Abstract
Spatial transcriptomics enables the study of how cells coordinate their molecular states within tissue, providing insight into both normal function and disease processes. A key challenge is to identify gene expression programs that vary continuously across space and are coordinated between cell types. We present CoPro, a computational framework for detecting the spatially coordinated progression of cellular states. CoPro can operate in both supervised and unsupervised modes to identify gene programs that co-vary within or between cell types, and to disentangle multiple overlapping spatial patterns. CoPro can be applied to single-cell-level spatial transcriptomics datasets, including MERFISH, SeqFISH+, Xenium, and histology-imputed transcriptomic data. We demonstrate the utility of CoPro with data collected from colon, brain, liver, and kidney tissues. In the colon, CoPro separates epithelial differentiation along the crypt axis from spatially localized inflammatory signals. In the aging liver, it identifies multiple aging-associated cellular programs superimposed on anatomical zonation. In the brain, the flexible kernel design enables the decoupling of the gene expression gradient along the dorsal-ventral and medial-lateral axes. In the kidney, CoPro identifies tubule-vasculature coordination that is essential in nephron function. These results demonstrate CoPros utility for analyzing spatial coordination of gene expression in complex tissues and disentangling overlapping biological processes, such as anatomical organization and disease-associated variation.