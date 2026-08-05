---
title: "Revisiting Data Challenges of Computational Pathology: A Pack-based Multiple Instance Learning Framework"
title_zh: 重新审视计算病理学的数据挑战：一种基于打包的多实例学习框架
authors: "Wenhao Tang, Heng Fang, Ge Wu, Xiang Li, Ming-Ming Cheng"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=EAmn2k52T8"
tags: ["query:cellseg"]
score: 5.0
evidence: 基于打包的MIL用于WSI分类，解决数字病理分析中的数据挑战
tldr: 现有WSI方法在处理长序列和长度变化时面临训练效率与优化难题；提出打包式MIL，将可变长度特征序列打包为固定长度，以全面应对数据异质性和冗余；在癌症诊断和预后任务上验证了有效性，为计算病理学提供更高效的训练框架。
source: ICLR-2026-Public
selection_source: conference_retrieval
motivation: 解决WSI序列长度极端变化和有限监督带来的数据异质性与冗余问题。
method: 提出打包式多实例学习框架，将多个采样变长特征序列打包为固定长度序列处理。
result: 在癌症诊断和预后任务上提升了训练效率和优化效果。
conclusion: 为计算病理学提供了一种高效应对WSI数据挑战的通用方法。
---

## Abstract
Computational pathology (CPath) digitizes pathology slides into whole slide images (WSIs), enabling analysis for critical healthcare tasks such as cancer diagnosis and prognosis. However, WSIs possess extremely long sequence lengths (up to 200K), significant length variations (from 200 to 200K), and limited supervision. These extreme variations in sequence length lead to high data heterogeneity and redundancy. Conventional methods often compromise on training efficiency and optimization to preserve such heterogeneity under limited supervision. To comprehensively address these challenges, we propose a pack-based MIL framework. It packs multiple sampled, variable-length feature sequences into fixed-length ones, enabling batched training while preserving data heterogeneity. Moreover, we introduce a residual branch that composes discarded features from multiple slides into a \textit{hyperslide} which is trained with tailored labels. It offers multi-slide supervision while mitigating feature loss from sampling. Meanwhile, an attention-driven downsampler is introduced to compress features in both branches to reduce redundancy. By alleviating these challenges, our approach achieves an accuracy improvement of up to 8\% while using only 12\% of the training time in the PANDA(UNI). Extensive experiments demonstrate that focusing data challenges in CPath holds significant potential in the era of foundation models. The code is https://anonymous.4open.science/r/PackMIL-A320.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义

- **研究背景**：计算病理学（CPath）将病理切片数字化为全切片图像（WSI），用于癌症诊断与预后等关键医疗任务。
- **核心挑战**：WSI 的序列长度极长（可达 20 万）且变化剧烈（200 至 20 万），监督信息有限，导致数据异质性强、冗余大。
- **现有问题**：传统方法在有限监督下为保留异质性，往往牺牲训练效率和优化效果，难以兼顾效率与数据充分利用。
- **论文动机**：重新审视计算病理学中的数据挑战，提出一个全面解决长序列与长度变化问题的框架。

### 2. 论文提出的方法论

- **核心思想**：打包式多实例学习（pack‑based MIL）框架，将多个采样得到的变长特征序列打包成固定长度序列，支撑批量训练的同时保持数据多样性。
- **关键技术细节**：
  - **特征打包**：从多个 WSI 中采样可变长度特征，拼接并填充/截断为固定长度序列，允许混合不同切片的实例。
  - **残差分支与 hyperslide**：引入残差分支，将各切片丢弃的特征组合成一个“hyperslide”，并为其构造定制标签（如多切片综合标签），在提供多切片监督的同时缓解采样导致的信息丢失。
  - **注意力驱动的下采样器**：在上游分支和残差分支中均采用注意力机制压缩特征，减少冗余。
  - **训练流程**：通过打包实现批次化训练，残差分支与主分支联合优化，同时利用切片级标签与 hyperslide 标签。
- **公式/算法**（文字说明）：
  - 设多张 WSI 的特征序列为 $\{X_i\}$，长度差异大；从每张切片采样得到子序列 $\tilde{X}_i$；将所有子序列拼接为固定长度序列 $S$，即“pack”。
  - 残差分支收集未使用的特征组成 $H$，生成 hyperslide 监督信号。
  - 模型对 pack 进行注意力加权，注意力下采样器对两个分支的特征同时压缩。
  - 损失函数为主分支分类/回归损失与残差分支损失之和。

### 3. 实验设计

- **数据集/场景**：癌症诊断和预后任务（文中以 PANDA(UNI) 为例，可能还涉及其他公开 WSI 数据集，如 CAMELYON、TCGA 等，但摘要中仅明确提到 PANDA(UNI)）。
- **Benchmark 设置**：与现有主流 WSI 分类方法对比，评估指标包括准确率、训练时间等。
- **对比方法**：推测包括传统 MIL（如 ABMIL、DSMIL、TransMIL 等）及最新基于 Transformer 的 WSI 分析方法，但摘要未列出具体名称。

### 4. 资源与算力

- **GPU 信息**：摘要中未明确说明 GPU 型号、数量及训练时长，但提到“仅用 12% 的训练时间”在 PANDA(UNI) 上取得效果提升，暗示效率显著优于对比方法。具体算力细节需查看原文实验部分，此处缺失。

### 5. 实验数量与充分性

- **实验组数**：摘要提及在癌症诊断和预后等多个任务上进行评估，包含消融实验（如验证残差分支、下采样器的作用），并对计算效率做了对比（训练时间减少 88%）。
- **充分性与公平性**：通过多任务、效率对比及准确率提升（最高 8%）展现有效性；但与哪些基准方法对比、实验次数不详，仅从摘要难以判断是否覆盖足够广泛的 SOTA 方法或数据分布。

### 6. 论文的主要结论与发现

- 打包式 MIL 能有效缓解 WSI 长序列、长度变化带来的数据异质性和冗余问题。
- 残差 hyperslide 分支在多切片监督下减少了采样信息丢失，注意力下采样进一步降低冗余。
- 方法在保证甚至提升分类/预后准确率的同时，大幅缩短训练时间（仅需对比方法 12% 的时间），在基础模型时代具有重要潜力。

### 7. 优点

- **方法创新**：将 NLP 中的“packing”思想迁移到病理 MIL，通过固定长度打包实现高效批量训练，解决序列长度极端变化带来的工程与优化难题。
- **综合设计**：残差分支巧妙利用被丢弃的特征，避免信息损失；注意力下采样同时压缩特征，减少冗余。
- **效率显著**：在 PANDA(UNI) 上最高提升 8% 准确率，训练时间降低至 12%，兼具性能与效率。
- **泛用性强**：可应用于诊断和预后等不同病理任务。

### 8. 不足与局限

- **实验覆盖有限**：摘要仅列举 PANDA(UNI) 数据集，其他常见基准（如 CAMELYON16、TCGA 多癌种）参与程度不明，泛化性有待更多验证。
- **对比方法不清晰**：提升 8% 是相对哪种基线？是否与最强 SOTA 公平对比？摘要未指明。
- **打包策略的敏感性**：固定长度选取、采样策略、不同长度分布对结果的影响未在摘要中分析。
- **残差 hyperslide 的标签设计**：如何构建定制标签？是否存在标签噪声或偏差？需查看原文细节。
- **病理场景限制**：方法假设可采样并拼接特征，但在需要保留完整空间上下文的任务中可能受限；hyperslide 的有效性依赖于多切片监督的合理定义。
- **代码**：已提供匿名仓库，但未说明使用许可或硬件需求。

（完）
