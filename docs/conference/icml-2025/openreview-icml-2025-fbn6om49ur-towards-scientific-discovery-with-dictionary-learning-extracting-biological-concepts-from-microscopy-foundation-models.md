---
title: "Towards scientific discovery with dictionary learning: Extracting biological concepts from microscopy foundation models"
title_zh: 通过字典学习迈向科学发现：从显微镜基础模型中提取生物学概念
authors: "Konstantin Donhauser, Kristina Ulicna, Gemma Elyse Moran, Aditya Ravuri, Kian Kenyon-Dean, Cian Eastwood, Jason Hartford"
date: 2025-05-01
pdf: "https://openreview.net/pdf?id=fBn6om49Ur"
tags: ["query:pathology-ai"]
score: 7.0
evidence: 从细胞显微镜基础模型中提取生物学概念
tldr: 该论文针对显微镜基础模型内部表征难以解释的问题，提出将稀疏字典学习算法ICFL与PCA白化预处理结合，从细胞显微镜基础模型中提取语义连贯的生物学概念。实验成功恢复了多个与细胞形态和功能相关的概念，验证了字典学习在科学数据上的有效性。该方法为从细胞分析中自动发现可解释的形态参数提供了新途径，直接支持细胞形态参数提取的需求。
source: ICML-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-icml-2025-fbn6om49ur/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1761, \"height\": 568, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-fbn6om49ur/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1768, \"height\": 435, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-fbn6om49ur/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 864, \"height\": 240, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-fbn6om49ur/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1767, \"height\": 292, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-fbn6om49ur/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 851, \"height\": 550, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-fbn6om49ur/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 852, \"height\": 503, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-fbn6om49ur/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1687, \"height\": 598, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-fbn6om49ur/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1776, \"height\": 249, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-fbn6om49ur/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1609, \"height\": 428, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-fbn6om49ur/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1747, \"height\": 1740, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-fbn6om49ur/fig-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1778, \"height\": 1879, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-fbn6om49ur/fig-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1753, \"height\": 1011, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-fbn6om49ur/fig-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 1753, \"height\": 1010, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-fbn6om49ur/fig-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 1754, \"height\": 1013, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-fbn6om49ur/fig-015.webp\", \"caption\": \"\", \"page\": 0, \"index\": 15, \"width\": 1747, \"height\": 1004, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-fbn6om49ur/fig-016.webp\", \"caption\": \"\", \"page\": 0, \"index\": 16, \"width\": 1754, \"height\": 1016, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-fbn6om49ur/fig-017.webp\", \"caption\": \"\", \"page\": 0, \"index\": 17, \"width\": 1733, \"height\": 1467, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-fbn6om49ur/fig-018.webp\", \"caption\": \"\", \"page\": 0, \"index\": 18, \"width\": 1728, \"height\": 1117, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-fbn6om49ur/fig-019.webp\", \"caption\": \"\", \"page\": 0, \"index\": 19, \"width\": 1673, \"height\": 1163, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-icml-2025-fbn6om49ur/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 802, \"height\": 202, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-fbn6om49ur/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 878, \"height\": 408, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-fbn6om49ur/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 835, \"height\": 445, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-fbn6om49ur/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 970, \"height\": 127, \"label\": \"Table\"}]"
motivation: 现有基础模型在科学数据（如细胞显微镜图像）中缺乏可解释概念提取方法，限制了知识发现。
method: 提出将稀疏字典学习算法（ICFL）与PCA白化预处理相结合，从显微镜基础模型的内部表征中提取语义连贯的生物学概念。
result: 成功从显微镜基础模型中恢复了多个具有生物学意义的概念，验证了该方法的有效性。
conclusion: 表明稀疏字典学习可以揭示显微镜基础模型中隐藏的生物学知识，为自动化形态特征发现打下基础。
---

## Abstract
Sparse dictionary learning (DL) has emerged as a powerful approach to extract semantically meaningful concepts from the internals of large language models (LLMs) trained mainly in the text domain. In this work, we explore whether DL can extract meaningful concepts from less human-interpretable scientific data, such as vision foundation models trained on cell microscopy images, where limited prior knowledge exists about which high-level concepts should arise. We propose a novel combination of a sparse DL algorithm, Iterative Codebook Feature Learning (ICFL), with a PCA whitening pre-processing step derived from control data. Using this combined approach, we successfully retrieve biologically meaningful concepts, such as cell types and genetic perturbations. Moreover, we demonstrate how our method reveals subtle morphological changes arising from human-interpretable interventions, offering a promising new direction for scientific discovery via mechanistic interpretability in bioimaging.

---

## 论文详细总结（自动生成）

# 论文详细总结：Towards scientific discovery with dictionary learning: Extracting biological concepts from microscopy foundation models

## 1. 论文的核心问题与整体含义（研究动机和背景）

- **核心问题**：神经网络的内部表征通常难以解释，尤其是无监督学习的基础模型（如掩码自编码器 MAE）在科学数据（如细胞显微镜图像）中能否提取出语义连贯的高层概念？当前的成功主要依赖文本监督或人类可理解领域，而在缺乏先验知识的生物学领域中，字典学习能否奏效尚未可知。
- **研究动机**：显微镜基础模型能够检测精细的细胞形态差异，但现有方法（如余弦相似度）只能给出“哪些扰动相似”而不能解释“为何相似”。因此，需要一种方法自动发现并解释模型中所编码的生物学概念，从而推动科学发现。
- **整体含义**：本文证明稀疏字典学习结合适当的预处理可以从无监督显微镜基础模型中提取有意义的生物学概念（如细胞类型、基因扰动、亚细胞结构），为生物图像的可解释性和自动知识发现开辟新路径。

## 2. 论文提出的方法论：核心思想、关键技术细节、公式或算法流程

### 2.1 核心思想
基于“叠加假设”（neural networks encode many more concepts than neurons），假设每个 token 表示是稀疏概念方向的线性组合。通过字典学习（W ∈ R^{d×M}）和稀疏编码（z ∈ R^M），将高维表示分解为可解释的稀疏特征。

### 2.2 关键技术细节
- **算法：Iterative Codebook Feature Learning (ICFL)**  
  - 改进了正交匹配追踪（OMP），提出批处理版本（Batched-OMP），每次迭代选择与残差最相关的 L 个特征方向，求解最小二乘，然后更新残差。重复 J 次，得到最多 K = J*L 个非零项的特征 z。
  - 与标准 OMP 区别：字典 W_dec 不是固定的，通过梯度下降更新以最小化重建损失。
  - 训练中为防止特征坍塌，对余弦相似度大于 0.9 的列随机重置（random reset）。

- **PCA 白化预处理**  
  - 以控制组（未扰动细胞）的数据为中心，计算其协方差矩阵的特征向量，对扰动样本应用白化变换 T(x) = W(x-μ)，使控制组分布变为零均值单位协方差。
  - 这一步骤作为弱监督：减小控制组中主导方向（如细胞周期）的影响，突出扰动引起的变异。

### 2.3 算法流程（文字说明）
1. **输入**：MAE 模型内部层（如第 16/33 层）的 token 表示 x（1024 或 1664 维）。
2. **预处理**：减去控制组均值 → PCA 白化 → 单位归一化。
3. **训练 ICFL**：  
   - 初始化字典 W_dec（随机正态），偏置 b_pre。
   - 对每个 batch：用 Batched-OMP 从当前字典中提取稀疏特征 z；固定 z，用梯度下降更新 W_dec 和 b_pre 来最小化重建误差。
   - 每 100 步后执行随机重置以防止特征坍塌。
4. **输出**：稀疏特征向量 z（M=8192 个特征方向，每个样本约 100 个非零值）。

## 3. 实验设计：数据集、场景、基准、对比方法

### 3.1 数据集
- **数据来源**：Cell Painting 显微镜图像（256×256×6 像素），来自 RxRx1 和 RxRx3 数据集。
- **基础模型**：两个 MAE（ViT-L/8 和 ViT-G/8），分别称为 MAE-L（330M 参数）和 MAE-G（1.9B 参数）。
- **特征提取位置**：中间层（MAE-L 第 16 层，MAE-G 第 33 层）的残差流或注意力输出，取所有 patch token（1024 个）的平均作为 well 级表示。

### 3.2 任务与基准（Benchmark）
定义了五个分类任务：
| 任务 | 类别数 | 样本数 | 原始线性准确率（MAE-G） |
|------|--------|--------|--------------------------|
| (1) 细胞类型 | 23 | 110,971 | 97.2% |
| (2) 实验批次 | 272 | 80,000 | 87.8% |
| (3) siRNA 扰动 | 1,138 | 81,224 | 51.6% |
| (4) CRISPR 扰动 | 5 | 79,555 | 94.6% |
| (5) 功能基因群 | 39 | 57,863 | 32.1% |

### 3.3 对比方法
- **TopK Sparse Autoencoder** (SAE)：基于 Makazhani & Frey 2013，Gao et al. 2024。
- **CellProfiler 手工特征**：964 个经专家设计的细胞形态特征，作为人类可解释的上限。
- **消融**：是否使用 PCA 白化、不同 token 源（残差流 vs 注意力输出）、不同模型规模（MAE-L vs MAE-G）、不同稀疏度、不同学习率。

## 4. 资源与算力
- **文中明确说明**：
  - 字典学习模型训练：40M tokens，batch size 8192，300k 迭代，学习率 5×10⁻⁵。
  - GPU 型号、数量、训练时长 **未明确说明**。仅推测使用了多 GPU 但具体细节缺失。
- **基础模型训练**：参考 Kraus et al. 2024 和 Kenyon-Dean et al. 2025，未提供资源细节。

## 5. 实验数量与充分性

### 5.1 实验数量
- **主实验**：五个分类任务的线性探测比较（图 4A），ICFL vs TopK SAE vs 原始表示，有/无 PCA 白化。
- **消融实验**：  
  - 稀疏度对重建质量与探测准确率的影响（图 4B、4C、9）。  
  - 学习率（图 9）。  
  - Token 来源（残差流 vs 注意力输出，表 4，图 17）。  
  - 模型规模（MAE-L vs MAE-G，图 17、19）。  
  - 死特征数量（表 1）。  
- **选择性分数分析**：对比 ICFL 和 TopK 在不同任务上的特征选择性（图 8、18、19）。
- **可解释性验证**：  
  - 通道特异性可视化（图 5）。  
  - 单细胞级 recall 验证（表 3，图 6）。  
  - 对粘附连接基因群的深入案例（图 10、6）。
- **与 CellProfiler 对比**：图 2 展示了选择性分数分布和相关性（Pearson 0.71）。

### 5.2 充分性与公平性
- **优点**：覆盖了多种任务（简单到复杂）、多组消融、以及与人类设计特征（CellProfiler）的直接比较，实验设计较为全面。线性探测使用 balanced test accuracy，避免了类别不平衡的影响。
- **潜在不足**：
  - 未比较其他字典学习方法（如 K-SVD、Gated SAE、JumpReLU SAE）。
  - 未在公开基准（如 RXRX1 官方分类任务）上报告标准指标（如 F1）。
  - 可解释性部分依赖定性分析和少量人工标注（仅 5 张图，124 个细胞），结论任意外推需谨慎。

## 6. 论文的主要结论与发现

1. **ICFL + PCA 白化能有效提取语义连贯的生物学特征**，且比 TopK SAE 显著减少死特征（8192 个方向中仅 55 个死特征，而 TopK 有 7640 个）。
2. **线性探测保留大部分生物学信息**：对简单任务（细胞类型、CRISPR 扰动）几乎完整保留；对困难任务（siRNA、功能群）保留约 60-80%。
3. **特征选择性高**：ICFL 有更多特征达到高选择性（如 455 个特征对细胞类型的平均选择性 > 0.5）。
4. **ICFL 与 CellProfiler 手工特征性能相当**（选择性分数 Pearson r=0.71），但使用更少的非零值。
5. **ICFL 重建质量优于 TopK**：相同稀疏度下余弦相似度更高。
6. **模型规模增大提升特征质量**：MAE-G 比 MAE-L 获得更好的探测准确率与选择性。
7. **可解释性潜力**：可通过令牌级热力图识别扰动特异性细胞亚群（如粘附连接受影响 vs 逃逸细胞），召回率达 87.1%。

## 7. 优点：方法或实验设计上的亮点

- **算法创新**：ICFL 结合了批处理 OMP 的稀疏编码灵活性和梯度下降的字典更新，天然避免死特征，计算效率高。
- **弱监督策略**：利用控制数据做 PCA 白化，巧妙降低不相关变异的影响，提升特征选择性。
- **系统性评估**：线性探测 + 选择性分数 + 手工特征对比 + 人类专家验证，多维度验证特征有效性。
- **实际生物学价值**：展示了特征的语义对应关系（如粘附连接、线粒体、ER），并能在单细胞分辨率下识别扰动效果。
- **代码与数据**：论文提供了清晰的方法描述，潜在可复现。

## 8. 不足与局限

- **计算资源未透明**：未报告训练字典学习的 GPU 型号、数量和时长，影响可复现性评估。
- **对比方法不足**：仅与 TopK SAE 和 CellProfiler 对比，未涉及更先进的 SAE 变体（如 Gated SAE、JumpReLU SAE）或其他字典学习算法（K-SVD）。
- **实验泛化性限制**：
  - 仅使用 Cell Painting 一个显微技术（6 通道），未测试其他染色或成像模式。
  - 基础模型仅为 MAE（ViT），未探索其他架构（如 DINOv2）。
- **可解释性验证有限**：单细胞识别的召回率仅基于 5 张图片、124 个细胞，样本量小；特征对齐标签的因果性未验证（仅为相关性）。
- **细粒度任务性能瓶颈**：对 1138 类 siRNA 扰动和 39 类功能群，线性探测准确率大幅下降（< 60%），说明无法捕捉所有微妙变化。
- **依赖控制数据**：PCA 白化需要来自同一分布的未扰动数据，在某些真实场景下可能无法获取。

（完）
