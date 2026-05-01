---
title: "Single-cell, label-free morphology profiling of iPSC-derived microglia reveals dynamic state transitions"
title_zh: 单细胞、无标记的 iPSC 来源小胶质细胞形态学分析揭示动态状态转变
authors: "Chen, T., Li, X., Dolga, A. M."
date: 2026-04-29
pdf: "https://www.biorxiv.org/content/10.64898/2026.04.28.721424v1.full.pdf"
tags: ["query:sam"]
score: 10.0
evidence: 结合Cellpose-SAM分割的无标记单细胞形态分析流程
tldr: 本研究旨在克服传统荧光标记方法的局限，开发了一种基于活细胞无标记成像与自动分割分析的单细胞形态学分析流程，用于追踪iPSC来源的微胶质细胞在不同炎症因子刺激下的动态状态转变，揭示微胶质形态变化是一个连续、可量化的多维过程，不同刺激通过独特形态分布反映其功能特异性。
source: biorxiv
selection_source: fresh_fetch
motivation: 尽管微胶质细胞形态反映其功能状态，但现有研究主要依赖荧光标记和终点成像，缺乏连续、无标记的动态分析手段。
method: 本研究建立了结合活细胞无标记成像、Cellpose-SAM分割和CellProfiler特征提取的单细胞形态追踪流程。
result: 研究识别出四种主要形态状态，发现不同炎症刺激导致细胞在形态连续景观中呈现特征性占据模式，IFNγ诱导的变化最显著并伴随ROS升高。
conclusion: 微胶质细胞在炎症刺激下的形态变化呈连续谱状态，不同刺激通过特征化的形态分布模式体现特异性反应。
---

## 摘要
小胶质细胞在环境和炎症信号的刺激下会表现出多样的形态，这些形态反映了其功能状态。然而，对人源 iPSC 衍生小胶质细胞（iMGLs）形态变化的表征仍受限于对荧光标记、终点成像以及粗略分类（例如树枝状与变形虫状状态）的依赖。在本研究中，我们开发了一种无标记的分析流程，结合了活细胞成像、Cellpose-SAM 分割以及基于 CellProfiler 的特征提取，用以在单细胞分辨率下随时间跟踪 iMGL 的形态变化。将这一框架应用于 LPS 与 IFNγ 共刺激的 24 小时时间序列实验，揭示了快速而瞬态的形态重构，响应在 2–4 小时内达到峰值，随后部分减弱。在单细胞分辨率下，四种形态状态捕捉了主要的变异轴线，共刺激导致形态显著向一个单一的“Spread”状态重新分布。将分析扩展至单一炎症刺激（LPS、IFNγ、IL-1β、IL-6 和 TNF）时，观察到状态组成出现梯度化但重叠的变化，其中 IFN 诱导了最强的响应，而 IL-1β 的作用最弱。重要的是，仅依靠状态层面的变化不足以区分特定刺激的响应。相反，单细胞密度映射揭示了在共享形态空间中存在不同的占据模式。此外，纹理复杂性提供了一个独立的特征层，可以进一步区分不同刺激条件，表明刺激特异性通过连续的高维形态特征而非离散状态来表征。在形态与功能的关联方面，IFNγ 不仅产生了最大程度的形态重分布，也是唯一显著增加 24 小时细胞内 ROS 水平的刺激，这表明特定炎症信号可同时协调形态重构与氧化还原活化。综上所述，这些结果支持一种模型：小胶质细胞通过在连续形态景观中的梯度性占据来响应炎症刺激，每种刺激所引起的特异性响应模式超越了离散状态的划分。

## Abstract
In response to environmental and inflammatory cues, microglia adopt diverse morphologies reflecting their functional state. However, characterizing these morphological alterations in human iPSC-derived microglia (iMGLs) remains limited by reliance on fluorescent labeling, endpoint imaging, and coarse categorical classifications (e.g., ramified vs amoeboid states). Here, we developed a label-free pipeline combining live-cell imaging, Cellpose-SAM segmentation, and CellProfiler-based feature extraction to track iMGL morphology at single-cell resolution over time. Applying this framework to a 24-hour time course of LPS and IFN{gamma} co-stimulation revealed rapid and transient morphological remodeling, with responses peaking within 2-4 hours and partially attenuating thereafter. At single-cell resolution, four morphological states captured the major axes of variation, with co-stimulation driving a pronounced redistribution toward a single Spread state. Extending the analysis to individual inflammatory stimuli (LPS, IFN{gamma}, IL-1{beta}, IL-6, and TNF) revealed graded but overlapping shifts in state composition, with IFN inducing the strongest response, whereas IL-1{beta} showed minimal effects. Importantly, state-level changes alone were insufficient to distinguish stimulus-specific responses. Instead, single-cell density mapping revealed distinct occupancy patterns within a shared morphological landscape. In addition, texture complexity provided an independent feature layer that further separated among treatments, indicating that stimulus identity is represented by continuous, high-dimensional morphological features beyond discrete state assignments. Linking morphology to function, IFN{gamma} produced the largest morphological redistribution and was also the only stimulus to significantly elevate intracellular ROS at 24 h, indicating that morphological remodeling and redox activation can be coordinately engaged by specific inflammatory signals. Together, these findings support a model in which microglia respond to inflammatory stimuli by graded occupancy of a continuous morphological landscape, with each stimulus producing a stimulus-specific occupancy pattern that extends beyond discrete state assignments.

---

## 论文详细总结（自动生成）

# 单细胞、无标记的 iPSC 来源小胶质细胞形态学分析揭示动态状态转变 — 中文结构化总结

---

## 一、研究核心问题与整体含义

- **研究动机**：微胶质细胞（microglia）是中枢神经系统的主要免疫细胞，其形态与功能状态密切相关。传统研究多依赖荧光标记和终点成像，只能捕捉到静态、粗略的形态分类（如树枝状与变形虫状），无法追踪动态过程。
- **问题核心**：如何在无需荧光标记的前提下，实现人源诱导多能干细胞（iPSC）来源的微胶质细胞（iMGL）的高分辨率动态形态追踪。
- **整体目标**：建立一个无标记的单细胞形态分析流程，揭示微胶质细胞在不同炎症刺激下的连续性形态变化及其功能对应关系，推动形态-功能关联机制的量化研究。

---

## 二、方法论：核心思想与关键技术

- **核心思想**  
  通过活细胞无标记成像获取原始数据，结合自动分割与多维特征提取，实现单细胞层面的时间动态形态分析。

- **关键组成流程**  
  1. **成像模块**：使用活细胞无标记显微技术，采集高分辨率的时间序列图像。  
  2. **分割模块**：结合 **Cellpose**（基于深度学习的细胞分割模型）与 **SAM（Segment Anything Model）**，获得高准确度的细胞边界。  
  3. **特征提取与建模**：通过 **CellProfiler** 提取多维形态特征（面积、分支复杂度、纹理、圆度等），再利用聚类与降维算法识别主轴变化及状态空间。  
  4. **动态分析**：对时间序列数据进行密度映射与轨迹分析，探讨细胞在连续形态景观中的占据模式及过渡路径。  

- **算法逻辑（文字描述）**  
  输入：无标记显微图像序列 → 自动分割（Cellpose + SAM） → 特征提取（CellProfiler） → 降维表达（如 PCA/UMAP） → 聚类识别形态状态 → 动态轨迹分析与刺激特征映射。

---

## 三、实验设计

- **实验对象**：人源 iPSC 衍生的小胶质细胞（iMGLs）。
- **实验场景与刺激条件**：
  - 联合刺激：LPS + IFNγ（模拟强炎症反应，观察 24 小时动态变化）。
  - 单独刺激：LPS、IFNγ、IL-1β、IL-6、TNF（比较不同炎症因子的形态影响）。
- **数据类型**：基于时间序列的显微图像，单细胞分辨率分析。
- **分析基线（benchmark）**：无直接对比深度学习模型，而是定量比较多种刺激下的形态状态分布与密度再分布。
- **对比方式**：跨刺激条件的状态比例变化与形态空间占据模式比对，辅以细胞内 ROS 测定进行功能关联。

---

## 四、资源与算力

- **论文中未明确说明** 所使用的计算算力环境（如 GPU 型号、数量、运行时间等）。  
- 根据常见实践推测：Cellpose-SAM 分割及 CellProfiler 特征提取可在单 GPU 或高性能 CPU 环境下处理，无需大规模训练。  
- 无大规模深度学习训练任务，主要为推理与分析阶段。

---

## 五、实验数量与充分性

- **实验组合**：
  1. 时间序列实验：LPS + IFNγ 的 24 小时连续观察；
  2. 多刺激条件实验：五种炎症因子单独作用；
  3. 功能验证实验：ROS 定量分析。
- **实验数量与充分性**：
  - 涉及至少 6 个刺激场景（联合 + 5 个单独刺激），覆盖典型炎症刺激谱。
  - 多维度特征与密度分析均在单细胞层面进行，数据量和重复性较高。
  - 实验设计较为平衡，但缺乏跨批次生物重复与跨实验室验证的说明。

---

## 六、主要结论与发现

- 微胶质细胞形态变化是连续谱而非离散分类；
- 四种主要形态状态可描述形态变化的主轴（例如从分枝状到扩展状的连续过渡）；
- 不同炎症刺激引发特征性占据模式：
  - **IFNγ**：诱导最强形态重构与细胞内 ROS 上升；
  - **IL-1β**：响应最弱；
  - **TNF、IL-6、LPS**：产生中等程度的变化；
- 形态复杂度与纹理特征提供了额外维度，用于区分不同刺激；
- 形态与功能响应可协调发生，表明炎症信号通过高维形态特征反映其功能特异性。

---

## 七、优点与创新亮点

- **方法学创新**：
  - 首次将 **Cellpose 与 SAM** 联合用于无标记单细胞形态追踪，赋予高分割准确度；
  - **连续形态景观分析** 替代传统的离散分类，为形态动力学提供新模型。
- **分析维度丰富**：
  - 融合时间、空间与高维特征，揭示微胶质状态的多维动力学。
- **应用潜力**：
  - 可广泛用于神经炎症模型、药物筛选、细胞功能态监测。

---

## 八、不足与局限

- **算力与通用性**：未提供算法性能指标、计算资源需求或可复现细节。
- **样本覆盖**：仅基于 iPSC 来源微胶质细胞，未验证原代人或动物微胶质的泛化性。
- **功能验证有限**：形态与功能对应主要依赖 ROS 变化，其他功能指标（如吞噬活性、分泌谱）尚未验证。
- **技术兼容性问题**：无标记成像对光学质量要求高，限制了大规模高通量应用。

---

（完）
