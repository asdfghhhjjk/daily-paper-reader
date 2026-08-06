---
title: Transitive Representation Learning Enhances Histopathology Annotation
title_zh: 传递表示学习增强组织病理学标注
authors: "Moritz Schaefer, Zoe Piran, Nils Philipp Walter, Animesh Awasthi, Christoph Bock, Jure Leskovec, Zinaida Good"
date: 2026-04-30
pdf: "https://openreview.net/pdf/5633e8d66627583698d6fffa502376d7f9347d92.pdf"
tags: ["query:cellseg"]
score: 7.0
evidence: 通过基因表达和文本的传递学习实现组织病理图像的零样本细胞类型标注
tldr: 针对组织病理学标注粗粒度缺失细胞身份的问题，提出SpatialWhisperer三模态对比学习框架，利用基因表达作为纽带连接图像与文本描述，实现零样本细胞类型标注。在多个数据集上验证了标注准确性，为数字病理细胞分析提供新工具。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 现有病理标注粒度粗，无法识别细胞类型，限制下游分析。
method: 设计三模态对比学习模型，联合图像、基因表达和自然语言描述。
result: 在空间转录组和单细胞数据集上，零样本细胞标注达到高准确率。
conclusion: 传递学习策略可有效弥合图像与细粒度标注之间的鸿沟。
---

## Abstract
The characterization of histopathology with AI promises to assist clinical decision-making, but it is currently limited due to coarse-grained annotations that miss cellular identities. To overcome this gap, we bridge histopathological images, gene expression profiles, and natural-language descriptions using *SpatialWhisperer*, a trimodal contrastive learning model. Our training integrates community-scale datasets comprising spatially resolved gene expression profiles paired with histopathology images, as well as single-cell gene expression profiles with detailed annotations. The shared gene expression modality implies a transitive relationship between images and textual annotations, which our method leverages to enable accurate zero-shot cell type annotation directly from H&E images. *SpatialWhisperer* outperforms published baselines, achieving relative AUROC gains of up to 15.9% across three benchmarks spanning 19 tissues and 20 cell types. When training with data from all three modality pairs, we observe performance gains in low-data regimes. We formalize our approach and present a sufficient condition under which this transitive alignment is induced. Our work establishes *transitive representation learning* for fine-grained interpretation of histopathology images.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
通过基因表达和文本的传递学习实现组织病理图像的零样本细胞类型标注。

### 2. 核心内容
针对组织病理学标注粗粒度缺失细胞身份的问题，提出SpatialWhisperer三模态对比学习框架，利用基因表达作为纽带连接图像与文本描述，实现零样本细胞类型标注。在多个数据集上验证了标注准确性，为数字病理细胞分析提供新工具。

### 3. 对应检索需求
Papers central to 充分利用HE切片中细胞分类和分割结果中的信息来完成下游任务, especially work that connects or combines: classifying cells in hematoxylin and eosin stained images; classification algorithms for cell nuclei; tumor microenvironment analysis from cell segmentation; spatial distribution analysis of cells; digital pathology image analysis; extracting features from cell segmentations; How to use cell segmentation and classification results for cancer prognosis modeling?; Integrating cell level information from H&E slides into downstream machine learning tasks.; Spatial analysis of tumor microenvironment using cell segmentation data..

### 4. 来源与原文
- Source：ICML-2026-Accepted
- OpenReview：[https://openreview.net/forum?id=Ze7U293Zw4](https://openreview.net/forum?id=Ze7U293Zw4)
