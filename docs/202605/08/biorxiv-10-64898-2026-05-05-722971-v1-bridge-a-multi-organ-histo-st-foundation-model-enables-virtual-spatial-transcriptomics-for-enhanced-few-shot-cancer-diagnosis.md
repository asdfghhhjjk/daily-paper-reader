---
title: "BRIDGE: A Multi-organ Histo-ST Foundation Model Enables Virtual Spatial Transcriptomics for Enhanced Few-shot Cancer Diagnosis"
title_zh: BRIDGE：一种多器官Histo-ST基础模型，实现虚拟空间转录组学以增强少样本癌症诊断
authors: "Liang, Z., ZHAO, W., Wang, F., Chen, G., Huang, Y., Yu, L."
date: 2026-05-08
pdf: "https://www.biorxiv.org/content/10.64898/2026.05.05.722971v1.full.pdf"
tags: ["query:cellrep"]
score: 7.0
evidence: 对齐病理图像中的形态特征和基因组信息
tldr: "本文提出多器官基础模型BRIDGE，通过在十三种器官与三种测序技术间预训练，成功实现形态与基因组信息的跨器官融合，比现有模型在少样本条件下提高约30%的预测精度，并在多癌种生存预测中表现优异，显示出广泛的临床应用潜力。"
source: biorxiv
selection_source: fresh_fetch
motivation: 现有虚拟空间转录组生成方法依赖单器官模型且需大量数据，难以满足临床少样本应用需求。
method: 研究团队构建了基于13种人类器官和三种测序技术的多器官预训练模型BRIDGE，将组织形态与基因组信息对齐于共享潜在空间。
result: BRIDGE在预测空间表达和癌症生存上均超越最新模型，在零样本和多癌类型场景仍保持高准确度。
conclusion: BRIDGE展现出强大的跨器官和癌症类型泛化能力，为少样本场景下的癌症分子诊断提供了高效可靠的解决方案。
---

## 摘要
近期研究探索了从组织学图像生成虚拟空间转录组学（ST）谱图的方法，为实验室测量的分子分析提供了一种有前景的替代方案。然而，现有方法主要依赖于单器官模型，并需要大量器官特定的训练数据，这限制了它们在临床实践中少样本（针对特定器官或技术少于10张切片）情况下的准确性。在此，我们提出BRIDGE这一多器官基础模型，该模型在13种人体器官和三种测序技术下超过60万个组织学-ST配对数据上进行了预训练。通过在共享的多器官潜在空间中稳健地对齐形态学特征与基因组信息，BRIDGE能利用不同组织之间的共同生物学知识，实现准确且具普适性的泛癌分子分析。在无需额外器官特定微调的情况下，BRIDGE能够准确预测80个生物标志基因的空间表达，其平均皮尔逊相关系数（PCC）达到0.474——较现有最先进模型在三种临床少样本场景下提升30%。利用生成的虚拟ST数据，BRIDGE在癌症生存预测中的表现超越了当前最先进的病理学基础模型，在六个TCGA队列中实现了平均一致性指数（C-index）0.724。值得注意的是，BRIDGE在包括三种未见过的癌症类型的零样本场景中依然保持卓越性能，平均C-index达到0.717，显示出其超越器官与亚型界限的强大泛化能力。此外，BRIDGE生成的虚拟空间转录组在预后准确性上可与整体RNA-seq匹敌，表明其作为实验室测序的空间信息替代方案的潜力。总体而言，BRIDGE是虚拟ST领域一种高数据效率的工具，可在临床少样本情境中促进生物医学发现，并推动样本不足癌症的诊断进展。

## Abstract
Recent studies have explored generating virtual spatial transcriptomics (ST) profiles from histological images, offering a promising alternative to laboratory-measured molecular profiling. However, existing approaches predominantly rely on single-organ models and require substantial organ-specific training data, restricting their accuracy under challenging few-shot conditions in clincical practice, where less than 10 slides are available for specific organs or techniques. Here, we present BRIDGE, a multi-organ foundation model pre-trained on over 600,000 paired histology-ST profiles across 13 human organs and three sequencing techniques. By robustly aligning morphological features and genomic information within a shared multi-organ latent space, BRIDGE can leverage common biological knowledge across distinct tissues to enable accurate and generalizable pan-cancer molecular profiling. Without additional organ-specific fine-tuning, BRIDGE accurately predicts the spatial expression of 80 biomarker genes, achieving an average Pearson correlation coefficient (PCC) of 0.474-a 30% improvement over existing state-of-the-art models under three clinically challenging few-shot scenarios. With generated virtual ST, BRIDGE outperforms current state-of-the-art pathology foundation models in predicting cancer survival, achieving an average concordance index (C-index) of 0.724 across six TCGA cohorts. Notably, BRIDGE maintains exceptional performance even in zero-shot scenarios involving three cancer types not seen during its training, achieving an average C-index of 0.717, thereby demonstrating its strong generalization capability that transcends organ- and subtype-specific boundaries. Moreover, BRIDGE-generated virtual spatial transcriptomes match the prognostic accuracy of bulk RNA-seq, highlighting their potential as a spatially informative alternative to laboratory sequencing. In general, BRIDGE represents a data-efficient tool in virtual ST that facilitates biomedical discoveries in clinical few-shot contexts and advances diagnosis of understudied cancers without sufficient samples.