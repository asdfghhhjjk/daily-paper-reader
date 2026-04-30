---
title: "Single-cell, label-free morphology profiling of iPSC-derived microglia reveals dynamic state transitions"
title_zh: 单细胞无标记形态谱分析揭示 iPSC 衍生小胶质细胞的动态状态转换
authors: "Chen, T., Li, X., Dolga, A. M."
date: 2026-04-29
pdf: "https://www.biorxiv.org/content/10.64898/2026.04.28.721424v1.full.pdf"
tags: ["query:sam"]
score: 8.5
evidence: 在活细胞成像中使用 Cellpose-SAM 进行单细胞形态分析。
tldr: 本研究针对iPSC衍生微胶质细胞在炎症刺激下的动态形态变化，建立了基于活细胞成像和AI分割的无标记单细胞分析流程，揭示微胶质形态变化是连续的高维景观，不同炎症信号通过特定形态占据模式和功能耦合呈现特异响应。
source: biorxiv
selection_source: fresh_fetch
motivation: 旨在克服人源iPSC衍生微胶质细胞形态研究中对荧光标记与终点成像的依赖，揭示其动态功能状态变化。
method: 研究开发了结合活细胞成像、Cellpose-SAM分割与CellProfiler特征提取的无标记单细胞形态追踪流程。
result: 实验发现炎症刺激引发微胶质细胞快速、可逆的形态重塑，不同刺激呈现重叠但可区分的形态态势分布，其中IFNγ诱导最强响应且提升ROS水平。
conclusion: 研究表明，微胶质细胞形态变化以连续景观形式反映刺激响应，具体刺激通过不同形态占据模式体现功能特异性。
---

## 摘要
在环境和炎症信号的作用下，小胶质细胞会表现出多种形态，这些形态反映了其功能状态。然而，人源 iPSC 衍生小胶质细胞（iMGLs）形态变化的特征研究仍受限于对荧光标记、终点成像以及粗分类（例如树突状 vs. 阿米巴状状态）的依赖。本研究建立了一种无标记分析流程，结合活细胞成像、Cellpose-SAM 分割以及基于 CellProfiler 的特征提取，用于随时间跟踪 iMGL 的单细胞形态变化。将该框架应用于 LPS 和 IFN{gamma} 共刺激的 24 小时时程分析中，结果显示快速且短暂的形态重塑，响应在 2–4 小时内达到峰值，随后部分减弱。在单细胞水平上，四种形态状态捕捉了主要的变异轴线，共刺激诱导了显著的形态再分布，趋向一个单一的“Spread”状态。进一步将分析扩展至单一炎症刺激（LPS、IFN{gamma}、IL-1{beta}、IL-6 和 TNF）发现，状态组成呈梯度但重叠的变化，其中 IFN 诱导的响应最强，而 IL-1{beta} 的影响最小。重要的是，仅凭状态层面的变化不足以区分刺激特异性的响应。相反，单细胞密度映射揭示了在共享形态学景观中的不同占据模式。此外，纹理复杂度提供了一个独立的特征层，可进一步区分不同处理，表明刺激身份通过连续的高维形态特征而非离散状态被表征。将形态与功能联系起来，IFN{gamma} 不仅引起了最大的形态再分布，也是唯一在 24 小时显著提高细胞内 ROS 水平的刺激，说明特定的炎症信号可协同驱动形态重塑与氧化还原活化。综上，这些发现支持这样一个模型：小胶质细胞通过在连续形态学景观中的梯度占据来响应炎症刺激，每种刺激都会在该景观中形成具有特异性的占据模式，超越离散状态的划分。

## Abstract
In response to environmental and inflammatory cues, microglia adopt diverse morphologies reflecting their functional state. However, characterizing these morphological alterations in human iPSC-derived microglia (iMGLs) remains limited by reliance on fluorescent labeling, endpoint imaging, and coarse categorical classifications (e.g., ramified vs amoeboid states). Here, we developed a label-free pipeline combining live-cell imaging, Cellpose-SAM segmentation, and CellProfiler-based feature extraction to track iMGL morphology at single-cell resolution over time. Applying this framework to a 24-hour time course of LPS and IFN{gamma} co-stimulation revealed rapid and transient morphological remodeling, with responses peaking within 2-4 hours and partially attenuating thereafter. At single-cell resolution, four morphological states captured the major axes of variation, with co-stimulation driving a pronounced redistribution toward a single Spread state. Extending the analysis to individual inflammatory stimuli (LPS, IFN{gamma}, IL-1{beta}, IL-6, and TNF) revealed graded but overlapping shifts in state composition, with IFN inducing the strongest response, whereas IL-1{beta} showed minimal effects. Importantly, state-level changes alone were insufficient to distinguish stimulus-specific responses. Instead, single-cell density mapping revealed distinct occupancy patterns within a shared morphological landscape. In addition, texture complexity provided an independent feature layer that further separated among treatments, indicating that stimulus identity is represented by continuous, high-dimensional morphological features beyond discrete state assignments. Linking morphology to function, IFN{gamma} produced the largest morphological redistribution and was also the only stimulus to significantly elevate intracellular ROS at 24 h, indicating that morphological remodeling and redox activation can be coordinately engaged by specific inflammatory signals. Together, these findings support a model in which microglia respond to inflammatory stimuli by graded occupancy of a continuous morphological landscape, with each stimulus producing a stimulus-specific occupancy pattern that extends beyond discrete state assignments.