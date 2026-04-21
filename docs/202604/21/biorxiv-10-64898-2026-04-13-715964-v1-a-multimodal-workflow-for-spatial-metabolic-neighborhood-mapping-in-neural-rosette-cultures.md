---
title: A Multimodal Workflow for Spatial Metabolic Neighborhood Mapping in Neural Rosette Cultures
authors: "Adebayo, O. N., Turaga, A., Chung, M., Fernandez, F., Kemp, M. L."
date: 2026-04-13
pdf: "https://www.biorxiv.org/content/10.64898/2026.04.13.715964v1.full.pdf"
tags: ["query:cellrep"]
score: 7.5
evidence: 用于识别神经玫瑰花结和细胞分辨率代谢映射的分析框架
tldr: 描述了一种用于神经培养物空间代谢映射和细胞级表征的多模态工作流。
source: biorxiv
selection_source: fresh_fetch
figures_json: "[{\"url\": \"assets/figures/biorxiv/biorxiv-10-64898-2026-04-13-715964-v1/fig-001.webp\", \"caption\": \"Figure 2. 441\", \"page\": 25, \"index\": 1, \"width\": 952, \"height\": 1209}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-64898-2026-04-13-715964-v1/fig-002.webp\", \"caption\": \"Figure 4. 448\", \"page\": 26, \"index\": 2, \"width\": 1060, \"height\": 927}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-64898-2026-04-13-715964-v1/fig-003.webp\", \"caption\": \"Figure 1. 438\", \"page\": 24, \"index\": 3, \"width\": 1089, \"height\": 483}]"
motivation: 用于识别神经玫瑰花结和细胞分辨率代谢映射的分析框架。
method: 方法与实现细节请参考摘要与正文。
result: 结果与对比结论请参考摘要与正文。
conclusion: 总体而言，该工作在所述任务上展示了有效性，并提供了可复用的思路或工具。
---

## Abstract
Neural rosettes are hallmarks of the neural progenitor cell stage that is a necessary pre-condition for manufacturing central nervous system lineages. Characterization of early changes during differentiation through positional arrangement and metabolic shifts that occur in a multi-day protocol would facilitate cell culture quality monitoring and optimization of batch culture yield. We describe an analytical framework for identifying neural rosettes from confocal microscopy within a colony of differentiating stem cells and translating co-registered, cell-resolved MALDI imaging data into interpretable readouts that are compatible with cell manufacturing needs. Rather than evaluating hundreds of ion images sequentially, the pipeline converts each region of interest into a single-cell feature matrix and summarizes whole-spectrum variation using PCA, graph-based Leiden clustering, and UMAP visualization. The resultant metabolic neighborhoods provide quantification of molecular heterogeneity within colonies and - when mapped back to x-y space - form coherent spatial domains. Together, these outputs create a practical bridge between multimodal MALDI capabilities and process-relevant interpretation: neighborhoods can be compared across conditions, ranked markers can be prioritized as putative critical quality attributes, and spatial organization can be quantified without manual, feature-by-feature screening.