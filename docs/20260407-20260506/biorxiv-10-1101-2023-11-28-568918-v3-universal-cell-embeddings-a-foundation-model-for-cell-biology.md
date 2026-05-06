---
title: "Universal Cell Embeddings: A Foundation Model for Cell Biology"
title_zh: 通用细胞嵌入：面向细胞生物学的基础模型
authors: "Rosen, Y., Roohani, Y., Agrawal, A., Samotorcan, L., Tabula Sapiens Consortium,, Quake, S. R., Leskovec, J."
date: 2026-04-08
pdf: "https://www.biorxiv.org/content/10.1101/2023.11.28.568918v3.full.pdf"
tags: ["query:cellrep"]
score: 7.0
evidence: 用于细胞生物学和表征的通用细胞嵌入基础模型
tldr: 本文提出Universal Cell Embedding（UCE）基础模型，通过无监督学习整合多物种细胞图谱数据，构建能够跨组织和物种表示细胞状态的统一潜表示空间。UCE在嵌入3600万细胞后展现出识别发育谱系和新物种数据的能力，为细胞类型分析与功能推断提供新工具。
source: biorxiv
selection_source: fresh_fetch
motivation: 细胞类型与状态的多样性使建立一个跨组织与物种的通用细胞表示成为细胞生物学的重要目标。
method: 使用完全自监督的训练方式，将多来源、多物种的单细胞转录组数据嵌入到统一的潜在空间中。
result: UCE模型在无监督条件下整合了来自人类及其他物种的细胞图谱数据，生成统一生物潜空间，成功嵌入3600万细胞，揭示细胞类型与组织的结构关系并预测新细胞类型的功能。
conclusion: UCE实现了细胞跨物种的统一表示，为细胞生物学分析与发现提供了基础模型框架。
---

## 摘要
建立一个用于细胞的通用表示空间，以涵盖人体及跨物种细胞类型的巨大分子多样性，将对细胞生物学产生变革性影响。近期利用单细胞转录组学方法构建细胞图谱、以分子定义细胞类型的工作，为这一目标提供了必要的数据。本文提出了通用细胞嵌入（Universal Cell Embedding，简称 UCE）基础模型。UCE 在无任何数据标注的情况下，完全以自监督方式在来自人类及其他物种的细胞图谱数据上进行训练。UCE 的建模方法旨在创建一个统一的生物学潜在空间，可以表示跨不同组织和物种的细胞。该通用细胞嵌入能够有效捕捉重要的生物学变异，尽管不同数据集存在实验噪声。UCE 的通用性一个重要方面在于：新细胞无需额外数据标注、模型训练或微调即可映射到该嵌入空间中。我们应用 UCE 构建了综合巨规模图谱（Integrated Mega-scale Atlas），嵌入了 3600 万个细胞，涵盖来自数百项实验、数十种组织和八个物种的超过 1000 个独特命名细胞类型。我们在该通用细胞嵌入空间中发现了关于细胞类型和组织结构的新见解，并利用其推断新发现细胞类型的功能。UCE 的嵌入空间表现出涌现特性，揭示了模型未明确训练的生物学规律，例如识别发育谱系以及嵌入未参与训练集的全新物种数据。总体而言，通过实现每一种细胞状态与类型的通用表示，UCE 为单细胞数据的分析、标注和假设生成提供了有价值的工具。

## Abstract
Developing a universal representation space for cells which encompasses the tremendous molecular diversity of cell types within the human body and more generally, across species, would be transformative for cell biology. Recent work using single-cell transcriptomic approaches to create molecular definitions of cell types in the form of cell atlases has provided the necessary data for such an endeavor. Here, we present the Universal Cell Embedding (UCE) foundation model. UCE was trained on a corpus of cell atlas data from human and other species in a completely self-supervised way without any data annotations. UCEs modeling approach is to create a unified biological latent space that can represent cells across diverse tissues and species. This universal cell embedding captures important biological variation despite the presence of experimental noise across diverse datasets. An important aspect of UCEs universality is that new cells can be mapped to this embedding space with no additional data labeling, model training or fine-tuning. We applied UCE to create the Integrated Mega-scale Atlas, embedding 36 million cells, with more than 1,000 uniquely named cell types, from hundreds of experiments, dozens of tissues and eight species. We uncovered new insights about the organization of cell types and tissues within this universal cell embedding space, and leveraged it to infer function of newly discovered cell types. UCEs embedding space exhibits emergent behavior, uncovering biology that it was never explicitly trained for, such as identifying developmental lineages and embedding data from novel species not included in the training set. Overall, by enabling a universal representation for every cell state and type, UCE provides a valuable tool for analysis, annotation and hypothesis generation over single cell data.