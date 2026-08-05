---
title: "HiFusion: Hierarchical Intra-Spot Alignment and Regional Context Fusion for Spatial Gene Expression Prediction from Histopathology"
title_zh: "HiFusion: 面向组织病理图像空间基因表达预测的层次化点内对齐与区域上下文融合"
authors: "Ziqiao Weng, Yaoyu Fang, Jiahe Qian, Xinkun Wang, Lee A D Cooper, Weidong Cai, Bo Zhou"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/38036/41998"
tags: ["query:tme-evidence"]
score: 7.0
evidence: "从H&E全切片图像预测空间基因表达，助力肿瘤微环境分析。"
tldr: "为解决从H&E染色图像预测基因表达时忽略点内生物异质性和形态噪声的问题，提出HiFusion框架，通过层次化点内建模与区域上下文融合，提升空间转录组学推断的准确性。"
source: AAAI-2026-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38036/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1836, \"height\": 871, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38036/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 876, \"height\": 892, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38036/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1796, \"height\": 816, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38036/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1830, \"height\": 491, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38036/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 791, \"height\": 351, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38036/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 810, \"height\": 209, \"label\": \"Table\"}]"
motivation: 现有方法难以捕捉点内细胞异质性，且易受形态噪声干扰。
method: 设计层次化点内建模模块提取精细形态表示，并结合区域上下文融合。
result: 预期在基因表达预测任务上取得更优性能。（摘要未完整）。
conclusion: "为低成本的肿瘤微环境分析提供了基于H&E图像的解决方案。"
---

## Abstract
Spatial transcriptomics (ST) bridges gene expression and tissue morphology but faces clinical adoption barriers due to technical complexity and prohibitive costs. While computational methods predict gene expression from H&E-stained whole-slide images (WSIs), existing approaches often fail to capture the intricate biological heterogeneity within spots and are susceptible to morphological noise when integrating contextual information from surrounding tissue. To overcome these limitations, we propose HiFusion, a novel deep learning framework that integrates two complementary components. First, we introduce the Hierarchical Intra-Spot Modeling module that extracts fine-grained morphological representations through multi-resolution sub-patch decomposition, guided by a feature alignment loss to ensure semantic consistency across scales. Concurrently, we present the Context-aware Cross-scale Fusion module, which employs cross-attention to selectively incorporate biologically relevant regional context, thereby enhancing representational capacity. This architecture enables comprehensive modeling of both cellular-level features and tissue microenvironmental cues, which are essential for accurate gene expression prediction. Extensive experiments on two benchmark ST datasets demonstrate that HiFusion achieves state-of-the-art performance across both 2D slide-wise cross-validation and more challenging 3D sample-specific scenarios. These results underscore HiFusion’s potential as a robust, accurate, and scalable solution for ST inference from routine histopathology.

---

## 论文详细总结（自动生成）

### 1. 研究动机与核心问题
空间转录组学（ST）可同时获取基因表达与组织空间位置信息，但其临床应用受限于实验成本高、技术复杂、通量低。从常规H&E染色全切片图像（WSI）中直接预测空间基因表达成为一种有前景的替代方案。然而，现有深度学习方法主要存在两个瓶颈：
- **忽略点内（intra‑spot）生物异质性**：多数模型将每个测序点视为均质区域，无法捕捉点内不同细胞类型、细胞核纹理等精细形态差异。
- **区域上下文整合易受噪声干扰**：直接扩大感受野纳入周围组织时，可能引入与目标点无关的形态噪声，缺乏对语义相关性的显式建模。

因此，论文提出HiFusion框架，旨在**同时挖掘点内多尺度精细结构并自适应融合区域上下文**，从而提升基因表达预测的准确性和稳健性。

### 2. 方法论核心
HiFusion由两个互补模块构成，总体架构如图1所示。

#### 2.1 层次化点内建模（HISM）
- **多分辨率分解**：将原始点图像（Level‑0, 224×224）划分为非重叠子块，例如2×2（Level‑1）和7×7（Level‑2）网格，对应组织→细胞→亚细胞级尺度。
- **共享编码与特征对齐**：所有层级输入通过同一个ResNet‑18编码器提取特征，并对精细层特征进行空间重排、插值对齐至Level‑0特征图尺寸。引入**特征对齐损失**（L1范数）约束各尺度特征与全点特征的一致，强化跨尺度语义一致性。
- **多尺度预测辅助监督**：每一层特征均通过共享的全连接层产生辅助基因表达预测，与主损失联合优化。

#### 2.2 上下文感知跨尺度融合（CCF）
- **区域编码**：以目标点为中心裁剪448×448的邻域图像，经轻量ResNet‑10编码并全局平均池化，得到区域查询向量Q。
- **自适应多尺度融合**：对Level‑0、1、2特征通过可学习权重（softmax标度）加权求和，再经自适应平均池化（2×2网格）形成键K和值V。
- **残差交叉注意力**：以区域查询Q为query，融合点内表示K、V进行多头交叉注意力，输出经层归一化和残差连接后，通过全连接层预测最终基因表达谱。

#### 2.3 损失函数
\[ \mathcal{L}_{\text{total}} = \underbrace{\mathcal{L}_{\text{main}} + \mathcal{L}_{\text{aux}}}_{\mathcal{L}_{\text{reg}}} + \lambda \mathcal{L}_{\text{align}} \]
其中\(\mathcal{L}_{\text{main}}\)为最终预测与真值的均方误差（MSE），\(\mathcal{L}_{\text{aux}}\)为各尺度辅助预测的MSE平均，\(\mathcal{L}_{\text{align}}\)为上述特征对齐损失，\(\lambda\)设为1。

### 3. 实验设计与基准对比
#### 3.1 数据集
- **HER2**：36张WSI（12个患者，3或6层切片），13,620个点，点直径100 μm。
- **ST‑Data**：16名乳腺癌患者，三层切片，41,544个点。
- 预处理：每点选取表达量前250的基因，进行库大小归一化+对数变换。

#### 3.2 评估设置
1. **2D slide‑wise交叉验证**：4折交叉验证，确保同一患者的切片只出现在训练或测试集。
2. **3D sample‑specific验证**：每个患者的第一层切片用于训练，其余层用于测试，评估个体内泛化能力。

#### 3.3 基线方法
ST‑Net（DenseNet）、HisToGene（ViT）、Hist2ST（ConvMixer+GNN）、EGN（对比检索）、TRIPLEX（三支路多分辨率）、ASIGN（3D图网络，SOTA），以及ASIGN的2D和3D版本。所有方法均在同条件下重新训练和评估。

#### 3.4 评价指标
MSE、MAE、Pearson相关系数（PCC）。

### 4. 算力资源
- **GPU**：单块NVIDIA RTX 4090。
- **训练配置**：Adam优化器（动量0.9，权重衰减10⁻⁵），初始学习率3×10⁻⁴，余弦退火调度（最低1×10⁻⁶），批量大小32，训练50个epoch。
- **训练时长**：文中未明确给出具体时长，但基于单GPU和中等数据量可推断训练较为轻量。

### 5. 实验数量与充分性
论文开展了较全面的实验，包含：
- **主对比实验**：2个数据集 × 2种评估范式，共4组核心结果。
- **消融实验**：
  - 图像分解层级组合（7种配置，仅HER2）；
  - 特征对齐损失有无（两个数据集）；
  - 交叉注意力token数量（从2×2到7×7）；
  - 邻域图像大小（N=1,2,3,4倍点尺寸）。
- **定性分析**：对3种癌症标志基因（ERBB2, KRT19, CD74）进行了空间分布可视化。
- **额外分析**：3D vs 2D策略对比、补充材料中的ST‑Data消融结果等。

实验覆盖了关键超参数和模块有效性，使用公开数据集和严格交叉验证，与SOTA方法公平比较（相同环境、重新实现），统计学显著性检验（p<0.05），整体设计**充分且客观**。

### 6. 主要结论与发现
- HiFusion在两个数据集上均取得最优性能，尤其在**2D slide‑wise**场景下，MSE较SOTA降低2%~4%，PCC显著提升。
- **3D intra‑sample learning**（个体内单层训练）比先前的3D全局配准策略表现更好，揭示了患者特异性模式的重要性，同时大幅降低标注成本。
- 消融实验证实：多层次点内分解（特别是1×1+2×2+7×7）与特征对齐损失能有效提升精度；中等大小的邻域上下文（2倍点尺寸）和少量token（2×2）可抑制噪声，提升注意力效果。
- 癌症标志基因的空间预测与真值高度吻合，证明方法在肿瘤微环境分析中的临床潜力。

### 7. 方法优点
- **双重视角建模**：首次将点内多尺度细粒度特征与区域上下文通过交叉注意力有机融合，克服了粗粒度点表示和盲目扩大上下文的缺陷。
- **跨尺度语义对齐**：通过显式特征对齐损失，保证不同分辨率特征的一致性，提升训练稳定性和泛化性。
- **轻量化设计**：使用共享编码器和残差注意力，计算开销可控，可在单块消费级GPU上训练。
- **评估范式全面**：不仅使用传统的cross‑patient验证，还引入更具挑战性的intra‑patient 3D验证，凸显模型的实际部署价值。

### 8. 不足与局限
- **数据集规模与多样性有限**：仅使用两个乳腺癌数据集，未在其他癌种或ST技术（如10x Visium、Slide‑seq）上验证，泛化性待考。
- **基因选择受限于平均表达量**：仅预测前250个高表达基因，低表达但具生物学意义的基因被忽略。
- **上下文建模相对简单**：区域编码仅用轻量网络和平均池化，未探索更精细的局部结构或图关系。
- **超参数敏感性未充分讨论**：虽然做了部分消融，但损失权重λ、学习率等未系统研究，可能影响复现稳定性。
- **缺乏真实场景验证**：所有实验均基于处理后数据，未与湿实验ST进行直接临床对比，距实际落地仍有距离。

（完）
