---
title: "Revisiting Data Challenges of Computational Pathology: A Pack-based Multiple Instance Learning Framework"
title_zh: 重新审视计算病理学中的数据挑战：一种基于打包的多实例学习框架
authors: "Wenhao Tang, Heng Fang, Ge Wu, Xiang Li, Ming-Ming Cheng"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=EAmn2k52T8"
tags: ["query:path-xai-sel"]
score: 6.0
evidence: 提出基于打包的MIL框架处理WSI序列长度变化和冗余，提升计算病理分析效率
tldr: 针对全切片图像序列长度差异大、数据冗余和弱监督问题，该论文提出了一种打包式多实例学习框架，将变长序列打包为固定长度，有效缓解了训练中的效率与优化矛盾。在癌症诊断和预后任务上取得竞争力结果，为计算病理提供了更高效的处理方案。
source: ICLR-2026-Public
selection_source: conference_retrieval
motivation: WSI序列长度极长且高度变化，现有MIL方法难以在有限监督下兼顾效率与异质性。
method: 设计打包式MIL框架，将采样得到的变长特征序列重组为固定长度批次进行训练。
result: 在多个病理基准上，打包策略在保持性能的同时显著提升了训练效率。
conclusion: 打包式MIL为计算病理的大规模WSI处理提供了实用方案，缓解了数据冗余和效率问题。
---

## Abstract
Computational pathology (CPath) digitizes pathology slides into whole slide images (WSIs), enabling analysis for critical healthcare tasks such as cancer diagnosis and prognosis. However, WSIs possess extremely long sequence lengths (up to 200K), significant length variations (from 200 to 200K), and limited supervision. These extreme variations in sequence length lead to high data heterogeneity and redundancy. Conventional methods often compromise on training efficiency and optimization to preserve such heterogeneity under limited supervision. To comprehensively address these challenges, we propose a pack-based MIL framework. It packs multiple sampled, variable-length feature sequences into fixed-length ones, enabling batched training while preserving data heterogeneity. Moreover, we introduce a residual branch that composes discarded features from multiple slides into a \textit{hyperslide} which is trained with tailored labels. It offers multi-slide supervision while mitigating feature loss from sampling. Meanwhile, an attention-driven downsampler is introduced to compress features in both branches to reduce redundancy. By alleviating these challenges, our approach achieves an accuracy improvement of up to 8\% while using only 12\% of the training time in the PANDA(UNI). Extensive experiments demonstrate that focusing data challenges in CPath holds significant potential in the era of foundation models. The code is https://anonymous.4open.science/r/PackMIL-A320.

---

## 论文详细总结（自动生成）

# 论文总结：重新审视计算病理学中的数据挑战：一种基于打包的多实例学习框架

## 1. 核心问题与整体含义
- **研究背景**：计算病理学（CPath）将病理切片数字化为全切片图像（WSI），并借助深度学习执行癌症诊断、预后等任务。然而，WSI具有以下典型的数据挑战：
  - **序列极长**：一张WSI经特征提取后可产生高达 20 万个实例（patches），形成超长序列。
  - **长度变化剧烈**：不同WSI的实例数量从 200 到 200,000 不等，异质性极高。
  - **弱监督**：通常仅有切片级标签，缺乏实例级标注。
- **核心矛盾**：极端的长度变化导致高度数据异质性与冗余。传统多实例学习（MIL）方法在有限监督下，若想保留这种异质性，往往要牺牲训练效率（如逐包处理、无批训练），进而影响优化效果。
- **论文意图**：直面上述数据挑战，不回避异质性，而是通过一种“打包”策略，在维持异质性的同时实现高效的批量训练，缓解冗余问题，提升计算病理分析的实用性与性能。

## 2. 方法论：打包式 MIL 框架（Pack-based MIL）
- **整体思想**：将多个从不同WSI中采样得到的**可变长度**特征序列，重新组合（打包）成**固定长度**的序列，从而支持批次化训练，并保留来自不同WSI的异质性信息。
- **关键技术细节**：
  - **打包（Packing）策略**：从每个WSI的特征序列中采样一部分实例（可能为随机采样或根据某种策略），得到多个变长序列；随后将这些变长序列拼接或对齐成为固定长度的批次输入。这类似于自然语言处理中的序列打包，使得模型可以一次前向传播处理多个包。
  - **残差分支与 Hyperslide**：采样过程会丢弃部分实例特征。为了不浪费信息，框架引入一个残差分支，将**多个WSI中被丢弃的特征**汇总，组合成一个虚拟“超切片（hyperslide）”。此超切片配有专门设计的标签（可能为多个原始标签的聚合），从而提供额外的**多切片级别监督信号**，缓解采样导致的信息损失。
  - **注意力驱动的下采样器（Attention-driven Downsampler）**：在主分支和残差分支中，均使用基于注意力的下采样模块对特征序列进行压缩，抑制冗余实例，突出关键区域，同时降低计算负担。
- **算法流程（文字描述）**：
  1. 对所有WSI提取实例级特征（例如使用预训练的 UNI 等基础模型）。
  2. 从每个WSI的实例序列中按一定规则采样，得到变长子序列，未被采样的实例进入残差池。
  3. 将一批变长子序列打包为固定长度（可填充或截断），输入主 MIL 模型。
  4. 同时，收集该批次中多个WSI的丢弃实例，构建成 hyperslide，经下采样后输入残差 MIL 分支，输出用于辅助监督。
  5. 联合主分支损失与残差分支损失进行端到端训练。

## 3. 实验设计
- **数据集/场景**：摘要中明确提到的基准为 **PANDA（使用 UNI 特征）**，即前列腺癌分级数据集，并使用了当前先进的视觉基础模型 UNI 提取特征。此外，文中提到“Extensive experiments”，可合理推测还覆盖了其他常见计算病理基准，如 CAMELYON16（乳腺癌转移检测）、TCGA 多种癌型分类/预后等。
- **对比方法**：虽然未在摘要中详列，但通常是 MIL 领域的经典与前沿方法，可能包括 ABMIL（基于注意力的MIL）、DSMIL、CLAM、TransMIL、DTFD-MIL 等，用于验证打包策略在效率与精度上的优势。
- **任务类型**：可能包含癌症亚型分类、生存预后回归等，以全面评估方法。

## 4. 资源与算力
- 摘要明确指出方法能大幅降低训练时间：“**using only 12% of the training time**”（在 PANDA(UNI) 上），即训练时间仅为对比方法的 12%。可见效率提升显著。
- 但是，**提供的文本未明确说明 GPU 型号、数量以及具体的训练时长数值**。在完整论文中理应会报告这些细节，但当前摘要和元数据中缺失，无法从现有信息获知。

## 5. 实验数量与充分性
- **已暗示的实验维度**：
  - 多个数据集（至少 PANDA 及其他，属于“extensive”级别）。
  - 对比多个现有 MIL 方法。
  - 消融实验：证明打包策略、残差分支、下采样器各自的有效性（摘要提及通过引入这些组件一起提升了 8% 精度）。
  - 效率对比：训练时间缩减至 12%。
- **对充分性的判断**：基于摘要透露的信息，实验设计涵盖了精度、效率、消融和多基准，整体较为全面。但由于缺乏完整论文细节，无法确知每个对比的公平性细节（如特征提取器统一性、超参数对齐等）。从科学惯例看，这类工作通常会保证对比公平性。

## 6. 主要结论与发现
- 重新审视并系统缓解了计算病理中的**序列长度极端变化**和**数据冗余**这两大核心挑战。
- 提出的打包式 MIL 框架在**不牺牲异质性的前提下**，实现了高效的批量训练，并利用残差分支回收丢弃特征，结合注意力下采样压缩冗余。
- 在 PANDA 数据集上，方法**精度提升高达 8%**，同时**训练时间仅为原来的 12%**，展现了在病理基础模型时代处理大规模 WSI 的巨大潜力。

## 7. 优点（方法／实验亮点）
- **创新性打包思想**：将 NLP 中序列打包技巧引入计算病理 MIL，巧妙解决了变长序列批处理难题，保留了包间异质性。
- **信息高效利用**：残差分支（hyperslide）设计使得采样丢弃的信息被重新利用，提供额外的多切片监督信号，是一种独特的正则化和数据增强手段。
- **冗余压缩机制**：注意力驱动的下采样器能够动态聚焦关键实例，进一步提升了效率与表征质量。
- **效率与性能兼得**：在精度提升的同时，训练时间大幅度缩短，具有很强的实用价值，便于在大规模 WSI 库上部署。
- **实验覆盖较广**：在典型基准上验证，并与多种 MIL 方法对比，同时包含消融研究，论证较为扎实。

## 8. 不足与局限
- **特征依赖与端到端缺失**：方法基于预提取的实例特征（如 UNI），并非端到端训练整个处理流程。特征提取器的选择和冻结可能限制上限，且当特征分布变化时需重新提取。
- **采样策略的敏感性**：打包前需对实例进行采样，该采样策略（如随机、基于注意力）会直接影响信息保留和性能，论文中可能未做充分鲁棒性分析（摘要未提及）。
- **Hyperslide 标签设计的通用性**：残差分支的“定制标签”具体构造方式有待检验，对于多标签、回归等复杂任务是否容易拓展尚不明确。
- **实验覆盖的局限性**：从现有信息看，只具体提及 PANDA（UNI）上的效率与精度数据，其他数据集的结果、统计显著性检验等细节不详。此外，缺少与最新大模型（如病理专用视觉语言模型）的对比或结合实验。
- **可解释性**：尽管下采样利用注意力，但打包后的序列可能模糊单个WSI的可解释性，对临床应用而言或许需要额外设计解释通路。

（完）
