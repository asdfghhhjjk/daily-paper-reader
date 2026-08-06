---
title: "GROVER: Graph-guided Representation of Omics and Vision with Expert Regulation for Adaptive Spatial Multi-omics Fusion"
title_zh: GROVER：图引导的组学与视觉表示学习及专家调控的自适应空间多组学融合
authors: "Yongjun Xiao, Dian Meng, Xinlei Huang, Yanran Liu, Shiwei Ruan, Ziyue Qiao, Xubin Zheng"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/37104/41066"
tags: ["query:profile"]
score: 7.0
evidence: 图引导的组织病理图像与空间组学融合用于下游组织分析
tldr: 多模态空间组学与组织病理图像融合面临语义异质和分辨率不匹配难题。GROVER通过图引导的表示学习与专家调控，自适应地对齐不同模态，消除语义模糊，实现精准的组织微环境联合表征，提升疾病分析的全面性。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
motivation: 空间组学缺乏病理形态上下文，且组学、成像与空间模态间存在巨大异质性，导致融合模糊。
method: 提出图引导的表示学习框架，结合专家调控模块，自适应融合组织学图像与多种空间组学数据。
result: 在组织区域分析任务上，GROVER有效缓解模态冲突，取得优于直接融合的表示和下游性能。
conclusion: 图引导的多模态融合策略为空间层面的组织微环境综合建模提供了可解释且强大的方案。
---

## Abstract
Effectively modeling multimodal spatial omics data is critical for understanding tissue complexity and underlying biological mechanisms. While spatial transcriptomics, proteomics, and epigenomics capture molecular features, they lack pathological morphological context. Integrating these omics with histopathological images is thus critical for comprehensive disease tissue analysis. However, substantial heterogeneity across omics, imaging, and spatial modalities poses significant challenges. Naive fusion of semantically distinct sources often leads to ambiguous representations. Additionally, the resolution mismatch between high-resolution histology images and lower-resolution sequencing spots complicates spatial alignment. Biological perturbations during sample preparation further distort modality-specific signals, hindering accurate integration. To address these challenges, we propose Graph-guided Representation of Omics and Vision with Expert Regulation for Adaptive Spatial Multi-omics Fusion (GROVER), a novel framework for adaptive integration of spatial multi-omics data. GROVER leverages a Graph Convolutional Network encoder based on Kolmogorov–Arnold Networks to capture the nonlinear dependencies between each modality and its associated spatial structure, thereby producing expressive, modality-specific embeddings. To align these representations, we introduce a spot-feature-pair contrastive learning strategy that explicitly optimizes the correspondence across modalities at each spot. Furthermore, we design a dynamic expert routing mechanism that adaptively selects informative modalities for each spot while suppressing noisy or low-quality inputs. Experiments on real-world spatial omics datasets demonstrate that GROVER outperforms state-of-the-art baselines, providing a robust and reliable solution for multimodal integration.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义
- **核心问题**：空间多组学数据（如转录组、蛋白质组、表观组）虽然提供了分子层面的空间分布信息，但缺乏病理形态学上下文，难以全面解析组织微环境。整合组织病理学图像可弥补这一缺失，但面临巨大挑战：
  - 组学、图像与空间模态之间存在显著语义异质性，简单融合易导致表示模糊。
  - 高分辨率病理图像与低分辨率测序点（spot）存在空间分辨率不匹配，对齐困难。
  - 样本制备过程中的生物学扰动会扭曲模态特异性信号，影响整合准确性。
- **整体含义**：提出一种自适应融合框架 **GROVER**，旨在通过图引导的表示学习和专家调控机制，动态整合空间多组学与病理图像，为组织复杂性解析提供更鲁棒、可靠的统一嵌入。

### 2. 论文提出的方法论
- **核心思想**：
  - 采用图结构建模空间关系与模态内特征相似性，使用基于 **Kolmogorov–Arnold 网络（KAN）** 的图卷积编码器提取表达性嵌入。
  - 引入 **spot‑特征对对比学习**，在弱配对条件下对齐跨模态语义，缓解组学与图像的语义鸿沟。
  - 设计 **自适应混合专家（MoE）架构**，依据每个测序点的局部信号质量，动态选择或抑制不同模态的贡献，实现鲁棒融合。
- **关键技术细节**：
  - **图构建**：对每个模态分别构建空间邻接图（基于坐标KNN）和特征图（基于特征KNN），联合编码空间与语义结构。
  - **KAN‑GCN 编码器**：将标准GCN的线性变换替换为KAN的非线性函数，增强消息传递的表达能力。通过空间‑特征注意力融合来自空间图与特征图的嵌入。
  - **Spot‑特征对对比学习**：
    - 利用预训练病理基础模型提取与空间坐标对应的图像块嵌入，实现空间对齐。
    - 设计双向掩码对比损失：为每个模态对（RNA‑ADT、RNA‑Image、ADT‑Image）计算余弦相似度，并通过动态阈值剔除语义高度相似的假阴性样本，再计算掩码InfoNCE损失，强制跨模态一致性。
  - **自适应 MoE 融合**：
    - 聚合对齐后的三模态嵌入，经门控网络输出各模态置信度，经 softmax 与阈值过滤（γ=0.3）得到自适应权重。
    - 每个模态配备独立专家（前馈网络），加权求和获得最终融合表示；若所有权重低于阈值，则退化为最高置信度模态的专家输出。
    - 采用图解码器重构各模态原始特征，与对比损失联合优化总目标。
- **公式/算法流程**（文字说明）：
  1. 输入：多模态特征 \(F^{(m)}\) 与空间坐标 \(S\)。
  2. 构建空间图 \(G_S\) 与特征图 \(G_F^{(m)}\)。
  3. 通过 KAN‑GCN 提取空间与特征嵌入，经注意力融合为模态感知嵌入 \(\tilde{e}_i^{(m)}\)。
  4. 对嵌入进行掩码对比学习，对齐模态对，得到对齐后嵌入 \(\hat{e}_i^{(m)}\)。
  5. 通过门控网络计算每个spot的各模态权重，经阈值滤波后与专家输出加权融合，得到最终统一表示 \(z_i\)。
  6. 解码器重构各模态特征，总损失由重构损失与对比损失加权组成（λ=2）。

### 3. 实验设计
- **数据集**（4 个公共10x Visium 空间多组学数据集）：
  - 人类乳腺癌基因与蛋白表达数据集
  - 人类胶质母细胞瘤基因与蛋白表达数据集
  - 人类扁桃体基因与蛋白表达数据集
  - 人类扁桃体附加抗体基因与蛋白表达数据集
  - 数据集均包含转录组、蛋白质组和H&E染色组织学图像。
- **Benchmark 与对比方法**：
  - 对比了最新的多模态空间组学方法：**MISO**（支持图像模态）、**SpatialGlue**（双模态注意力）、**COSMOS**（图卷积+加权近邻）。
  - 评估指标（9种聚类评价指标）：ARI、NMI、FMI、SC、AMI、Jaccard、DBI、CHI、Purity。
  - 使用RNA和ADT分别得到的细胞类型标签进行聚类评估，报告五个聚类数设置下的均值和标准差。
- **实验设置**：
  - 聚类任务用于评估空间域识别能力。
  - 消融实验：移除MoE模块（改为简单求和）、移除对比损失、将KAN‑GCN替换为标准GCN。
  - 参数敏感性分析：对置信阈值γ和对比损失权重λ进行分析。

### 4. 资源与算力
- **硬件配置**：双 NVIDIA RTX A5000 GPU（24 GB），双 Intel Xeon Silver 4210R CPU（2.40 GHz, 20 核×2）。
- **训练情况**：在给定计算配置下，GROVER 在 300 个训练轮次内收敛。

### 5. 实验数量与充分性
- **实验组数**：
  - 在 **4 个数据集** 上与 **3 种基线方法** 进行定量比较，共 9 项指标，每个实验重复多次并报告标准差。
  - 完成 **消融实验**（1 个数据集上展示，其余数据集结果见附录），验证各模块的有效性。
  - **参数敏感性实验**（1 个数据集）分析关键超参数的影响。
  - **定性可视化**（4 个数据集的聚类结果空间分布图）。
- **充分性与公平性**：
  - 数据集均使用公开基准，涵盖不同组织类型和抗体组合，增加了泛化性验证。
  - 对比方法均来自近期顶会/顶刊，具有较强的代表性，且统一使用公开预处理数据与评估协议，比较公平。
  - 消融与敏感性分析系统地证明了各组件的必要性，实验设计全面。

### 6. 论文的主要结论与发现
- GROVER 在所有四个数据集和多数聚类指标上均优于现有方法，特别是在空间一致性指标（SC、CHI）和聚类准确性指标（ARI、FMI）上提升显著。
- 自适应 MoE 能够动态过滤低质量模态信号，避免均匀融合带来的性能下降（例如 MISO 虽然支持图像但效果不佳）。
- Spot‑特征对对比学习有效对齐了语义异构的多模态数据，显著增强了空间结构保真度。
- KAN‑GCN 凭借非线性变换能力，在捕捉复杂空间‑特征交互方面优于传统 GCN。
- 参数分析显示模型对阈值 γ 和对比权重 λ 具有良好的鲁棒性。

### 7. 优点
- **新颖的自适应融合框架**：首次将基于KAN的图编码与动态专家路由引入空间多组学整合，解决了模态质量不均匀的痛点。
- **高效的跨模态对齐策略**：掩码对比学习方案有效缓解了语义鸿沟和假阴性问题，增强了图像与组学之间的对应关系。
- **全面的实验验证**：在四个真实数据集、多指标、与强基线对比下表现出一致的领先性能，消融分析充分论证了各组件的贡献。
- **模块化设计**：支持灵活接入各类预训练病理基础模型，易于扩展和迭代。
- **代码开源**，可复现性强。

### 8. 不足与局限
- **实验覆盖**：
  - 仅在 10x Visium 转录组+蛋白质组+图像的数据上测试，未涉及表观组（如 ATAC）或更高分辨率的空间技术（如 Stereo‑seq、MERFISH），泛化性有待进一步验证。
  - 未在疾病预后、细胞通讯等更下游的分析任务上评估，尚不清楚统一嵌入对更广泛生物问题的增益。
- **偏差风险**：
  - 聚类评价的标签来自 RNA 和 ADT 分别注释，可能存在不同的生物学划分，导致部分方法标准差较高，解释时需谨慎。
  - 预训练图像编码器的选择会影响性能，论文未系统比较不同基础模型的影响。
- **应用限制**：
  - 阈值 γ 设为 0.3，虽实验稳健，但不同数据集可能需要微调。
  - 模型复杂度较高（KAN‑GCN + MoE + 三重对比），训练时间可能长于简单基线，但论文未与基线的效率进行对比分析。
  - 掩码对比损失的阈值 δ 设定细节未在正文详细说明，可能影响特定场景下的假阴性过滤效果。

（完）
