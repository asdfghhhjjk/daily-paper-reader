---
title: "SAMGTD: Spatial-Aware Masked Graph Transformer-Diffusion Model for Enhanced Cell Type Deconvolution in Spatial Transcriptomics"
title_zh: SAMGTD：空间感知掩码图变换器-扩散模型增强的空间转录组细胞类型反卷积
authors: "Shilin Zhang, Suixue Wang, Qingchen Zhang, Xiulong Liu"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/38862/42824"
tags: ["query:immuno-topo"]
score: 8.0
evidence: 空间感知掩码图变换器用于空间转录组学的细胞类型反卷积，处理肿瘤微环境的空间拓扑。
tldr: 空间转录组学中的“dropout”事件限制了细胞类型反卷积的性能。本文提出SAMGTD，结合空间感知掩码图变换器和扩散模型，有效捕获空间位置与基因表达的关系，在反卷积任务上取得提升，为肿瘤免疫微环境的空间解析提供了新工具。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
motivation: 空间转录组学中普遍存在“dropout”事件，现有方法难以充分捕捉空间位置与基因表达的关系。
method: 提出SAMGTD，通过空间感知的掩码图变换器与扩散模型联合建模。
result: 在细胞类型反卷积任务上性能优于现有方法。
conclusion: SAMGTD能有效利用空间信息，为肿瘤微环境研究提供精确的细胞解析。
---

## Abstract
Recent advances in spatial transcriptomics have enabled the integration of gene expression profiles with precise spatial coordinates, which have facilitated the exploration of tumor occurrence and development mechanisms, as well as the development of more effective targeted and immunotherapy approaches for tumor treatment. Deciphering cell type represents a critical challenge in spatial transcriptomics research. Existing methods are limited by the pervasive “dropout” events in spatial transcriptomics, hindering their ability to fully capture the relationship between spatial location and gene expression, thereby compromising the performance of cell type deconvolution. To address these limitations, we propose a spatial-aware masked graph transformer-diffusion model (SAMGTD) for enhanced cell type deconvolution in spatial transcriptomics. For spatial transcriptomics, the masked graph transformer model is designed to adaptively capture complex dependencies between spatial locations and gene expression. It employs a masking strategy that guides the model to focus on important local information during training, while the multi-head attention mechanism captures global context. More importantly, the spatial diffusion model is constructed to achieve the dual enhancement of spatial transcriptomics, including denoising and data imputation. It incorporates the multi-head attention mechanism and residual blocks, effectively addressing the “dropout” issue commonly encountered in spatial transcriptomics. For scRNA-seq, we construct a variational autoencoder to reduce noise interference while preserving key gene expression information. Finally, we construct a spatial-aware contrastive learning model to integrate scRNA-seq and spatial transcriptomics for cell type deconvolution. Experiments conducted on three datasets demonstrate that SAMGTD outperforms baseline methods.

---

## 论文详细总结（自动生成）

## 论文总结：SAMGTD

### 1. 核心问题与整体含义

- **研究背景**：空间转录组学能够同时获取基因表达谱与空间坐标，为解析肿瘤微环境中细胞的空间组织、相互作用及发展机制提供关键数据。细胞类型反卷积（即从空间点阵中推测各点对应的细胞类型组成）是空间转录组分析的核心任务之一。
- **核心问题**：空间转录组数据普遍存在“dropout”事件（即大量的零值或低表达，因技术限制导致部分基因表达未被检出），现有方法难以充分捕捉空间位置与基因表达之间的复杂依赖关系，从而降低了细胞类型反卷积的精度。
- **整体含义**：本文提出 **SAMGTD**（空间感知掩码图变换器-扩散模型），旨在通过增强空间转录组数据质量（去噪与插补）、有效建模空间-基因依赖关系，并整合单细胞 RNA 测序（scRNA‑seq）与空间转录组数据，提升细胞类型反卷积的性能，为肿瘤免疫微环境的空间解析提供更精确的工具。

### 2. 方法论

**核心思想**：联合利用**掩码图变换器**捕获空间局部与全局特征，利用**空间扩散模型**增强数据质量（去噪、填充缺失），再用**空间感知对比学习**融合 scRNA‑seq 和增强后的空间转录组数据完成反卷积。

**关键技术细节与流程**：

- **数据预处理**：
  - 选取 top 4096 高变基因，每点总表达归一化至 10000，对数变换，再缩放到单位方差。
- **空间-基因图构建**：
  - 以 KNN 构建无向图 \(G_{\text{spatial}}\)，节点为空间点（spots），边为相邻关系，用二元邻接矩阵表示。
- **掩码图变换器模块** (Masked Graph Transformer)：
  - 对基因表达执行概率性掩码（伯努利分布，\(p=0.4\)），强制模型关注局部重要信息。
  - 采用多头注意力机制计算点之间的注意力权重，并融入边特征。
  - 使用门控残差连接缓解过平滑问题，最终输出潜在表示 \(P_{sp}\)，再重构得到 \(R_{sp}\)，通过 MSE 损失训练重构能力。
- **空间扩散模型模块** (Spatial Diffusion Model, SDM)：
  - 将每个点的 4096 维基因向量转化为 64×64 伪图像作为输入。
  - 正向过程逐步加噪（马尔可夫链），反向过程用 U‑Net（含残差块与多头注意力）预测噪声，通过变分下界优化。
  - 目的：同时实现去噪和数据插补，生成增强的空间转录组表达矩阵 \(D_{sp}\)。
- **scRNA‑seq 去噪模块 (VAE)**：
  - 对 scRNA‑seq 数据采用相同的预处理。
  - 利用变分自编码器（VAE）降噪，保留关键表达信息，输出降噪后的单细胞矩阵 \(R_{sc}\)。
- **空间感知对比学习反卷积模块**：
  - 定义可学习的反卷积矩阵 \(O \in \mathbb{R}^{N_{sc} \times N_{sp}}\)，映射细胞与空间点。
  - 通过 \(O\) 将 \(R_{sc}\) 映射为预测的空间表达 \(D'_{sp}\)。
  - 损失函数结合了**重构损失**（\(D'_{sp}\) 与增强后的 \(D_{sp}\) 的 MSE）与**对比损失**（最大化相邻点相似度，最小化非相邻点相似度）。
  - 最终反卷积矩阵给出各点的细胞类型比例。

### 3. 实验设计

- **数据集**：
  - 人淋巴结数据集（Human Lymph Node）：真实空间转录组数据，以生发中心（GC）区域已知的细胞类型分布作为基准。
  - 人背外侧前额叶皮层数据集（DLPFC）：真实数据，以层状结构作为基准。
  - 小鼠视觉皮层模拟数据集（Simulated Dataset）：通过网格化处理生成的模拟数据集，每个点含1‑18个细胞，具有精确的细胞类型真值。
- **对比方法**：
  - cell2location（基于贝叶斯模型的经典方法）
  - GraphST（基于图神经网络与自监督学习的方法）
- **评估指标**：
  - 可视化空间分布一致性
  - AUC（曲线下面积）定量评估

### 4. 资源与算力

- **硬件平台**：Linux 系统，配备 **4 颗 Intel Xeon Gold 6248R CPU**（3.0 GHz，24核/CPU），**2 块 NVIDIA A100 GPU**（每块 80 GB 显存）。
- **训练时长**：文中未提及具体训练耗时，仅说明采用无监督训练。
- **其他配置**：人淋巴结数据集和 DLPFC 数据集使用 top 4096 高变基因，模拟数据集使用 top 256 高变基因（因总基因数仅882）。超参数 \(\lambda_1=1，\lambda_2=10\)。

### 5. 实验数量与充分性

- **实验组数**：
  - 在 **3 个数据集** 上分别进行了完整的细胞类型反卷积实验，并提供可视化与 AUC 对比。
  - 针对人淋巴结数据集进行了 **消融实验**，对比缺少掩码图变换器、空间扩散模块、VAE 模块、空间感知对比学习模块时的性能。
- **充分性与公平性**：
  - 数据集涵盖真实与模拟、不同组织类型，评估维度多样（空间分布可视化 + AUC 定量），较为充分。
  - 对比方法选择具有代表性（cell2location 和 GraphST），均在相同预处理流程下评估，具有一定公平性。
  - 消融实验覆盖关键模块，验证了各组件的贡献，但未展示与其他先进方法（如 Tangram、RCTD 等）的比较，方法对比范围可进一步扩大。

### 6. 主要结论与发现

- SAMGTD 在三个数据集上均取得最优的细胞类型反卷积性能，尤其在空间分布一致性和 AUC 指标上显著优于 cell2location 和 GraphST。
- 掩码图变换器和空间扩散模块对性能提升贡献最大，有效缓解了 dropout 问题并增强了空间特征表达。
- 模型为肿瘤微环境分析提供了更精确的细胞解析工具，有望助力靶向和免疫治疗的开发。

### 7. 优点

- **模块化设计且逻辑清晰**：预处理→空间图构建→掩码图变换器编码→扩散增强→VAE去噪→对比学习反卷积，各模块分工明确。
- **双重视角解决 dropout**：既用扩散模型直接增强空间数据（去噪+插补），又通过掩码策略提升表示鲁棒性。
- **空间感知对比学习**：充分利用空间邻域信息约束反卷积矩阵，增强了细胞类型映射的准确性。
- **实验验证较扎实**：在真实和模拟数据集上均进行了可视化与定量评估，并包含消融实验验证模块有效性。

### 8. 不足与局限

- **对比基准较少**：仅与两种方法对比，未纳入近年其他先进方法（如 Tangram、RCTD、SPOTlight、CARD 等），结论的普适性可能受限。
- **计算资源需求较高**：使用 4096 维基因构建伪图像并训练扩散模型，对 GPU 显存和计算力要求较高，可能限制其在普通硬件上的应用。
- **超参数敏感性未讨论**：掩码概率、扩散步数、对比学习权重等关键参数的选择依据与敏感性未深入分析。
- **缺乏跨平台/跨技术泛化实验**：未验证在不同空间转录组技术（如 10x Visium、Slide-seq、MERFISH 等）上的迁移性能。
- **解释性与生物学验证不足**：反卷积结果仅通过已知空间模式验证，未开展下游生物学分析（如细胞互作、通路富集）或独立实验验证。
- **训练时长未报告**：无法评估方法的实际部署效率。

（完）
