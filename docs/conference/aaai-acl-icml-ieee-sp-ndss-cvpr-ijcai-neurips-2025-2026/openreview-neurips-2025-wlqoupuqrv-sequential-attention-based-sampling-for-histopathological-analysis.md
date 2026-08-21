---
title: Sequential Attention-based Sampling for Histopathological Analysis
title_zh: 基于序列注意力的组织病理学分析采样方法
authors: "Tarun G, Naman Malpani, Gugan Thoppe, Devarajan Sridharan"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=wlqoUpuQrv"
tags: ["query:cell-path"]
score: 6.0
evidence: 基于强化学习的注意力采样用于组织病理学WSI分析
tldr: 针对千兆像素WSI分析中诊断信息稀疏且标注少的问题，提出SASHA，一种基于深度强化学习的序列注意力采样方法，学习定位高信息量的感兴趣区域进行高效分析。该方法在减少计算量的同时保持诊断性能。其注意力采样策略可用于组织病理学图像的快速分析，但未针对细胞级特征进行建模。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
motivation: WSI全分辨率分析计算不可行，且诊断信息只集中在少数区域。
method: 提出SASHA，用深度强化学习进行序列注意力采样定位信息区域。
result: 实现高效组织病理学图像分析，提高计算效率。
conclusion: 为WSI分析提供智能采样范式，是计算病理学的高效工具。
---

## Abstract
Deep neural networks are increasingly applied in automated histopathology. Yet, whole-slide images (WSIs) are often acquired at gigapixel sizes, rendering them computationally infeasible to analyze entirely at high resolution. Diagnostic labels are largely available only at the slide-level, because expert annotation of images at a finer (patch) level is both laborious and expensive. Moreover, regions with diagnostic information typically occupy only a small fraction of the WSI, making it inefficient to examine the entire slide at full resolution.
Here, we propose SASHA -- Sequential Attention-based Sampling for Histopathological Analysis -- a deep reinforcement learning approach for efficient analysis of histopathological images. 
First, SASHA learns informative features with a lightweight hierarchical, attention-based multiple instance learning (MIL) model. 
Second, SASHA samples intelligently and zooms selectively into a small fraction (10-20\%) of high-resolution patches to achieve reliable diagnoses.
We show that SASHA matches state-of-the-art methods that analyze the WSI fully at high resolution, albeit at a fraction of their computational and memory costs. In addition, it significantly outperforms competing, sparse sampling methods. 
We propose SASHA as an intelligent sampling model for medical imaging challenges that involve automated diagnosis with exceptionally large images containing sparsely informative features. Model implementation is available at: https://github.com/coglabiisc/SASHA.

---

## 论文详细总结（自动生成）

# 论文总结：SASHA——基于序列注意力的组织病理学分析采样方法

> 说明：以下内容主要依据论文摘要与元数据整理。由于提供的 PDF 提取文本仅包含 OpenReview 验证页面，未能获取正文、图表和实验细节，因此部分条目将明确标注“未提供”或“无法从摘要判断”。

## 1. 论文的核心问题与整体含义（研究动机和背景）

- **核心问题**：全切片图像（WSIs）通常达到千兆像素级别，在全分辨率下完整分析在计算上不可行。
- **标注困难**：诊断标签大多只在切片级（slide-level）可用，细粒度（patch 级）专家标注既费力又昂贵。
- **信息稀疏性**：具有诊断价值的区域通常只占整张 WSI 的很小一部分，全分辨率检查整张切片效率低下。
- **整体含义**：需要一种智能采样策略，只选择少量高分辨率、高信息量的区域进行分析，从而在保持诊断性能的同时大幅降低计算与内存成本。
- **论文目标**：提出 SASHA，即 Sequential Attention-based Sampling for Histopathological Analysis，用深度强化学习实现高效、稀疏但可靠的病理图像分析。

## 2. 论文提出的方法论

- **核心思想**：将 WSI 分析建模为序列决策问题，通过深度强化学习智能选择少量高分辨率 patch，而不是均匀或全分辨率扫描整张切片。
- **关键技术细节（来自摘要）**：
  - 首先，SASHA 使用一个**轻量级的分层注意力多实例学习（MIL）模型**学习信息性特征。
  - 其次，SASHA 进行**智能采样**，并**选择性地放大**一小部分（10–20%）高分辨率 patch，以实现可靠诊断。
  - 该过程本质上是一个**序列注意力采样**机制：模型逐步关注最可能包含诊断信息的区域。
- **算法流程（文字说明）**：
  1. 利用分层注意力 MIL 模型从 WSI 中提取/学习特征表示。
  2. 基于强化学习的采样策略根据当前观察选择下一步要检查的区域。
  3. 对选中的少量高分辨率 patch 进行高倍放大与分析。
  4. 汇总所选区域的信息，输出切片级诊断结果。
- **公式或网络结构细节**：由于未能获取正文，具体的奖励函数、状态/动作定义、注意力聚合公式、网络结构、训练策略等**均未在摘要中给出**。

## 3. 实验设计

- **数据集 / 场景**：摘要未列出具体数据集名称。结合领域背景，可能涉及组织病理学 WSI 数据集，但**无法从提供内容确认**。
- **Benchmark 设置**：
  - 与**在全分辨率下完整分析 WSI 的 state-of-the-art 方法**进行比较。
  - 与**竞争性的稀疏采样方法**进行比较。
- **对比方法类别**：
  - 全分辨率 SOTA 方法：作为性能上界参考。
  - 稀疏采样方法：作为同类高效分析方法的直接对比。
- **主要评估维度**：
  - 诊断性能（是否匹配全分辨率 SOTA）。
  - 计算成本和内存成本（相比全分辨率方法的降低幅度）。
- **具体指标、数据集划分、统计检验等**：未在摘要中提供。

## 4. 资源与算力

- **未明确说明**。
- 摘要中未提及 GPU 型号、GPU 数量、训练时长、显存占用、推理速度等算力信息。
- 尽管摘要声称“以一小部分计算和内存成本匹配 SOTA”，但具体数值和硬件配置需要在正文中确认。

## 5. 实验数量与充分性

- **实验数量**：摘要未给出具体实验组数。可确认的实验方向至少包括：
  - 与全分辨率 SOTA 方法的对比实验。
  - 与稀疏采样方法的对比实验。
  - 可能包含不同采样比例（10–20%）的配置实验，但摘要未明确。
- **充分性**：从摘要难以判断实验是否充分。需要正文中的消融实验、多数据集验证、敏感性分析等才能客观评估。
- **客观性与公平性**：摘要仅报告“匹配 SOTA”和“显著优于稀疏采样方法”，但未提供具体指标、误差范围或统计显著性，暂时无法评价实验公平性。

## 6. 论文的主要结论与发现

- **性能匹配**：SASHA 能够匹配在全分辨率下完整分析 WSI 的 state-of-the-art 方法。
- **成本优势**：相比全分辨率方法，SASHA 的计算和内存成本显著降低。
- **优于稀疏采样**：SASHA 显著优于现有的竞争性稀疏采样方法。
- **适用范围**：SASHA 被提出作为一类智能采样模型，适用于包含稀疏信息特征的超大医学图像的自动诊断任务。
- **可用性**：模型实现已在 GitHub 开源：https://github.com/coglabiisc/SASHA。

## 7. 优点（方法或实验设计亮点）

- **计算效率高**：通过只分析 10–20% 的高分辨率 patch，显著降低计算和内存开销。
- **智能采样策略**：使用深度强化学习进行序列决策，比均匀采样或随机采样更具针对性。
- **结合 MIL 与 RL**：先通过注意力 MIL 提取特征，再让 RL 进行选择性放大，形成分层、渐进的分析流程。
- **性能不妥协**：在稀疏采样条件下仍能匹配全分辨率 SOTA，表明采样策略有效保留了诊断信息。
- **针对信息稀疏性**：明确针对 WSI 中诊断区域只占很小一部分的特点设计，具有实际临床计算病理学价值。
- **可复现性**：提供了开源代码。

## 8. 不足与局限

- **正文细节缺失**：本次提供的文本未能包含完整论文，无法评估网络结构、训练稳定性、奖励设计等关键技术细节。
- **数据集未知**：摘要未列出具体数据集，泛化性和临床代表性无法判断。
- **未针对细胞级特征建模**：根据元数据提示，该方法未针对细胞级特征进行专门建模；若某些诊断依赖细胞形态细节，采样粒度可能不够。
- **稀疏采样风险**：只分析 10–20% 的 patch，理论上可能漏掉小而关键的诊断区域，尤其是在病灶极微小或弥散分布时。
- **对比实验信息有限**：摘要未给出具体对比方法名称、指标数值、统计显著性和误差棒，难以评估结论的稳健性。
- **应用限制**：作为研究性方法，从匹配 SOTA 到临床部署之间仍可能存在泛化、解释性和监管层面的差距。

（完）
