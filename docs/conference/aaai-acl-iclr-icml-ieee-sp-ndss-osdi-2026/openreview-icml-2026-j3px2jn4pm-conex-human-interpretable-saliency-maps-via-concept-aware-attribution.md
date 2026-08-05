---
title: "ConEx: Human-Interpretable Saliency Maps via Concept-Aware Attribution"
title_zh: ConEx：基于概念感知归因的人类可解释显著性图
authors: "Yehonatan Elisha, Oren Barkan, Ziv Weiss Haddad, Noam Koenigstein"
date: 2026-04-30
pdf: "https://openreview.net/pdf/83a5d0003e201e3aa951ea8f7d9701597f5f7ee6.pdf"
tags: ["query:path-xai-sel"]
score: 6.0
evidence: 基于概念的显著性图允许根据可解释的概念选择显著区域
tldr: 提出ConEx框架，自动发现类别特定概念并生成概念感知的显著性图，揭示每个概念在图像中的位置，为基于可解释概念的显著区域选择提供方法，尽管未在病理图像上验证，但具备迁移潜力。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 现有像素级显著性解释缺乏与语义概念的关联，限制了解释的可理解性。
method: 自动发现类别概念，学习概念激活向量，并利用掩码机制生成忠实的概念感知显著性图。
result: 在多个图像分类数据集上，ConEx生成的解释更忠实于模型，且概念纯度更高。
conclusion: 概念驱动的显著性图为模型可解释性提供了新维度，可启发组织病理图像中的区域选择。
---

## Abstract
Many visual explanation methods in computer vision highlight pixel importance but struggle to link these low-level cues to semantically meaningful concepts, limiting their interpretability and trustworthiness. We introduce Concept-based Explanations (ConEx), a novel framework that bridges saliency visualization with concept-based reasoning to provide both faithfulness and interpretability. ConEx automatically discovers class-specific concepts and represents them through concept activation vectors (CAVs), learned without manual supervision using an architecture-specific masking mechanism that reduces noise introduced by the segmentation masks to enhance concept purity. ConEx generates faithful saliency maps that reveal where each concept appears in the image and how it contributes to the prediction. To evaluate the reliability of these learned concepts, we propose two complementary metrics, Vector-Concept Match (VCM) and Concept-Class Match (CCM), that quantify concept alignment and enable direct comparison with existing methods. Extensive experiments across diverse settings demonstrate that ConEx achieves state-of-the-art performance on faithfulness, segmentation, and concept-quality benchmarks. Overall, ConEx advances the field toward truly interpretable and concept-grounded explanations in vision models.

---

## 论文详细总结（自动生成）

由于提供的 PDF 内容仅包含 OpenReview 的验证页面，未能获取论文正文。以下总结基于论文元数据（标题、摘要、标签等）及潜在的应用场景进行合理推断。部分细节（如具体数据集、算力等）因正文缺失无法给出，文中会明确说明。

## 1. 论文的核心问题与整体含义
- **核心问题**：当前计算机视觉中的视觉解释方法多聚焦于像素级重要性（如显著图），但缺乏将低层像素线索与高层语义概念（如“条纹”“人脸”）相关联的能力，导致解释可理解性差，难以建立用户信任。
- **整体含义**：提出 **ConEx (Concept-based Explanations)** 框架，旨在将基于概念的推理与显著图可视化相融合，既保证解释对模型的忠实性，又提供人类可解释的概念级解释，从而架起像素归因与语义概念之间的桥梁。

## 2. 论文提出的方法论
- **自动概念发现与表示**：ConEx 自动发现每个类别特定的语义概念，并用 **概念激活向量（CAVs）** 来表示这些概念，整个过程无需人工标注监督。
- **掩码机制提升概念纯度**：设计了一种特定于模型架构的掩码机制，用于降低由分割掩码引入的噪声，从而增强所发现概念的纯度（即概念与特定视觉模式的对齐度）。
- **概念感知显著图生成**：对输入图像，ConEx 生成忠实于模型的显著图，不仅能显示哪些区域重要，还能揭示 **每个概念出现在图像中的位置** 以及 **该概念如何影响最终类别预测**。
- **评估指标**：为量化习得概念的可靠性，提出了两个互补指标：
  - **Vector-Concept Match (VCM)**：衡量概念激活向量与实际视觉概念的匹配程度。
  - **Concept-Class Match (CCM)**：衡量概念与特定类别的关联紧密度。
  这些指标可实现与现有概念解释方法的直接比较。

## 3. 实验设计
- **数据集/场景**：摘要中提到“在多种设置下进行广泛实验”，但未列出具体数据集名称。根据任务推测，可能包括标准图像分类基准（如 ImageNet、CUB 等常用于概念分析的数据集）。
- **基准与方法对比**：
  - 基准类型：忠实性（faithfulness）、分割质量（segmentation）和概念质量（concept-quality）基准。
  - 对比方法：与现有基于显著图或概念的解释方法进行对比（具体方法名未知）。
- **评估维度**：利用提出的 VCM 和 CCM 指标进行概念对齐评估，并与基线比较。

## 4. 资源与算力
- 论文摘要及元数据中 **未提及任何算力信息**（如 GPU 型号、数量、训练时长等）。正文缺失，无法确认。

## 5. 实验数量与充分性
- **实验数量**：摘要仅用“extensive experiments across diverse settings”概括，无法得知确切组数（如消融实验、不同数据集上的对比实验数量）。
- **充分性与客观性**：从摘要表述“achieves state-of-the-art performance on faithfulness, segmentation, and concept-quality benchmarks”推断，实验覆盖了多个主流基准，并引入了公平的评估指标。但缺少正文细节，无法评价实验是否完全客观或存在潜在偏差风险。

## 6. 论文的主要结论与发现
- ConEx 在忠实性、分割质量和概念质量等多个基准上均达到最先进水平。
- 概念驱动的显著性图为模型可解释性提供了新维度：不仅能回答“模型关注哪里”，还能回答“关注了哪些概念”。
- 提出的 VCM 和 CCM 指标能有效量化概念的可信度，为后续概念解释研究提供评估工具。

## 7. 优点（亮点）
- **无需人工监督**：概念发现和概念激活向量学习完全自动化，避免了昂贵的人工概念标注。
- **掩码去噪设计**：通过架构特异性掩码机制减少分割噪声，提升了概念纯度，这是对现有概念方法的改进。
- **解释的多维度性**：同时提供像素级重要性和概念级语义，显著增强了可解释性和可信任度。
- **可量化评估**：自建的对齐指标使概念质量评估有了可比性，有助于推动领域标准化。

## 8. 不足与局限
- **应用领域局限**：根据元数据中的证据（“尽管未在病理图像上验证，但具备迁移潜力”），ConEx 目前仅在自然图像分类上验证，尚未在医学影像（如组织病理图像）等高风险领域测试，其实用性和泛化能力待考察。
- **细节不可知**：由于正文缺失，无法分析掩码机制的适用范围、对分割方法质量的依赖、计算开销等潜在限制。
- **可能的概念覆盖偏差**：自动发现的概念可能偏好视觉显著的模式，忽略对分类同样重要但不易分割的弱概念。

（完）
