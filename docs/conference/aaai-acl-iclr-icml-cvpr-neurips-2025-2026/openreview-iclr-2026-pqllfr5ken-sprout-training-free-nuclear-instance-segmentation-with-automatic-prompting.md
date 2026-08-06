---
title: "SPROUT: Training-free Nuclear Instance Segmentation with Automatic Prompting"
title_zh: SPROUT：基于自动提示的免训练细胞核实例分割
authors: "Wen Zhang, Qin Ren, Wenjing Liu, Haibin Ling, Chenyu You"
date: 2025-09-04
pdf: "https://openreview.net/pdf?id=pqLlFR5ken"
tags: ["query:cellseg"]
score: 8.0
evidence: "免训练细胞核实例分割，为从H&E图像中提取细胞特征提供基础"
tldr: 针对病理图像细胞核分割标注成本高、现有方法需微调的问题，提出SPROUT框架，利用组织学染色先验构建切片特定参考，通过免训练方式实现零样本实例分割，为下游细胞级分析提供了轻量高效的细胞分割工具。
source: ICLR-2026-Public
selection_source: conference_retrieval
motivation: 病理图像细胞核分割依赖昂贵标注和大量计算，免训练方法尚待探索。
method: 提出SPROUT，使用染色先验构造参考并利用基础模型进行免训练的核实例分割。
result: 在多个基准上达到与微调方法相当的精度，且无需任何标注和训练。
conclusion: SPROUT为数字病理中的细胞分割提供了可立即应用的工具，加速下游任务。
---

## Abstract
Nuclear instance segmentation is a cornerstone task in digital pathology, with broad potential to drive clinical decision-making and accelerate therapeutic discovery. Recent advances in large vision foundation models have shown promise for zero-shot segmentation in biomedical domains. However, most efforts in pathology still rely on pre-trained vision models through fine-tuning or adapter modules. These approaches demand costly annotations and heavy computation, leaving efficient training-free methods largely unexplored.
To this end, we propose SPROUT, a simple yet effective framework for annotation-free prompting. Specifically, we leverage histology-informed stain priors to construct slide-specific references for mitigating domain gaps and instantiate a prototype-guided partial optimal transport scheme to progressively refine nuclear representations. In addition, we embed high-quality positive and negative prompts into the Segment Anything Model (SAM) without any fine-tuning.
Extensive experiments across multiple histopathology benchmark datasets demonstrate that SPROUT achieves competitive performance while requiring neither annotations nor retraining. These results establish SPROUT as a scalable, training-free solution for nuclear instance segmentation in computational pathology. Our codes are available at here.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
免训练细胞核实例分割，为从H&E图像中提取细胞特征提供基础。

### 2. 核心内容
针对病理图像细胞核分割标注成本高、现有方法需微调的问题，提出SPROUT框架，利用组织学染色先验构建切片特定参考，通过免训练方式实现零样本实例分割，为下游细胞级分析提供了轻量高效的细胞分割工具。

### 3. 对应检索需求
Papers central to 充分利用HE切片中细胞分类和分割结果中的信息来完成下游任务, especially work that connects or combines: classifying cells in hematoxylin and eosin stained images; classification algorithms for cell nuclei; tumor microenvironment analysis from cell segmentation; spatial distribution analysis of cells; digital pathology image analysis; extracting features from cell segmentations; How to use cell segmentation and classification results for cancer prognosis modeling?; Integrating cell level information from H&E slides into downstream machine learning tasks.; Spatial analysis of tumor microenvironment using cell segmentation data..

### 4. 来源与原文
- Source：ICLR-2026-Public
- OpenReview：[https://openreview.net/forum?id=pqLlFR5ken](https://openreview.net/forum?id=pqLlFR5ken)
