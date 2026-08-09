---
title: "GROVER: Graph-guided Representation of Omics and Vision with Expert Regulation for Adaptive Spatial Multi-omics Fusion"
title_zh: GROVER：面向自适应空间多组学融合的组学与视觉图引导表示与专家调控
authors: "Yongjun Xiao, Dian Meng, Xinlei Huang, Yanran Liu, Shiwei Ruan, Ziyue Qiao, Xubin Zheng"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/37104/41066"
tags: ["query:path-xai-sel"]
score: 4.0
evidence: 整合多组学与组织病理图像的计算病理学方法
tldr: 多模态空间组学数据与组织病理图像整合面临异质性和分辨率不匹配挑战。GROVER提出图引导的表示学习，利用专家调控自适应融合多源数据，解决语义歧义和空间对齐问题，实现综合疾病组织分析。实验表明该方法能有效整合多模态信息。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-37104/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1845, \"height\": 905, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-37104/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1592, \"height\": 933, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-37104/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 877, \"height\": 339, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-37104/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1774, \"height\": 867, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-37104/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1845, \"height\": 223, \"label\": \"Table\"}]"
motivation: 多组学与病理图像异质性强，分辨率不匹配。
method: 图引导表示学习与专家调控自适应融合机制。
result: 有效整合多模态数据，提升疾病组织分析能力。
conclusion: GROVER为空间多组学融合提供了新框架。
---

## Abstract
Effectively modeling multimodal spatial omics data is critical for understanding tissue complexity and underlying biological mechanisms. While spatial transcriptomics, proteomics, and epigenomics capture molecular features, they lack pathological morphological context. Integrating these omics with histopathological images is thus critical for comprehensive disease tissue analysis. However, substantial heterogeneity across omics, imaging, and spatial modalities poses significant challenges. Naive fusion of semantically distinct sources often leads to ambiguous representations. Additionally, the resolution mismatch between high-resolution histology images and lower-resolution sequencing spots complicates spatial alignment. Biological perturbations during sample preparation further distort modality-specific signals, hindering accurate integration. To address these challenges, we propose Graph-guided Representation of Omics and Vision with Expert Regulation for Adaptive Spatial Multi-omics Fusion (GROVER), a novel framework for adaptive integration of spatial multi-omics data. GROVER leverages a Graph Convolutional Network encoder based on Kolmogorov–Arnold Networks to capture the nonlinear dependencies between each modality and its associated spatial structure, thereby producing expressive, modality-specific embeddings. To align these representations, we introduce a spot-feature-pair contrastive learning strategy that explicitly optimizes the correspondence across modalities at each spot. Furthermore, we design a dynamic expert routing mechanism that adaptively selects informative modalities for each spot while suppressing noisy or low-quality inputs. Experiments on real-world spatial omics datasets demonstrate that GROVER outperforms state-of-the-art baselines, providing a robust and reliable solution for multimodal integration.

---

## 论文详细总结（自动生成）

### 一、论文的核心问题与整体含义
- **研究动机**：空间多组学（转录组、蛋白组等）能捕获分子特征，但缺乏组织病理形态学背景；整合组学与组织病理图像对深入理解组织微环境至关重要。然而，不同模态间存在显著异质性（语义鸿沟、分辨率不匹配、样本制备中的生物扰动），传统的简单融合容易导致模糊表示，且现有方法通常无视空间位点层面的数据质量差异。
- **整体含义**：提出一种自适应多模态空间组学融合框架 GROVER，通过图引导的编码、位点级对比对齐和动态专家路由，在不同质量、不同分辨率的输入下稳健地整合转录组、蛋白组和图像模态，获得可分辨空间域的联合表示。

### 二、方法论
- **核心思想**：以图结构同时捕获空间邻近性和模态内特征相似性，利用 Kolmogorov–Arnold 增强的图卷积网络（KAN‑GCN）提取非线性表达；在位点层级通过掩码对比学习对齐不同模态；并通过自适应的 Mixture‑of‑Experts（MoE）动态加权融合，自动抑制低质量模态。
- **关键技术细节**：
  - **双图构建**：对每个模态，基于空间坐标构建空间图 \(G_S\)，基于特征 KNN 构建模态特征图 \(G_F^{(m)}\)。
  - **KAN‑GCN 编码器**：将传统 GCN 的线性变换替换为 KAN 的可学习一元函数矩阵，得到空间嵌入 \(e_{S,i}\) 和特征嵌入 \(e_{F,i}^{(m)}\)。再通过注意机制融合两者：
    \[
    \tilde{e}_i^{(m)} = \alpha_i^{(S)} e_{S,i} + \alpha_i^{(F)} e_{F,i}^{(m)}.
    \]
  - **位点‑特征‑对对比学习**：为缓解跨模态语义差异，计算余弦相似度，构建掩码 \(M^{(m)}\) 过滤掉高度相似的负样本，然后用对称的掩码 InfoNCE 损失对齐任意两个模态对（RNA‑ADT、RNA‑图像、ADT‑图像）。
  - **自适应混合专家**：用门控网络对每个位点给出三个模态的置信度权重，低于阈值 γ 的模态被屏蔽并重新归一化；每个模态由一个独立的前馈专家处理，最终表示为各专家输出的加权和。
- **训练目标**：联合最小化每个模态的重建损失（空间‑图解码器）和所有模态对的对比损失，平衡系数 λ。
- **算法流程**（见原文 Algorithm 1）：构建图 → 每轮对每个模态编码、注意融合 → 计算对比损失 → MoE 路由得到联合表示 → 计算重建损失 → 反向传播更新。

### 三、实验设计
- **数据集**：
  1. 10x Visium 人乳腺癌（基因+蛋白）
  2. 10x Visium 人胶质母细胞瘤（基因+蛋白）
  3. 10x Visium 人扁桃体（基因+蛋白）
  4. 10x Visium 人扁桃体附加抗体（基因+蛋白）
  所有数据集均包含 H&E 组织病理图像。
- **基准方法**：MISO（支持图像模态）、SpatialGlue、COSMOS。
- **评价指标**：ARI、NMI、FMI、SC、AMI、Jaccard、DBI、CHI、Purity，共9种聚类评估指标。使用 RNA 和 ADT 分别的细胞类型标签作为两种聚类参考，取5种不同聚类数（10到6）的均值和标准差。

### 四、资源与算力
- 所有实验在配备两块 NVIDIA RTX A5000（24 GB）GPU 和双 Intel Xeon Silver 4210R CPU 的工作站上运行。
- GROVER 在该配置下经过 300 个 epoch 内收敛。

### 五、实验数量与充分性
- 共在 **4 个真实空间多组学数据集**上进行定量评估，每个数据集均与3种基线对比，报告9项指标的平均与标准差，覆盖40组以上主实验。
- **消融实验**：在“人扁桃体附加抗体”数据集上逐步移除 MoE 模块、对比损失、KAN‑GCN，观察性能变化（其他数据集结果见附录）。
- **参数敏感性**：对置信度阈值 γ 和对比损失权重 λ 进行扫描，在胶质母细胞瘤数据集上分析稳定性。
- 实验设计较为全面，多数据集、多指标、多消融，对比方法公开、评估标准统一，具有客观性和公平性。

### 六、主要结论与发现
- GROVER 在所有数据集和多数指标上排名前二，尤其显著提升 SC、CHI 等指标，说明融合嵌入具有更好的簇内紧凑性和空间结构保持能力。
- 仅用两种分子模态的 SpatialGlue 有时表现优于包含图像的 MISO，揭示均匀融合所有模态并非最优，侧面验证自适应加权的必要性。
- 可视化结果显示 GROVER 能清晰勾勒生发中心等结构边界，而对比方法存在过分割或模糊现象。
- 消融实验证实三个组件均对最终性能产生积极影响，MoE 模块的移除导致 ARI/NMI/FMI 显著下降。

### 七、优点
- **方法创新**：将 KAN 引入 GCN 编码器，增强非线性表达；提出位点‑特征‑对掩码对比损失，缓解跨模态语义鸿沟和假阴性问题；引入动态专家路由，实现位点级别的质量感知融合。
- **设计全面**：同时建模空间图与特征图，注意力融合局部信息，端到端联合重建与对比学习。
- **实验扎实**：4 数据集、9 指标、多种消融和敏感性分析，与近期前沿方法充分对比，结果具有说服力。
- **模块化与可扩展性**：图像编码器可灵活替换任何预训练病理基础模型（如 OmiCLIP），易于跟进技术进步。

### 八、不足与局限
- **图像特征提取依赖预训练模型**：论文使用了 OmiCLIP，但未对比不同图像编码器的影响，实际部署中模型选择可能影响表现。
- **仅评估聚类任务**：下游任务只展示了空间域识别（聚类），未涉及其他分析任务（如细胞类型反卷积、基因标记发现）的泛化能力。
- **缺少更多组织类型或技术平台数据**：所有数据均来自 10x Visium CytAssist（FFPE），未在其它空间技术（如 MERFISH、Visium HD）上验证。
- **超参数敏感性**：尽管敏感性分析显示模型对 γ 和 λ 相对稳定，但未讨论 KAN 内部结构（如样条阶数、网络层数）的调优和影响。
- **计算开销**：KAN 和非线性变换可能增加训练时间，论文未与标准 GCN 在效率上进行对比。
- **潜在偏差**：聚类标签来自 RNA 和 ADT 分别定义的细胞类型，两种模态标签不完全统一，可能引入评估偏差，文中仅以均值和标准差简要说明，未深入讨论。

（完）
