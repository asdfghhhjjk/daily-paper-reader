---
title: "CenSegNet: a generalist high-throughput deep learning framework for centrosome phenotyping at spatial and single-cell resolution in heterogeneous tissues"
title_zh: CenSegNet：一种可在异质组织中实现空间与单细胞分辨率中心体表型分析的通用高通量深度学习框架
authors: "Cheng, J., Fan, K., Bailey, M., Du, X., Jena, R., Savva, C., Reed, E., Gou, M., Zuo, P., Beers, S., Cutress, R., Cai, X., Elias, S."
date: 2026-05-04
pdf: "https://www.biorxiv.org/content/10.1101/2025.09.15.676250v3.full.pdf"
tags: ["query:cellrep"]
score: 7.0
evidence: 免疫组化图像中中心体表型分析的深度学习框架
tldr: 该研究针对传统图像分析无法解析中心体异常空间特征的问题，开发了CenSegNet深度学习框架，实现不同组织类型下中心体和上皮结构的高分辨分割，在乳腺癌组织微阵列分析中揭示中心体异常的多样空间分布及临床相关性，提供了开源通用平台。
source: biorxiv
selection_source: fresh_fetch
motivation: 传统图像分析难以精确解析中心体异常在肿瘤组织中的空间复杂性和表型异质性。
method: 研究提出了一个双分支架构并结合不确定性引导优化的深度学习框架，用于中心体和组织结构的高分辨率分割。
result: CenSegNet在多种组织和成像模式中均表现出优异的分割准确性与形态保真度，并揭示了中心体异常与临床特征、预后之间的关联。
conclusion: CenSegNet为空间分辨的中心体表型分析提供了高通量、通用、可扩展的工具，推动癌症和上皮疾病中中心体异常机制研究。
---

## 摘要
中心体异常（CA）是上皮癌的标志之一，但由于传统图像分析的局限，其空间复杂性和表型异质性仍缺乏清晰刻画。本研究提出 CenSegNet（Centrosome Segmentation Network，中心体分割网络），一种模块化深度学习框架，可在多种组织类型中实现高分辨率、上下文感知的中心体和上皮结构分割。通过结合双分支架构与基于不确定性的精细化策略，CenSegNet 在免疫荧光与免疫组化等多种成像模式下均表现出最先进的性能与广泛的泛化能力，在准确性与形态保真度上均优于现有模型。应用于包含来自 127 位患者的 911 个乳腺癌样本核心的组织芯片（TMA）后，CenSegNet 首次实现了在单细胞分辨率下对数值及结构性 CA 的空间定量分析。这些 CA 亚型在机制上相互独立，表现出不同的空间分布、随年龄变化的动态特征，以及与组织学肿瘤分级、激素受体状态、基因组改变和淋巴结受累的相关性。结构性 CA 水平进一步与总体生存率相关，支持空间分辨 CA 模式的临床意义。肿瘤边缘处的不一致 CA 表型与局部侵袭性及基质重塑有关。为促进广泛应用与可重复性，CenSegNet 作为开源 Python 库发布。综上所述，本研究确立了 CenSegNet 作为一种可扩展且具普适性的完整组织空间分辨中心体表型分析平台，从而系统解析中心体生物学及其在癌症与其他上皮疾病中的失调机制。

## Abstract
Centrosome abnormalities (CA) are a hallmark of epithelial cancers, yet their spatial complexity and phenotypic heterogeneity remain poorly resolved due to limitations in conventional image analysis. We present CenSegNet (Centrosome Segmentation Network), a modular deep learning framework for high-resolution, context-aware segmentation of centrosomes and epithelial architecture across diverse tissue types. Integrating a dual-branch architecture with uncertainty-guided refinement, CenSegNet achieves state-of-the-art performance and generalisability across both immunofluorescence and immunohistochemistry modalities, outperforming existing models in accuracy and morphological fidelity. Applied to tissue microarrays (TMAs) containing 911 breast cancer sample cores from 127 patients, CenSegNet enables the first large-scale, spatially resolved quantification of numerical and structural CA at single-cell resolution. These CA subtypes are mechanistically uncoupled, exhibiting distinct spatial distributions, age-dependent dynamics, and associations with histological tumour grade, hormone receptor status, genomic alterations, and nodal involvement. Structural CA levels are additionally associated with overall survival, supporting the clinical relevance of spatially resolved CA patterns. Discordant CA profiles at tumour margins are linked to local aggressiveness and stromal remodelling. To support broad adoption and reproducibility, CenSegNet is released as an open-source Python library. Together, our findings establish CenSegNet as a scalable, generalisable platform for spatially resolved centrosome phenotyping in intact tissues, enabling systematic dissection of the biology of this organelle and its dysregulation in cancer and other epithelial diseases.