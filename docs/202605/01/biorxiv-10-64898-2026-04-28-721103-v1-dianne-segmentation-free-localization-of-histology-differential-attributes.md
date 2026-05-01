---
title: "DIANNE: Segmentation-Free Localization of Histology Differential Attributes"
title_zh: DIANNE：基于组织学差异属性的无分割定位方法
authors: "Domanskyi, S., Rubinstein, J. C., Sheridan, T. B., Thiesen, A., Noorbakhsh, J., Alcoforado Diniz, J., Ramasamy, R., Baker, D. S., Sheldon, R., Wu, Q., Kuchel, G., Robson, P., Chuang, J. H."
date: 2026-05-01
pdf: "https://www.biorxiv.org/content/10.64898/2026.04.28.721103v1.full.pdf"
tags: ["query:cellrep"]
score: 8.5
evidence: 用于快速训练和推理空间差异属性的数字病理学方法
tldr: "本研究提出DIANNE，一个无需分割的数字病理定位方法，以正类混合增强方式实现快速弱监督训练，可在H&E及空间组学图像中实现秒级差异特征定位，支持实时交互分析并揭示新型空间表型。"
source: biorxiv
selection_source: fresh_fetch
motivation: 当前数字病理依赖大量人工标注，难以应对新型空间特征探索的需求。
method: 提出基于正类混合增强的快速弱监督训练方法，实现分割自由的差异属性定位。
result: DIANNE能在秒级时间内定位和可视化差异性分类器，实现即时模型再训练和多种组织类型分析。
conclusion: DIANNE为理解已知和新型组织空间表型提供了一种高效、可扩展的计算工具。
---

## 摘要
在组织学和空间组学图像中，病理学专家主导的区分可为健康与疾病提供重要见解，数字病理学借助人工智能实现这些评估的自动化。现有数字病理学方法在训练计算模型时依赖于前期人工标注，这一过程耗时且费力。预标注不适合探索新的空间行为——这是由空间分析技术进步所带来的主要需求——因为标注标准和数据需求尚不明确。为应对这些挑战，我们提出了 DIANNE，这是一种基于训练阶段正类混合增强（Positive Class Mixup Augmentation）的数字病理学方法，可实现空间差异属性的快速训练与推理。DIANNE 能够在工作站上于几秒内完成从基础模型推导出的整张 H&E 切片中差异分类器的无分割定位，从而支持交互式空间微环境研究。预测模型可在响应局部或区域标注变更时实现实时再训练，从仅需数十个标注块的切片中揭示关键生物属性。我们展示了 DIANNE 在肿瘤检测、伪影识别以及胰腺、胎膜和肾组织结构探索中的有效性。DIANNE 还可用于 IHC、多重免疫荧光以及注册的空间转录组+H&E 图像分析。DIANNE 已在 Jupyter 工具包中实现，可通过弱监督训练快速构建高分辨率分类器。DIANNE 提供了一种可量化理解已知与新型空间表型的实用系统。

## Abstract
Pathologist-guided distinctions within histology and spatial omic images provide insights into health and disease, with digital pathology leveraging artificial intelligence to automate such assessments. To train computational models, current digital pathology methods rely on upfront manual annotations, which are time-consuming to generate. Pre-annotation is poorly suited to investigating novel spatial behaviors - a major need driven by advances in spatial profiling - for which annotation criteria and data needs will be uncertain. To address these challenges, we present DIANNE, a digital pathology approach for rapid training and inference of spatial differential attributes based on train-time Positive Class Mixup Augmentation. DIANNE can compute foundation model-derived segmentation-free localization of differential classifiers across whole slide H&E images within seconds on a workstation, enabling interactive investigation of spatial niches. Predictive models can be re-trained in real-time in response to patch or regional annotation changes, clarifying determinative biological attributes across slides from only a few dozen annotated patches. We demonstrate the effectiveness of DIANNE for tumor detection, artifact identification, and exploration of pancreatic, fetal membranes and kidney tissue structures. DIANNE also provides analogous capabilities for IHC, multiplex immunofluorescence, and registered spatial transcriptomic+H&E images. DIANNE is implemented in a Jupyter toolkit, enabling rapid development of high-resolution classifiers from weakly-supervised training. DIANNE provides a practical system to quantitatively understand known and novel spatial phenotypes.