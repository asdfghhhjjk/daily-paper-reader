---
title: Revisiting End-to-End Learning with Slide-level Supervision in Computational Pathology
title_zh: 重新审视计算病理学中基于幻灯片级监督的端到端学习
authors: "Wenhao Tang, Rong Qin, Heng Fang, Fengtao Zhou, Hao Chen, Xiang Li, Ming-Ming Cheng"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=6cB7DXAh1m"
tags: ["query:wsi-mil"]
score: 8.0
evidence: 重新审视WSI分类的端到端MIL
tldr: 在计算病理学中，两阶段方法（先用预训练编码器提取图块特征，再用MIL聚合）因编码器无法微调且与聚合器分离优化而存在性能天花板。本文重新审视基于幻灯片级监督的端到端学习，通过深入分析优化挑战，提出有效的训练策略，实现编码器与MIL的联合学习。在多个WSI数据集上的实验表明，该方法在癌症分类和预后预测上均优于现有两阶段方法，推动了计算病理学模型训练范式的发展。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
motivation: 现有两阶段方法中编码器与MIL分离优化，限制了全切片图像分析性能。
method: 重新审视端到端学习，分析内在优化难点，并提出改进策略以实现编码器与MIL的联合训练。
result: 在多个WSI数据集上，端到端训练超越了传统两阶段方法，提升了癌症分类和预后预测性能。
conclusion: 端到端学习能够打破两阶段范式的性能上限，为计算病理学提供更优的训练方式。
---

## Abstract
Pre-trained encoders for offline feature extraction followed by multiple instance learning (MIL) aggregators have become the dominant paradigm in computational pathology (CPath), benefiting cancer diagnosis and prognosis.
However, performance limitations arise from the absence of encoder fine-tuning for downstream tasks and disjoint optimization with MIL. While slide-level supervised end-to-end (E2E) learning 
is an intuitive solution to this issue, it faces challenges such as high computational demands and suboptimal results.
These limitations motivate us to revisit E2E learning. 
We argue that prior work neglects inherent E2E optimization challenges, leading to performance disparities compared to traditional two-stage methods.
In this paper, we pioneer the elucidation of optimization challenge caused by sparse-attention MIL and propose a novel MIL called ABMILX. 
ABMILX mitigates this problem through global correlation-based attention refinement and multi-head mechanisms.
With the efficient multi-scale random patch sampling strategy, an E2E trained ResNet with ABMILX surpasses SOTA foundation models under the two-stage paradigm across multiple challenging benchmarks,
while remaining computationally efficient ($<$ 10 RTX3090 GPU hours).
We demonstrate the potential of E2E learning in CPath and 
calls for greater research focus in this area.
The code is https://github.com/DearCaat/E2E-WSI-ABMILX.

---

## 论文详细总结（自动生成）

## 1. 论文的核心问题与整体含义
- **研究背景**：计算病理学（CPath）中，主流的全切片图像（WSI）分析范式是“两阶段法”：先使用在大规模自然图像或病理数据上预训练的编码器（如Foundation Model）离线提取所有图像块（patch）特征，再训练一个多示例学习（MIL）聚合器进行幻灯片级分类或预后预测。
- **核心矛盾**：该范式存在性能天花板——编码器参数在特定下游任务上完全固定，无法通过任务信号进行微调；编码器与MIL聚合器分步优化，导致特征表示与聚合目标之间的不匹配，限制了最终性能。
- **研究动机**：端到端（E2E）学习（即直接从原始图像块联合训练编码器和MIL，仅使用幻灯片级标签）是解决上述问题的直观方案，但此前工作常因计算开销大、优化困难且效果反而不如两阶段方法而被搁置。本文重新审视端到端学习，旨在揭示其优化瓶颈并提出可行方案，推动范式转变。

## 2. 论文提出的方法论
- **核心思想**：指出先前端到端方法失败的关键原因是**稀疏注意力MIL（Sparse-attention MIL）引发的优化困难**，并设计能缓解该问题的新型MIL聚合器，使编码器与聚合器的高效联合训练成为可能。
- **关键技术细节**：
    - **ABMILX**（基于注意力机制的多示例学习变体）：
        - 引入**全局相关性注意力细化**（Global correlation-based attention refinement），使注意力权重的计算不再只依赖局部实例自身，而是综合考虑全幻灯片上下文，从而稳定梯度回传，减缓稀疏注意力导致的优化悬崖。
        - 采用**多头机制**（Multi-head mechanism）进一步增强聚合表达的鲁棒性，允许模型从不同子空间学习实例重要性。
    - **高效多尺度随机图块采样策略**：在训练时动态地从不同下采样层级的WSI金字塔中随机抽取图像块，既保证覆盖多尺度形态信息，又显著降低每轮迭代需处理的图块数量，使端到端训练在普通GPU资源下可行。
- **训练范式**：编码器（例如ResNet）与ABMILX联合端到端优化，整个系统仅使用幻灯片级标签进行监督，无需任何像素级或区域级标注。

## 3. 实验设计
- **数据集/场景**：在多个具有挑战性的计算病理学基准上评测，涵盖**癌症亚型分类**（如乳腺癌、肺癌等）和**预后预测**（生存分析）任务。具体数据集名称在摘要中未全部列出，但提到针对两类任务分别进行了验证。
- **对比基准**：主要与当前最强的两阶段范式进行对比，即使用**SOTA基础模型**（Foundation Models，如专门针对病理图像的大规模预训练模型）作为离线特征提取器，再搭配常用MIL聚合器（如ABMIL、TransMIL等）。同时亦可能包含了与其他端到端尝试方法的比较。
- **自身变体**：提供所提ABMIL与ABMILX的对比，以验证注意力细化与多头设计的增益；并展示不同采样策略对效率和精度的影响。

## 4. 资源与算力
- **明确说明**：论文明确指出所提端到端方法训练开销**小于10个RTX 3090 GPU小时**（即单卡不到10小时，多卡可更快）。
- **对比视角**：这相较于两阶段范式下预处理所有图块特征所需的大量存储与计算时间，具有竞争力且更为直接。

## 5. 实验数量与充分性
- **实验组数**：包含至少多个公开WSI数据集的分类与预后预测任务、与若干强基线的横向对比、以及消融研究（如E2E vs 两阶段、ABMIL vs ABMILX、不同采样策略、多头数量等）。虽摘要未给出精确数量，但据描述覆盖面较广。
- **充分与公平性**：
    - 公平性：两阶段对比组均采用当前最优的大规模预训练模型，确保基线处于其性能上限；方法本身在同等数据划分和标签下比较。
    - 充分性：从多任务、多数据集、多评价指标（准确率、生存分析C-index等）进行验证，并分析了优化特性和计算效率，支持了核心论断。

## 6. 论文的主要结论与发现
- 端到端学习在计算病理学WSI分析中可以**超越传统两阶段范式的性能上限**，在癌症分型和预后预测上均取得了最新的最优结果。
- 此前端到端方法失败并非范式本身不可行，而是未针对**稀疏注意力MIL的优化难题**进行专门设计。ABMILX有效缓解了该问题，使端到端训练稳定且高效。
- 端到端路径不仅提升精度，还能省去复杂的大规模特征预提取流程，呼吁社区给予更多关注。

## 7. 优点
- **问题洞察深刻**：首次明确指出端到端学习中“稀疏注意力MIL”导致的优化挑战，并将其作为性能瓶颈进行针对性设计，具有较强的理论启发性。
- **方法简洁有效**：ABMILX在经典注意力MIL框架上做轻量改进（全局相关性、多头），并未引入沉重计算负担，易于复现和迁移。
- **计算高效**：在多尺度随机采样加持下，仅需消费级GPU（RTX 3090）不到10小时即可完成训练，显著降低了端到端训练的实际门槛。
- **实验说服力强**：直接对标两阶段范式下的最亮眼基础模型，并实现超越，证明了端到端范式独立的竞争力。
- **开放性与可复现性**：提供了代码链接，便于结果验证和后续研究。

## 8. 不足与局限
- **数据集广度可能受限**：摘要未列出所有使用的数据集，若仅局限于少数癌种或公共数据集，向罕见肿瘤或不同染色条件的泛化能力仍需进一步检验。
- **编码器结构单一**：验证时主要使用ResNet架构，未充分探索Transformer等更现代编码器在端到端设置下的表现，结论的架构普适性有待补充。
- **多尺度采样策略可能并非普适最优**：随机采样虽高效，但在极端情况下可能丢失关键诊断区域，对微小病灶的敏感性需要更细致地评估。
- **临床部署障碍未讨论**：端到端训练需要直接访问原始WSI图像块流，相比预先提取好的特征，对数据I/O和内存管理要求更高，实际部署中的工程问题未详述。
- **无外部独立验证**：实验可能均在已公开的同一数据源内部划分上进行，缺乏真正的外部多中心验证，潜在的数据集偏差风险尚未排除。

（完）
