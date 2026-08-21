---
title: "MExD: An Expert-Infused Diffusion Model for Whole-Slide Image Classification"
title_zh: MExD：专家注入扩散模型用于全切片图像分类
authors: "Zhao, Jianwei, Li, Xin, Yang, Fan, Zhai, Qiang, Luo, Ao, Zhao, Yang, Cheng, Hong, Fu, Huazhu"
date: 2025-06-01
pdf: "https://openaccess.thecvf.com/content/CVPR2025/papers/Zhao_MExD_An_Expert-Infused_Diffusion_Model_for_Whole-Slide_Image_Classification_CVPR_2025_paper.pdf"
tags: ["query:cell-path"]
score: 7.0
evidence: 使用专家注入扩散模型进行全切片图像分类
tldr: MExD针对全切片图像分类中图像尺寸大、噪声多、数据不平衡的问题，提出结合专家混合聚合和扩散生成过程的模型，选择性地提取关键特征并直接生成类别分布，提升了分类鲁棒性。
source: CVPR-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-zhao-mexd-an-expert-infused-diffusion-model-for-whole-slide-image-classification-cvpr-2025-paper/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 857, \"height\": 519, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-zhao-mexd-an-expert-infused-diffusion-model-for-whole-slide-image-classification-cvpr-2025-paper/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1794, \"height\": 626, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-zhao-mexd-an-expert-infused-diffusion-model-for-whole-slide-image-classification-cvpr-2025-paper/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 859, \"height\": 541, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-zhao-mexd-an-expert-infused-diffusion-model-for-whole-slide-image-classification-cvpr-2025-paper/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1753, \"height\": 735, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-zhao-mexd-an-expert-infused-diffusion-model-for-whole-slide-image-classification-cvpr-2025-paper/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 832, \"height\": 474, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-zhao-mexd-an-expert-infused-diffusion-model-for-whole-slide-image-classification-cvpr-2025-paper/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1742, \"height\": 1068, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-zhao-mexd-an-expert-infused-diffusion-model-for-whole-slide-image-classification-cvpr-2025-paper/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 871, \"height\": 308, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-zhao-mexd-an-expert-infused-diffusion-model-for-whole-slide-image-classification-cvpr-2025-paper/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 869, \"height\": 458, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-zhao-mexd-an-expert-infused-diffusion-model-for-whole-slide-image-classification-cvpr-2025-paper/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 870, \"height\": 452, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-zhao-mexd-an-expert-infused-diffusion-model-for-whole-slide-image-classification-cvpr-2025-paper/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 869, \"height\": 534, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-zhao-mexd-an-expert-infused-diffusion-model-for-whole-slide-image-classification-cvpr-2025-paper/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 869, \"height\": 455, \"label\": \"Table\"}]"
motivation: WSI分类面临大量非信息区域、噪声和数据不平衡挑战。
method: 结合Mixture-of-Experts机制与扩散模型，通过MoE聚合器均衡补丁特征并扩散生成类别分布。
result: 有效过滤噪声、解决数据不平衡，提升WSI分类性能。
conclusion: 为全切片图像分类提供了一种鲁棒的专家扩散方法。
---

## Abstract
Whole Slide Image (WSI) classification poses unique challenges due to the vast image size and numerous non-informative regions, which introduce noise and cause data imbalance during feature aggregation. To address these issues, we propose MExD, an Expert-Infused Diffusion Model that combines the strengths of a Mixture-of-Experts (MoE) mechanism with a diffusion model for enhanced classification. MExD balances patch feature distribution through a novel MoE-based aggregator that selectively emphasizes relevant information, effectively filtering noise, addressing data imbalance, and extracting essential features. These features are then integrated via a diffusion-based generative process to directly yield the class distribution for the WSI. Moving beyond conventional discriminative approaches, MExD represents the first generative strategy in WSI classification, capturing fine-grained details for robust and precise results. Our MExD is validated on three widely-used benchmarks--Camelyon16, TCGA-NSCLC, and BRACS--consistently achieving state-of-the-art performance in both binary and multi-class tasks.

---

## 论文详细总结（自动生成）

## 1. 论文的核心问题与整体含义

- **研究背景**：全切片图像（WSI）分类是数字病理学中的关键任务，但 WSI 尺寸极大（1 亿到 100 亿像素），无法直接输入常规深度网络。
- **核心挑战**：
  - 图像中存在大量非信息区域，带来噪声。
  - 正负实例比例严重不平衡（阳性癌灶区域通常远少于阴性区域），导致模型偏向多数类。
  - 传统“分解-聚合”策略（尤其是多实例学习 MIL）中，特征聚合方法（平均池化、最大池化等）难以捕捉补丁之间的复杂关系和空间依赖，且易受噪声干扰。
- **整体含义**：论文提出 MExD，首次将**生成式扩散模型**与**专家混合（MoE）机制**结合用于 WSI 分类，从判别式范式转向生成式范式，以更鲁棒地建模数据分布、抑制噪声并缓解数据不平衡。

## 2. 方法论

### 2.1 总体框架
MExD 由三个核心组件组成：
- **Patch 特征提取器（PFE）**：将每个 WSI 切分为补丁，使用预训练 ViT（MoCo V3）或 CTransPath（SRCL）提取实例特征 `{b_i}`。
- **Dyn-MoE 聚合器**：利用 MoE 动态选择最具判别力的补丁，输出专家洞察集合 `g_α` 和先验预测 `ρ_θ`。
- **扩散分类器（Diff-C）**：基于去噪扩散概率模型（DDPM），以 `ρ_θ` 为先验条件，以 `g_α` 为条件信息，生成最终类别分布。

### 2.2 Dyn-MoE 聚合器
- 输入实例特征 `{b_i}` 经过 Adapter（两个 Transformer 层和 PPEG 卷积块）得到带全局依赖的特征 `{l_i}`。
- 设置 **K 个阳性专家 + 1 个阴性专家**，每个专家拥有一个路由网络 `R_r`（单层 2 类 MLP + softmax）。
- 路由机制：每个实例被分配到对应专家子分支，再根据路由得分保留 top-k 实例（稀疏化）。
- 每个专家对筛选后的实例做平均池化得到类中心潜在特征 `e_r`，再经过 `(K+1)` 类分类器 `C_ex` 输出专家置信度 `c_r`。
- 同时，所有专家稀疏化后的实例集合与可学习类别嵌入 `d` 拼接，再经 Adapter 和线性分类器得到先验预测 `ρ_θ`。

### 2.3 扩散分类器（Diff-C）
- **前向扩散**：将真实标签 one-hot 编码为连续 1D 信号 `f_0`，在扩散过程中注入先验预测 `ρ_θ` 作为条件期望，使终点近似 `ρ_θ` 而非纯噪声。
- **逆向去噪**：使用三层 MLP 作为去噪网络 `D`，输入专家特征的加权平均 `Z = Σ c_r · e_r`、当前噪声信号 `f_t`、先验 `ρ_θ` 和时间步 `t`，预测噪声 `ϵ_θ`。
- 逐步从 `f_T` 重建出 `f_0`，直接得到 WSI 的类别分布。

### 2.4 训练目标
- **第一阶段**：训练 Dyn-MoE 辅助模型，使用联合损失 `L_a`，包含先验预测和专家子分支的交叉熵损失之和。
- **第二阶段**：固定 Dyn-MoE，训练去噪网络最小化噪声估计 MSE 损失 `L_e = ||ϵ - ϵ_θ||²`。

## 3. 实验设计

### 3.1 数据集
- **Camelyon16**：乳腺癌淋巴结转移检测，二分类。270 训练 / 130 测试。
- **TCGA-NSCLC**：肺癌亚型分类（LUSC vs. LUAD），二分类。836 训练 / 210 测试。
- **BRACS**：乳腺病变亚型分类（良性、非典型、恶性），三分类。395 训练 / 87 测试。
- 补丁提取：256×256 分辨率，20× 放大倍数，分别产生约 2.8M、5.2M、2.4M 个补丁。

### 3.2 评估协议
- 采用 **5 折交叉验证**，报告 F1-score、ACC、AUC 及其标准差。
- 使用 **PAvPU** 指标和假设检验（配对 t 检验）评估模型不确定性。

### 3.3 对比方法
- 与 12 种 SOTA 方法对比：ABMIL、DSMIL、CLAM-SB、CLAM-MB、TransMIL、DTFD-MIL、MHIM-MIL、MambaMIL、ACMIL、IBMIL、WiKG、PAMIL。
- 使用两种特征提取器（CTransPath 和 ViT）进行公平比较，所有模型在相同实例包和推荐设置下重新训练（PAMIL 结果直接引用）。

## 4. 资源与算力

- 论文提到训练使用 **NVIDIA Tesla A100 GPU**，但未说明具体数量。
- 训练分为两阶段：
  - Dyn-MoE：100 epochs，RAdam 优化器，初始学习率 2e-4，权重衰减 1e-5。
  - Diff-C：200 epochs，Adam 优化器，初始学习率 1e-3，余弦学习率调度。
- **未报告具体训练时长、显存占用或总计算量（FLOPs）**，这是实验报告中的一处不完整。

## 5. 实验数量与充分性

### 5.1 实验类型与规模
- **基准对比**：3 个数据集 × 2 种特征提取器 × 12+ 种对比方法，共数十组对比实验。
- **消融实验**：
  - 组件消融（Dyn-MoE、Diff-C 的独立贡献）。
  - 与 4 种经典 MIL 基线（ABMIL、DSMIL、MeanPooling、MaxPooling）的兼容性实验。
  - 采样比例 α 分析（负专家 α0 和正专家 α1 的多种组合，共 9 组）。
  - 先验预测 ρθ 的有效性分析（有无 ρθ，不同去噪步数 T 从 100 到 400）。
- **不确定性评估**：PAvPU 对比，Q-Q 图验证正态性假设。
- **可视化**：补丁级路由得分分布，展示专家选择关键区域的能力。

### 5.2 充分性与客观性评价
- 实验覆盖较全面，包含多个数据集、多种特征提取器、消融和超参数分析。
- 公平性较好：使用相同实例包和推荐设置重训基线；采用 5 折交叉验证报告均值和标准差。
- 但仍存在不足：未与其他生成式分类方法对比（因为尚属首创）；未报告推理时间；部分基线（PAMIL）结果直接引用，可能带来不公平性。

## 6. 主要结论与发现

- MExD 在 Camelyon16、TCGA-NSCLC、BRACS 上**均取得 SOTA 性能**，无论使用 CTransPath 还是 ViT 特征提取器。
- 例如基于 CTransPath 的 MExD：
  - Camelyon16：F1 97.29%，ACC 97.48%，AUC 98.87%，超越 PAMIL 等。
  - TCGA-NSCLC：F1 96.51%，ACC 96.53%，AUC 98.13%。
  - BRACS：F1 75.17%，ACC 76.13%，AUC 88.08%。
- Dyn-MoE 能有效筛选关键补丁，缓解数据不平衡；Diff-C 利用先验和专家信息提高鲁棒性。
- 不确定性评估表明，MExD 在正确预测时具有更高的置信度，有利于人机协同。

## 7. 优点

- **创新性强**：首次将生成式扩散模型引入 WSI 分类，开辟了新的研究方向。
- **MoE 与扩散模型深度融合**：Dyn-MoE 不仅做特征聚合，还为扩散过程提供专家洞察和先验预测，实现判别与生成的统一。
- **有效缓解数据不平衡**：通过正/负专家分支和稀疏化路由，提高对稀有阳性补丁的敏感性。
- **增强鲁棒性**：生成式去噪过程能隐式抑制噪声干扰，提高预测稳定性。
- **可插拔设计**：对特征提取器不敏感，在不同预训练模型上均表现优异。
- **实验较充分**：多数据集、多基线、多消融和超参数分析，验证了各组件的有效性。
- **不确定性可解释性**：引入假设检验和 PAvPU，为临床辅助决策提供可靠性参考。

## 8. 不足与局限

- **推理效率未评估**：扩散模型需要多步去噪（100-400 步），可能推理耗时较长，但论文未报告推理时间或计算成本。
- **算力报告不完整**：未说明 GPU 数量、训练时长、显存占用等具体资源消耗。
- **对比有限**：作为首个生成式方法，缺乏与其他生成式分类器的比较；PAMIL 结果直接引用可能引入偏差。
- **多分类性能仍待提升**：BRACS 三分类任务上 ACC 约 76-81%，仍有较大提升空间。
- **MoE 扩展性**：专家数量与类别数线性相关，对于大规模多类别/多标签场景可能面临扩展困难。
- **数据集覆盖有限**：仅使用 3 个公开数据集，缺少更多癌种、不同染色协议或外部队列的验证。
- **假设检验依赖正态性**：不确定性评估基于 t 检验和正态性假设，可能在某些数据分布下不完全稳健。
- **缺少可解释性深度分析**：虽然展示了补丁选择可视化，但未系统分析专家路由的语义意义或错误模式。

（完）
