---
title: Deep Learning Enables Automated Segmentation and Quantification of Ultrastructure from Transmission Electron Microscopy Images
title_zh: 深度学习实现透射电子显微镜图像中超微结构的自动分割与定量分析
authors: "Zou, A., Tan, W., Ji, J., Rojas-Miguez, F., Dodd, L., Oei, E., Vargas, S. R., Yang, H., Berasi, S. P., Chen, H., Henderson, J. M., Fan, X., Lu, W., Zhang, C."
date: 2026-04-17
pdf: "https://www.biorxiv.org/content/10.1101/2025.11.05.686793v2.full.pdf"
tags: ["query:pathseg"]
score: 7.0
evidence: 显微镜图像超微结构的自动分割
tldr: 本文提出了 TEAMKidney，一个基于深度学习的 TEM 图像自动分割与量化框架，可跨物种和设备准确测量肾脏超微结构，显著减少人工分析负担，在多类肾病图像上验证了高精度并与专家测量高度一致。
source: biorxiv
selection_source: fresh_fetch
figures_json: "[{\"url\": \"assets/figures/biorxiv/biorxiv-10-1101-2025-11-05-686793-v2/fig-001.webp\", \"caption\": \"Table 1. Data Collection and Selection Criteria. 843\", \"page\": 40, \"index\": 1, \"width\": 954, \"height\": 446}]"
motivation: TEM 图像分析依赖人工操作且缺乏专用算法，导致耗时和结果不一致。
method: 结合自训练语义分割与 TEM 专用全景分割模型处理复杂超微结构。
result: 团队通过 TEAMKidney 在人类和动物 TEM 图像中揭示与肾病相关的关键超微结构变化。
conclusion: TEAMKidney 显示出深度学习可显著提升超微结构分析的效率和准确性，推动临床与研究的自动化。
---

## 摘要
透射电子显微镜（Transmission Electron Microscopy, TEM）已成为观测细胞亚结构的关键技术，被广泛应用于临床诊断与生物医学研究。然而，由于缺乏专用的计算方法，TEM 数据的分析仍然极为耗时，并且不同操作者之间的一致性较差。在本研究中，我们提出了 TEAMKidney——一种基于深度学习的框架，可在不同物种、倍率及仪器平台上对 TEM 图像中的超微结构进行精确且可扩展的测量。我们收集了来自多种肾脏疾病患者及不同动物模型的 12,991 张 TEM 图像。通过将基于自训练的语义分割阶段与专为 TEM 设计的全景分割模型相结合，我们解决了 TEM 数据分析中的两大挑战：准确标注训练数据的缺乏，以及复杂超微结构高精度分割的困难。将 TEAMKidney 应用于人类与动物图像中，我们成功揭示了与疾病相关的两种关键肾小球超微结构变化：肾小球基底膜与足细胞足突。与现有工具相比，TEAMKidney 的性能显著提升，并与临床评估中病理专家的测量结果高度一致。通过在保持专家级精度的同时降低对人工描绘的依赖，TEAMKidney 证明了深度学习在临床病理及生物医学研究中可显著减轻图像分析负担的潜力。

## Abstract
Transmission electron microscopy (TEM) has become an essential technique for observing subcellular ultrastructure, and is widely used in both clinical diagnosis and biomedical research. However, analysis of TEM data remains extremely labor-intensive and often inconsistent across operators due to the lack of dedicated computational methods. Here, we present TEAMKidney, a deep learning framework for accurate and scalable measurement of ultrastructures in TEM images across species, magnifications, and instrument platforms. We collected 12,991 TEM images from patients with multiple kidney diseases and from different animal models. By combining a self-training-based semantic segmentation stage with a TEM-tailored panoptic segmentation model, we address two major challenges in TEM data analysis: the lack of accurately labeled training data and the difficulty of achieving high segmentation accuracy for complex ultrastructure. Application of TEAMKidney to both human and animal images successfully reveals disease-associated changes in two critical glomerular ultrastructures: the glomerular basement membrane and podocyte foot processes. In addition to significantly outperforming existing tools, TEAMKidney shows close agreement with pathological expert measurements used in clinical assessment protocols. By reducing dependence on manual tracing while preserving expert-level accuracy, TEAMKidney demonstrates that deep learning can substantially reduce the burden of image analysis in both clinical pathology and biomedical research settings.