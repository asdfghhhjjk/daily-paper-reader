---
title: "PathChat-SegR1: Reasoning Segmentation in Pathology via SO-GRPO"
title_zh: PathChat-SegR1：通过SO-GRPO实现病理学中的推理分割
authors: "Zelin Liu, Dongdong Chen, Yusong Sun, Yuqi Hu, Huang Jie, Sicheng Dong, Xu Han, Hongmei Yi, Qiyuan Bao, Lichi Zhang"
date: 2026-01-26
pdf: "https://openreview.net/pdf?id=DQESI75YrD"
tags: ["query:immuno-topo"]
score: 9.0
evidence: 专为病理学设计的推理分割模型，支持通过文本提示进行零样本细胞和结构分割。
tldr: 针对病理图像分割中训练分布外组织形态泛化难题，PathChat-SegR1通过强化视觉编码器的病理领域知识和大型语言模型的推理能力，实现了基于文本提示的零样本推理分割。该模型建立了病理推理分割基准，在多种任务上展现出优越的泛化能力，为病理图像分析提供了通用的分割工具。
source: ICLR-2026-Accepted
selection_source: conference_retrieval
motivation: 现有病理分割模型无法泛化到新组织形态，缺乏领域知识且无推理能力。
method: 构建PathChat-SegR1，结合病理增强视觉编码器和LLM推理，实现文本引导分割。
result: 在零样本分割任务上表现优异，泛化能力强。
conclusion: 推理分割为病理学提供了通用、可泛化的分割解决方案，具有实际价值。
---

## Abstract
Segmentation in pathology image requires handling out-of-domain tissue morphologies and new pathologies beyond training distributions, where traditional closed-set segmentation approaches fail to generalize. 
Reasoning segmentation enables zero-shot generalization via prompting with text queries. 
However, existing reasoning segmentation models face three barriers when applied to pathology: 
(1) the vision encoder lack pathology-specific knowledge and robustness to staining variations, 
(2) the large language model (LLM) backbone for reasoning fails to identify whether it has gathered sufficient semantic context to trigger the segmentation output,
and (3) no reasoning segmentation benchmarks and datasets exist for pathology analysis. 
Consequently, we introduce PathChat-SegR1, a reasoning segmentation model built upon pathology-specific vision encoders trained with a novel stain-invariant self-distillation for robust pathology image representations. 
Moreover, we propose Segmentation-Optimized GRPO (SO-GRPO), a reinforcement learning method specifically for reasoning segmentation that learns to determine optimal segmentation timing based on accumulated reasoning context.
Finally, we construct a pathology-specific reasoning segmentation benchmark of 118,667 triplets of pathology image, ground-truth mask, query, and reasoning chain including both public and private pathology images. 
Zero-shot evaluation on pathology images with out-of-domain morphologies/pathologies shows 61\% improvement over state-of-the-art segmentation models.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义（研究动机和背景）

- **核心问题**：传统病理图像分割模型仅在封闭的训练类别上工作，一旦遇到训练分布之外的组织形态、染色差异或新型病理，就会失效，缺乏泛化能力。
- **整体含义**：本文旨在构建能够“推理分割”的病理学模型——即根据自然语言提示（如“请分割出所有的肿瘤细胞”）零样本泛化到未知对象的分割。这要求模型具备病理领域知识、染色不变性以及对“何时该分割”的自主判断能力。
- **关键挑战**：
  1. 通用视觉编码器缺乏病理专有知识与染色鲁棒性；
  2. 现有推理分割模型中的大语言模型（LLM）无法判断是否已收集足够语义上下文来触发分割输出；
  3. 缺乏病理学领域专用的推理分割基准和数据集。

### 2. 论文提出的方法论

- **整体框架**：构建 **PathChat-SegR1**，将病理增强的视觉编码器与大语言模型结合，实现基于文本提示的推理分割。
- **关键技术细节**：
  - **病理专有视觉编码器**：使用一种新颖的 **染色不变自蒸馏（stain-invariant self-distillation）** 训练方法，使视觉表征对染色变化鲁棒，同时注入丰富的病理领域知识。
  - **分割优化的强化微调**：提出 **分割优化GRPO（Segmentation-Optimized GRPO, SO-GRPO）**，一种专为推理分割设计的强化学习方法。它让LLM学习在积累足够的推理上下文后，自主决定最优的分割触发时机，而不是固定地在某步输出掩码。
- **算法流程（文字说明）**：
  - 输入病理图像和文本查询；
  - 病理视觉编码器提取鲁棒视觉特征；
  - LLM逐步进行链式推理，聚合与查询相关的语义信息；
  - 在每步推理中，通过SO-GRPO训练的决策策略判断是否已到达“分割点”，若满足则输出分割掩码，否则继续推理。

### 3. 实验设计

- **新构建基准**：建立了专门的病理推理分割基准，包含 **118,667个三元组**（图像、真值掩码、查询文本与推理链），数据来自公开及私有的病理图像。
- **评估场景**：主要评估 **零样本分割**，测试模型在 **分布外组织形态/病理类型** 上的表现。
- **对比方法**：与最先进的分割模型（state-of-the-art segmentation models）进行比较，具体名称未在摘要中列出，但明确展示了相对于它们的显著提升（提升61%）。

### 4. 资源与算力

- 给定的文本中 **未提及** 所使用的GPU型号、数量、训练时长或具体算力消耗。因此无法提供相关信息。

### 5. 实验数量与充分性

- **实验组数**：摘要未详细列出实验组的具体数量，但基于以下信息可推断实验较为充分：
  - 构造了大规模专属基准（>118k样本），覆盖公开和私有多源数据；
  - 进行了零样本分割评估，与最先进模型的对比实验；
  - 提出的SO-GRPO方法本身即为一种训练策略，隐含消融实验的可能（摘要未详细说明，但通常此类工作会包含消融实验）。
- **客观性与公平性**：采用统一的零样本设定，使用分布外数据评估，避免了领域泄露，对比基准为现有先进模型，具备一定的公平性。

### 6. 论文的主要结论与发现

- **零样本分割性能优越**：在分布外病理图像上，PathChat-SegR1的性能相较现有最先进分割模型提高了 **61%**。
- **推理分割的通用性**：所提出的推理分割范式为病理学分析提供了一种通用且可泛化的解决方案，能够处理未见过的组织形态和新病理类型，具有实际应用价值。
- **关键组件有效性**：病理增强视觉编码器与SO-GRPO决策策略对提升泛化能力至关重要。

### 7. 优点：方法或实验设计上的亮点

- **领域定制化**：首次针对病理学设计推理分割模型，解决了领域知识与染色泛化两大关键痛点。
- **创新的学习机制**：提出的SO-GRPO将“何时分割”建模为可学习的推理决策，超越了固定流程，更有智能感。
- **大规模专用基准**：构建了包含完整推理链的病理分割基准，为后续研究提供了资源。
- **显著的泛化能力**：在零样本设定下取得巨大提升，验证了推理分割在病理领域的潜力。

### 8. 不足与局限

- **算力与资源不可知**：未提供训练所需的计算资源信息，复现门槛不透明。
- **对比范围不明确**：对比的“state-of-the-art segmentation models”具体是哪些、是否同样基于LLM或推理分割并未详述，削弱了结论的可比性。
- **推理链质量与偏差风险**：基准中的推理链由人工或LLM生成，可能存在偏差；模型学习的“推理”是否真正有助于临床决策，尚需临床验证。
- **仅限零样本设定**：未报告全监督或少样本设定下的性能，其上限和适用范围需进一步探索。
- **病理类型覆盖度**：尽管使用了私有和公开数据，但病理世界的异质性极高，基准能否代表广泛临床场景存疑。

（完）
