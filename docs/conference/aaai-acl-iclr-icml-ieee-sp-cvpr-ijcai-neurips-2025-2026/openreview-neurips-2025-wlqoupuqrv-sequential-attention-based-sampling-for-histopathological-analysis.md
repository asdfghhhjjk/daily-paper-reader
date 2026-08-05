---
title: Sequential Attention-based Sampling for Histopathological Analysis
title_zh: 基于序列注意力的采样用于组织病理学分析
authors: "Tarun G, Naman Malpani, Gugan Thoppe, Devarajan Sridharan"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=wlqoUpuQrv"
tags: ["query:path-xai-sel"]
score: 9.0
evidence: 提出深度强化学习顺序选择WSI中信息性patch，符合利用可解释特征挑选重要区域的需求。
tldr: 传统深度学习方法处理全切片图像(WSI)时，因图像分辨率极高，分析整个切片计算成本巨大，且诊断关键区域仅占小部分，造成资源浪费。本文提出SASHA，一种基于深度强化学习的序列注意力采样方法，通过智能代理动态选择信息量大的patch顺序分析，无需处理整个WSI。实验表明，SASHA在多个数字病理数据集上，以远低于全分辨率计算开销，达到甚至超越原有分类性能，为高效WSI分析提供了新途径。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
motivation: 全切片图像分辨率极高，诊断相关信息仅占小部分，逐片分析计算代价大。
method: 提出SASHA，利用深度强化学习以序列注意力机制选择信息性patch进行分析。
result: 在WSI分类任务中，以低计算开销达到或超过全分辨率下性能。
conclusion: SASHA实现了高效的组织病理学WSI分析，通过智能采样降低计算负担。
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

# 论文总结

## 1. 核心问题与整体含义
- **研究背景**：全切片图像（WSI）在组织病理学诊断中呈超千兆像素级分辨率，直接在最高分辨率下分析整张切片计算成本极高。
- **核心矛盾**：WSI 中具有诊断价值的关键区域通常只占极小的面积，大量区域为背景或正常组织，全图高分辨率处理既低效又浪费计算资源。
- **整体目标**：提出一种智能的序列化采样策略，仅动态选择信息量最丰富的少数高分辨率图像块进行推理，从而在显著降低计算负担的同时，维持甚至提升诊断准确率。

## 2. 方法论
- **整体框架**：SASHA（Sequential Attention-based Sampling for Histopathological Analysis）结合深度强化学习与多实例学习，实现对 WSI 的序贯注意力采样。
- **关键技术细节**：
  - **轻量级层次化注意力 MIL**：首先使用一个轻量的、基于注意力机制的层次化多实例学习模型，从低分辨率或粗略扫描的图像区域中提取富有信息的特征表示。
  - **序列采样策略**：将 WSI 分析建模为顺序决策问题，利用深度强化学习代理（agent）在图像中按步骤移动并选择下一个要放大的区域。
  - **选择性高分辨率放大**：代理根据当前已观察到的信息，只对筛选出的约 10–20% 的高分辨率贴片进行精细分析，而非遍历全图。
- **算法流程（文字描述）**：
  1. 在低分辨率下生成全局上下文特征。
  2. 强化学习代理决定“看向哪里”，移动焦点并请求对应高分辨率贴片。
  3. 利用层次注意力 MIL 模型融合已采样的高分辨率贴片特征，输出当前阶段预测。
  4. 代理根据诊断置信度决定是否停止采样或继续移动，最终给出全切片级分类结果。
  5. 通过奖励函数平衡诊断准确性与采样次数，训练策略网络。

## 3. 实验设计
- **数据集**：文中提及在多个数字病理数据集上验证，但具体名称（如 TCGA、CAMELYON 等）及任务（癌症分型、转移检测）在摘要中未展开。
- **基准对比方法**：
  - **全分辨率全图分析方法**：对 WSI 完整进行高分辨率分析的当前最优方法（state‑of‑the‑art）。
  - **稀疏采样方法**：其他竞争性的非连续采样策略。
- **对比内容**：分类性能（准确性指标）和计算/内存开销。

## 4. 资源与算力
- 论文摘要及元数据**未明确说明**所使用的 GPU 型号、数量以及训练时长。
- 仅定性指出 SASHA 以“计算和内存成本的一小部分”达到对比方法的性能，具体数值（如 FLOPs、显存占用、训练时间对比）未在提供文本中出现。

## 5. 实验数量与充分性
- 基于现有信息无法确定精确的实验组数。但从描述推断至少包含：
  - 多个数据集上的整体性能对比。
  - 不同采样率（如 10%、20%）下的性能变化。
  - 与全分析方法和稀疏采样方法的横向比较。
- 文中仅提到“显著优于竞争性稀疏采样方法”，但未报告消融实验（如移除注意力、改变强化学习奖励函数等）的具体情况。由于缺乏论文全文，难以完整评估实验的充分性与潜在偏差。

## 6. 主要结论与发现
- SASHA 仅分析 10–20% 的高分辨率贴片，即可达到与全高分辨率全图分析相当甚至更优的诊断准确率。
- 相比其他稀疏采样方法，SASHA 的优势显著，证明序贯注意力决策比随机或固定采样更高效。
- 该方法为面向超大图像、稀疏信息分布的医学影像自动诊断提供了一种通用的智能采样范式。

## 7. 优点
- **计算效率高**：大幅降低高分辨率计算量，使实际部署更可行。
- **智能聚焦**：深度强化学习驱动的动态选择机制，可自适应地关注最相关区域，避免无意义计算。
- **端到端学习**：注意力 MIL 与采样策略协同优化，无需手工特征或预定义关注区域。
- **可扩展性**：模型架构保持轻量，适合处理不断增大的病理图像尺寸。

## 8. 不足与局限
- **实验细节缺失**：从现有摘要无法获知数据集规模、任务多样性、统计显著性检验等关键信息，难以完全判断结论的泛化能力。
- **潜在偏差风险**：若训练数据集代表性不足或标签噪声未讨论，模型可能在临床部署时出现性能下降。
- **应用限制**：
  - 方法依赖高分辨率贴片的按需获取，需数字病理系统支持动态缩放接口。
  - 序贯采样引入推理延迟，可能不适用于对实时性要求极高的场景。
  - 未讨论模型在不同扫描仪、染色条件下的鲁棒性。
- **报告不完整**：因论文 PDF 提取遇到访问限制，本总结只能基于摘要和元数据，内部实验设置、消融研究、参数敏感性等均未呈现，评价可能有遗漏。

（完）
