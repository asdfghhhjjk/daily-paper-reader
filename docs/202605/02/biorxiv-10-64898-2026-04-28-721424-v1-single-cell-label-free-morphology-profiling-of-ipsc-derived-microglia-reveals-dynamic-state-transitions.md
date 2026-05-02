---
title: "Single-cell, label-free morphology profiling of iPSC-derived microglia reveals dynamic state transitions"
authors: "Chen, T., Li, X., Dolga, A. M."
date: 2026-04-29
pdf: "https://www.biorxiv.org/content/10.64898/2026.04.28.721424v1.full.pdf"
tags: ["query:sam"]
score: 8.0
evidence: 在活细胞成像中使用Cellpose-SAM进行单细胞形态分析
tldr: 一种利用Cellpose-SAM的无标记流水线，用于追踪iPSC衍生小胶质细胞的单细胞形态转变。
source: biorxiv
selection_source: fresh_fetch
motivation: 在活细胞成像中使用Cellpose-SAM进行单细胞形态分析。
method: 方法与实现细节请参考摘要与正文。
result: 结果与对比结论请参考摘要与正文。
conclusion: 总体而言，该工作在所述任务上展示了有效性，并提供了可复用的思路或工具。
---

## Abstract
In response to environmental and inflammatory cues, microglia adopt diverse morphologies reflecting their functional state. However, characterizing these morphological alterations in human iPSC-derived microglia (iMGLs) remains limited by reliance on fluorescent labeling, endpoint imaging, and coarse categorical classifications (e.g., ramified vs amoeboid states). Here, we developed a label-free pipeline combining live-cell imaging, Cellpose-SAM segmentation, and CellProfiler-based feature extraction to track iMGL morphology at single-cell resolution over time. Applying this framework to a 24-hour time course of LPS and IFN{gamma} co-stimulation revealed rapid and transient morphological remodeling, with responses peaking within 2-4 hours and partially attenuating thereafter. At single-cell resolution, four morphological states captured the major axes of variation, with co-stimulation driving a pronounced redistribution toward a single Spread state. Extending the analysis to individual inflammatory stimuli (LPS, IFN{gamma}, IL-1{beta}, IL-6, and TNF) revealed graded but overlapping shifts in state composition, with IFN inducing the strongest response, whereas IL-1{beta} showed minimal effects. Importantly, state-level changes alone were insufficient to distinguish stimulus-specific responses. Instead, single-cell density mapping revealed distinct occupancy patterns within a shared morphological landscape. In addition, texture complexity provided an independent feature layer that further separated among treatments, indicating that stimulus identity is represented by continuous, high-dimensional morphological features beyond discrete state assignments. Linking morphology to function, IFN{gamma} produced the largest morphological redistribution and was also the only stimulus to significantly elevate intracellular ROS at 24 h, indicating that morphological remodeling and redox activation can be coordinately engaged by specific inflammatory signals. Together, these findings support a model in which microglia respond to inflammatory stimuli by graded occupancy of a continuous morphological landscape, with each stimulus producing a stimulus-specific occupancy pattern that extends beyond discrete state assignments.