---
title: A Decade of Deep Learning-based Biomedical Image Segmentation
title_zh: 基于深度学习的生物医学图像分割十年回顾
authors: "Yu, S., Wang, H., Wang, N., Chen, S., Wu, J., Yuan, Z., Qi, T., Zhou, Z., Xia, F., Ma, J., Zhou, Y."
date: 2026-04-30
pdf: "https://www.biorxiv.org/content/10.64898/2026.04.27.721127v1.full.pdf"
tags: ["query:cellrep"]
score: 6.0
evidence: 深度学习在生物医学图像分割（包括病理区域）中的应用综述
tldr: 本文回顾了过去十年深度学习驱动的生物医学影像分割领域，从专用模型到通用基础模型的演进过程，分析了由局部到全局建模的技术转变，提出首个提示式分割方法的系统分类，并探讨数据集、评估方法及临床应用前景。
source: biorxiv
selection_source: fresh_fetch
motivation: 生物医学影像分割对疾病诊断和定量分析至关重要，但现有模型受限于局部判别学习能力，迫切需要更通用的模型框架。
method: 论文回顾了十年来深度学习在生物医学影像分割的演变，提出首个可提示分割方法的系统分类体系，并评述相关数据集与评估协议。
result: 研究总结了从专用模型到基于Transformer与生成预训练的通用基础模型的转变，并展示了其在不同医学领域的适应性提升。
conclusion: 未来生物医学分割的发展需解决可信度与临床集成问题，以实现通用生物医学智能模型的潜力。
---

## 摘要
生物医学图像分割是计算生物医学中的一个基本问题，旨在精确描绘生物医学图像中的解剖和生物结构、组织类型或病理区域。准确的分割对于在广泛的生物和医学应用中实现图像解释、决策制定和定量分析至关重要。在过去的十年中，该领域经历了深刻的范式转变，从任务特定的专业模型发展到通用的基础模型。本综述对这一演变进行了深入分析，追溯了局部判别学习的局限性如何推动了向基于Transformer的全局建模以及大规模生成式预训练的转变。为帮助读者在多样化的交互范式中导航，我们引入了第一个系统化的可提示（promptable）生物医学图像分割分类体系，将现有方法划分为六种不同类型，使用户能够根据视觉示例直观选择合适的提示策略，并快速定位相关文献（提示类型可视化）。除模型架构外，我们还讨论了数据集开发、评估协议及跨放射学、病理学和生物学的特定应用适配等方面的并行进展。将这些强大的基础模型与严谨的领域特定适配相结合，具有显著提升患者疗效和医疗效率的潜力。最后，我们强调了信任度和临床集成方面的关键挑战，必须克服这些问题，才能充分实现下一代生物与医学通用模型的潜力。

## Abstract
Biomedical image segmentation is a fundamental problem in computational biomedicine that aims to precisely delineate anatomical and biological structures, tissue types, or pathological regions in biomedical images. Accurate segmentation is essential for interpretation, decision-making, and quantitative analysis across a wide range of biological and medical applications. Over the past decade, the field has undergone a profound paradigm shift, evolving from task-specific specialist models to universal foundation models. This review provides an in-depth analysis of the evolution, tracing how the limitations of local discriminative learning drove the transition toward transformer-based global modeling, and large-scale generative pre-training. To help navigate the diverse landscape of interaction paradigms, we introduce the first systematic taxonomy of promptable biomedical image segmentation, categorizing existing methods into six distinct types, enabling users to intuitively select appropriate prompting strategies based on visual demonstrations and quickly pinpoint relevant literature (Prompt Type Visualization). Beyond model architectures, we discuss parallel advancements in dataset development, evaluation protocols, and application-specific adaptations across radiology, pathology, and biology. Integrating these powerful foundation models with rigorous domain-specific adaptation has great potential to improve patient outcomes and healthcare efficiency. Finally, we highlight key challenges in trustworthiness and clinical integration that must be overcome to realize the potential of the next generation of biological and medical generalists.