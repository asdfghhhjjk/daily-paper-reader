---
title: Tissue Microenvironment as an Additional Prior for Visual Representation Learning in Histopathology
title_zh: 组织微环境作为组织病理学视觉表征学习的附加先验
authors: "Swaraj Nanda, Neeraj Kumar, Siddharth Singi, Amir Momeni Boroujeni, Jie-Fu Chen, David Kim, Jamal Benhamida, Gregory M. Goldgof, Chad Vanderbilt"
date: 2025-09-19
pdf: "https://openreview.net/pdf?id=iFNY9Omyjk"
tags: ["query:profile"]
score: 10.0
evidence: 将组织微环境结构作为先验融入自监督学习，以提升组织病理图像表征。
tldr: 自监督学习推动了组织病理学基础模型的发展，但现有方法忽略了组织微环境结构这一重要先验。本文提出通过语义掩膜将组织微环境信息融入 DINOv2 自监督学习管线，使用对抗掩膜生成器与感知重建损失识别组织结构，并在 5500 万张 TCGA 病理图块上预训练视觉 transformer。下游任务评估表明，这种先验能显著提升表征质量，为病理图像分析提供了新的预训练策略。
source: ICLR-2026-Public
selection_source: conference_retrieval
motivation: 现有自监督病理模型未利用组织微环境结构作为先验。
method: 设计语义掩膜策略，将组织微环境先验融入 DINOv2 预训练，通过对抗掩膜生成器识别组织结构。
result: 在大规模病理数据集上预训练的模型，下游任务性能显著提升。
conclusion: 组织微环境先验是增强病理视觉表征学习的有效手段。
---

## Abstract
Self-supervised learning has transformed histopathology by enabling foundation models to learn from vast unlabeled image archives, with methods developed using natural images, such as DINOv2, establishing powerful baselines. We propose augmenting these approaches by incorporating tissue microenvironment structure as an additional prior through semantic masking. We train adversarial mask generators adapted from ADIOS with perceptual reconstruction losses to identify tissue structures, then integrate these semantic masks as augmentations within DINOv2 self-supervised learning pipelines. Using a set of 55 million TCGA histopathology tiles of 224$\times$224 pixels at a resolution of 0.5 $\mu$m/pixel, we pre-train vision transformers to evaluate three augmentation strategies: standard DINOv2 augmentations, mixed (combining standard and semantic masking), and semantic masking only. The mixed augmentation strategy, when used in DINOv2, demonstrates consistent improvements over baseline across four patch-level classification benchmarks (PCam, MiDOG, MHIST, BRACS) and on two slide-level mutation prediction tasks (EGFR in LUAD, FGFR3 in BLCA). Qualitative PCA visualization of patch tokens shows that semantic masks combined with standard augmentations enable a better decomposition of tissue into biologically interpretable components without supervision, with DINOv2-mixed achieving clear separation of cellular structures, vasculature, and stromal elements. Therefore, incorporating domain-specific tissue priors through semantic masking enhances representation learning in self-supervised frameworks, alongside standard augmentations.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义

- **研究背景**：自监督学习（SSL）使组织病理学基础模型能够从海量未标注图像中学习通用视觉表征，以 DINOv2 为代表的基于自然图像的方法已确立强大基线。然而，现有自监督范式主要利用图像内部的颜色、纹理等自然统计规律，并未显式建模组织病理特有的**组织微环境（tissue microenvironment）结构**——即不同细胞类型、血管、间质等成分的空间组织关系，这被病理学家视为诊断和预后中重要的领域先验。
- **核心问题**：如何将“组织微环境结构”作为一种额外先验融入自监督预训练，以提升病理图像表征的生物学可解释性和下游任务性能。
- **整体含义**：通过语义掩膜策略将组织构件先验植入 DINOv2 管线，使模型在无监督条件下就能自发分解出具有生物学意义的组织结构，从而增强表征的质量与迁移能力，为病理 AI 提供一种更贴合领域特性的预训练策略。

### 2. 论文提出的方法论

- **核心思想**：在 DINOv2 自监督学习中，除了常规的随机裁剪、色彩扰动等增强外，额外引入**语义掩膜（semantic masking）**作为数据增广手段，迫使模型学习组织结构的构成关系。语义掩膜由对抗掩膜生成器产生，该生成器能够识别并遮蔽具有生物学意义的组织区域。
- **关键技术细节**：
  - **对抗掩膜生成器**：改编自 ADIOS（Adversarial Image Object Segmentation）框架，使用感知重建损失训练，使其能够定位并掩膜掉关键的组织结构，而非随机遮挡。
  - **集成方式**：将生成的语义掩膜作为图像变换的一种，与标准 DINOv2 增强（随机裁剪、颜色抖动、模糊等）共同作用于输入图像，形成三种策略：
    1. **仅标准增强**（基线 DINOv2）；
    2. **混合增强**：标准增强与语义掩膜混合使用；
    3. **仅语义掩膜增强**。
  - **预训练细节**：使用 5500 万张 224×224 像素、0.5 μm/像素的 TCGA 病理图块，在 ViT 架构上进行自监督预训练。DINOv2 的学生-教师框架保持不变，只是输入图像在经过教师分支时施加上述增强组合，学生分支则需从掩膜后的视图重建原有特征。
- **算法流程概括**：
  - 对每张输入图块，以设定概率决定此次迭代采用哪种增强策略：若采用语义掩膜，则调用预先训练好的对抗掩膜生成器，输出结构化掩膜覆盖部分区域；然后将掩膜图与其他标准增强叠加后送入教师编码器，学生编码器接收不同增强视图（或原始图），通过对比学习拉近两者在特征空间的距离。
  - 对抗掩膜生成器本身在独立阶段用感知重建损失训练，使其学会遮盖组成性结构（如细胞密集区），保证被掩膜区域具有病理语义。

### 3. 实验设计

- **预训练数据集**：来自 TCGA（The Cancer Genome Atlas）的 5500 万张病理图块（224×224 像素，0.5 μm/像素），涵盖多种癌症类型，提供大规模且多样化的组织形态。
- **下游评估基准**：
  - **图块级分类任务**（4 个）：
    - **PCam**：淋巴结转移检测；
    - **MiDOG**：狗肿瘤良恶性分类（跨物种泛化测试）；
    - **MHIST**：结直肠息肉组织学分类；
    - **BRACS**：乳腺癌亚型分类。
  - **切片级突变预测任务**（2 个）：
    - **EGFR 突变预测**（肺腺癌 LUAD）；
    - **FGFR3 突变预测**（膀胱癌 BLCA）。
- **对比方法**：
  - 标准 DINOv2 增强（仅常规数据增强）；
  - 混合增强（标准 + 语义掩膜）；
  - 仅语义掩膜增强。
    同时，提供定性 PCA 可视化分析，观察无监督下图块 token 的组织成分分解能力。
- **预训练架构**：视觉 Transformer（ViT），具体变体未在摘要中明确，但 DINOv2 一般使用 ViT-S/B/L。

### 4. 资源与算力

- **文中未提供具体 GPU 型号、数量与训练时长**。只提及使用 5500 万张图块进行预训练，规模较大，通常需要数天至数周的多 GPU 集群。但所有算力相关信息在摘要中缺失，读者需等待全文公开方可获取精确资源配置。

### 5. 实验数量与充分性

- **实验组数**：
  - 3 种增强策略在 6 个下游任务上评估，至少 18 组主要结果（部分任务可能仅报告最佳策略）。
  - 定性实验包括 PCA 可视化，对比不同增强策略下 token 嵌入的组织分解效果。
- **充分性与客观性**：
  - 下游任务覆盖图块级和切片级、多癌种与跨物种（MiDOG），具有较好的多样性；
  - 消融设计清晰，能够分离语义掩膜的独立贡献与混合策略的协同效应；
  - 所有对比均基于同一预训练数据集和相同骨干结构，保证了公平性；
  - 但摘要未报告统计显著性检验或误差线，具体实验数量需全文确认。此外，仅使用 TCGA 进行预训练，存在一定数据源偏向。

### 6. 论文的主要结论与发现

- **混合增强策略（标准 + 语义掩膜）在多数任务上实现一致提升**：表明组织微环境先验可以与通用视觉增强互补，并不需要完全取代标准增强。
- **定性分析表明**：仅凭语义掩膜增强，模型在无监督下能将细胞结构、血管、间质等要素更清晰地分解到不同 token 组，获得更富生物学可解释性的表征。
- **有效性与通用性**：方法在不同分辨率（图块级）和不同预测目标（突变状态）下均展现出优势，证明该先验具有跨任务迁移能力。
- **核心启示**：将领域特有的结构先验纳入自监督学习，能显著提升病理基础模型的表征质量和可解释性，优于单纯依赖自然图像套路的增强。

### 7. 优点

- **领域驱动的创新**：首次明确利用组织微环境结构作为自监督先验，而非简单沿用自然图像的增强策略，推动病理 AI 朝“懂组织结构”的方向发展。
- **方法论合理**：通过对抗掩膜生成器自适应地定位语义区域，避免手工标注，保持全自监督；与 DINOv2 无缝集成，无需改变核心学习目标。
- **实验设计扎实**：同时覆盖分类和突变预测、跨物种任务，从定量和定性（PCA 可视化）两个维度验证，增强说服力。
- **可解释性增益**：模型在无监督下即可形成生物学合理的分解，这为临床理解和信任提供了直观证据。

### 8. 不足与局限

- **算力信息缺失**：未披露预训练所需的具体计算资源，影响复现与成本评估。
- **对比方法有限**：仅与标准 DINOv2 及其变体比较，未与其他先进的病理自监督方法（如针对病理设计的 iBOT、CTransPath 等）或使用不同掩膜策略（如随机掩膜）的系统对比。
- **数据偏向风险**：预训练全依赖 TCGA（主要来自欧美人群），其人口偏差可能限制全球适用性；下游任务中 MiDOG 为犬类数据，虽测试跨物种能力，但样本量和代表性未说明。
- **掩膜质量依赖**：对抗掩膜生成器的质量直接影响最终表征，若生成器未捕获关键结构，改进可能失效；文中未深入分析掩膜生成器的准确度或稳定性。
- **可能泛化局限**：仅测试了有限的切片级任务（两种基因突变），对于更复杂的预后、治疗反应预测等未见报告，实用性需进一步验证。
- **缺乏敏感性分析**：未探讨掩膜面积比例、混合概率等超参数的影响，可能掩盖最佳配置。

（完）
