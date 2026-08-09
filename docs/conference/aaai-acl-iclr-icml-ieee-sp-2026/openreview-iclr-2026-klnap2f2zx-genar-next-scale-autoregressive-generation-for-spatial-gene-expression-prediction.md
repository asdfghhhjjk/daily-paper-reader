---
title: "GenAR: Next-Scale Autoregressive Generation for Spatial Gene Expression Prediction"
title_zh: GenAR：面向空间基因表达预测的跨尺度自回归生成
authors: "Jiarui Ouyang, Yihui Wang, Yihang Gao, Yingxue Xu, Shu Yang, Hao Chen"
date: 2025-09-15
pdf: "https://openreview.net/pdf?id=KlnAP2F2Zx"
tags: ["query:path-xai-sel"]
score: 8.0
evidence: 多尺度自回归框架从HE图像预测空间基因表达
tldr: "针对H&E图像预测空间基因表达中忽视共表达和连续回归的问题，提出多尺度自回归生成框架，将表达值离散化并分层预测，生成生物学更合理的结果。"
source: ICLR-2026-Public
selection_source: conference_retrieval
motivation: 现有方法独立预测基因，忽略共表达且采用不恰当的连续回归。
method: 构建层次化基因分组，离散化表达统计，多尺度自回归细化。
result: 预测结果更符合生物学实际，优于独立回归方法。
conclusion: "提供了一种更准确的H&E-to-表达预测框架，助力低成本空间组学。"
---

## Abstract
Spatial Transcriptomics (ST) offers spatially resolved gene expression but remains costly. Predicting expression directly from widely available Hematoxylin and Eosin (H&E) stained images presents a cost-effective alternative. However, most computational approaches (i) predict each gene independently, overlooking co-expression structure, and (ii) cast the task as continuous regression despite expression being discrete counts. This mismatch can yield biologically implausible outputs and complicate downstream analyses. We introduce GenAR, a multi-scale autoregressive framework that refines predictions from coarse to fine. GenAR (a) clusters genes into hierarchical groups to expose cross-gene dependencies, (b) models expression as discrete token generation over a fixed vocabulary of integer count tokens to directly predict raw counts, and (c) conditions decoding on fused histological and spatial embeddings. From an information-theoretic view, the discrete formulation operates directly on the physical count scale, and the coarse-to-fine factorization aligns with a principled conditional decomposition. Extensive experimental results on four ST datasets across different tissue types demonstrate that GenAR achieves state-of-the-art performance, offering potential implications for precision medicine and cost-effective molecular profiling. Code will be publicly available.

---

## 论文详细总结（自动生成）

# 论文总结：GenAR — 面向空间基因表达预测的跨尺度自回归生成

## 1. 核心问题与整体含义
*   **研究背景**：空间转录组学可在组织原位捕获基因表达，但实验技术成本高昂。从廉价的苏木精-伊红染色组织图像直接预测空间基因表达，是一种极具吸引力的替代方案。
*   **现有方法的缺陷**：当前计算方法大多存在两个根本性问题：
    *   对每个基因独立预测，完全忽略了基因之间的共表达结构与生物学依赖关系。
    *   将本质为离散计数数据的表达值强行建模为连续回归问题，导致预测结果在生物学上不自然、不合理，并困扰下游分析。
*   **研究动机**：亟需一种能够显式捕捉基因间依赖、且天然适配计数数据特性的生成式框架，从而输出更具生物学真实性的空间表达图谱。

## 2. 方法论
### 核心思想
GenAR 将预测任务重新定义为**多尺度自回归生成问题**：从粗到细逐级生成基因表达值，每一步都以前序生成结果为条件，从而捕捉跨基因依赖关系。

### 关键技术细节
1.  **层次化基因分组**：依据表达模式的相似性，将基因聚类为层次树状分组，使得相近基因共享预测上下文，为跨基因依赖提供结构化先验。
2.  **离散化表达建模**：
    *   将原始的整数表达计数映射到一个固定的 token 词汇表，每个 token 对应一个计数区间。
    *   模型直接预测离散的计数 token，而非连续值，使回归问题转换为更自然的序列生成任务，从信息论角度直接操作在物理计数尺度上。
3.  **从粗到细的自回归解码**：
    *   首先以组织学图像和空间坐标的融合嵌入为条件，预测最高层（最粗粒度）的基因分组表达 token。
    *   随后逐步向下细化，在每一层利用已预测的粗粒度表达作为条件，生成更精细的基因表达。
    *   这种粗到细的分解对应于条件概率的链式分解，保证了建模的严谨性。
4.  **多模态条件嵌入**：解码过程融合了从 H&E 图像提取的组织学特征与空间位置嵌入，为表达生成提供空间上下文。

> *注：论文中应包含精确的概率分解公式和自回归模型架构细节，但此处未提供原文详述。*

## 3. 实验设计
*   **数据集**：在来自不同组织类型的四个空间转录组数据集上进行了评估（具体数据集名称与来源在摘要中未详列）。
*   **基准与对比方法**：将 GenAR 与当前性能最优的预测方法进行比较（摘要指出“achieves state-of-the-art performance”，但未逐个列出对比方法）。对比应涵盖传统的单基因独立回归模型以及可能的其他生成式方法。
*   **评估场景**：实验设计应涵盖了跨组织类型的泛化能力测试，以验证方法在不同生物学背景下均优于逐基因独立预测基线。

## 4. 资源与算力
**文中未明确提及所使用的 GPU 型号、数量或训练时长。** 所有相关硬件与计算资源信息在当前提供的摘要和元数据中均未涉及。

## 5. 实验数量与充分性
*   **实验组数**：基于摘要，至少包含了四组不同数据集上的主实验，并极有可能包含消融实验以验证各组件的贡献（如离散化对比连续回归、自回归分解对比独立预测、层次化分组对比单一水平等）。但具体实验数量与具体设计因正文缺失无法确认。
*   **充分与公平性**：
    *   *充分性*：跨四种组织类型验证已在某种程度上证明了方法的域迁移能力；消融研究若存在，则能支撑关键设计选择。
    *   *客观公平性*：与现有最先进方法的比对应是公平的，但需检查是否统一采用相同的训练/测试划分、图像预处理流程和评估指标，这些细节缺失。

## 6. 主要结论与发现
*   GenAR 在四个多组织数据集上一致地超越了基线方法，取得了最优预测性能。
*   通过多尺度自回归离散生成，模型输出的表达谱更加贴近真实生物学模式，避免了连续回归造成的非自然预测值。
*   该方法为低成本、高通量的分子图谱分析提供了精确的计算工具，对精准医学具有潜在推动作用。

## 7. 优点
*   **生物学合理性增强**：显式捕捉基因共表达结构，生成结果更符合生物学预期，可直接用于下游分析。
*   **理论根基扎实**：将离散计数预测建模为 token 生成，从信息论与概率分解角度给出了优雅的形式化，摆脱了不合适的连续假设。
*   **多尺度结构化**：层次化基因分组与粗到细生成，有效利用了不同解析度的表达信息，提升预测精度与解释性。
*   **通用性强**：在多种组织类型上取得最优效果，表明架构对组织背景的鲁棒性。

## 8. 不足与局限
*   **信息缺失导致的评估不完整**：
    *   未提供具体数据集名称、规模和对比方法列表，无法深入判断实验设置的广度和潜在偏向。
    *   缺少训练算力和时间成本说明，难以评估实际应用部署的可行性。
*   **方法可能局限**：
    *   层次基因分组依赖预聚类，对于全新组织或处理罕见基因时固定分组可能不够灵活。
    *   自回归生成在推理时需逐级解码，潜在推理速度慢于独立预测模型，可能不适合实时应用。
    *   离散化 token 的词汇表大小选择对分辨率敏感，对极低或极高表达基因的建模可能存在精度损失（需原文验证）。
*   **泛化性验证有限**：四个数据集虽跨组织，但可能仍不足以代表所有组织与病理状态，对临床样本的稳定性未经验证。

（完）
