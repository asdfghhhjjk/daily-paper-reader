---
title: Decoding Condition-Specific Cellular Crosstalk in Spatial Omics via Bilinear Edge Classification
title_zh: 通过双线性边分类在空间组学中解码条件特异的细胞互作
authors: "Karin, J., Friedman, R., Nitzan, M."
date: 2026-05-06
pdf: "https://www.biorxiv.org/content/10.64898/2026.05.03.722470v1.full.pdf"
tags: ["query:cellrep"]
score: 6.0
evidence: 表征组织中的个体细胞特征和空间配置
tldr: 本文提出双线性分类模型 Casei，从细胞邻近图的边而非节点出发建模空间组学数据，以识别条件特异的细胞间互作。该方法揭示了肝纤维化、动脉粥样硬化及脑老化中的空间重组规律，拓展了组织状态变化的解析维度。
source: biorxiv
selection_source: fresh_fetch
motivation: 现有空间转录组工具难以捕捉跨条件的细胞间协调变化，限制了对组织状态变化的深入理解。
method: 提出基于双线性边分类的框架 Casei，以细胞间相互作用为核心建模空间组学数据。
result: Casei 揭示了肝纤维化、动脉粥样硬化和脑老化中的特异性细胞交互与空间重组，如从内皮到巨噬网络的转变等。
conclusion: Casei 为研究复杂组织在不同生物条件下的空间重组提供了新视角，有助于揭示多细胞系统功能丧失的机制。
---

## 摘要
组织是由多细胞构成的结构性群体，其功能来源于个体细胞特征与相应空间构型的结合，这种结合影响细胞的相互作用及其响应模式。在疾病进展或衰老等过程中，组织可能经历结构重组，包括不同细胞类型的共定位变化、功能性微环境的构建或破坏，以及细胞间通讯轴的中断。这类变化主要体现在细胞的空间重组上，而非单个细胞的转录状态。虽然空间转录组学计算工具在表征组织结构方面已取得显著进展，但目前用于刻画不同生物条件下组织状态变化的多数方法仍停留在单细胞层面或依赖离散的细胞类型标签，从而限制了检测相邻细胞间协同转录变化的能力，而这些变化对于区分不同条件尤为重要。我们提出了名为 Casei 的双线性分类框架，该框架在细胞邻近图上运行，通过将相互作用（边）而非细胞（节点）作为生物推断的基本单元，直接建模空间组学数据中与特定条件相关的细胞间互作。为捕捉此类条件特异性信号，我们利用一个模型，其归纳偏置与细胞间通过邻近细胞基因间协同关系实现的相互作用相一致。Casei 能够发现与条件相关的多细胞互作及空间表达程序，并表征多细胞功能与结构的丧失。将该方法应用于哺乳动物肝纤维化、动脉粥样硬化和脑衰老，Casei 揭示了生物学上有意义的空间重组现象，包括动脉粥样硬化斑块中从内皮细胞主导网络向巨噬细胞主导网络的转变、纤维化中的肝细胞分区破坏，以及衰老白质中少突胶质细胞—小胶质细胞间的相互作用。

## Abstract
Tissues are multicellular structured communities whose function emerges from a combination of individual cellular characteristics along with their corresponding spatial configuration, affecting their interactions and response patterns. During processes such as disease progression or aging, tissues can undergo structural reorganization, including changes in co-localization of different cell types, assembly or destruction of functional niches, and disruption of intercellular communication axes. Such changes can manifest primarily in the spatial reorganization of cells rather than in the transcriptional states of individual cells. While computational tools for spatial transcriptomics have made significant progress in characterizing tissue architecture, most approaches for characterizing changes in tissue states across biological conditions operate at the level of individual cells or rely on discrete cell type labels, thus limiting the ability to detect coordinated transcriptional changes between neighboring cells that distinguish one condition from another. We present Casei, a bilinear classification framework operating on cellular proximity graphs, which directly models condition-specific cell-cell interactions in spatial omics data by focusing on interactions (edges), rather than cells (nodes), as the fundamental unit of biological inference. To capture such condition-specific signals, we leverage a model whose inductive bias aligns with cellular interactions through coordinated gene-gene relationships of neighboring cells. Casei enables the discovery of condition-associated multicellular interactions and spatial expression programs, and characterizes the loss of multicellular function and structure. Applied to mammalian liver fibrosis, atherosclerosis, and brain aging, Casei reveals biologically meaningful spatial reorganization, including the shift from endothelial- to macrophage-dominated networks in atherosclerotic plaques, disruption of hepatocyte zonation in fibrosis, and oligodendrocyte-microglia crosstalk in aging white matter.