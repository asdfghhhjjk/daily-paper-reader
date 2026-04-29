---
title: Pan-cancer virtual spatial transcriptomics from routine histology with Phoenix
title_zh: 通过 Phoenix 从常规组织学实现跨癌种虚拟空间转录组学
authors: "Tran, M., Gindra, R. H., Putze, P., Senbai, K., Palla, G., Kos, T., Falcomata, C., Wang, C., Guo, R., Boxberg, M., Berclaz, L. M., Lindner, L. H., Bergmayr, L., Knoesel, T., Jurmeister, P., Klauschen, F., Homicsko, K., Gottardo, R., Eckstein, M., Matek, C., Mock, A., Theis, F. J., Saur, D., Peng, T."
date: 2026-04-29
pdf: "https://www.biorxiv.org/content/10.64898/2026.04.25.720812v1.full.pdf"
tags: ["query:cellrep"]
score: 8.5
evidence: 从组织学预测空间分辨率单细胞基因表达
tldr: 该研究为解决空间转录组学高成本和数据不足的问题，提出了基于潜在流匹配的生成模型Phoenix，可从常规病理图像准确推断单细胞空间基因表达，在多种癌症及物种实验中展现出高准确性和良好泛化性，发现新的治疗相关空间标志物。
source: biorxiv
selection_source: fresh_fetch
motivation: 现有空间转录组数据有限且成本高，亟需能从常规组织学图像预测基因表达的计算方法。
method: 研究提出Phoenix，一种基于潜在流匹配的生成模型，用于从组织切片推断单细胞空间基因表达。
result: Phoenix在多个癌种及跨物种样本中准确重建基因表达，发现并验证了新的空间生物标志物。
conclusion: Phoenix确立了从常规病理切片实现虚拟空间转录组学的可扩展框架，为研究组织结构、治疗反应及疾病机制提供新途径。
---

## 摘要
空间转录组学将基因表达与组织架构联系起来，提供了细胞组织的机制性视角。然而，现有的数据集仅涵盖少数供体，无法体现人类疾病的复杂性。实验成本仍然高昂，大规模测定对于群体水平研究来说难以实现，因此迫切需要准确的计算方法。尽管如此，从标准组织学图像预测基因表达仍是一个尚未解决的问题，因为当前的方法在未知的队列和疾病中泛化性能较差。在本文中，我们提出了 Phoenix，这是一种潜变量流匹配生成模型，能够以高精度推断跨癌种、空间分辨的单细胞基因表达。Phoenix 可以在计算机模拟中分析治疗反应：应用于763例头颈癌患者时，它识别出三种新的空间生物标志物，并在两种癌症（乳腺癌，n = 84；卵巢癌，n = 157）以及不同治疗方案（铂类、trastuzumab）中得到验证。Phoenix 的泛化能力超越了癌瘤类型：在一个大型肉瘤队列（802个组织芯片样本）中，它在留出样本中准确预测了细胞类型特异性特征，并捕捉到了化疗诱导的免疫重塑。Phoenix 还可以跨物种应用：在一个小鼠模型中，它准确预测了胰腺癌谱系标记基因和突变 mKrasG12D 等位基因的表达。综上，Phoenix 建立了从常规组织学实现虚拟空间转录组学的可扩展框架，为研究组织结构、治疗反应和疾病机制提供了新途径。

## Abstract
Spatial transcriptomics links gene expression to tissue architecture, providing a mechanistic view of cellular organization. Yet existing datasets cover few donors and miss the complexity of human disease. Experimental costs remain prohibitive, and large-scale profiling is impractically slow for population-level studies. Accurate computational methods are urgently needed. Predicting gene expression from standard histology, however, remains an open problem, as current approaches transfer poorly to unseen cohorts and diseases. Here, we present Phoenix, a latent flow matching generative model that infers pan-cancer spatially resolved single-cell gene expression with high accuracy. Phoenix analyzes treatment response in silico: Applied to 763 head and neck cancer patients, it identified three new spatial biomarkers that we validated across two cancers (breast cancer, n = 84; ovarian cancer, n = 157) and treatment regimens (platinum, trastuzumab). Phoenix generalizes beyond carcinomas: In a large sarcoma cohort (802 tissue microarray cores), it accurately predicted cell-type-specific signatures in held-out samples and captured chemotherapy-induced immune remodeling. Phoenix also extends across species: In a mouse model, it accurately predicted the expression of pancreatic cancer lineage markers and the mutant mKrasG12D allele in silico. Together, Phoenix establishes virtual spatial transcriptomics from routine histology as a scalable framework for studying tissue organization, therapeutic response, and disease mechanisms.