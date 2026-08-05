---
title: "RPMIL: Rethinking Uncertainty-Aware Probabilistic Multiple Instance Learning for Whole Slide Pathology Diagnosis"
title_zh: RPMIL：重新思考不确定性感知的概率多实例学习用于全切片病理诊断
authors: "(PDF |   Details)"
date: 2025-08-01
pdf: "https://www.ijcai.org/proceedings/2025/0275.pdf"
tags: ["query:profile"]
score: 7.0
evidence: 用于全切片病理诊断的MIL方法，整合补丁级信息
tldr: RPMIL重新思考不确定性感知的概率多实例学习，用于全切片病理诊断，有望改善跨补丁信息融合。
source: IJCAI-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/ijcai-2025-accepted/ijcai-2025-275/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 888, \"height\": 659, \"label\": \"Figure\"}, {\"url\": \"assets/figures/ijcai-2025-accepted/ijcai-2025-275/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1809, \"height\": 721, \"label\": \"Figure\"}, {\"url\": \"assets/figures/ijcai-2025-accepted/ijcai-2025-275/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1763, \"height\": 481, \"label\": \"Figure\"}, {\"url\": \"assets/figures/ijcai-2025-accepted/ijcai-2025-275/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1748, \"height\": 486, \"label\": \"Figure\"}, {\"url\": \"assets/figures/ijcai-2025-accepted/ijcai-2025-275/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1770, \"height\": 444, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/ijcai-2025-accepted/ijcai-2025-275/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1827, \"height\": 715, \"label\": \"Table\"}, {\"url\": \"assets/tables/ijcai-2025-accepted/ijcai-2025-275/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 899, \"height\": 364, \"label\": \"Table\"}, {\"url\": \"assets/tables/ijcai-2025-accepted/ijcai-2025-275/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 891, \"height\": 439, \"label\": \"Table\"}, {\"url\": \"assets/tables/ijcai-2025-accepted/ijcai-2025-275/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 893, \"height\": 341, \"label\": \"Table\"}]"
motivation: 全切片病理图像分析需要有效整合补丁信息，现有方法未充分考虑不确定性。
method: 提出RPMIL，一种概率MIL方法，建模不确定性以增强诊断。
result: （无摘要，假设在诊断任务中表现改进）。
conclusion: RPMIL为WSI诊断提供了一种更鲁棒的概率聚合策略。
---

## Abstract
No abstract is available.

---

## 论文详细总结（自动生成）

## 论文核心问题与整体含义

全切片病理图像（WSI）的癌症诊断通常遵循多实例学习（MIL）范式：将一张 WSI（bag）切分为大量补丁（instance），再聚合成一个固定包级特征用于分类。  
现有方法几乎都属于**点估计**范畴，即每个包被映射到一个确定的嵌入向量。这种确定性建模在训练包数量有限时，难以捕获数据的完整变异性，容易导致过拟合和次优的决策边界。  
本文从不确定性估计的视角重新思考 MIL 建模，提出**RPMIL**，一种**不确定性感知的概率多实例学习**方法，目标是将包特征建模为概率分布而非固定点，从而更好地表征数据多样性，并联合利用实例分布和包分布共同驱动预测。

---

## 方法论

### 核心思想
- 将传统 MIL 中的确定性聚合器替换为**概率聚合器**，学习包特征的**分布**（而不是点值）。
- 假设实例特征本身也构成分布，并在预测时联合利用实例分布与包分布，模拟病理学家通过识别肿瘤区域（实例）判断 WSI 是否恶化的过程。

### 关键技术细节
- **包分布构建**：使用变分自编码器（VAE）将实例特征压缩到低维潜在空间，输出包特征的均值 `μ` 和方差 `σ²`，形成正态分布 `z ~ N(μ, σ²)`。
- **重参数化采样**：从分布中采样任意数量的包特征 `z` 供后续分类，采样数量可控制。
- **预测方式**（两种）：
  1. 仅用包分布：  
     `P(y|x) = ∫ P(z|x) P(y|z) dz`（用 MCMC 近似）。
  2. 联合实例与包分布：  
     `P(y|x) = ∫ P(z|x) [∫ P(y|x,z) P(x|z) dx] dz`  
     其中 `P(x|z)` 通过交叉注意力实现（`z` 作 query，`x` 作 key/value），融合后经池化和分类器得到最终预测。
- **损失函数**：
  - 标准交叉熵损失；
  - KL 散度损失，使 `P(z|x)` 靠近标准正态先验；
  - 均方误差（MSE）损失，限制采样特征的均值与点估计特征之间的偏离。
  总损失：  
  `L = λ1·CE + λ2·KL + λ3·MSE`（文中 λ1=1，λ2=λ3=0.5）。

---

## 实验设计

### 数据集
- **Camelyon16**：乳腺癌淋巴结转移分类，官方划分 270 训练 / 129 测试 WSI。
- **TCGA-NSCLC**：非小细胞肺癌亚型分类（LUAD vs LUSC），共 1053 张 WSI，按 6:1.5:2.5 划分训练/验证/测试。

### 预处理与特征提取
- 在 20× 倍数下切分为 256×256 不重叠补丁。
- 特征提取器：ResNet-50（ImageNet 预训练，1024 维）和 PLIP（大规模病理图文预训练，512 维）。

### 对比方法（Benchmark）
- 经典池化：Mean‑pooling、Max‑pooling
- 注意力 MIL：ABMIL、CLAM (SB/MB)、TransMIL、MMIL
- 分布/不确定性相关：DGMIL（实例分布）、DTFD（伪包扩充）、DGR‑MIL（全局表示）
- RPMIL 自身使用两个特征提取器版本（Ours+ResNet‑50，Ours+PLIP）

### 评估指标
ACC、F1‑score、AUC，所有实验重复 5 次汇报均值±标准差。

---

## 资源与算力

文中明确提到所有实验在 **NVIDIA GeForce RTX 3090** 上运行，但未说明使用的 GPU 数量及具体训练时长。

---

## 实验数量与充分性

**实验规模较充实**，包括：
- **主对比实验**：两个数据集 × 多种基线方法，报告全面指标。
- **两大核心消融**：
  1. 点估计 vs 仅包分布 vs 联合实例‑包分布（Table 2）。
  2. 损失函数消融：去除 MSE、去除 KL、两者均去（Table 3）。
- **参数敏感性**：
  - 采样次数（1、10、100、1000）对性能的影响（Figure 3）。
- **方差有效性验证**：
  - 按包方差从大到大删除样本，观察指标提升（Figure 4），验证方差作为不确定性度量的合理性。
- **聚合器与池化组合**：
  - 不同聚合器（mean/max/attention）与池化（mean/max）的组合（Table 4）。
- **可视化分析**：注意力热力图对比（Figure 5）。

实验设计公平，均采用统一特征提取器与划分标准，消融充分，能支撑主要结论。但未与其他概率 MIL 方法（如 Bayes‑MIL、AGP）进行横向对比，也未测试更多癌种或大样本场景。

---

## 主要结论与发现

1. **不确定性估计优于点估计**：在相同聚合器下，使用包分布 `P(y|z)` 比点估计 `P(y|z=g(x))` 在 ACC、F1、AUC 上均有明显提升。
2. **联合实例分布与包分布大幅提升性能**：加入实例‑包交叉注意力后，性能进一步显著提高，优于仅用包分布。
3. **增加采样数量可稳定并提升结果**：采样数从 1 增加到 1000，性能逐步上升，方差降低。
4. **包方差可衡量不确定性**：删除高方差样本后，模型指标持续上升，说明方差可作为不确定性辅助信息。
5. **RPMIL 在两个公开数据集上达到 SOTA**，尤其在使用 PLIP 特征时，性能均优于现有 MIL 方法。

---

## 优点

- 从不确定性角度重新审视 MIL，为传统点估计方法提供了有理论依据的升级路径。
- 概率包分布 + 实例‑包联合建模的设计新颖，贴合病理诊断逻辑。
- 采样机制灵活，可通过增加采样稳定预测。
- 提供了清晰的公式推导与损失设计，可解释性强。
- 实验消融详尽，明确验证了各组件（KL/MSE 损失、采样数、联合分布）的贡献。
- 使用了两种不同的特征提取器（ResNet 和 PLIP），展示方法的泛化潜力。

---

## 不足与局限

- **计算成本**：多次采样（尤其是 1000 次）会显著增加推理开销，文中未分析推理时间或讨论工程优化。
- **对比不全面**：未与 Bayes‑MIL、AGP 等同样引入不确定性的 MIL 方法比较，无法体现相对优势。
- **数据集局限**：仅测试了 Camelyon16 和 NSCLC 两个二分类任务，未在多类、多中心或更具挑战的数据（如泛癌）上验证。
- **超参数固定**：λ2=λ3=0.5 未经调优探讨，对 Loss 权重的敏感性未展开。
- **袋大小不均衡影响未知**：未分析包内实例数量差异对分布建模的影响。
- **先验假设简单**：假设 P(z|x) 为正态分布，实际数据分布可能更复杂，VAE 的表示能力有限。

（完）
