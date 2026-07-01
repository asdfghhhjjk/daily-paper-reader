---
title: Randomized-MLP Regularization Improves Domain Adaptation and Interpretability in DINOv2
title_zh: 随机化MLP正则化改善DINOv2中的领域适应性和可解释性
authors: "Joel Valdivia Ortega, Lorenz Lamm, Franziska Eckardt, Benedikt Schworm, Marion Jasnin, Tingying Peng"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=Rzqs4q9ooa"
tags: ["query:pathology-ai"]
score: 4.0
evidence: 引入RMLP正则化提高DINOv2在医学成像中注意力图的可解释性
tldr: DINOv2在医学图像中常将低信息量图块用于低可解释性表示。本文提出随机化MLP正则化，通过对比学习鼓励语义对齐，微调后提升下游性能同时产生更可解释的注意力图，为病理图像特征提取的可解释性提供了通用改进方法。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
motivation: 解决DINOv2在医学成像中注意力图可解释性差的问题，以利于透明特征提取。
method: 提出随机化MLP正则化，结合对比学习微调DINOv2。
result: 在下游任务中保持或提升性能，同时生成更可解释的注意力图。
conclusion: RMLP正则化有效提升医学图像模型的域适应性和可解释性。
---

## Abstract
Vision Transformers (ViTs), such as DINOv2, achieve strong performance across domains but often repurpose low-informative patch tokens in ways that reduce the interpretability of attention and feature maps. This challenge is especially evident in medical imaging, where domain shifts can degrade both performance and transparency. In this paper, we introduce Randomized-MLP (RMLP) regularization, a contrastive learning-based method that encourages more semantically aligned representations. We apply RMLP when fine-tuning DINOv2 to both medical and natural image modalities, showing that it improves or maintains downstream performance while producing more interpretable attention maps. We also provide a mathematical analysis of RMLPs, offering insights into its role in enhancing ViT-based models and advancing our understanding of contrastive learning in this context.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体背景

- **研究动机**：当前基于 Vision Transformer (ViT) 的模型（如 DINOv2）在跨领域图像分析中表现出色，但在医学成像等具有显著领域偏移（domain shift）的场景下，模型倾向于将低信息量的图像块（patch tokens）重复利用，导致注意力图和特征图的可解释性下降。
- **核心问题**：领域偏移会使模型性能与透明度同时受损，而现有方法缺乏对特征语义对齐的有效约束，尤其不利于需要可解释性的医学图像分析。
- **整体含义**：本文旨在通过一种新的正则化技术，在不损失下游任务性能的前提下，提升 DINOv2 在医学图像领域上的特征可解释性和领域适应能力。

### 2. 论文提出的方法论

- **核心思想**：引入 **随机化 MLP 正则化 (Randomized-MLP, RMLP)**，在 DINOv2 微调过程中加入对比学习目标，鼓励模型学习更具语义对齐的表示，避免模型过度依赖低信息量区域，从而生成更可解释的注意力图。
- **关键技术细节**：
  - RMLP 在微调时对 MLP 层的参数或输入施加随机化操作（具体随机化方式未在摘要中详述），以此作为正则化项。
  - 结合对比学习框架，使同一语义类别或相同区域的特征在嵌入空间中更接近，不同语义的特征相互推开。
  - 该正则化直接作用于 DINOv2 的 patch token 表示，引导注意力集中在有诊断意义的结构上。
- **数学分析**：作者对 RMLP 进行了数学分析，探讨其在 ViT 模型中增强表征能力的作用，并深化对对比学习在该背景下机制的理解。

### 3. 实验设计

- **数据集/场景**：
  - 涉及**医学图像模态**以及**自然图像模态**（Natural image modalities），但具体数据集名称（如组织病理学、放射学等数据集）在摘要中未指明。
- **Benchmark 设置**：
  - 以 DINOv2 原始模型或标准微调为基准，评估引入 RMLP 后的性能变化。
  - 比较指标包括下游任务性能（如分类、分割等）以及注意力图的可解释性。
- **对比方法**：
  - 标准微调的 DINOv2（无 RMLP）。
  - 可能包含其他正则化或对比学习方法，但摘要未详细列出。

### 4. 资源与算力

- 论文摘要和元数据中**未明确说明**所使用的 GPU 型号、数量、训练时长等算力信息。
- 由于论文接受于 NeurIPS 2025，通常在正式版本或附录中会补充算力细节，但基于现有材料无法提供。

### 5. 实验数量与充分性

- **实验组数**：由于缺乏完整论文，仅能根据摘要推断实验至少涵盖：
  - 医学图像 vs. 自然图像的跨域微调实验。
  - 有无 RMLP 的对比（可能包括消融实验，如不同随机化强度）。
  - 对注意力图可解释性的定性与定量评估。
- **充分性与公平性**：
  - 摘要强调该方法能在“保持或提升下游性能”的同时提升可解释性，说明实验设计兼顾性能与可解释性双重目标，具备基本公平性。
  - 但具体实验数量、统计检验、多中心验证等细节未知，因此无法断定是否完全充分；从接受会议等级（NeurIPS）推测实验应较完备。

### 6. 论文的主要结论与发现

- **性能与可解释性兼顾**：RMLP 正则化能够在医学与自然图像微调中，维持甚至提升下游任务性能，同时生成更可解释的注意力图。
- **机制分析**：数学分析揭示了 RMLP 如何通过对比学习促进语义对齐，为 ViT 在跨域迁移中的表示学习提供了新见解。
- **通用性**：该方法作为一种通用的ViT微调策略，有望应用于多种医学影像任务，增强特征提取的透明性。

### 7. 优点

- **创新性正则化**：将随机化与对比学习结合，专门针对 ViT 在领域偏移下的注意力退化问题，思路新颖。
- **双重收益**：在常见只追求性能提升的背景下，同时提升可解释性，更符合医学 AI 的实际需求。
- **理论支撑**：提供了数学分析，增加了方法的可信度和推广性。
- **通用性强**：不仅在医学图像上有效，在自然图像上也得到验证，显示方法的普适性。

### 8. 不足与局限

- **细节缺失**：基于现有摘要，无法得知随机化 MLP 的具体实现（如随机化的范围、强度、对比损失形式），削弱了复现性。
- **数据集范围未知**：不清楚具体使用了哪些医学和自然图像数据集，影响对其实验覆盖面的评估。
- **评估维度有限**：摘要未提及评估可解释性的具体标准（是专家评分、Grad-CAM 定位精度还是其他指标），可能减弱说服力。
- **应用限制**：方法仅在 DINOv2 上验证，尚未探索在其他 ViT 架构（如 Swin、MAE）或更多样化医学任务（如检测、报告生成）上的效果。
- **算力需求不明**：无算力报告，难以评估实用性。

（完）
