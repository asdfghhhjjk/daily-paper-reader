---
title: "H2O: A Foundation Model Bridging Histopathology to Spatial Multi-Omics Profiling"
title_zh: H2O：连接病理组织学与空间多组学表征的基础模型
authors: "Gu, Y., Wu, Z., Yan, R., Wang, Z., Li, Y., Lin, S., Cui, Y., Lai, H., Luo, X., Zhou, S. K., Yuan, Z., Yao, J."
date: 2026-04-24
pdf: "https://www.biorxiv.org/content/10.64898/2026.04.21.717342v1.full.pdf"
tags: ["query:pathseg"]
score: 9.5
evidence: "连接H&E组织病理学与空间多组学的视觉Transformer基础模型。"
tldr: "H2O是一个通过跨模态学习从常规H&E图像推断空间转录组学的病理基础模型。"
source: biorxiv
selection_source: fresh_fetch
motivation: "连接H&E组织病理学与空间多组学的视觉Transformer基础模型。"
method: 方法与实现细节请参考摘要与正文。
result: 结果与对比结论请参考摘要与正文。
conclusion: 总体而言，该工作在所述任务上展示了有效性，并提供了可复用的思路或工具。
---

## 摘要
空间组学技术已经彻底革新了组织的分子分析，但仍受到高成本和有限可扩展性的制约。虽然苏木精-伊红（H&E）染色广泛应用，但缺乏分子特异性。在此，我们提出 H2O（Histopathology to Omics），一个通用的人工智能框架，用于桥接病理组织学与空间多组学之间的模态差异，实现从常规 H&E 图像直接推断空间转录组学（ST）和蛋白质组学（SP）图谱。H2O 通过对比学习整合视觉 Transformer（ViT）与大型语言模型（LLM），以对齐组织形态学特征与分子层面的语义知识。这种跨模态方法使模型能够将空间表达特征融入组织形态识别中，从而有效解码组织形态背后的分子异质性。H2O 在涵盖 25 个器官与癌症类型、共 130 万对 H&E–空间图像补丁的泛组织数据集上进行训练，能够以高度一致性预测来源于组织学的空间组学表达，并在三个癌症基准数据集上持续超越当前最先进模型。值得注意的是，H2O 可以直接从 H&E 图像恢复 MIF–CD74/CD44 信号通路，展示了其在无分子测序的情况下推断具有生物学意义的细胞间通信的能力。在三个额外的公共队列（涵盖胎儿及儿童胸腺组织、人类转移性淋巴结及乳腺癌）上的应用中，H2O 跨越人类发育、三维空间框架及整合多组学研究场景，产生与生物学一致的洞见，展现出卓越的准确性、稳健性与广泛的通用性。H2O 通过计算生成转录组与蛋白质组图谱，将常规病理组织学转化为一个具备空间分辨率的多组学分析门户，从而增强组织表型解析，并促进具有可扩展性的整合组织图谱构建。

## Abstract
Spatial omics technologies have revolutionized the molecular profiling of tissues but remain constrained by high costs and limited scalability. While hematoxylin and eosin (H&E) staining is ubiquitous, it lacks molecular specificity. Here, we present H2O (Histopathology to Omics), a generalist AI framework that bridges the modality gap between histopathology and spatial multi-omics, enabling the direct inference of spatial transcriptomics (ST) and proteomics (SP) landscapes from routine H&E images. H2O integrates Vision Transformers (ViT) with Large Language Models (LLM) via contrastive learning to align histological morphology with semantic molecular knowledge. This cross-modal approach allows the model to incorporate spatial expression profiles into histological pattern recognition, effectively decoding the molecular heterogeneity underlying tissue morphology. Trained on a pan-tissue dataset of 1.3 million paired H&E-spatial patches across 25 organs and cancer types, H2O predicts spatial omics expression from histology with high concordance to sequenced measurements and consistently outperforms state-of-the-art models across three cancer benchmarks. Notably, H2O recovers the MIF-CD74/CD44 signaling axis directly from H&E images, highlighting its capacity to infer biologically meaningful cell-cell communication without molecular profiling. Applying on three additional public cohorts covering fetal and paediatric thymus tissues, human metastatic lymph node, and breast cancer, encompassing human development, 3D spatial frameworks, and integrative multi-omics, H2O yields biologically concordant insights, demonstrating superior accuracy, robustness, and generalizability across real-world applications in diverse scenarios. H2O converts routine histopathology into a portal for spatially resolved multi-omics profiling by computationally generating transcriptomic and proteomic landscapes, thereby enhancing tissue phenotyping and enabling scalable, integrative tissue-atlas construction.