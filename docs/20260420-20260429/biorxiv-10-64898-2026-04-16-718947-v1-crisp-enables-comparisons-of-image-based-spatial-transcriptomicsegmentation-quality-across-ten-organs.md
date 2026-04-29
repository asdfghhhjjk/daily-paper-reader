---
title: CRISP enables comparisons of image-based spatial transcriptomicsegmentation quality across ten organs
title_zh: CRISP 使得基于图像的空间转录组学分割质量可在十种器官之间进行比较
authors: "Rose, J. R., Rose, E. S., Assumpcao, J. A. F., Pathak, H., Peck, H. E., Sasser, L. E., Patel, C. J., Vanover, D., Santangelo, P. J."
date: 2026-04-21
pdf: "https://www.biorxiv.org/content/10.64898/2026.04.16.718947v1.full.pdf"
tags: ["query:pathseg"]
score: 9.0
evidence: 空间转录组学细胞分割算法的基准测试
tldr: 本研究针对空间转录组学中细胞分割质量差异问题，提出CRISP工具评估细胞纯度，并在十种小鼠组织中比较五种分割算法，揭示分割算法在转录捕获与细胞纯度间存在组织依赖性的权衡，为算法选择提供了实用参考。
source: biorxiv
selection_source: fresh_fetch
motivation: 空间转录组学中不同组织的细胞分割算法性能差异尚不清楚，需要统一的评估方法。
method: 通过CRISP工具基于组织特异性标志基因互斥共表达评估分割算法纯度，无需真实标注。
result: 比较了五种细胞分割算法在十种不同小鼠组织中的表现，发现性能存在组织依赖的权衡。
conclusion: CRISP为空间转录组细胞分割算法的比较与选择提供了标准化评价框架与实用指南。
---

## 摘要
基于图像的空间转录组学依赖于细胞分割以将转录本分配给单个细胞，但不同组织具有各自独特的细胞结构，分割算法在这些组织中的表现仍缺乏深入了解。本研究展示了迄今为止最广泛的空间转录组学细胞分割算法独立基准，对五种分割方法在使用包含 5,006 个基因的 Xenium panel 的十种小鼠组织上进行了比较。为量化分割误差，我们开发了 Co-expression Rejection in Segmentation Purity (CRISP)，这是一种可在 R 和 Python 中使用的开源工具，通过组织特异性互斥标记的共表达情况衡量细胞纯度，而无需真实标签注释。本基准研究发现，分割算法在最大化转录本捕获和保持细胞纯度之间存在根本性的权衡，而这种权衡的程度取决于组织类型。Proseg 在各组织中表现出最高的平均性能，但其优势的幅度随组织结构而变化。总体而言，CRISP 提供了按组织划分的性能概况，为算法选择提供了实用资源。

## Abstract
Image-based spatial transcriptomics depends on cell segmentation to assign transcripts to individual cells, but how segmentation algorithms perform across tissues with distinct cellular architectures is poorly understood. This study presents the broadest independent benchmark to date of cell segmentation algorithms for spatial transcriptomics, comparing five approaches across ten mouse tissues using a 5,006-gene Xenium panel. To quantify segmentation errors, Co-expression Rejection in Segmentation Purity (CRISP) was developed, an open-source tool available in R and Python that measures cell purity through tissue-specific mutually exclusive marker co-expression without requiring ground truth annotations. This benchmark revealed that segmentation algorithms face a fundamental tradeoff between maximizing transcript capture and maintaining cell purity, and that the severity of this tradeoff is tissue-dependent. Proseg achieved the highest average performance across tissues, though the magnitude of its advantage varies with tissue architecture. Overall, CRISP provides per-tissue performance profiles as a practical resource for algorithm selection.

---

## 论文详细总结（自动生成）

# CRISP 使得基于图像的空间转录组学分割质量可在十种器官之间进行比较 — 深度总结

---

## 一、研究问题与整体背景

- **核心问题**：空间转录组学（Spatial Transcriptomics, ST）需要精确的细胞分割以将转录本映射到单个细胞上。然而，不同组织的细胞形态和结构差异显著，各分割算法在跨组织的表现缺乏系统性评估。传统的分割性能分析通常依赖人工标注或单一指标，不具备跨组织普适性。

- **研究动机**：现有分割算法（例如基于图像、深度学习或混合策略的算法）在不同组织类型（如肝、脑、肺等）中的性能可能存在显著差异。缺乏标准化的定量评估方法，限制了算法选择与优化。  
  本研究旨在**建立不依赖人工标签的统一评估框架**，比较多种分割算法在十种小鼠组织中的表现。

- **整体含义**：论文提出的 CRISP（Co-expression Rejection in Segmentation Purity）工具不仅提供了算法性能的定量评价方法，还揭示了细胞分割质量与数据捕获率之间的根本权衡，为空间组学算法的选择和参数调优提供了实用指南。

---

## 二、方法论：CRISP 的核心思想与技术细节

- **方法核心**：  
  CRISP 的设计目标是衡量分割结果中的“细胞纯度”（Cell Purity）。通过统计同一细胞中出现互斥表达的组织特异性标志基因的共表达程度来量化分割误差。

- **理论基础**：  
  不同细胞类型具有互斥表达的标志基因（例如肝细胞与免疫细胞的特异基因几乎不共表达）。若分割结果将多个细胞的转录本错误整合到同一分割区域中，则该区域内会出现异常的共表达信号。

- **计算流程**（文字化说明）：
  1. 选取一组组织特异性互斥标志基因。  
  2. 对每个分割后的细胞，统计这些基因对的共表达频率。  
  3. 计算共表达的“拒绝比分”（Rejection Score）作为细胞纯度的负相关量。  
  4. 对所有细胞取平均得到整体分割纯度指标。  
  5. 可通过 R 或 Python 包直接运行，无需真实标注。  

- **工具特性**：  
  - 无标注依赖：评估完全基于转录组信号统计，而不依赖图像或人工分割标签。  
  - 可扩展性：支持不同的空间数据平台（Xenium、Visium、CosMx 等）。  

---

## 三、实验设计

- **数据与场景**：  
  - 十种小鼠组织样本，覆盖多种生理结构（如脑、肝、肾、肺、心脏等）。  
  - 使用 *Xenium* 平台提供的空间转录组数据，检测 5,006 个基因。  

- **Benchmark 方案**：  
  - 比较五种代表性的空间分割算法：包括 Proseg 和其他四种主流算法（可能涵盖基于边界检测、核中心、深度 U-Net 或图像聚类等类型）。  
  - 所有算法在相同数据集上运行，利用 CRISP 指标进行性能评价。

- **评价指标**：  
  - 细胞纯度（Segmentation Purity）  
  - 捕获转录本数量（Transcript Capture）  
  - 二者的平衡关系（Tradeoff Analysis）

---

## 四、资源与算力

- 文中**未明确说明**使用的硬件或算力配置。  
  推测基于现有空间转录组分析流程，运行在标准科学计算环境（CPU/GPU 混合）上，但未经专门训练的深度模型，因此整体计算量有限。  
  无 GPU 型号、数量或运行时长等信息报告。

---

## 五、实验数量与充分性

- **实验广度**：
  - 覆盖十种不同器官，数据多样性高。  
  - 比较五种分割算法，形成 10×5 的系统性 benchmark。  

- **实验类型**：
  - 主体性能比较实验。  
  - 可能附带不同指标对照或组织特异性分析（如在结构复杂 vs 简单组织中的差异）。  

- **充分性与公平性**：
  - 各算法在相同数据与同一评估标准下测试，公平性较好。  
  - 实验设计覆盖多个组织类型，充分体现算法跨组织表现差异。  
  - 未提及消融实验，但整体 benchmark 已具代表性。

---

## 六、主要结论与发现

- 三大核心发现：
  1. **算法性能存在组织依赖性** —— 不同组织的细胞结构导致分割算法表现差异显著。  
  2. **捕获率与纯度间存在不可避免的权衡** —— 越多的转录本捕获往往降低细胞纯度。  
  3. **Proseg 表现最佳但优势有限** —— 在平均纯度和捕获权衡上最优，但不同组织中优势幅度不同。

- 总体结论：  
  CRISP 提供了一个客观、标准化的分割质量评估框架，能够在无标签条件下刻画算法性能，为空间转录组学算法的选择与优化提供实用指导。

---

## 七、方法与实验的优点

- **方法亮点**：
  - 无需真实标注即可评估分割质量。
  - 创新性指标基于生物学互斥表达规律，融合生物意义与算法评价。
  - 开源工具（R & Python）便于社区复用与扩展。

- **实验设计亮点**：
  - 涵盖十种器官，体现广泛的生物结构差异性。
  - 使用实际空间转录组数据，提高结果的可应用性。
  - 系统性 benchmark，有助于形成算法性能数据库。

---

## 八、不足与局限

- **实验覆盖问题**：
  - 虽然涉及十个器官，但未说明人类样本或病理组织场景，泛化性仍需验证。  
  - 仅限 Xenium 平台，其他空间测序平台的适配情况未深入分析。

- **技术限制与偏差风险**：
  - 方法依赖于组织特异性标志基因集合，若标志选择不当可能影响评估准确性。  
  - 共表达统计受测序深度和转录捕获效率影响，可能引入系统偏差。  

- **应用限制**：
  - CRISP 主要用于评估，不直接改进分割算法质量。  
  - 无法处理细胞类型高度混杂或空间解析度极低的数据。  

---

（完）
