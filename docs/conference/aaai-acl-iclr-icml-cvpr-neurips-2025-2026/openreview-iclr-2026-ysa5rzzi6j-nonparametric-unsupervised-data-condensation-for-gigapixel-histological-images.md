---
title: Nonparametric Unsupervised Data Condensation for Gigapixel Histological Images
title_zh: 面向千兆像素组织学图像的非参数无监督数据浓缩
authors: "Duong M. Nguyen, Trong Nghia Hoang, Thanh Trung Huynh, Phi Le Nguyen, Minh N. Do"
date: 2025-09-20
pdf: "https://openreview.net/pdf?id=Ysa5RZZi6J"
tags: ["query:immuno-topo"]
score: 5.0
evidence: 将全切片图像浓缩为原型，提升数字病理深度学习的效率
tldr: 全切片组织图像（WSI）尺寸巨大，达到数GB，直接用于标准深度学习管线不可行。现有方法通过提取固定数量的特征原型来浓缩WSI，但忽略了不同切片间复杂性和多样性的差异，导致关键信息损失。NICER提出非参数概率数据浓缩框架，将每个WSI自适应分解为特征模式与概念原型，既能捕获异质性又能保持紧致。实验证明该框架能大幅减少训练成本而几乎不牺牲性能，为千兆像素级病理图像的高效深度分析提供了实用解决方案，尤其适用于需要处理大量切片的计算病理学下游任务。
source: ICLR-2026-Public
selection_source: conference_retrieval
motivation: 现有数据浓缩方法使用固定数量原型，未能适应WSI的复杂性和多样性，导致信息丢失。
method: 提出概率数据浓缩框架，非参数地自适应构建特征原型以表示全切片图像。
result: 在保留关键信息的同时大幅减少数据量，实现高效模型训练。
conclusion: 自适应原型浓缩策略能更好地平衡WSI信息的完整性与计算效率。
---

## Abstract
Histological whole-slide images (WSIs) are central to computational pathology but are extremely large, often several gigabytes, making them infeasible for direct use in standard vision pipelines. Prior approaches reduce training cost by condensing WSIs into a fixed number of representative features (prototypes), but this approach overlooks the varying complexity and diversity of WSIs, leading to loss of critical information. To this end, we propose **NICER**, a probabilistic data condensation framework that decomposes each WSI into feature patterns to capture heterogeneity and concept prototypes to ensure compactness. By reformulating prototype construction as a nonparametric condensation problem, NICER adapts the number of prototypes to slide complexity while preserving relevant information. Experiments on four histological datasets show that NICER outperforms prior methods, yielding superior efficiency trade-offs, setting a new paradigm for histological representation learning.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
将全切片图像浓缩为原型，提升数字病理深度学习的效率。

### 2. 核心内容
全切片组织图像（WSI）尺寸巨大，达到数GB，直接用于标准深度学习管线不可行。现有方法通过提取固定数量的特征原型来浓缩WSI，但忽略了不同切片间复杂性和多样性的差异，导致关键信息损失。NICER提出非参数概率数据浓缩框架，将每个WSI自适应分解为特征模式与概念原型，既能捕获异质性又能保持紧致。实验证明该框架能大幅减少训练成本而几乎不牺牲性能，为千兆像素级病理图像的高效深度分析提供了实用解决方案，尤其适用于需要处理大量切片的计算病理学下游任务。

### 3. 对应检索需求
digital pathology image analysis using deep learning。

### 4. 来源与原文
- Source：ICLR-2026-Public
- OpenReview：[https://openreview.net/forum?id=Ysa5RZZi6J](https://openreview.net/forum?id=Ysa5RZZi6J)
