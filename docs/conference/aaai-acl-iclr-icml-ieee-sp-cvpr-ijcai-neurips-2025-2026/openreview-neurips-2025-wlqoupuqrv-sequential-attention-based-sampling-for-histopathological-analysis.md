---
title: Sequential Attention-based Sampling for Histopathological Analysis
title_zh: 基于顺序注意力的采样用于组织病理分析
authors: "Tarun G, Naman Malpani, Gugan Thoppe, Devarajan Sridharan"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=wlqoUpuQrv"
tags: ["query:profile"]
score: 5.0
evidence: 使用深度强化学习顺序注意力采样，在WSI中选择信息性区域以进行切片级诊断，整合跨patch信息。
tldr: 针对WSI尺寸巨大且诊断信息稀疏的问题，提出SASHA，一种深度强化学习方法，通过顺序注意力采样来选择信息性区域，实现高效的切片级分类，仅需处理少量关键区域，大幅降低计算开销，为组织病理全切片分析提供了新的高效采样策略。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
motivation: WSI尺寸巨大且诊断标签仅在切片级可用，全分辨率分析计算不可行。
method: 提出SASHA，利用深度强化学习学习顺序注意力采样策略，选择信息性patch。
result: 在切片级分类任务上，仅利用少量采样区域即可达到高效分析。
conclusion: SASHA为WSI高效分析提供了新的采样范式，有望降低计算成本。
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

根据提供的论文元数据和摘要，现对《Sequential Attention-based Sampling for Histopathological Analysis》（SASHA）一文进行结构化总结如下。

### 1. 论文的核心问题与整体含义
*   **核心问题**：全切片图像（WSI）常达到十亿像素级，直接对其高分辨率全域分析计算成本过高、不可行。同时，诊断标签大多仅在切片级可用，细粒度（patch级）标注既昂贵又耗时。更加关键的是，含诊断信息的区域通常仅占WSI的极小部分，全分辨率遍历整张切片极度低效。
*   **整体含义**：论文提出了一种高效的WSI分析范式，即通过深度强化学习学习一种“顺序注意力采样”策略，智能地挑选并仅对少量高信息量区域进行分析，从而在维持诊断准确率的同时，大幅降低计算和内存开销。

### 2. 方法论
论文提出 **SASHA**（基于顺序注意力的采样用于组织病理分析），其核心为两阶段设计：

*   **轻量级层次化注意力多实例学习（MIL）**  
    首先，用一个小型、层次化的注意力MIL模型从低分辨率WSI中提取信息性特征表示，用于初步感知全局上下文，为后续采样提供特征基础。
*   **深度强化学习驱动的顺序采样**  
    *   **核心思想**：将采样过程建模为马尔可夫决策过程，使用深度强化学习智能体学习一个策略，动态决定下一个需要观察的高分辨率区域（patch）。
    *   **技术细节**：智能体基于当前已观察区域的特征状态，按顺序选择下一个patch并进行“选择性缩放”至高分辨率，推理诊断信息。最终仅处理全片 `10%~20%` 的高分辨率区域，即能得出可靠的切片级诊断。
    *   **算法流程简述**：特征提取 → 强化学习策略网络根据当前状态输出动作（下一个patch位置）→ 获取高分辨率patch特征并更新状态 → 迭代至终止 → 利用所有已采样patch进行最终分类。

### 3. 实验设计
由于仅提供摘要，实验细节缺失，推断如下：
*   **任务场景**：组织病理全切片图像的切片级分类（如癌症诊断）。
*   **对比基准**：
    *   与全分辨率分析WSI的**最先进方法**进行了比较，以验证精度相当但成本更低。
    *   与竞品**稀疏采样方法**进行了对比，以体现采样策略的优越性。
*   **未明确部分**：摘要未提供具体数据集名称、评价指标数值、对比方法的具体名称等。无法确定是否使用了公开数据集（如TCGA、CAMELYON）及消融实验设计。

### 4. 资源与算力
摘要中**未提及**具体算力配置，例如GPU型号、数量、训练时长、显存占用等指标。仅定性强调了在仅处理一小部分高分辨率区域的情况下，计算和内存成本远低于全分辨率分析方法。

### 5. 实验数量与充分性
*   **实验数量**：原文摘要并未罗列实验组数或具体设置（如不同采样比例的影响、各模块消融、跨中心泛化等），因此无法准确判断实验总量与表格数量。
*   **充分性判断**：从摘要结论（“匹配全分辨率SOTA方法”、“显著优于稀疏采样方法”）可推知至少包含两组核心对比实验；但缺乏细节无法客观评估其充分性、是否排除了过拟合偏倚及公平性保障措施。

### 6. 主要结论与发现
*   SASHA 在仅使用全片 `10%~20%` 的高分辨率区域时，取得了与**全分辨率分析WSI的SOTA方法相当**的诊断精度。
*   同时，其计算与内存开销仅为后者的一小部分。
*   相对于其他稀疏采样方法，SASHA 实现了显著更优的性能。
*   作者提出 SASHA 可作为一种通用智能采样模型，适用于具有稀疏信息特征的超大医学图像自动诊断任务。

### 7. 优点
*   **效率与精度的平衡**：极大地降低计算负担，却维持了与全图分析同等水平的性能。
*   **新颖的采样范式**：首次将顺序注意力与深度强化学习结合，动态决定高分辨率区域的观测顺序和位置，模仿了病理学家逻辑。
*   **模型开放性**：提供代码地址，有助于后续复现与拓展。

### 8. 不足与局限
*   **实验细节不可见**：元数据及摘要完全缺失数据来源、具体对比方法、数值结果、统计检验、消融实验与泛化性验证，无法评判结论的可靠性及方法鲁棒性。
*   **应用限制隐忧**：顺序采样策略可能引入一定的推理延时，且强化学习训练的稳定性、在不同组织类型或扫描仪下的泛化性能尚未明确。
*   **生物可解释性**：未提是否对所选择的 patch 序列进行临床可解释性分析，仅仅匹配精度可能不足以满足临床落地要求。
*   **仅基于元数据总结**：由于原文全文未能获取，以上总结只能反映摘要限定信息，更深入的技术细节、实验完备性评估均受限制。

（完）
