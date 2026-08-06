---
title: Tissue Microenvironment as an Additional Prior for Visual Representation Learning in Histopathology
title_zh: 组织微环境作为组织病理学视觉表示学习的附加先验
authors: "Swaraj Nanda, Neeraj Kumar, Siddharth Singi, Amir Momeni Boroujeni, Jie-Fu Chen, David Kim, Jamal Benhamida, Gregory M. Goldgof, Chad Vanderbilt"
date: 2025-09-19
pdf: "https://openreview.net/pdf?id=iFNY9Omyjk"
tags: ["query:immuno-topo"]
score: 8.0
evidence: 将组织微环境结构作为先验融入自监督组织病理学表示学习
tldr: 该论文针对现有组织病理学自监督学习方法未充分利用组织微环境结构信息的问题，提出通过对抗式掩码生成器提取组织结构语义掩码，并将其作为增强融入DINOv2自监督学习管线。在5500万张TCGA组织病理学图像上的预训练实验表明，所提方法能学习更丰富的表示，提升下游任务性能。该方法为在组织病理学视觉表示学习中显式建模微环境先验提供了新途径。
source: ICLR-2026-Public
selection_source: conference_retrieval
motivation: 现有自监督学习方法在组织病理学中忽略了组织微环境结构这一重要先验信息。
method: 利用对抗式掩码生成器提取组织结构作为语义掩码，并将其作为增广集成到DINOv2训练中。
result: 在大规模数据上预训练后，下游任务性能显著提升。
conclusion: 显式建模微环境结构可以增强组织病理学图像的表示学习。
---

## Abstract
Self-supervised learning has transformed histopathology by enabling foundation models to learn from vast unlabeled image archives, with methods developed using natural images, such as DINOv2, establishing powerful baselines. We propose augmenting these approaches by incorporating tissue microenvironment structure as an additional prior through semantic masking. We train adversarial mask generators adapted from ADIOS with perceptual reconstruction losses to identify tissue structures, then integrate these semantic masks as augmentations within DINOv2 self-supervised learning pipelines. Using a set of 55 million TCGA histopathology tiles of 224$\times$224 pixels at a resolution of 0.5 $\mu$m/pixel, we pre-train vision transformers to evaluate three augmentation strategies: standard DINOv2 augmentations, mixed (combining standard and semantic masking), and semantic masking only. The mixed augmentation strategy, when used in DINOv2, demonstrates consistent improvements over baseline across four patch-level classification benchmarks (PCam, MiDOG, MHIST, BRACS) and on two slide-level mutation prediction tasks (EGFR in LUAD, FGFR3 in BLCA). Qualitative PCA visualization of patch tokens shows that semantic masks combined with standard augmentations enable a better decomposition of tissue into biologically interpretable components without supervision, with DINOv2-mixed achieving clear separation of cellular structures, vasculature, and stromal elements. Therefore, incorporating domain-specific tissue priors through semantic masking enhances representation learning in self-supervised frameworks, alongside standard augmentations.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义（研究动机和背景）
- **核心问题**：当前组织病理学领域的自监督视觉表示学习（如 DINOv2）主要沿用自然图像的方法，通过标准数据增强来学习特征，却普遍忽略了组织病理图像中“组织微环境结构”这一重要的领域专属先验信息。
- **整体含义**：论文旨在将组织微环境结构（如细胞结构、血管、基质成分的空间组织方式）作为额外先验融入自监督预训练，以学到更丰富、更具生物学可解释性的组织表示，从而提升下游任务性能。

### 2. 论文提出的方法论
- **核心思想**：通过“语义掩码”将组织微环境结构显式地作为增强信号，与标准图像增强结合，来改进自监督学习框架 DINOv2。
- **关键技术细节**：
  - **对抗式掩码生成器**：基于 ADIOS 方法进行适配，训练一个掩码生成器来识别并分割组织病理图像中的结构区域。该生成器使用感知重建损失（perceptual reconstruction losses）来提取组织的语义掩码。
  - **增强集成**：将生成的语义掩码作为一种新型增强方式，直接整合到 DINOv2 的自监督学习管线中。具体策略包括：仅使用标准 DINOv2 增强、混合使用标准增强和语义掩码、仅使用语义掩码。
  - **算法流程（文字描述）**：给定病理图块，先通过预训练的对抗式掩码生成器获得组织语义掩码；将该掩码视为一种变换，与颜色扰动、裁剪等标准增强混合或独立地作用于输入图像，再送入视觉 Transformer 进行 DINOv2 式的对比学习，从而迫使模型关注组织微环境级别的结构信息。

### 3. 实验设计
- **预训练数据**：来自 TCGA 的 5500 万张组织病理学图块，尺寸 224×224 像素，分辨率 0.5 µm/像素。
- **下游评估基准**：
  - **块级分类任务**（4个）：PCam、MiDOG、MHIST、BRACS。
  - **切片级突变预测任务**（2个）：肺腺癌（LUAD）中的 EGFR 突变、膀胱尿路上皮癌（BLCA）中的 FGFR3 突变。
- **对比方法**：三种增强配置的 DINOv2 预训练模型：标准 DINOv2 增强（基线）、混合增强（标准 + 语义掩码）、纯语义掩码增强。在相同下游任务上进行比较。
- **定性分析**：对块级别 token 进行 PCA 可视化，观察不同增强策略下组织成分的分离情况。

### 4. 资源与算力
- **说明**：提供的摘要和元数据中**未明确提及**所使用的 GPU 型号、数量、训练时长、总计算量等资源与算力信息。仅知晓使用了 5500 万张图块的大规模预训练，具体算力消耗未知。

### 5. 实验数量与充分性
- **实验组数**：主要围绕 3 种预训练增强策略，在 6 个下游任务（4 个块级分类 + 2 个切片级突变预测）上进行评估，并辅以定性的 PCA 可视化实验。
- **充分性与客观性**：实验覆盖了多个公开病理基准，对比基线明确（标准 DINOv2 增强），展示了混合策略的增益。但所提供内容未报告多次运行的方差、统计显著性检验或详细的消融研究（如语义掩码生成器的不同设计选择），因此难以判断实验是否在统计层面充分客观。

### 6. 论文的主要结论与发现
- 混合增强策略（标准 DINOv2 增强 + 语义掩码）在所有 4 个块级分类基准和 2 个切片级突变预测任务上，一致优于仅使用标准增强的基线。
- PCA 可视化显示，混合增强使模型在无监督条件下能将组织块分解为更具生物学意义的成分，清晰分离出细胞结构、血管和基质元素。
- 显式建模组织微环境结构可以作为域特定先验，有效增强自监督框架在组织病理学中的表示学习。

### 7. 优点
- **方法新颖**：首次将组织微环境结构作为语义掩码先验融入 DINOv2 框架，为领域自监督学习提供了新思路。
- **策略灵活**：提出混合增强策略，既保留了标准增强的泛化能力，又引入了病理特有的结构先验。
- **可解释性提升**：通过定性分析表明，所学表示能无监督地分解出有生物学意义的组织成分。
- **下游任务广泛**：在块级和切片级、分类和突变预测等不同粒度的任务上验证了有效性。

### 8. 不足与局限
- **资源信息缺失**：摘要未提供算力、训练时长等关键资源信息，难以评估方法的实际应用成本。
- **实验细节不透明**：未提及语义掩码生成器的具体结构、训练细节，以及混合增强的具体实现（如应用概率、强度等），消融实验不足。
- **偏差风险**：基于 TCGA 单一数据源预训练，可能引入机构或染色偏差，泛化至其他来源数据的能力未知。
- **依赖掩码质量**：方法的增益高度依赖对抗式掩码生成器识别组织结构的准确性，若掩码不可靠可能引入噪声。
- **任务覆盖有限**：下游任务虽覆盖分类和突变预测，但缺少分割、检测或更多癌种突变预测等任务的验证。

（完）
