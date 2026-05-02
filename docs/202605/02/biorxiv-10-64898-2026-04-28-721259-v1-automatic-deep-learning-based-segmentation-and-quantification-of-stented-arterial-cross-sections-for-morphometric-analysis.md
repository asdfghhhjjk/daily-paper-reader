---
title: Automatic deep learning-based segmentation and quantification of stented arterial cross-sections for morphometric analysis
authors: "Kraftberger, M., Spirgath, K., Haase, T., Bandelin, R., Meyer, T., Jaitner, N., Tzschätzsch, H."
date: 2026-04-30
pdf: "https://www.biorxiv.org/content/10.64898/2026.04.28.721259v1.full.pdf"
tags: ["query:pathseg"]
score: 8.0
evidence: 组织学动脉横截面的自动分割与定量分析
tldr: 开发了一个自动深度学习框架，用于组织学动脉切片的形态计量分析。
source: biorxiv
selection_source: fresh_fetch
motivation: 组织学动脉横截面的自动分割与定量分析。
method: 方法与实现细节请参考摘要与正文。
result: 结果与对比结论请参考摘要与正文。
conclusion: 总体而言，该工作在所述任务上展示了有效性，并提供了可复用的思路或工具。
---

## Abstract
Arterial vascular diseases, such as atherosclerosis, are among the most serious global health threats. In preclinical studies, morphometric analysis of histological arterial cross-sections is considered the gold standard for assessing vascular remodeling and the effectiveness of therapeutic interventions. However, morphometric analysis is usually performed manually, which is time-consuming, subjective, and requires significant user interaction. This paper presents a fully automated, operator-independent framework for the precise morphometric analysis of stented arterial cross-sections, extending the previously developed qHisto (quantitative histology) framework for the quantification of various histological components. A neural network for the segmentation of arterial structures was trained and evaluated using 819 cross-sections. In addition, a quantitative analysis of vascular morphology, fibrin area, and lumen asymmetry was performed using 72 cross-sections from coated and uncoated balloons. The model achieved high segmentation accuracy with a median Dice similarity coefficient of 0.892-0.996. Compared to manual evaluation, the system reduces analysis time by 90%, enabling efficient processing of large datasets. Furthermore, morphometric analysis with qHisto showed significant differences between coated and uncoated balloons, e.g. regarding lumen area (AUC = 0.86) and fibrin ratio (AUC = 0.94). Our developed framework enables fully automated, comprehensive and standardized analysis of histological arterial cross-sections. This helps to reduce time-consuming, repetitive manual assessments and thus facilitates research of disease mechanisms and treatment effects in preclinical studies.