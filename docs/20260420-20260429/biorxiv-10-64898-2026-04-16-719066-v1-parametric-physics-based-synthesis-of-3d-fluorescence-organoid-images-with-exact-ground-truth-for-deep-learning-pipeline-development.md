---
title: Parametric Physics-Based Synthesis of 3D Fluorescence Organoid Images with Exact Ground Truth for Deep Learning Pipeline Development
title_zh: 基于物理的参数化合成三维荧光类器官图像：用于深度学习流程开发的精确真值生成
authors: "Bhattiprolu, S."
date: 2026-04-22
pdf: "https://www.biorxiv.org/content/10.64898/2026.04.16.719066v1.full.pdf"
tags: ["query:pathseg"]
score: 8.0
evidence: 3D图像中细胞体和细胞核标签掩码的框架
tldr: 本研究针对3D类器官荧光显微成像中深度学习训练数据不足的问题，提出了一个参数化物理建模框架，可生成具备真实光学特性与精确细胞标签的合成图像，为算法开发与评估提供高质量数据源。
source: biorxiv
selection_source: fresh_fetch
motivation: 深度学习分析3D类器官图像需要大量标注数据，但人工标注成本高昂且耗时，亟需自动化生成具备真实特征的合成数据。
method: 采用基于力导向球体填充与Laguerre镶嵌的细胞建模，并结合光学衍射、噪声和荧光扩散等物理效应生成合成图像。
result: 提出了一个基于物理建模的参数化框架，能生成具有精确标注的3D荧光类器官图像。
conclusion: 该框架为器官类荧光图像的合成及深度学习管线的开发提供了可控、可解释且高保真的新途径。
---

## 摘要
三维类器官培养已成为研究人体组织生物学、疾病机制和药物反应的强大模型。类器官的荧光共聚焦显微成像会生成复杂的体积图像数据，这些数据越来越多地被用于通过深度学习流程进行细胞分割、形态测量和表型分析。然而，训练和评估此类流程需要大量带注释的数据集，而人工标注过程既昂贵又耗时。本文提出了一种参数化、基于物理的计算框架，用于生成具有精确真值的合成三维荧光类器官图像，包括细胞体和细胞核的标签掩膜。

该框架通过基于力导向的球体堆积模拟细胞排列，可选空腔排除机制用于形成囊性类器官；通过幂图（Laguerre）镶嵌建模细胞形态，并考虑极性上皮细胞的顶底延展及表面平整；通过低频坐标位移建模膜曲率；通过不规则椭球形变及平滑径向偏心方向混合建模核形态；光学效应方面包括深度依赖的点扩散函数展宽、基于物理的染料扩散梯度（具有残余内部平台）、z轴衰减、雾化、散粒噪声以及通道串扰。坏死核心模型包含三种核表型：浓缩型（pyknotic）、幽灵型（ghost）和核碎裂型（karyorrhectic），反映了真实坏死区的组织学多样性。

该框架提供五种特定条件预设，基于已发表的生物测量进行校准，涵盖胰腺导管腺癌（PDAC）渗透压应激、HMECyst正常及囊性类器官，以及具有坏死核心的大型原发PDAC类器官。与生成对抗网络方法不同，我们的方法无需训练数据，可由构造获得精确真值，并能系统且可解释地控制每一个形态和光学参数。该框架作为开源Python软件发布，配备PyQt5图形界面，并输出兼容arivis Pro、FIJI和napari以及其他显微图像分析软件的OME-TIFF格式。

## Abstract
1Three-dimensional organoid cultures have emerged as powerful models for studying human tissue biology, disease mechanisms, and drug responses. Fluorescence confocal microscopy of organoids generates complex volumetric image data that is increasingly analyzed using deep learning pipelines for cell segmentation, morphometry, and phenotyping. However, training and benchmarking such pipelines requires large annotated datasets, the manual curation of which is prohibitively expensive and time-consuming. Here we present a parametric, physics-based computational framework for generating synthetic 3D fluorescence organoid images with exact ground-truth cell body and nucleus label masks.

The framework models cell placement using force-directed sphere packing with optional hollow lumen exclusion for cyst-forming organoids, cell morphology using power-diagram (Laguerre) tessellation with apical-basal elongation and surface flattening for polarized epithelial cells, membrane curvature using low-frequency coordinate displacement, nuclear shape using irregular ellipsoid deformation with smooth radial eccentricity direction blending, and optical effects using depth-dependent point-spread function broadening, a physically motivated staining diffusion gradient with residual interior plateau, z-attenuation, haze, shot noise, and channel crosstalk. The necrotic core model uses a three-phenotype nuclear population, pyknotic, ghost, and karyorrhectic, reflecting the histological diversity of real necrotic zones.

Five condition-specific presets are provided, calibrated to published biological measurements and covering PDAC osmotic stress, HMECyst normal and cyst-forming organoids, and a large primary PDAC organoid with a necrotic core. Unlike generative adversarial network approaches, our method requires no training data, produces exact ground truth by construction, and allows systematic and interpretable control over every morphological and optical parameter. The framework is released as open-source Python software with a PyQt5 graphical interface and produces OME-TIFF output compatible with arivis Pro, FIJI, and napari, as well as most other microscopy image analysis software.