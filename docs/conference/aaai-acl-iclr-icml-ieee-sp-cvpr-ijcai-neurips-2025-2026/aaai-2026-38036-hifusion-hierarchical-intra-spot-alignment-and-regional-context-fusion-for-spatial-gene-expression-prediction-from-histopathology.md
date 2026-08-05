---
title: "HiFusion: Hierarchical Intra-Spot Alignment and Regional Context Fusion for Spatial Gene Expression Prediction from Histopathology"
title_zh: "HiFusion: 层次化点内对齐与区域上下文融合用于组织病理图像预测空间基因表达"
authors: "Ziqiao Weng, Yaoyu Fang, Jiahe Qian, Xinkun Wang, Lee A D Cooper, Weidong Cai, Bo Zhou"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/38036/41998"
tags: ["query:cellseg"]
score: 4.0
evidence: "从H&E染色全切片图像预测空间基因表达，涉及数字病理图像分析。"
tldr: "该论文提出HiFusion框架，通过层次化点内建模模块提取细粒度形态表示，并融合区域上下文信息，从H&E全切片图像中预测空间基因表达。尽管不直接涉及细胞分割分类，但体现了利用H&E图像进行下游预测的数字病理学分析方法。"
source: AAAI-2026-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38036/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1836, \"height\": 871}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38036/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 876, \"height\": 892}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38036/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1796, \"height\": 816}]"
tables_json: "[{\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38036/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1830, \"height\": 491}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38036/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 791, \"height\": 351}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38036/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 810, \"height\": 209}]"
motivation: 现有方法未能捕获点内生物学异质性且易受形态噪声干扰。
method: 结合层次化点内建模模块和区域上下文融合来预测基因表达。
result: 在空间基因表达预测上优于现有方法，提高了异质性捕获能力。
conclusion: HiFusion为从组织病理图像预测基因表达提供了新框架，有助于降低成本。
---

## Abstract
Spatial transcriptomics (ST) bridges gene expression and tissue morphology but faces clinical adoption barriers due to technical complexity and prohibitive costs. While computational methods predict gene expression from H&E-stained whole-slide images (WSIs), existing approaches often fail to capture the intricate biological heterogeneity within spots and are susceptible to morphological noise when integrating contextual information from surrounding tissue. To overcome these limitations, we propose HiFusion, a novel deep learning framework that integrates two complementary components. First, we introduce the Hierarchical Intra-Spot Modeling module that extracts fine-grained morphological representations through multi-resolution sub-patch decomposition, guided by a feature alignment loss to ensure semantic consistency across scales. Concurrently, we present the Context-aware Cross-scale Fusion module, which employs cross-attention to selectively incorporate biologically relevant regional context, thereby enhancing representational capacity. This architecture enables comprehensive modeling of both cellular-level features and tissue microenvironmental cues, which are essential for accurate gene expression prediction. Extensive experiments on two benchmark ST datasets demonstrate that HiFusion achieves state-of-the-art performance across both 2D slide-wise cross-validation and more challenging 3D sample-specific scenarios. These results underscore HiFusion’s potential as a robust, accurate, and scalable solution for ST inference from routine histopathology.

---

## 论文详细总结（自动生成）

# HiFusion 论文结构化总结

## 1. 论文的核心问题与整体含义
- **研究背景**：空间转录组学（ST）能同时获取基因表达与组织空间位置，但因成本高昂、操作复杂，难以在临床大规模推广。H&E染色全切片图像（WSI）成本低、常规可用，且形态特征与基因表达相关，因此从WSI直接预测基因表达成为替代方案。
- **核心问题**：现有深度学习方法存在两大局限：
  - 大多将每个测量点（spot）视为均质整体，**忽略点内细胞、亚细胞等微观层次结构的异质性**。
  - 整合周边组织上下文信息时，常采用大尺寸邻域，容易引入与目标点**无关的形态噪声**，缺乏对语义相关性的显式建模。
- **整体含义**：HiFusion旨在通过层次化点内建模和上下文感知融合，更精确地捕获点内多尺度形态与组织微环境线索，实现从常规病理图像中稳健、准确且可扩展的空间基因表达预测。

## 2. 论文提出的方法论
### 2.1 核心思想
构建双分支框架：**层次化点内建模（HISM）** 提取点内多分辨率细粒度特征并保持语义一致性；**上下文感知跨尺度融合（CCF）** 利用交叉注意力选择性整合区域背景信息，增强表达力。

### 2.2 关键技术细节
- **层次化点内建模与对齐（HISM）**
  - 将 spot 图像（224×224）分解为非重叠子块：Level-0 原图，Level-1 为 2×2 网格，Level-2 为 7×7 网格（模拟细胞/亚细胞尺度）。
  - 共享 ResNet-18 编码器提取多层特征图，对子块特征按空间位置重构并插值对齐至 Level-0 分辨率。
  - **特征对齐损失**：计算 Level-1 和 Level-2 重构特征与 Level-0 特征的 L1 距离，确保尺度间语义一致性。
- **上下文感知跨尺度融合（CCF）**
  - 对每个 spot 提取 448×448 邻域图像，经轻量 ResNet-10 编码并全局平均池化，生成区域查询向量 $Q_N$。
  - 将三个尺度的点内特征经可学习权重（softmax）加权融合，再经自适应平均池化到 $k\times k$ 网格，展平为键 $K_S$ 和值 $V_S$。
  - 执行残差多头交叉注意力：以 $Q_N$ 为 query，$K_S$, $V_S$ 为键值对，输出与 $Q_N$ 残差连接后，通过 LayerNorm + 全连接层预测基因表达 $\hat{y}_i$。
- **损失函数**
  - 主回归损失：预测与真实表达的均方误差（MSE）。
  - 辅助损失：各尺度特征经共享全连接层产生辅助预测的 MSE，平均后与主损失相加。
  - 总损失 $L_{total} = L_{reg} + \lambda L_{align}$，其中 $\lambda=1$。

### 2.3 流程简图
输入 spot 图像和邻域图像 → HISM 产多尺度点内特征（经对齐）→ CCF 融合多尺度特征并作为键值、邻域特征为查询进行交叉注意力 → 残差连接后预测基因表达。

## 3. 实验设计
- **数据集**
  - **HER2**：HER2 阳性乳腺癌数据集，36 张全切片，13620 个 spots。
  - **ST-Data**：乳腺癌数据集，16 个样本，41544 个 spots。
  - 均选取表达量最高的 250 个基因作为预测目标，并经过标准化（spot 内总计数归一化+log变换）。
- **评价范式**
  - **2D slide-wise 交叉验证**：按患者分层 4 折交叉验证，避免同一患者数据泄露。
  - **3D 样本特异性验证**：每个患者第一层组织切片训练，其余层测试，评估样本内泛化。
- **对比方法**：ST-Net、HisToGene、Hist2ST、EGN、TRIPLEX、ASIGN（2D 与 3D 版本）。
- **评估指标**：MSE、MAE、PCC。

## 4. 资源与算力
- 文中明确说明：所有实验在 **单块 NVIDIA RTX 4090 GPU** 上运行。
- 训练配置：优化器 Adam，初始学习率 3e-4，余弦退火调度，batch size 32，共训练 **50 个 epoch**。

## 5. 实验数量与充分性
- **主对比实验**：在两个数据集、两种独立评估范式下与 7 种基线方法全面比较（表1），实验规模较大。
- **消融实验**：
  - HISM 子块分解层级组合（共 8 种配置，表2）。
  - 特征对齐损失的有无（表3）。
  - CCF 中 spot token 数量（网格大小从2×2到7×7）的影响（图2a）。
  - 邻域图像尺寸（从224到1120）的影响（图2b）。
  - 癌症标志基因（ERBB2, KRT19, CD74）预测可视化与定量对比（图3）。
- **充分性与公平性**：实验覆盖关键模块与超参，对比方法使用论文原实现并统一条件，结果包含统计显著性检验（p<0.05），整体设计客观、充分。

## 6. 论文的主要结论与发现
- HiFusion 在两个数据集的 2D 和 3D 测试中均达到最先进水平，尤其在 2D 交叉验证中较次优方法有显著提升。
- 层次化点内分解（特别是 1×1+2×2+7×7 组合）和特征对齐损失对性能增益关键。
- 邻域尺寸并非越大越好：两倍 spot 尺寸达到最优，过大反而引入噪声降低性能。
- 3D 样本特定学习能以更低的标签成本和计算量实现强患者内泛化，具有临床应用潜力。

## 7. 优点
- **多尺度层次化建模**：显式分解 spot 图像，兼顾组织、细胞与亚细胞尺度形态。
- **语义一致性约束**：通过特征对齐强制不同尺度表示蕴含相同高层语义，提升鲁棒性。
- **选择性上下文融合**：交叉注意力让模型自动关注背景中与目标 spot 生物相关的部分，抑制无关噪声。
- **评估范式新颖全面**：同时采用传统 2D 交叉验证和更贴近实际的 3D 样本特异性测试，结论更具说服力。
- **轻量高效**：仅使用 ResNet-18/10，单卡 4090 可完成训练，便于复现与部署。

## 8. 不足与局限
- **数据范围有限**：只在两种乳腺癌数据集上验证，对其他组织类型、疾病或技术平台的泛化性未经验证。
- **基因子集限制**：仅预测表达量最高的 250 个基因，可能遗漏表达量低但具有关键调控功能的基因。
- **上下文尺寸固定**：邻域 patch 尺寸为超参数，未探索自适应的上下文范围选择。
- **点内分块刚性**：采用固定网格分解，未结合组织学先验知识（如细胞分割），可能丢失语义边界。
- **3D 对比显示 ASIGN-3D 欠拟合**：文中归因于患者间差异和配准失真，但未深入分析该现象对其他 3D 方法的启示。
- **未考虑多模态融合的更深层交互**：区域上下文仅作为查询，未来可探索更加强大的双向或图级融合。

（完）
