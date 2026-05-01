---
title: "Semi supervised GAN for smart microscopy, fast and data efficient cell cycle classification"
title_zh: 用于智能显微镜的半监督GAN：快速且数据高效的细胞周期分类
authors: "Manick, R., El Habouz, Y., Guillout, M., Martin, C., Bonnet-gelebart, J., Ruel, L., Pastezeur, S., Chanteux, O., Bouchareb, O., Tramier, M., Pecreaux, J."
date: 2026-04-27
pdf: "https://www.biorxiv.org/content/10.64898/2026.04.23.720294v1.full.pdf"
tags: ["query:cellrep"]
score: 8.0
evidence: 在显微镜中使用半监督GAN进行细胞周期分类
tldr: 本文提出一种半监督生成对抗网络（SGAN），用于低资源条件下的细胞周期阶段分类，通过结合未标注显微图像和合成样本，实现高准确度和强泛化性，为智能显微镜实时图像分析提供数据高效的解决方案。
source: biorxiv
selection_source: fresh_fetch
motivation: 智能显微镜需要在有限标注数据下实现实时、准确的生物事件识别与分类。
method: 采用半监督生成对抗网络结合未标注图像和合成数据进行细胞周期分类。
result: "在Mitocheck数据集上，SGAN仅用少量标注和未标注数据就达到了93±2%的分类准确率。"
conclusion: SGAN具有良好的可迁移性和稳定性，能够支持不同细胞结构和显微镜系统的智能图像分析。
---

## 摘要
现代光学显微镜已实现全自动化，但要将其真正转变为智能系统，还需根据检测到的目标和动态生物事件实时调整采集设置。关键在于分类算法，这些算法通常依赖定制化软件，并且一般专为某一狭窄定义的生物应用设计。此外，它们往往需要大量带标注的数据集以实现有效训练。我们提出了一种用于低资源条件下细胞周期阶段稳健分类的半监督生成对抗网络（SGAN），可适配多种细胞结构。该框架结合未标注的显微图像与合成生成样本，以缓解标注不足问题，同时在未标注数据子集类别不平衡时仍保持稳定性能。在包含五种有丝分裂类别的Mitocheck数据集上测试时，该模型仅使用每类80张标注图像和600张未标注图像，便实现了93{+/-}2%的准确率。所提出的算法具有通用性，可通过迁移学习轻松适应新的标注方案、分类目标、细胞系或显微成像模式。SGAN非常适合集成到自动化显微镜中，从而在多样的生物和显微应用中实现高效且可适应的图像分析。

## Abstract
Modern optical microscopes are fully motorised; however, transforming them into truly smart systems requires real-time adjustment of acquisition settings in response to detected objects and dynamic biological events. At the core are classification algorithms that commonly depend on customised softwares and are generally designed for narrowly-defined biological applications. In addition, they often require substantial annotated datasets for effective training. We introduce a semi-supervised generative adversarial network (SGAN) for robust cell-cycle stage classification under low-resource conditions, adaptable to diverse cellular structures. The framework combines unlabelled microscopy images with synthetically generated samples to mitigate limited annotation, while preserving stable performance even when the unlabelled subset is class-imbalanced. Tested on the Mitocheck dataset, which features five mitosis classes, the model achieved 93{+/-}2% accuracy using only 80 labelled per class and 600 unlabelled images. The proposed algorithm is generic and can be readily adapted to new labeling schemes, classification targets, cell lines, or microscopy modalities through transfer learning. SGAN is well suited for integration into automated microscopes, enabling efficient and adaptable image analysis across diverse biological and microscopy applications.