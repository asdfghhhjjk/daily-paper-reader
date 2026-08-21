---
title: "Mantpy: a framework for extracellular matrix analysis in spatial proteomics"
title_zh: Mantpy：空间蛋白质组学中细胞外基质分析框架
authors: "Ghafoor, M., Parkinson, J. E., Pham, T., Georgaka, S., Hayley, M. J., Jokl, E., Hanley, K. P., Allen, J. E., Sutherland, T. E., Rattray, M."
date: 2026-08-19
pdf: "https://www.biorxiv.org/content/10.1101/2025.06.04.657781v4.full.pdf"
tags: ["query:cell-graph"]
score: 6.0
evidence: 构建细胞与细胞外基质的空间图进行联合分析
tldr: 空间蛋白质组学技术已能同时原位分析细胞与细胞外基质（ECM），但分析工具仍以细胞为中心，忽略ECM的关键作用。Mantpy框架将ECM及其与细胞的界面表示为空间图，直接从基质标记构建ECM图并与细胞图连接，支持图统计、可解释图深度学习和可视化。在人类肠道、感染小鼠肝脏和小鼠肺中，Mantpy恢复分层组织结构、解析疾病相关基质组成与组织、表征细胞-基质关联。该工作将空间分析单元从细胞扩展到周围基质，发布ECM数据集并兼容scverse生态系统。
source: biorxiv
selection_source: fresh_fetch
motivation: 空间蛋白质组学可同时分析细胞和细胞外基质，但现有工具仍以细胞为中心，忽略ECM的关键作用。
method: Mantpy将ECM及其与细胞界面表示为空间图，从基质标记构建ECM图并与细胞图连接，支持图统计、可解释图深度学习和可视化。
result: 在人类肠道、感染小鼠肝脏和小鼠肺中，Mantpy恢复组织层次、解析疾病相关基质组成与组织、表征细胞-基质关联。
conclusion: Mantpy将空间分析单元从细胞扩展到周围基质，发布ECM数据集并兼容scverse生态。
---

## 摘要
空间蛋白质组学技术如今能够在原位同时分析细胞与细胞外基质（ECM）。然而，尽管ECM在健康与疾病中发挥重要作用，分析工具仍以细胞为中心。在此，我们提出Mantpy，一个将ECM及其与细胞的界面表示为空间图的框架。Mantpy直接从基质标记物构建ECM图，并将其与细胞图连接以进行细胞-ECM联合分析，支持图统计、可解释的图深度学习以及可视化。从单一ECM标记物到ECM与细胞标记物的多重组合，Mantpy恢复了人肠道中的分层组织结构，解析了感染小鼠肝脏中疾病相关的基质组成与组织方式，并表征了小鼠肺中的细胞-基质关联。Mantpy随附包含ECM的数据集发布，并与scverse生态系统互操作，将空间分析的单位从细胞拓展至其周围的基质。

## Abstract
Spatial proteomics technologies now profile cells and the extracellular matrix (ECM) together in situ. Yet analysis tools remain cell-centric, despite the ECM playing an essential role in health and disease. Here we present Mantpy, a framework that represents the ECM, and its interface with cells, as spatial graphs. Mantpy builds ECM graphs directly from matrix markers and links them with cell graphs for joint cell-ECM analysis, supporting graph statistics, explainable graph deep learning and visualisation. From a single ECM marker to multiplexed panels of ECM and cellular markers, Mantpy recovers layered tissue architecture in human intestine, resolves disease-associated matrix composition and organisation in infected mouse liver, and characterises cell-matrix associations in mouse lung. Released with ECM-inclusive datasets and interoperating with the scverse ecosystem, Mantpy extends the unit of spatial analysis beyond the cell, to the matrix that surrounds it.