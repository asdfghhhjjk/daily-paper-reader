---
title: Decoding Condition-Specific Cellular Crosstalk in Spatial Omics via Bilinear Edge Classification
title_zh: 通过双线性边分类在空间组学中解码条件特异性细胞间通信
authors: "Karin, J., Friedman, R., Nitzan, M."
date: 2026-05-06
pdf: "https://www.biorxiv.org/content/10.64898/2026.05.03.722470v1.full.pdf"
tags: ["query:cellrep"]
score: 6.0
evidence: 解码疾病进展中的细胞通讯和细胞空间重组
tldr: 本文提出Casei，一个基于双线性边分类的空间组学分析框架，以细胞间相互作用为核心单元，能识别条件特异的细胞通讯模式，利用肝纤维化、动脉粥样硬化和脑衰老数据验证其在揭示组织空间重组中的有效性。
source: biorxiv
selection_source: fresh_fetch
motivation: 现有空间转录组分析方法难以捕捉条件特异的细胞间协调转录变化，限制了对组织状态重组的理解。
method: 提出名为Casei的双线性边分类框架，通过细胞邻近图直接建模空间组学中的条件特异性细胞间相互作用。
result: Casei成功应用于肝纤维化、动脉粥样硬化及脑衰老数据，揭示了细胞网络重组及空间功能破坏的生物学模式。
conclusion: Casei展现了在不同生理状态下揭示细胞重组和失调的强大能力，为空间组学领域提供了一种高效分析多细胞相互作用的新途径。
---

## 摘要
组织是多细胞结构的群体，其功能源于个体细胞特征与相应空间结构的结合，从而影响细胞的相互作用及响应模式。在疾病进展或衰老等过程中，组织可能经历结构性重组，包括不同细胞类型共定位的变化、功能性微环境的形成或破坏，以及细胞间通信轴的失调。这些变化主要体现在细胞的空间重新组织，而非单个细胞的转录状态。尽管空间转录组学的计算工具在表征组织结构方面取得了显著进展，大多数用于比较不同生物条件下组织状态变化的方法仍停留在单细胞层面，或依赖离散的细胞类型标签，从而限制了检测邻近细胞间协调转录变化的能力，而这些变化恰恰区分不同条件。我们提出了 Casei，一种运行于细胞邻近图上的双线性分类框架，它通过关注细胞之间的相互作用（边），而非单个细胞（节点），直接在空间组学数据中建模条件特异性的细胞-细胞相互作用。为了捕捉此类条件特异信号，我们利用一种在归纳偏置上与细胞间相互作用相契合的模型，通过邻近细胞间协同的基因-基因关系来实现。Casei 能够发现与条件相关的多细胞相互作用及空间表达程序，并刻画多细胞功能与结构的丧失。在哺乳动物肝纤维化、动脉粥样硬化和脑老化的研究中，Casei 揭示了具有生物学意义的空间重组现象，包括动脉粥样硬化斑块中从内皮细胞主导到巨噬细胞主导网络的转变、肝纤维化中肝细胞分区的破坏，以及老化白质中少突胶质细胞与小胶质细胞间的通信。

## Abstract
Tissues are multicellular structured communities whose function emerges from a combination of individual cellular characteristics along with their corresponding spatial configuration, affecting their interactions and response patterns. During processes such as disease progression or aging, tissues can undergo structural reorganization, including changes in co-localization of different cell types, assembly or destruction of functional niches, and disruption of intercellular communication axes. Such changes can manifest primarily in the spatial reorganization of cells rather than in the transcriptional states of individual cells. While computational tools for spatial transcriptomics have made significant progress in characterizing tissue architecture, most approaches for characterizing changes in tissue states across biological conditions operate at the level of individual cells or rely on discrete cell type labels, thus limiting the ability to detect coordinated transcriptional changes between neighboring cells that distinguish one condition from another. We present Casei, a bilinear classification framework operating on cellular proximity graphs, which directly models condition-specific cell-cell interactions in spatial omics data by focusing on interactions (edges), rather than cells (nodes), as the fundamental unit of biological inference. To capture such condition-specific signals, we leverage a model whose inductive bias aligns with cellular interactions through coordinated gene-gene relationships of neighboring cells. Casei enables the discovery of condition-associated multicellular interactions and spatial expression programs, and characterizes the loss of multicellular function and structure. Applied to mammalian liver fibrosis, atherosclerosis, and brain aging, Casei reveals biologically meaningful spatial reorganization, including the shift from endothelial- to macrophage-dominated networks in atherosclerotic plaques, disruption of hepatocyte zonation in fibrosis, and oligodendrocyte-microglia crosstalk in aging white matter.