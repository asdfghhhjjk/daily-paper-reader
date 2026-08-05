---
title: Content-aware Information Compression and Selection for Whole Slide Image Analysis
title_zh: 面向全切片图像分析的内容感知信息压缩与选择
authors: "Tingting Zheng, Hongxun Yao, Sicheng Zhao, Yi Xiao"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/38350/42312"
tags: ["query:path-xai-sel"]
score: 8.0
evidence: 通过内容感知压缩选择WSI中的重要区域
tldr: CICS提出一种面向全切片图像分析的高效多实例学习框架，它通过上下文感知压缩技术自动丢弃不相关区域，并选择最具判别力的信息，大幅减少冗余计算，同时提升特征表示的质量。其核心在于将实例空间划分为子区域并学习压缩，从而聚焦于关键区域，避免噪声干扰。实验表明，该方法在多种WSI分析任务中显著提高了效率和准确性，为大规模病理图像分析提供了实用的解决方案，也为可解释性区域选择提供了新方向。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38350/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1688, \"height\": 730, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38350/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1603, \"height\": 633, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38350/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1825, \"height\": 389, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38350/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1825, \"height\": 735, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38350/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1825, \"height\": 735, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38350/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 869, \"height\": 309, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38350/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1817, \"height\": 504, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38350/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1818, \"height\": 399, \"label\": \"Table\"}]"
motivation: 现有MIL方法对所有实例进行搜索，导致冗余计算及无关特征干扰。
method: 提出CICS框架，包含上下文感知压缩（CAC）和信息选择模块，压缩不相关成分并选取关键区域。
result: CICS在WSI分析任务中实现了高效且高质量的压缩选择，性能优于现有方法。
conclusion: 该方法为大规模WSI分析提供了一种高效通用的压缩选择方案。
---

## Abstract
Recent advances in multi-instance learning (MIL) have demonstrated impressive performance in whole slide image (WSI) analysis. However, current methods search for cues and draw conclusions from all instances or regions, resulting in excessive redundant computation and suboptimal representation quality due to irrelevant and uninformative feature interference. To address these issues, we propose CICS, an efficient and general framework that performs compact information compression and selection for high-efficiency WSI analysis. In particular, CICS features two key components: (1) context-aware compression (CAC), which partitions the instance space into sub-regions and applies learnable compression to discard irrelevant components, reduce computational complexity while facilitating information selection, and (2) global-proximity selective attention (GPSA), which cherry-picks the most informative representation with a proximity-assisted global dynamic selection strategy. Building upon these innovations, CICS forms a plug-and-play module that reduces computational complexity through compact instance representations while improving feature quality by preserving the most informative cues. Extensive experiments on six WSI classification and survival prediction datasets show that CICS consistently improves the performance of multiple representative MIL methods. It achieves 2.5%, 7.7%, and 3.9% accuracy gain over the state-of-the-art Transformer-based TransMIL, Mamba-based MambaMIL, and graph-based WIKG methods on the ESCA dataset.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义
- **核心问题**：现有全切片图像分析（WSI）中的多实例学习（MIL）方法通常对所有实例或区域进行特征搜索与聚合，导致：
  - **冗余计算**：尤其在基于Transformer、Mamba或图的方法中，复杂度随实例数平方增长或多次特征相乘，计算开销极大。
  - **表示质量下降**：大量无关、无信息的实例特征产生干扰，扭曲模型对关键线索的关注，导致次优的预测性能。
- **整体含义**：论文旨在通过**内容感知的信息压缩与选择**，在保留判别性信息的前提下大幅压缩实例空间，并仅选择最具信息量的实例参与后续聚合，从而实现高效且高精度的WSI分析。

### 2. 提出的方法论
CICS框架包含两个核心模块：内容感知压缩（CAC）和全局-邻近选择性注意力（GPSA）。

- **内容感知压缩（CAC）**
  - 将每个实例的高维特征（$f^{ins}_j\in \mathbb{R}^{D}$）通过多层感知机（MLP）压缩为紧凑表示（$v^{ins}_j\in\mathbb{R}^{E}, E = D/\tau$），降低序列长度和特征维度。
  - 为保留判别性，引入压缩一致性损失 $\mathcal{L}_{cac}$，最小化压缩前后注意力得分的差异：$\frac{1}{N}\sum_{j=1}^{N}\big(\text{SoftMax}(W^f_j f^{ins}_j) - \text{SoftMax}(W^v_j v^{ins}_j)\big)^2$。
  - 同时结合任务损失 $\mathcal{L}_{task}$ 过滤无关信息。

- **全局-邻近选择性注意力（GPSA）**
  - 将实例空间划分为 $Z$ 个子区域 $R^v_z$（每区域含 $L=N/Z$ 个实例），并从高注意力实例中初始化全局记忆嵌入 $g_0\in\mathbb{R}^{M\times E}$。
  - 对每个子区域 $R^v_z$，分别计算其与**全局记忆** $g_{z-1}$ 和**邻近子区域** $R^{v}_{z+1}$ 的多头注意力得分 $\sigma^g_z$ 与 $\sigma^r_z$。
  - 将二者相加后与平均阈值比较，动态挑选出超出阈值的实例 $Q^v_z$（相比固定Top-K更灵活）。
  - 根据选出的实例更新全局记忆 $g_z$。
  - 最后，利用所选实例在未压缩空间中的对应特征 $\{Q^f_z\}_{z=1}^{Z}$，送入标准的MIL聚合器与预测器中完成训练与推理。

- **损失函数**：$\mathcal{L}_{CICS} = (1-\alpha)\mathcal{L}_{task}(Y, \text{MLP}(\{Q^v_z\})) + \alpha\mathcal{L}_{cac}$，其中 $\alpha$ 平衡压缩保持与任务性能。

- **计算复杂度**：Transformer聚合器复杂度由 $O(N^2D)$ 降至 $O(\bar{N}^2D)$（$\bar{N}<N$）；CAC与GPSA额外开销为 $O(ND'(D+E))$ 和 $O(NZ^2E)$，整体大幅降低。

### 3. 实验设计
- **数据集与任务**
  - 癌症分型分类：TCGA BRCA (952例，IDC vs ILC)，TCGA ESCA (156例，鳞状细胞癌 vs 腺癌)，BRACS (547例，良性/不典型/恶性三分类)。
  - 生存预测：TCGA BRCA, BLCA (376例), LUAD (541例), LUSC (512例)，使用阴性对数似然生存损失。
- **基准方法（baselines）**
  - 注意力型：ABMIL, CLAM, DSMIL, MHIM-ABMIL, IBMIL-ABMIL, ACMIL。
  -  Transformer型：TransMIL, DTFD, MHIM-TransMIL, IBMIL-TransMIL, ILRA。
  - 图型：WIKG；Mamba型：MambaMIL。
  - 共13种MIL方法，均使用官方仓库实现。
- **评估指标与验证**
  - 分类：Accuracy, AUC, F1（阈值0.5）。
  - 生存预测：C-index。
  - 5折交叉验证，报告各折均值与标准差。
- **特征提取**
  - 分类任务：ResNet18-ImageNet (512维) 用于BRCA/ESCA/BRACS；BRACS额外使用ViT-S/16-SSL (DINO预训练，384维) 验证鲁棒性。
  - 生存预测：PLIP基础模型提取512维特征。

### 4. 资源与算力
- **硬件**：单个NVIDIA RTX 3090 GPU。
- **软件**：PyTorch实现。
- **训练配置**：AdamW优化器，权重衰减 $1\times10^{-5}$，初始学习率 $1\times10^{-4}$，批次大小为1（一个WSI为一个包）。
- **未提及**：**未明确说明**单次训练的时长或总GPU小时数，也未提及多GPU分布式训练。

### 5. 实验数量与充分性
- **实验组数**（按组合估算）：
  - 分类实验：3个数据集 × 约9种核心基线方法与CICS的结合，每项报告3个指标（Acc, AUC, F1）；还额外对比了MHIM、IBMIL等即插即用方法，并图示化。
  - 生存预测实验：4个数据集 × 12种方法（含MaxMIL, MeanMIL等），报告C-index。
  - 消融实验：验证CAC各组件（有无$\mathcal{L}_{cac}$，随机掩码，Top-K压缩）及GPSA的GSA/PSA子模块，在ESCA和BRACS上进行。
  - 超参数分析：探究全局记忆大小 $M$ 与区域数量 $Z$ 的影响，使用ESCA数据集与ABMIL结合。
- **充分性评价**：
  - **数据集覆盖较广**：涵盖分类与生存预测，多种癌型，样本量从中等（ESCA）到较大（BRCA）均有。
  - **基线对比全面**：包含了注意力、Transformer、图、Mamba等多类主流MIL方法，且对比了先进的插件式方法（MHIM, IBMIL）。
  - **消融与超参数分析合理**：重要组件均被剥离分析，并探讨了核心超参数灵敏度。
  - **客观性与公平性**：统一使用5折交叉验证，公布标准差；所有基线使用官方代码实现；特征提取器、数据划分多遵循已有规范。实验设计较为公平、充分。

### 6. 主要结论与发现
- CICS能够**即插即用**地提升多种代表性MIL方法（包括注意力、Transformer、Mamba、图方法），在分类和生存预测上均取得一致的性能增益。
- 在ESCA数据集上，CICS分别将TransMIL、MambaMIL、WIKG的准确率提升了2.5%、7.7%、3.9%，同时大幅降低GFLOPs（最高减少46.6%）。
- 压缩与选择机制成功丢弃无关实例与特征，实现了高效与高质的平衡，且动态选择优于固定Top-K。
- 消融实验证明结合全局记忆与邻近关系的选择优于仅用其一，内容感知压缩损失 $\mathcal{L}_{cac}$ 对保持判别性至关重要。

### 7. 优点
- **框架通用性强**：可嵌入多种MIL聚合器，适用于分类和生存预测，无需结构改动。
- **效率与效果双赢**：不仅降低计算量，还提升预测性能，在计算病理中具有实际应用价值。
- **选择策略新颖**：GPSA融合全局判别线索与局部邻近上下文，动态阈值选择更具灵活性，优于硬性Top-K。
- **实验设计严谨**：多数据集、多基线、多编码器、多任务验证，消融充分，有效支撑了提出的观点。

### 8. 不足与局限
- **计算资源细节缺失**：未报告训练时间或整体算力消耗，难以评估实际效率提升的绝对时间。
- **压缩维度固定**：文中指出当前CACS对固定的压缩维度敏感，可能影响跨数据集的适应性，未来需探索动态压缩策略。
- **实验覆盖限制**：仅在TCGA等特定数据集上验证，未在更大规模或来自不同机构的外部数据集上测试泛化性；缺乏对实际病理工作流程（如染色差异、扫描仪差异）的鲁棒性评估。
- **可解释性未深入探讨**：虽然通过选择实例减少冗余，但对所选实例的病理学解释未做进一步分析，临床可解释性仍有待验证。
- **潜在偏差风险**：使用的特征编码器均基于预训练模型，其潜在的域迁移偏差可能影响最终公平性；生存预测中使用单一基础模型（PLIP），但未测试其他病理基础模型的影响。

（完）
