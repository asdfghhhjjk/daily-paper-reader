---
title: Clonal embeddings allow exploratory analysis of lineage-resolved single-cell data
title_zh: 克隆嵌入支持谱系解析的单细胞数据探索性分析
authors: "Isaev, S., Erickson, A. G., Adameyko, I., Kharchenko, P. V."
date: 2026-05-05
pdf: "https://www.biorxiv.org/content/10.64898/2026.04.30.720820v1.full.pdf"
tags: ["query:cellrep"]
score: 6.0
evidence: 直接从细胞表达流形中学习信息丰富的克隆嵌入
tldr: 该研究针对谱系追踪与单细胞转录组结合实验分析的困难，提出了机器学习方法clone2vec，通过从细胞表达流形中学习克隆嵌入，实现了克隆变异的可解释几何表示，在多种生物过程数据集中验证其能揭示新的谱系和调控模式。
source: biorxiv
selection_source: fresh_fetch
motivation: 当前高通量谱系追踪结合单细胞转录组分析虽能揭示命运偏向和调控因子，但克隆数据稀疏和注释依赖导致分析困难。
method: 研究提出了机器学习方法clone2vec，从细胞表达流形中学习克隆嵌入，无需依赖离散细胞类型标签。
result: clone2vec在胚胎发生、肿瘤发生及造血数据集中重建了已知克隆模式并发现新的连续变异轴，揭示相关调控通路。
conclusion: clone2vec为探索性分析谱系解析单细胞数据提供了稳健且通用的解决方案。
---

## 摘要
将高通量谱系追踪与单细胞转录组学相结合的检测方法正在改变对发育与疾病生物学的研究，不仅揭示主要的分化路径，还揭示连续的命运偏倚及其潜在调控因子。然而，大规模分析此类数据面临挑战，因为克隆数据具有稀疏特性且依赖于注释。为此，我们开发了一种机器学习方法——clone2vec——它直接从细胞表达流形中学习信息丰富的克隆嵌入，绕过离散的细胞类型标签，并在克隆由少量细胞表示时保持稳定。这种表示将克隆间的变异总结为可解释的几何结构，支持探索、克隆-基因关联的统计分析以及跨数据集的对齐。在涵盖胚胎发生、肿瘤形成和造血过程的前瞻性条形码数据集中，clone2vec再现了已知的克隆模式，并揭示出新的连续变异轴，涉及调控程序和发育途径。在利用TCR测序描述的肿瘤微环境中，clone2vec稳健地恢复了不同的Treg谱系以及跨癌种的保守CD8+ T细胞亚谱系，其中包括若干类似旁观者的克隆亚群。总体而言，clone2vec为谱系耦合的单细胞RNA测序数据的探索性分析提供了稳健且通用的解决方案。

## Abstract
Assays coupling high-throughput lineage tracing with single-cell transcriptomics are transforming studies of development and disease biology, revealing not only major differentiation routes but also continuous fate biases and their putative regulators. Yet, analysis of such data at scale presents challenges due to the sparse nature of clonal data and annotation dependencies. Towards that aim we developed a machine learning approach - clone2vec - which learns informative clone embeddings directly from the cellular expression manifold, bypassing discrete cell-type labels and remaining stable when clones are represented by few cells. This representation summarizes clonal variation as an interpretable geometry that supports exploration, statistics for clone-gene associations, and cross-dataset alignment. In prospective barcoding datasets spanning embryogenesis, tumorigenesis, and hematopoiesis, clone2vec recapitulates established clonal patterns and uncovers new axes of continuous variation that implicate regulatory programs and developmental pathways. In tumor microenvironments profiled with TCR sequencing, clone2vec robustly recovers distinct Treg lineages as well as conserved CD8+ T cell sublineages across cancer types, including several bystander-like clonal subsets. Overall, clone2vec provides a robust, general solution for the exploratory analysis of lineage-coupled scRNA-seq data.