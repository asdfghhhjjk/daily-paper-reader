---
title: Autofluorescence intensity patterns encode α/β cell identity in human islets
title_zh: 自发荧光强度模式编码人类胰岛中α/β细胞的身份信息
authors: "Squicccimarro, I., Azzarello, F., De Lorenzi, V., Raimondi, F., Ghelli, A., Beltram, F., Cardarelli, F."
date: 2026-05-04
pdf: "https://www.biorxiv.org/content/10.64898/2026.04.30.721886v1.full.pdf"
tags: ["query:cellrep"]
score: 6.0
evidence: 利用细胞内强度模式和形态特征进行细胞身份分类
tldr: 该研究提出利用内源性自发荧光的强度分布模式，通过局部三值模式描述符与形态特征实现人胰岛α、β细胞的无标记区分，准确率高达AUC 0.92，方法轻量且可解释，为非破坏性细胞类型识别提供新途径。
source: biorxiv
selection_source: fresh_fetch
motivation: 当前的人胰岛细胞类型识别方法依赖破坏性标记或昂贵的高级成像技术，亟需一种简单、无损且可推广的替代方案。
method: 研究使用旋转不变的局部三值模式（LTP）描述符结合形态特征来分析自发荧光图像并实现细胞分类。
result: 该方法在区分α与β细胞方面达到了AUC 0.92的高准确率，并证实细胞判别主要依赖于细胞内部强度分布而非整体形态。
conclusion: 自发荧光强度的结构模式可以在无损条件下准确识别胰岛中α和β细胞，为细胞类型识别提供了可解释且易获取的新方法。
---

## 摘要
理解完整人类胰岛中α-和β-细胞的行为对于阐明糖尿病中的代谢控制机制至关重要。当前的细胞类型识别策略依赖于破坏性标记，或依赖于如荧光寿命成像显微镜（Fluorescence Lifetime Imaging Microscopy，FLIM）等先进成像技术，这些方法虽然能提供丰富的代谢信息，但需要专门的仪器和采集流程。在本研究中，我们展示了由内源性自发荧光产生的细胞内结构化强度模式足以区分活体人类胰岛中的α-与β-细胞。通过将旋转不变的局部三值模式（Local Ternary Pattern, LTP）描述符与形态学特征相结合，我们实现了高精度分类（AUC = 0.92），优于先前报道的基准结果。所得框架轻量、可解释，并兼容标准成像配置，使无标记显微数据的分析更加易用且可扩展。可解释性分析表明，细胞区分主要由细微尺度的胞内强度组织驱动，而非整体形态。在所使用的光谱范围内，细胞质自发荧光主要受富含脂褐素颗粒的影响。与先前关于β-细胞中脂褐素积累较多的报道一致，本研究所识别的主要特征可能反映了不同内分泌细胞类型在颗粒丰度和空间组织方面的差异。这些发现表明，内源性的强度模式编码了足够的结构信息以可靠地区分α/β细胞，为胰岛细胞类型识别提供了一种具有生物学基础且完全无损的新方法。

## Abstract
Understanding the behavior of - and {beta}-cells within intact human islets is essential for elucidating mechanisms of metabolic control in diabetes. Current cell-type identification strategies rely on destructive labeling or on advanced imaging modalities such as Fluorescence Lifetime Imaging Microscopy (FLIM), which provide rich metabolic information but require specialized instrumentation and acquisition protocols. Here we show that structured intracellular intensity patterns derived from endogenous autofluorescence are sufficient to discriminate  and {beta} cells in living human islets. Using rotation-invariant Local Ternary Pattern (LTP) descriptors combined with morphological features, we achieve highly accurate classification (AUC = 0.92), improving upon previously reported benchmarks. The resulting framework is lightweight, interpretable, and compatible with standard imaging configurations, enabling accessible and scalable analysis of label-free microscopy data. Interpretability analyses demonstrate that discrimination is driven predominantly by fine-scale intracellular intensity organization rather than global morphology. In the spectral window employed, cytoplasmic autofluorescence is prominently shaped by lipofuscin-rich granules. Consistent with prior reports of higher lipofuscin accumulation in {beta}-cells, the dominant features identified here likely reflect differences in granule abundance and spatial organization between endocrine cell types. These findings indicate that endogenous intensity patterns encode sufficient structural information for reliable /{beta} discrimination, providing a biologically grounded and fully non-destructive framework for the identification of pancreatic islet cell types.