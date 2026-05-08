---
title: Reconstructing True 3D Spatial Omics at Single-Cell Resolution
title_zh: 单细胞分辨率下真实三维空间组学的重建
authors: "Yang, Y., Luo, Y., Zhang, K., Bu, Y., Xia, Z., Peng, H., Yan, R., Liu, Q., Chen, Y., Shen, L., Chen, E."
date: 2026-05-01
pdf: "https://www.biorxiv.org/content/10.64898/2026.04.28.721395v1.full.pdf"
tags: ["query:cellrep"]
score: 6.0
evidence: 在单细胞分辨率下重建3D空间组织
tldr: 本研究为解决三维空间组学受物理切片破坏和深度成像限制的问题，提出基于最优传输流匹配的连续动态向量场框架，实现单细胞分辨率的组织三维重建。该方法在多种空间组学数据中显著提升重建保真度，并成功构建大规模鼠脑三维细胞图谱，展现出高效和普适的重建能力。
source: biorxiv
selection_source: fresh_fetch
motivation: 三维空间组学受限于物理切片破坏性和成像深度，亟需非破坏性、高保真重建方法。
method: 提出基于最优传输流匹配的概率流微分方程框架，以连续动态向量场模型重建无限分辨率的组织状态。
result: 该方法在多种空间组学数据中提高了三维重建保真度，能重现真实组织结构，并成功构建包含3900万细胞的鼠脑连续三维图谱。
conclusion: 该研究表明所提出的框架能高效、可泛化地实现跨尺度和跨模态的真实三维空间组学重建。
---

## 摘要
捕捉细胞的三维（3D）组织结构对于解析复杂的生物过程至关重要，然而，由于物理切片的破坏性以及对完整组织成像的深度限制，全面的三维空间组学一直受到严重阻碍。目前的计算方法依赖于离散切片的2.5D堆叠，这种方式会扰乱组织的拓扑结构，且无法解析连续的深度依赖分子梯度。为弥合这一差距，我们提出了 DO_SCPLOWEEPC_SCPLOWSO_SCPLOWPATIALC_SCPLOW，这是一种基于最优传输流匹配的框架，将组织演化建模为连续的动态向量场。通过求解潜在的概率流常微分方程，DO_SCPLOWEEPC_SCPLOWSO_SCPLOWPATIALC_SCPLOW 能够在任意空间深度处直接提取不间断、无限分辨率的组织状态。结合 Deep STAR/RIBOmap 3D 技术，我们证明 DO_SCPLOWEEPC_SCPLOWSO_SCPLOWPATIALC_SCPLOW 较传统的 2.5D 方法具有更高的三维重建保真度，能够在真实数据集中生成更贴近组织原生微环境的结构。跨越多种空间组学模式，包括在人类乳腺癌中利用成像质谱流式细胞术进行空间蛋白质组学，以及在头颈鳞状细胞癌转移性淋巴结中利用 openST 进行空间转录组学，DO_SCPLOWEEPC_SCPLOWSO_SCPLOWPATIALC_SCPLOW 在不同数据集中均产生具有生物学可解释性和高保真的重建结果。我们在大规模小鼠脑数据集上评估了 DO_SCPLOWEEPC_SCPLOWSO_SCPLOWPATIALC_SCPLOW 的可扩展性和稳健性，成功重建了一个包含 3900 万个细胞的连续三维细胞图谱，仅用时 41.6 小时。系统的下游表征验证了其能够在不同脑区中再现一致的空间结构、细胞类型分布、转录组模式以及微环境结构。总体而言，这些结果表明 DO_SCPLOWEEPC_SCPLOWSO_SCPLOWPATIALC_SCPLOW 是一种可推广且高效的多尺度、多模态真实三维空间重建解决方案。

## Abstract
Capturing the three-dimensional (3D) organization of cells is essential for deciphering complex biological processes, yet comprehensive 3D spatial omics is severely hindered by the destructive nature of physical sectioning and the depth limitations of intact tissue imaging. Current computational methods rely on 2.5D stacking of discrete slices, which inherently disrupts tissue topology and fails to resolve continuous depth-dependent molecular gradients. To bridge this gap, we introduce DO_SCPLOWEEPC_SCPLOWSO_SCPLOWPATIALC_SCPLOW, an Optimal Transport flow matching framework that models tissue evolution as a continuous dynamic vector field. By solving the underlying probability flow ODEs, DO_SCPLOWEEPC_SCPLOWSO_SCPLOWPATIALC_SCPLOW enables the direct extraction of uninterrupted, infinitely resolvable tissue states at arbitrary spatial depths. Using Deep STAR/RIBOmap 3D technologies, we demonstrate that DO_SCPLOWEEPC_SCPLOWSO_SCPLOWPATIALC_SCPLOW achieves improved 3D reconstruction fidelity relative to 2.5D approaches, yielding structures that more closely recapitulate native tissue microenvironments in real-world datasets. Across diverse spatial omics modalities, including spatial proteomics using imaging mass cytometry in human breast cancer and spatial transcriptomics using openST in head and neck squamous cell carcinoma metastatic lymph nodes, DO_SCPLOWEEPC_SCPLOWSO_SCPLOWPATIALC_SCPLOW produces biologically interpretable and high-fidelity reconstructions across datasets. We evaluated the scalability and robustness of DO_SCPLOWEEPC_SCPLOWSO_SCPLOWPATIALC_SCPLOW on a large-scale mouse brain dataset, reconstructing a continuous 3D cellular atlas comprising 39 million cells within 41.6 hours. Systematic downstream characterization validated its ability to recapitulate consistent spatial architectures, cell-type distributions, transcriptomic patterns, and microenvironmental structures across brain regions. Collectively, these results demonstrate DO_SCPLOWEEPC_SCPLOWSO_SCPLOWPATIALC_SCPLOW as a generalizable and efficient solution for true 3D spatial reconstruction across scales and modalities.