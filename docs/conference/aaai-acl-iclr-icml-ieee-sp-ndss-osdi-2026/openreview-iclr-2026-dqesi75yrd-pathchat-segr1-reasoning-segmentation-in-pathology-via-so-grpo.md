---
title: "PathChat-SegR1: Reasoning Segmentation in Pathology via SO-GRPO"
title_zh: PathChat-SegR1：通过SO-GRPO进行病理学推理分割
authors: "Zelin Liu, Dongdong Chen, Yusong Sun, Yuqi Hu, Huang Jie, Sicheng Dong, Xu Han, Hongmei Yi, Qiyuan Bao, Lichi Zhang"
date: 2026-01-26
pdf: "https://openreview.net/pdf?id=DQESI75YrD"
tags: ["query:path-xai-sel"]
score: 7.0
evidence: 用于病理图像的推理分割模型，实现计算病理学中的零样本泛化。
tldr: PathChat-SegR1针对传统封闭集病理分割无法泛化到新组织形态的问题，提出一种基于推理的分割范式。通过引入病理知识视觉编码器、大语言模型推理以及SO-GRPO优化，模型能根据文本提示理解分割语义并输出分割掩膜。首次构建的病理推理分割基准表明，该方法在多种未见过的组织类型上均能准确分割，为计算病理学中的通用分割任务提供了有前景的方案。
source: ICLR-2026-Accepted
selection_source: conference_retrieval
motivation: 病理图像分割常面临训练集以外的新组织形态，闭集方法泛化不足，且缺乏病理推理分割基准。
method: 设计病理专用视觉编码器，利用大语言模型根据文本提示进行推理并通过SO-GRPO强化学习生成分割。
result: 在自建基准上，模型对未见组织类型取得良好的零样本分割性能，且能适应不同染色风格。
conclusion: 推理分割为病理图像分析提供了强大的泛化能力，有望成为处理开放世界病理任务的基础工具。
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

# PathChat-SegR1：通过SO-GRPO进行病理学推理分割

## 1. 核心问题与研究动机
- **核心问题**：病理图像分割经常需要处理训练集之外的新组织形态和新病变类型，传统的闭集分割方法（closed-set segmentation）泛化能力严重不足，无法应对开放世界中不断出现的“未见样本”。
- **研究动机与背景**：推理分割（reasoning segmentation）借助文本提示（text queries）能够实现零样本泛化，有望解决上述封闭集分割的难题。但现有推理分割模型直接应用到病理图像时面临三个关键障碍：
  - 视觉编码器缺乏病理学专门知识，对染色变化的鲁棒性差；
  - 用于推理的大语言模型（LLM）无法自行判断是否已积累足够的语义上下文以触发分割输出；
  - 尚无用于病理分析的推理分割基准和数据集。

## 2. 方法论
- **核心思想**：构建一个专用于病理图像的推理分割模型，通过病理专用视觉编码器、大语言模型推理机制以及针对分割任务优化的强化学习方法，实现根据文本查询进行零样本分割。
- **关键技术细节**：
  - **病理知识视觉编码器**：设计Pathology-specific vision encoder，并采用一种新型的染色不变自蒸馏（stain-invariant self-distillation）来获得鲁棒的病理图像表征，使其能适应不同染色风格和组织形态。
  - **SO-GRPO（Segmentation-Optimized GRPO）**：专门为推理分割设计的强化学习方法。它让LLM学会根据累积的推理上下文来确定最优的分割触发时机，解决“何时输出分割”的问题。
  - **算法流程概览**：病理图像经过染色不变的视觉编码器提取特征 → 结合文本查询由LLM进行逐步推理 → SO-GRPO强化学习训练LLM判断何时上下文足够并生成最终的分割掩膜。

## 3. 实验设计
- **数据集与基准**：作者构建了一个病理专用推理分割基准，包含 118 667 组（病理图像、真实掩膜、文本查询、推理链）的四元组数据，数据来源包括公开和私有的病理图像。
- **测试场景**：在含有训练集未见过的新组织形态/病变类型的病理图像上进行零样本评估。
- **对比方法**：与最先进的分割模型进行对比，未列出具体模型名称（元数据未提供细节），但声称推理分割范式相比传统闭集模型有巨大提升。

## 4. 资源与算力
- 论文元数据及所给文本中 **未明确说明** 使用的GPU型号、数量、训练时长或总计算量。此项信息缺失，需查阅原论文完整内容方可确认。

## 5. 实验数量与充分性
- 从现有信息推断，至少包含以下实验：
  - 零样本分割主实验（与现有SOTA模型对比）；
  - 不同染色风格下的泛化测试；
  - 可能涉及的消融实验（如视觉编码器设计、SO-GRPO的有效性等），但元数据中未给出具体实验数量。
- **充分性与公平性**：
  - 构建了包含公开和私有多源数据的大规模基准（118 667组样本），数据规模较充分；
  - 零样本评估严格限定在未见过的组织形态/病变类型上，能够客观衡量泛化能力；
  - 但缺少与其他推理分割模型（非病理专用）的直接对比细节，且私密数据的可复现性存在天然局限，可能会影响公平性评估。

## 6. 主要结论与发现
- PathChat-SegR1 在拥有未见过的组织形态/病变的病理图像上，零样本分割性能**比当前最先进的分割模型提升61%**。
- 推理分割范式能够为计算病理学提供强大的泛化能力，使单一模型可以处理开放世界中多样且不断演变的病理任务。
- 该方法对不同的染色风格具有鲁棒性，具备成为通用病理图像分割基础工具的潜力。

## 7. 优点
- **方法亮点**：
  - 首次将推理分割引入病理图像分析，并系统解决了三个领域特有障碍；
  - 提出的染色不变自蒸馏和SO-GRPO分别从图像表征和推理决策两个层面增强模型在病理场景下的实用性；
  - 构建了首个大规模病理推理分割基准，为该方向提供评价平台。
- **实验亮点**：
  - 零样本评估直接针对最难的新组织形态/病变，展示出极强的泛化优势；
  - 61%的相对提升具有显著的实用意义。

## 8. 不足与局限
- **实验覆盖不足**：元数据未提供与通用推理分割模型（如LISA等）在病理数据上的横向比较，无法判断究竟是病理专用视觉编码器还是推理分割范式本身带来了主要收益；未提及在常见闭集病理分割任务上的表现对比。
- **数据偏差风险**：基准中包含私密数据，其采集来源、标注一致性、机构偏向等信息缺失，可能影响通用性宣称。
- **应用限制**：模型依赖LLM推理，可能面临推理速度慢、计算开销大、依赖高质量查询等问题，实际临床部署的时效性与稳定性待验证；未见与病理医生诊断标准的一致性评估。
- **信息局限性**：由于仅依据元数据总结，缺失对模型架构细节、训练配置、完整消融实验的深入分析，上述不足可能因信息不全而有所偏差。

（完）
