---
title: Tissue Microenvironment as an Additional Prior for Visual Representation Learning in Histopathology
title_zh: 组织微环境作为组织病理视觉表征学习的附加先验
authors: "Swaraj Nanda, Neeraj Kumar, Siddharth Singi, Amir Momeni Boroujeni, Jie-Fu Chen, David Kim, Jamal Benhamida, Gregory M. Goldgof, Chad Vanderbilt"
date: 2025-09-19
pdf: "https://openreview.net/pdf?id=iFNY9Omyjk"
tags: ["query:profile"]
score: 9.0
evidence: 将组织微环境结构作为先验融入自监督组织病理表征学习
tldr: 提出在组织病理学自监督学习中，通过语义掩膜将组织微环境结构作为额外先验，融合到DINOv2框架中，增强视觉表征对组织微环境的感知能力，提升下游分类与回归任务表现。
source: ICLR-2026-Public
selection_source: conference_retrieval
motivation: 现有自监督学习方法未显式利用组织微环境结构，限制了表征对组织生物学细节的捕获。
method: 采用对抗掩膜生成器识别组织结构，将生成的语义掩膜作为数据增强融入DINOv2自监督学习。
result: 在大规模TCGA组织病理切片上预训练后，在多个下游任务上取得性能提升。
conclusion: 证明了组织微环境先验在自监督病理表征学习中的有效性，为下游任务提供更丰富的生物学特征。
---

## Abstract
Self-supervised learning has transformed histopathology by enabling foundation models to learn from vast unlabeled image archives, with methods developed using natural images, such as DINOv2, establishing powerful baselines. We propose augmenting these approaches by incorporating tissue microenvironment structure as an additional prior through semantic masking. We train adversarial mask generators adapted from ADIOS with perceptual reconstruction losses to identify tissue structures, then integrate these semantic masks as augmentations within DINOv2 self-supervised learning pipelines. Using a set of 55 million TCGA histopathology tiles of 224$\times$224 pixels at a resolution of 0.5 $\mu$m/pixel, we pre-train vision transformers to evaluate three augmentation strategies: standard DINOv2 augmentations, mixed (combining standard and semantic masking), and semantic masking only. The mixed augmentation strategy, when used in DINOv2, demonstrates consistent improvements over baseline across four patch-level classification benchmarks (PCam, MiDOG, MHIST, BRACS) and on two slide-level mutation prediction tasks (EGFR in LUAD, FGFR3 in BLCA). Qualitative PCA visualization of patch tokens shows that semantic masks combined with standard augmentations enable a better decomposition of tissue into biologically interpretable components without supervision, with DINOv2-mixed achieving clear separation of cellular structures, vasculature, and stromal elements. Therefore, incorporating domain-specific tissue priors through semantic masking enhances representation learning in self-supervised frameworks, alongside standard augmentations.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义（研究动机和背景）

- **研究背景**：自监督学习（Self‑supervised learning）已推动组织病理学基础模型的发展，使得模型能够从海量无标签图像中学习。以 DINOv2 为代表的自然图像自监督方法已成为强有力的基线。
- **核心问题**：现有自监督学习方法（如 DINOv2）主要依赖通用图像数据增强（如颜色抖动、裁剪等），并未显式利用组织病理图像特有的 **组织微环境（tissue microenvironment）结构**，这限制了视觉表征对细胞类型、血管、基质等生物学细节的捕获能力。
- **整体含义**：本文提出将组织微环境结构作为一种 **附加的先验信息**，通过语义掩膜（semantic masking）的方式融入自监督学习框架，从而增强表征对组织结构的感知，提升下游病理任务的表现。

### 2. 论文提出的方法论：核心思想、关键技术细节

- **核心思想**：在 DINOv2 的自监督学习流程中，除了传统的图像增强，额外引入 **语义掩膜** 作为数据增强策略。语义掩膜能够突出或遮挡特定的组织微环境区域，迫使模型学习与组织结构相关的语义特征。
- **关键技术细节**：
  - **对抗掩膜生成器**：基于 ADIOS 框架训练掩膜生成器，使用 **感知重建损失（perceptual reconstruction losses）** 来识别组织图像中的结构。
  - **语义掩膜集成**：将生成的语义掩膜作为一种数据增强形式，整合到 DINOv2 的教师‑学生网络训练中。
  - **三种增强策略对比**：
    1. 仅使用标准 DINOv2 增强（基线）。
    2. **混合增强**：标准增强 + 语义掩膜（最终提出的最优策略）。
    3. 仅使用语义掩膜增强。
- **流程简述**：将语义掩膜施加于输入图像（例如局部遮挡或变换某些区域），教师和学生网络同时看到增强后的视图，通过对比学习优化表征。

### 3. 实验设计：数据集、Benchmark 与对比方法

- **预训练数据集**：来自 **TCGA** 的 5500 万张组织病理学切块（tiles），尺寸 224×224 像素，分辨率 0.5 µm/pixel。
- **下游任务与 Benchmark**：
  - **图块级分类**：PCam、MiDOG、MHIST、BRACS 四个公开基准。
  - **切片级突变预测**：肺腺癌（LUAD）中的 EGFR 突变，膀胱尿路上皮癌（BLCA）中的 FGFR3 突变。
- **对比方法**：主要比较同一 DINOv2 框架下三种增强策略（标准、混合、纯语义掩膜）的性能差异。未提及与其他自监督框架（如 SimCLR、BYOL 等）的对比。

### 4. 资源与算力

- **文中明确信息**：预训练使用了 5500 万张病理切块，但 **未提及** 具体的 GPU 型号、数量、训练时长或总计算量（如 GPU 小时）。因此算力需求无法从现有材料中获知。

### 5. 实验数量与充分性

- **实验覆盖**：
  - 至少在 **4 个图块分类任务**、**2 个切片突变预测任务** 上测试了 3 种增强策略。
  - 同时进行了 **PCA 可视化定性分析**，观察 token 的分解程度。
- **充分性评价**：从摘要看，实验设计能够支持其核心结论，即混合增强策略相比纯标准增强有 consistent improvements。但摘要未提及消融实验（如不同掩膜比例、不同结构类型）或统计显著性检验，因此尚无法判断实验是否完全覆盖可能的消融变量。对比方法仅局限于 DINOv2 内部变体，与其他流行自监督方法的公平比较尚不明确。

### 6. 论文的主要结论与发现

- **性能提升**：在 DINOv2 中采用混合增强（标准增强 + 语义掩膜），在 4 个图块分类基准和 2 个突变预测任务上均取得较基线一致的性能改善。
- **表征分解**：PCA 可视化显示，语义掩膜与标准增强结合，使图像 token 在无监督条件下更好地分解出可解释的生物学成分（如细胞结构、血管、基质元素），其中 DINOv2‑mixed 实现了这些成分的清晰分离。
- **核心洞察**：将领域特定的组织先验通过语义掩膜融入自监督框架，能够在保持标准增强优势的同时，增强表征的生物学可解释性和下游判别能力。

### 7. 优点：方法或实验设计上的亮点

- **领域先验的巧妙引入**：不修改 DINOv2 架构，仅通过数据增强的方式将组织微环境先验注入，方法轻量且易于与现有框架结合。
- **可解释性增强**：不仅提升精度，还通过 PCA 可视化直观展示了表征对组织结构的分化能力，符合数字病理对可解释性的需求。
- **大规模预训练验证**：在 5500 万张真实病理图像上预训练，证明了方法的可扩展性和实用性。

### 8. 不足与局限：包括实验覆盖、偏差风险、应用限制等

- **信息缺失**：仅从摘要推断，缺少模型大小、训练超参数、统计检验、消融实验等细节，难以评估方法的鲁棒性和最优配置。
- **对比局限性**：仅在 DINOv2 框架内比较增强策略，未提供与其他自监督基线（如 iBOT、MAE、Pathology 专用模型如 CTransPath）的直接对比，难以判断绝对增益幅度。
- **偏差风险**：TCGA 数据虽然规模大，但来源偏于北美/欧洲人群，可能影响表征在其他人群或染色平台上的泛化性。
- **掩膜生成器依赖**：依赖于预训练的 ADIOS 掩膜生成器，其本身的质量和泛化能力会影响最终表征，但未讨论这一点。
- **计算成本未透明**：缺乏算力报告，阻碍其他研究者复现或评估资源需求。

（完）
