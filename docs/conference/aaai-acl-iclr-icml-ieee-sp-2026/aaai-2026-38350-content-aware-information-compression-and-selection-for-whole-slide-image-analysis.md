---
title: Content-aware Information Compression and Selection for Whole Slide Image Analysis
title_zh: 内容感知信息压缩与选择用于全切片图像分析
authors: "Tingting Zheng, Hongxun Yao, Sicheng Zhao, Yi Xiao"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/38350/42312"
tags: ["query:path-xai-sel"]
score: 10.0
evidence: 通过内容感知压缩选择WSI中的信息区域，丢弃无关区域以进行高效准确的分析
tldr: CICS提出内容感知压缩与选择框架，解决WSI分析中冗余计算和无关特征干扰问题。该方法划分实例空间并压缩无关区域，显著提升计算效率和分类准确率。实验表明，CICS在多个WSI基准上优于现有MIL方法，验证了重要区域选择对病理分类的关键作用。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38350/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1688, \"height\": 730}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38350/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1603, \"height\": 633}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38350/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1825, \"height\": 389}]"
tables_json: "[{\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38350/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1825, \"height\": 735}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38350/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1825, \"height\": 735}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38350/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 869, \"height\": 309}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38350/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1817, \"height\": 504}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38350/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1818, \"height\": 399}]"
motivation: 现有MIL方法搜索所有区域导致冗余计算和次优表示，无关特征干扰分类。
method: 提出CICS框架，通过上下文感知压缩和选择，划分实例空间并压缩无关区域。
result: 在多个WSI数据集上以更高效率取得领先的分类准确率。
conclusion: CICS为WSI分析提供高效区域选择方案，去除噪声区域提升诊断性能。
---

## Abstract
Recent advances in multi-instance learning (MIL) have demonstrated impressive performance in whole slide image (WSI) analysis. However, current methods search for cues and draw conclusions from all instances or regions, resulting in excessive redundant computation and suboptimal representation quality due to irrelevant and uninformative feature interference. To address these issues, we propose CICS, an efficient and general framework that performs compact information compression and selection for high-efficiency WSI analysis. In particular, CICS features two key components: (1) context-aware compression (CAC), which partitions the instance space into sub-regions and applies learnable compression to discard irrelevant components, reduce computational complexity while facilitating information selection, and (2) global-proximity selective attention (GPSA), which cherry-picks the most informative representation with a proximity-assisted global dynamic selection strategy. Building upon these innovations, CICS forms a plug-and-play module that reduces computational complexity through compact instance representations while improving feature quality by preserving the most informative cues. Extensive experiments on six WSI classification and survival prediction datasets show that CICS consistently improves the performance of multiple representative MIL methods. It achieves 2.5%, 7.7%, and 3.9% accuracy gain over the state-of-the-art Transformer-based TransMIL, Mamba-based MambaMIL, and graph-based WIKG methods on the ESCA dataset.

---

## 论文详细总结（自动生成）

## 论文总结

### 1. 核心问题与整体含义
- **研究背景**：全切片图像（WSI）分析在癌症诊断与预后中至关重要，当前主流范式是多实例学习（MIL），将WSI视为由大量未标注实例（图像块）组成的“包”。
- **核心问题**：现有MIL方法（尤其基于Transformer、Mamba 或图的方法）通常对所有实例或区域进行推理，带来大量冗余计算；且大量语义无关或低信息的实例特征会干扰模型，导致表示质量欠佳、产生预测偏差。
- **整体含义**：论文旨在通过“内容感知的信息压缩与选择”框架（CICS），在保留关键判别信息的前提下大幅减少冗余计算，提升WSI分析效率与精度。

### 2. 方法论
CICS是一个即插即用的通用框架，包含两个核心组件：
- **上下文感知压缩（CAC）**
  - 将每个实例的高维特征 \(f_j^{ins} \in \mathbb{R}^{1\times D}\) 通过可学习MLP压缩为紧凑表示 \(v_j^{ins} \in \mathbb{R}^{1\times E}\)（\(E = D/\tau\)）。
  - 为防止压缩损害判别力，引入压缩对齐损失 \(L_{cac}\)，强制压缩前后的注意力分数分布一致。
  - 整体损失同时包含任务驱动损失 \(L_{task}\)，以过滤无关信息。

- **全局邻近选择性注意力（GPSA）**
  - 将压缩后的实例按空间划分为 \(Z\) 个子区域。
  - 利用**全局记忆嵌入**（初始化为部分高注意力实例特征）和**邻近区域特征**，通过多头注意力计算全局与局部注意力分数，并融合两者。
  - 采用动态阈值策略（超过区域平均分数的实例被选中），而非固定top-K选择，从而自适应地保留最具信息量的实例。
  - 全局记忆嵌入根据选择结果不断更新。

- **整体流程**：压缩 → 分区 → GPSA选出区域内关键实例索引 → 根据索引提取对应的原始未压缩特征 → 送入下游MIL模型（任意聚合器+预测器）进行预测。这一设计既保留了特征的完整判别力，又显著降低了实例数量和计算复杂度（例如Transformer复杂度从 \(O(N^2D)\) 降至 \(O(\bar{N}^2 D)\)）。

### 3. 实验设计
- **数据集**：
  - 癌症预测：TCGA-BRCA（952例，IDC vs ILC）、TCGA-ESCA（156例，鳞癌 vs 腺癌）、BRACS（547例，三分类良性/不典型/恶性）。
  - 生存预测：TCGA-BRCA、TCGA-BLCA、TCGA-LUAD、TCGA-LUSC。
- **对比方法（Benchmark）**：共集成了13种代表性MIL方法，包括基于注意力的ABMIL、CLAM、DSMIL，基于Transformer的TransMIL、DTFD、ILRA，基于Mamba的MambaMIL，基于图的WIKG，以及增强策略MHIM、IBMIL、ACMIL等。所有基线均使用官方开源实现。
- **评价指标**：分类任务用准确率、AUC、F1分数；生存预测用C-index。
- **特征提取**：BRCA/ESCA/BRACS 使用 ResNet18-ImageNet（512维）或 ViT-S/16-SSL（384维）；生存预测部分用PLIP特征（512维）。

### 4. 资源与算力
- **硬件**：所有实验均在**单张 NVIDIA RTX 3090 GPU**上完成。
- **框架**：PyTorch 实现，优化器为 AdamW，学习率 1e-4，batch size=1（一张WSI为一个包）。
- **训练时长**：论文未明确给出每个实验或总训练时长，仅提及所用GPU型号和核心超参数。

### 5. 实验数量与充分性
实验覆盖较为广泛，可以认为充分且客观：
- 在**6个公开WSI数据集**上进行了分类与生存预测两大类任务评估。
- 与**13种不同架构的MIL方法**（含它们的组合）进行集成对比，报告了均值和标准差（多折交叉验证）。
- 消融实验系统分析了GPSA中的全局与邻近机制、CAC的压缩方式以及损失函数的作用。
- 超参数分析考察了分区数 \(Z\) 和全局记忆大小 \(M\) 的影响。
- 从论文展示的多个表格和图示看，对比公平（相同数据划分、相同特征提取方式、官方的基线复现），结果具备统计意义，且在不同任务上表现一致，说明结论可靠。

### 6. 主要结论与发现
- CICS 可以显著提升各类MIL方法的性能，同时大幅降低计算量（GFLOPs），在 ESCA 数据集上相对 TransMIL、MambaMIL、WIKG 分别取得 2.5%、7.7%、3.9% 的准确率增益。
- CAC 和 GPSA 两者协同工作：压缩剔除冗余、选择保留最相关信息，能更好应对组织异质性与计算瓶颈。
- 消融实验表明，全局与局部邻近信息的融合以及动态选择策略均对性能有重要贡献。

### 7. 优点
- **方法亮点**：
  - 即插即用、模型无关，可无缝集成到现有MIL流水线中。
  - 创新性地将特征压缩与实例选择联合优化，既降计算又提性能。
  - GPSA 动态选择机制替代固定 top-K，更适应WSI内部复杂性。
- **实验亮点**：
  - 覆盖多种主流MIL架构（注意力、Transformer、Mamba、图），在不同任务和多个数据集上均验证有效。
  - 同时报告性能增益与计算量减少（如 -46.6% FLOPs），效率提升直观。

### 8. 不足与局限
- **方法局限**：CICS 对固定的压缩维度较敏感，可能影响在不同数据集间的泛化能力（论文中也指出此限制）。
- **实验覆盖**：虽然数据集数量较多，但仍有局限，例如子类型数量不均衡（如 ESCA 样本量仅 156 例），结果波动可能受数据量影响；未在更大型、多尺度的病理学数据集上测试。
- **依赖外部特征提取器**：所有实验建立在预提取的特征之上，未提供端到端图块级别训练的实验，实际部署仍受下游特征提取质量约束。
- **计算成本关注点**：论文侧重理论复杂度降低，但未详细报告CICS模块本身的训练开销和推理时延绝对值，可能缺乏对实际落地成本的细致评估。
- **偏差风险**：使用的特征提取器均为ImageNet或特定病理模型，未见不同特征提取器对CICS增益的敏感性分析。

（完）
