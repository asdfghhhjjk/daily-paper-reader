---
title: A Decade of Deep Learning-based Biomedical Image Segmentation
authors: "Yu, S., Wang, H., Wang, N., Chen, S., Wu, J., Yuan, Z., Qi, T., Zhou, Z., Xia, F., Ma, J., Zhou, Y."
date: 2026-04-30
pdf: "https://www.biorxiv.org/content/10.64898/2026.04.27.721127v1.full.pdf"
tags: ["query:pathseg"]
score: 8.0
evidence: 生物医学图像分割从任务特定模型到基础模型的综述
tldr: 生物医学分割深度学习十年综述，涵盖Transformer和基础模型。
source: biorxiv
selection_source: fresh_fetch
motivation: 生物医学图像分割从任务特定模型到基础模型的综述。
method: 方法与实现细节请参考摘要与正文。
result: 结果与对比结论请参考摘要与正文。
conclusion: 总体而言，该工作在所述任务上展示了有效性，并提供了可复用的思路或工具。
---

## Abstract
Biomedical image segmentation is a fundamental problem in computational biomedicine that aims to precisely delineate anatomical and biological structures, tissue types, or pathological regions in biomedical images. Accurate segmentation is essential for interpretation, decision-making, and quantitative analysis across a wide range of biological and medical applications. Over the past decade, the field has undergone a profound paradigm shift, evolving from task-specific specialist models to universal foundation models. This review provides an in-depth analysis of the evolution, tracing how the limitations of local discriminative learning drove the transition toward transformer-based global modeling, and large-scale generative pre-training. To help navigate the diverse landscape of interaction paradigms, we introduce the first systematic taxonomy of promptable biomedical image segmentation, categorizing existing methods into six distinct types, enabling users to intuitively select appropriate prompting strategies based on visual demonstrations and quickly pinpoint relevant literature (\href{https://suhaoyu1020.github.io/MedicalSegmentation-PromptType-Website/}{Prompt Type Visualization}). Beyond model architectures, we discuss parallel advancements in dataset development, evaluation protocols, and application-specific adaptations across radiology, pathology, and biology. Integrating these powerful foundation models with rigorous domain-specific adaptation has great potential to improve patient outcomes and healthcare efficiency. Finally, we highlight key challenges in trustworthiness and clinical integration that must be overcome to realize the potential of the next generation of biological and medical generalists.