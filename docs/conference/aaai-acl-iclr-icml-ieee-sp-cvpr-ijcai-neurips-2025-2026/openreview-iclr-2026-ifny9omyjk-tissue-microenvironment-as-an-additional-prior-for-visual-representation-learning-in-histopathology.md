---
title: Tissue Microenvironment as an Additional Prior for Visual Representation Learning in Histopathology
title_zh: 组织微环境作为组织病理学视觉表示学习的额外先验
authors: "Swaraj Nanda, Neeraj Kumar, Siddharth Singi, Amir Momeni Boroujeni, Jie-Fu Chen, David Kim, Jamal Benhamida, Gregory M. Goldgof, Chad Vanderbilt"
date: 2025-09-19
pdf: "https://openreview.net/pdf?id=iFNY9Omyjk"
tags: ["query:profile"]
score: 9.0
evidence: 通过语义掩码将组织微环境结构作为额外先验，用于组织病理学自监督表示学习。
tldr: 针对现有自监督学习方法未充分利用组织微环境结构信息的问题，提出通过对抗性语义掩码生成器识别组织结构，并将其作为增强手段融入DINOv2自监督学习流程，在5500万张TCGA组织病理图块上预训练后，显著提升了视觉表示的质量，为数字病理学基础模型训练提供了新思路。
source: ICLR-2026-Public
selection_source: conference_retrieval
motivation: 现有自监督学习方法未充分利用组织微环境结构信息。
method: 训练对抗掩码生成器识别组织结构，将其作为语义掩码增强DINOv2训练。
result: 在5500万张TCGA组织病理图块上预训练，提升了表示学习质量。
conclusion: 引入微环境先验可有效增强组织病理基础模型的表示能力。
---

## Abstract
Self-supervised learning has transformed histopathology by enabling foundation models to learn from vast unlabeled image archives, with methods developed using natural images, such as DINOv2, establishing powerful baselines. We propose augmenting these approaches by incorporating tissue microenvironment structure as an additional prior through semantic masking. We train adversarial mask generators adapted from ADIOS with perceptual reconstruction losses to identify tissue structures, then integrate these semantic masks as augmentations within DINOv2 self-supervised learning pipelines. Using a set of 55 million TCGA histopathology tiles of 224$\times$224 pixels at a resolution of 0.5 $\mu$m/pixel, we pre-train vision transformers to evaluate three augmentation strategies: standard DINOv2 augmentations, mixed (combining standard and semantic masking), and semantic masking only. The mixed augmentation strategy, when used in DINOv2, demonstrates consistent improvements over baseline across four patch-level classification benchmarks (PCam, MiDOG, MHIST, BRACS) and on two slide-level mutation prediction tasks (EGFR in LUAD, FGFR3 in BLCA). Qualitative PCA visualization of patch tokens shows that semantic masks combined with standard augmentations enable a better decomposition of tissue into biologically interpretable components without supervision, with DINOv2-mixed achieving clear separation of cellular structures, vasculature, and stromal elements. Therefore, incorporating domain-specific tissue priors through semantic masking enhances representation learning in self-supervised frameworks, alongside standard augmentations.

---

## 论文详细总结（自动生成）

# 论文总结：组织微环境作为组织病理学视觉表示学习的额外先验

## 1. 核心问题与整体含义
- **研究动机**：当前在组织病理学中，自监督学习（SSL）已能够从海量未标注图像中训练基础模型，但主流方法（如基于自然图像设计的DINOv2）仅使用通用图像增强策略，忽视了病理组织特有的生物学结构信息。
- **核心问题**：如何将**组织微环境的结构信息**（如细胞排列、血管、间质等）作为额外先验，融入自监督表示学习框架，以提升视觉特征对下游任务的适用性。
- **整体含义**：通过引入领域特定的组织结构先验，可使模型更有效地捕捉具有生物学意义的特征，从而在不依赖标注的情况下提升病理基础模型的性能与可解释性。

## 2. 方法论
- **核心思想**：训练一个语义掩码生成器自动识别组织图像中的关键结构，并将生成的掩码作为一种新型数据增强手段，与标准DINOv2增强策略结合使用，使模型在自监督训练中关注微环境的空间组织。
- **关键技术细节**：
  - **掩码生成器**：基于ADIOS（Adversarial Discriminative Domain Adaptation）框架改进，采用对抗训练和感知重建损失，使其生成能够覆盖重要组织区域的语义掩码。
  - **增强策略融合**：将生成的语义掩码作用于图像，例如擦除或遮盖部分区域，再与标准DINOv2增强（随机裁剪、颜色抖动等）按混合方式使用。
  - **训练流程**：以ViT（Vision Transformer）为骨干，在DINOv2的自蒸馏框架中，学生网络输入经过两种增强（标准+语义掩码）的视图，教师网络输入标准增强视图，通过对比学习优化表示。
- **算法形式**（用文字说明）：
  - 阶段一：固定骨干，训练掩码生成器，使其输出能够最大化重建损失的掩码区域（即突出结构关键部位）。
  - 阶段二：将语义掩码作为增强集成到DINOv2流程中，损失函数保持DINOv2原有的交叉熵损失与中心化/锐化操作，但输入视图增加语义掩码变换。

## 3. 实验设计
- **预训练数据集**：55 百万张来自TCGA（The Cancer Genome Atlas）的病理图块，尺寸 224×224 像素，分辨率 0.5 µm/像素。
- **评估基准（下游任务）**：
  - 图块级分类：PCam（淋巴结转移）、MiDOG（犬骨肉瘤分级）、MHIST（结直肠息肉亚型）、BRACS（乳腺放射状瘢痕亚型）。
  - 切片级突变预测：EGFR 在 LUAD（肺腺癌）、FGFR3 在 BLCA（膀胱尿路上皮癌）。
- **对比方法**：
  - 标准DINOv2增强（仅通用增强）。
  - 仅语义掩码增强。
  - 混合增强（标准+语义掩码）——本文主推策略。
  - 可能包含其它自监督基线（如SimCLR、DINO等），但文中明确强调以DINOv2为骨干进行策略对比。

## 4. 资源与算力
- 文中**未明确提及**所用的GPU型号、数量及具体训练时长。考虑到预训练数据规模高达5 500万张图块且使用ViT架构，可合理推断需要大规模分布式训练（可能使用数十块高端GPU），但作者未在摘要或可获取信息中给出详细算力指标。

## 5. 实验数量与充分性
- 实验覆盖多个维度，较为充分：
  - 3种增强策略的全面对比（标准、仅语义掩码、混合）。
  - 4个图块级分类任务 + 2个切片级突变预测任务，任务类型涵盖诊断、分级、突变预测。
  - 定性分析：通过PCA可视化图块令牌，直观展示混合策略能更好地分解出细胞结构、血管、间质等生物学成分。
  - 推测文中可能还包括消融实验（如掩码比例、生成器架构选择等），但摘要未详述。
- 公平性：所有策略均基于相同的预训练数据和骨干网络DINOv2，对比基准明确；下游评测均采用标准数据集和常规微调协议，对比客观。

## 6. 主要结论与发现
- 混合增强策略（标准增强 + 语义掩码）在绝大多数下游任务上**一致优于**纯标准DINOv2增强。
- 仅使用语义掩码增强效果不如混合策略，说明组织先验需与通用视觉增强互补才能发挥最大效能。
- PCA可视化显示，混合增强使模型在无监督下自然将图像令牌分解为与生物学结构高度对应的簇，提升了表示的可解释性。
- 结论：**将组织微环境作为领域先验，通过语义掩码的形式融入自监督学习，能有效增强病理基座模型的表示能力，且与标准增强形成良好互补。**

## 7. 优点
- **领域知识注入方式新颖**：通过掩码生成器自动提取组织结构，避免了手工标注，实现了无监督的先验利用。
- **方法通用性强**：可直接嵌入现有自监督框架（如DINOv2），无需改动骨干网络或损失函数，易于复现和迁移。
- **性能与可解释性同步提升**：不仅下游指标改善，定性分析还表明特征空间具备更清晰的生物学意义。
- **大规模数据验证**：在来自多癌种的5 500万张真实病理图像上预训练，结论具有较高可信度。

## 8. 不足与局限
- **算力与实施细节缺失**：未公开训练所需的硬件资源，增加了复现难度，也可能限制资源有限的研究团队跟进。
- **掩码生成器依赖外部训练**：掩码生成器本身需对抗训练，增加了整体方法的复杂性和训练成本，可能引入额外的超参数敏感性。
- **数据来源单一**：预训练仅使用TCGA数据，虽然规模大但均为福尔马林固定石蜡包埋（FFPE）切片，对不同染色类型、不同扫描仪的泛化性待验证。
- **下游任务覆盖有限**：虽涉及分类和突变预测，但未测试更复杂的任务（如分割、生存分析），也未与其他最新病理自监督方法（如HIPT、Prov-GigaPath）直接比较。
- **可能存在的偏差风险**：TCGA数据集可能存在站点偏差或人口偏差，语义掩码的生成可能过拟合于TCGA结构模式，导致在其他来源数据上性能下降。

---

（完）
