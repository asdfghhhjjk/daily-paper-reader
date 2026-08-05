---
title: CLS-Tuned Attention for Whole-Slide Image Classification
title_zh: CLS微调注意力用于全切片图像分类
authors: "Peter Chen, Gavnar Shi"
date: 2025-09-19
pdf: "https://openreview.net/pdf?id=Sz2kL7UiEG"
tags: ["query:path-xai-sel"]
score: 9.0
evidence: 基于注意力的MIL用于WSI分类，产生可用于选择显著区域的补丁级注意力图
tldr: "该论文在基于注意力的MIL聚合器中微调[CLS]令牌，显著提升WSI分类准确率，并产生可解释的补丁级注意力图，用于选择WSI中的显著区域，方法简单有效。"
source: ICLR-2026-Public
selection_source: conference_retrieval
motivation: 现有WSI分类中的注意力MIL模型参数多且训练不稳定，注意力图可解释性未充分优化。
method: "提出仅微调[CLS]令牌的注意力MIL方法，冻结其他参数并引入CLS门控校准注意力。"
result: 在多个数据集上提升分类准确率，减少参数且产生更聚焦的注意力图。
conclusion: 简单改进能大幅提升WSI分类性能和注意力图质量，为显著区域选择提供可靠依据。
---

## Abstract
Whole-slide image (WSI) classification is commonly cast as multiple instance learning (MIL): a slide (bag) is positive if at least one patch (instance) is positive. Attention-based MIL models have become a de-facto choice because they produce slide-level predictions and instance-level attention maps. In this paper we show that a simple yet overlooked modification—fine-tuning only the [CLS] token within an attention-based MIL aggregator—consistently and substantially improves slide-level accuracy while reducing trainable parameters and training instability. Concretely, we insert a learnable [CLS] query token that attends to instance embeddings and we freeze the rest of the aggregator and the patch encoder; we also introduce a CLS-gate that calibrates attention logits without changing the backbone. Across three public WSI benchmarks and multiple backbones, CLS-tuning yields +4.02 to +6.34 absolute accuracy gains over strong attention-MIL baselines. We further provide a concise proof that linear combinations of bag features need not be linearly separable, clarifying why learned feature mappings (such as those induced by CLS-tuned attention) can recover linear separability at the bag level. Our approach is drop-in, architecture-agnostic, and training-efficient, making it attractive for large-scale WSI deployment.

---

## 论文详细总结（自动生成）

# 论文总结：CLS-Tuned Attention for Whole-Slide Image Classification

## 1. 论文核心问题与整体含义
- **研究背景**：全切片图像（WSI）分类常被建模为多实例学习（MIL）问题，其中一张切片（包）只要包含至少一个阳性小块（实例）即被标记为阳性。基于注意力的MIL聚合器已成为主流，因为它能同时产生切片级别预测和实例级别的注意力图。
- **核心问题**：现有注意力MIL模型参数较多、训练不稳定，且注意力图的可解释性尚未得到充分优化，未能充分发挥注意力机制在定位显著区域和提升分类精度上的潜力。
- **整体含义**：本文指出，一个简单却常被忽视的改进——仅微调注意力聚合器中的[CLS]令牌——即可显著提升切片级别分类准确率、降低可训练参数量并缓解训练不稳定，同时生成更聚焦、可解释性更强的注意力图，为显著区域选择提供可靠依据。

## 2. 方法论：核心思想与关键技术细节
- **核心思想**：冻结特征提取器和注意力聚合器中的大部分参数，只引入并微调一个可学习的[CLS]查询令牌（query token），通过该令牌对实例嵌入进行注意力计算，同时加入CLS门控机制校准注意力logits，而不修改骨干网络。
- **关键技术细节**：
  - 在基于注意力的MIL聚合器中插入一个可学习的[CLS]查询令牌，该令牌与实例嵌入交互，通过注意力机制汇聚包级特征。
  - 除[CLS]令牌和相关门控参数外，冻结整个聚合器及上游的patch编码器，大幅减少可训练参数。
  - 引入CLS门控，用于重新校准原始的注意力logits，提高注意力聚焦能力，且不改变骨干网络结构。
  - 该方法是一种即插即用的方法，与架构无关，且训练高效。

## 3. 实验设计：数据集、基准与对比方法
- **数据集**：三个公开的WSI基准数据集（具体名称摘要未列出，但声明为“three public WSI benchmarks”）。
- **基准对比方法**：强注意力MIL基线方法（strong attention-MIL baselines），以及多种骨干网络（multiple backbones）。
- **实验设置**：在多个数据集上评估切片级别的分类性能，并使用注意力图进行定性与定量分析，验证方法在准确率、参数效率和注意力质量上的提升。

## 4. 资源与算力
- 论文摘要中未明确提及所使用的GPU型号、数量、训练时长等算力细节。文中仅强调方法“training-efficient”（训练高效），但未给出具体算力数据。

## 5. 实验数量与充分性
- **实验范围**：跨越三个公开WSI基准数据集，使用多种骨干网络进行验证，并且以强注意力MIL模型作为基线进行对比。
- **消融实验**：摘要未详细描述消融实验的具体内容，但指出方法通过冻结参数和引入CLS门控取得了显著改进，暗示可能进行了相关消融研究（如对比仅微调[CLS]令牌与全参数训练等）。
- **充分性与公平性**：从摘要看，实验设计较为全面，覆盖多种数据集和骨干网络，采用绝对精度提升作为指标（+4.02 to +6.34 absolute accuracy gains），对比基线为公认的强注意力MIL方法，具备一定的客观性和公平性。但缺少对统计显著性、误差线等细节的描述。

## 6. 主要结论与发现
- 仅微调[CLS]令牌和引入CLS门控，即可在多个WSI基准上将分类准确率绝对提升4.02至6.34个百分点。
- 该方法大幅减少了可训练参数，缓解了训练不稳定性。
- 注意力图变得更加聚焦和可解释，有利于显著区域选择。
- 理论上证明，包特征的线性组合不一定线性可分，而通过学习得到的特征映射（如CLS微调注意力诱导的映射）能够恢复包级别的线性可分性，进一步解释了方法有效性的机理。
- 该方法为即插即用，架构无关，训练高效，适合大规模WSI部署。

## 7. 优点
- **简单有效**：仅通过微调一个[CLS]令牌和改进注意力校准，带来显著性能提升，实现复杂度低。
- **参数效率高**：冻结大部分参数，极大减少可训练参数量。
- **可解释性增强**：生成更聚焦的注意力图，能更准确地定位病变区域。
- **理论支撑**：提供了简洁的证明说明特征映射对包级别线性可分性的恢复作用，增强了方法的理论深度。
- **实用性强**：方法为即插即用，不依赖特定架构，易于集成到现有WSI分类流程中。

## 8. 不足与局限
- **数据集细节未公开**：摘要仅提及“三个公开WSI基准”，未给出具体名称（如TCGA、Camelyon等），无法判断数据多样性（不同癌症类型、染色方式等）和实验的代表性。
- **算力成本未量化**：没有说明训练所需的GPU资源或时间，难以评估实际部署的资源需求。
- **可能缺少与最新方法的对比**：仅与强注意力MIL基线比较，未提及是否对比了当前最先进的自监督MIL或图MIL方法。
- **注意力图评估的客观性**：虽然声称注意力图更聚焦，但缺少定量指标（如与病理学家标注的对比）验证其可解释性的提升。
- **理论证明适用边界未说明**：关于线性可分性的证明可能依赖于特定假设，实际WSI数据的噪声和异质性可能影响结论的普适性。
- **应用限制**：方法主要针对基于注意力的MIL聚合器，若未来主流聚合器发生根本改变，该技术可能需要重新适配。

（完）
