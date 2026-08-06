---
title: Sequential Attention-based Sampling for Histopathological Analysis
title_zh: 面向组织病理分析的序贯注意力采样
authors: "Tarun G, Naman Malpani, Gugan Thoppe, Devarajan Sridharan"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=wlqoUpuQrv"
tags: ["query:path-xai-sel"]
score: 6.0
evidence: 基于强化学习的采样选择WSI中有信息的图块，与数字病理中重要区域挑选相关。
tldr: 针对WSI数据量巨大且标注稀缺的问题，提出SASHA框架，利用深度强化学习以序贯注意力方式自动选取具有诊断意义的区域，从而以较低计算代价实现整张切片的分析。该方法在效率与诊断准确率之间取得平衡，为大规模病理图像分析提供了有效工具。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
motivation: WSI尺寸巨大，诊断标签仅在切片级，且有诊断价值的区域占比小，全高清分析不现实。
method: 提出SASHA，采用深度强化学习序贯地关注并采样重要区域。
result: 通过选择性采样实现高效分析，但摘要未列出具体性能数据。
conclusion: SASHA能够在维持诊断精度的同时显著降低计算负担。
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

# 论文总结：SASHA – 面向组织病理分析的序贯注意力采样

## 1. 论文的核心问题与整体含义
- **核心问题**：全切片图像（WSI）尺寸巨大（吉像素级），完全以高分辨率进行分析计算代价极高；同时，标注仅在切片级别可用，而有诊断价值的区域只占整张切片的很小部分。
- **整体含义**：提出一种基于深度强化学习的智能采样方法SASHA，通过序贯地关注并放大少数（10%~20%）高分辨率图块，以极低的计算与内存开销实现与全高清分析相媲美的诊断准确率。

## 2. 论文提出的方法论
- **核心思想**：将WSI分析建模为序贯决策过程，利用深度强化学习代理智能选择“值得高分辨率观察”的图块，避免对整张切片全高清处理。
- **关键技术细节**（基于摘要）：
  - 第一阶段：使用轻量级的层次化、基于注意力的多实例学习（MIL）模型学习具有诊断信息量的特征表示。
  - 第二阶段：基于学习到的特征，智能采样并选择性放大少量高分辨率图块（10-20%），做出可靠的切片级诊断。
  - 方法整体称为 **SASHA**（Sequential Attention-based Sampling for Histopathological Analysis）。
- 算法优化目标：在维持诊断精度的同时，显著降低计算与内存成本。

## 3. 实验设计
- **数据集/场景**：从摘要未披露具体数据集名称；元数据显示为“数字病理中重要区域挑选相关”。
- **Benchmark与对比方法**：
  - 与**全高清分析WSI的SOTA方法**对比。
  - 与**竞争性稀疏采样方法**对比。
- **实验结论（基于摘要）**：SASHA在极低的计算与内存开销下匹配全高清SOTA性能，并显著优于其他稀疏采样方法。

## 4. 资源与算力
- 摘要和元数据**未明确说明GPU型号、数量或训练时长**等资源信息。
- 仅提及“计算和内存成本”仅为SOTA方法的一部分（fraction）。

## 5. 实验数量与充分性
- 摘要未报告具体实验组数。从描述推断，至少包含：
  - 主流全高清SOTA对比；
  - 稀疏采样方法对比；
  - 可能包含不同采样比例（10-20%）的实验。
- 论文被NeurIPS 2025收录（元数据给出），通常意味着实验设计经过同行评审，具有一定充分性。但无法从摘要判断消融实验或统计检验细节是否完备。

## 6. 论文的主要结论与发现
- SASHA能够以远低于全高清方案的资源消耗，达到与全高清分析SOTA相媲美的诊断性能。
- 相比其他稀疏采样方法，SASHA具有显著优势。
- 该方法适用于医学影像中具有稀疏信息特征的大图像自动诊断问题。

## 7. 优点
- **效率高**：仅放大10-20%区域即可诊断，大幅降低计算和内存需求。
- **智能采样策略**：基于强化学习的序贯注意力机制，能动态关注信息量最大的区域。
- **可复现性**：代码已开源，模型实现公开可获取。

## 8. 不足与局限
- **实验覆盖**：摘要未提供具体数据集、诊断任务类型及性能数值，无法评估其跨中心泛化能力。
- **偏差风险**：仅依赖切片级弱标签，可能忽略细粒度注释中更复杂的模式；强化学习策略可能对奖励函数设计敏感。
- **应用限制**：仍需要训练MIL特征提取器，初始训练阶段仍需消耗一定资源；摘要未讨论对罕见类别或边界情况的鲁棒性。
- **信息不详**：由于提供的文本仅限摘要和元数据，无法对实验设计细节、消融研究、超参数敏感度等进行深入评估。

（完）
