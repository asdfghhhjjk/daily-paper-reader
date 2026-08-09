---
title: Do Pathology Foundation Models Encode Disease Progression? A Pseudotime Analysis of Visual Representations
title_zh: 病理基础模型是否编码疾病进展？视觉表征的伪时间分析
authors: "Pritika Vig, Renchin Wu, William Lotter"
date: 2026-01-23
pdf: "https://openreview.net/pdf/3c36acdfda826af2f5aabe662e70dca5b42dede3.pdf"
tags: ["query:path-xai-sel"]
score: 9.0
evidence: 分析病理基础模型的潜在空间是否编码疾病连续进展，与计算病理图像分析相关
tldr: 探究病理视觉基础模型是否隐式编码疾病连续进展，借鉴单细胞转录组分析的扩散伪时间方法，发现模型潜在空间确实捕捉到疾病过渡特征，为病理模型提供生物学解释性。
source: ICML-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 基础模型在分类上表现优异，但其表征是否反映连续疾病进程尚不明确。
method: 利用扩散伪时间分析基础模型的潜在表示组织方式。
result: 证实病理基础模型内在地编码了疾病进展的生物学信息。
conclusion: 该发现有助于开发更稳健、可解释的病理AI模型。
---

## Abstract
Vision foundation models trained on discretely sampled images achieve strong performance on classification benchmarks, yet whether their representations encode the continuous processes underlying their training data remains unclear. This question is especially pertinent in computational pathology, where we posit that models whose latent representations implicitly capture continuous disease progression may better reflect underlying biology, support more robust generalization, and enable quantitative analyses of features associated with disease transitions. Using diffusion pseudotime, a method developed to infer developmental trajectories from single-cell transcriptomics, we probe whether foundation models organize disease states along coherent progression directions in representation space. Across four cancer progressions and six models, we find that all pathology-specific models recover trajectory orderings significantly exceeding null baselines, with vision-only models achieving the highest fidelities $(\tau > 0.78$ on CRC-Serrated). Model rankings by trajectory fidelity on reference diseases strongly predict few-shot classification performance on held-out diseases ($\rho = 0.92$), and exploratory analysis shows cell-type composition varies smoothly along inferred trajectories in patterns consistent with known stromal remodeling. Together, these results demonstrate that vision foundation models can implicitly learn to represent continuous processes from independent static observations, and that trajectory fidelity provides a complementary measure of representation quality beyond downstream performance. While demonstrated in pathology, this framework could be applied to other domains where continuous processes are observed through static snapshots.

---

## 论文详细总结（自动生成）

# 论文总结：病理基础模型是否编码疾病进展？视觉表征的伪时间分析

## 1. 论文的核心问题与整体含义

- **核心问题**：视觉基础模型通常在离散采样的图像上进行训练，在分类任务上表现优异，但其学到的表征是否编码了训练数据背后隐含的**连续过程**（如疾病进展）仍不清楚。
- **研究动机与背景**：
  - 在计算病理学中，疾病进展（如癌前病变到侵袭癌）是一个连续过程，但病理切片往往仅提供某个时间点的静态图像。
  - 若模型能隐式捕捉这一连续过程，其表征将更符合底层生物学规律，可能提升泛化能力和对疾病过渡阶段特征的定量分析能力。
  - 该问题对于推动病理 AI 从单纯分类到生物学可解释分析具有重要意义。

## 2. 论文提出的方法论

- **核心思想**：借鉴单细胞转录组学中推断发育轨迹的**扩散伪时间（Diffusion Pseudotime）**方法，探究病理基础模型的潜在空间是否将疾病状态组织成具有连贯进展方向的轨迹。
- **关键技术细节**：
  - 扩散伪时间是一种基于图的算法，通过在高维表征空间中构建细胞（或样本）间的扩散过程，计算各样本在连续轨迹上的相对顺序（伪时间值），从而恢复潜在的发育或进展过程。
  - 将扩散伪时间应用于视觉基础模型提取的图像级特征（潜在表示），分析不同疾病状态的样本是否沿着一个平滑的、方向一致的伪时间轴排列。
  - 通过对比随机基线，量化模型恢复疾病进展轨迹的保真度（trajectory fidelity）。
- **公式或算法流程**（文字概括）：
  - 步骤 1：使用预训练的病理基础模型提取所有图像的嵌入向量。
  - 步骤 2：在嵌入空间中构建样本间的邻接图，计算扩散距离。
  - 步骤 3：选择起源点（如正常组织），基于扩散过程为每个样本计算伪时间值。
  - 步骤 4：将计算出的伪时间顺序与已知的疾病阶段顺序进行比较，用统计指标（如肯德尔秩相关系数 \(\tau\)）衡量一致性。

## 3. 实验设计

- **数据集/场景**：
  - 四种癌症进展过程（文中具体提及 CRC-Serrated，即锯齿状结直肠癌进展，其余三种未在摘要中列出）。
  - 使用六种不同的病理视觉基础模型。
- **基准对比**：
  - 将模型得到的伪时间排序与真实疾病进展阶段排序进行比较，与**随机基线**对比，检验是否统计显著超越偶然水平。
  - 模型排名（按轨迹保真度）还与少量样本下的分类性能（few-shot classification）进行关联分析，验证轨迹保真度作为表征质量补充指标的有效性。
- **对比方法**：
  - 主要对比不同病理基础模型在轨迹保真度上的差异，包括仅视觉模型（vision-only）和可能的多模态模型，发现仅视觉模型保真度最高（CRC-Serrated 上 \(\tau > 0.78\)）。
  - 探索性分析：观察沿推断的伪时间轨迹，细胞类型组成是否平滑变化，并与已知的基质重塑模式一致。

## 4. 资源与算力

- 文中**未明确提及**具体的 GPU 型号、数量或训练时长。由于研究主要使用预训练模型进行特征提取和伪时间分析，计算开销可能相对较小，但未提供具体算力信息。

## 5. 实验数量与充分性

- **实验组数**：
  - 涵盖 4 种癌症进展过程 × 6 个模型，共至少 24 组轨迹保真度评估。
  - 额外进行了与少样本分类性能的相关性分析，以及细胞类型组成的探索性实验。
- **充分性与公平性**：
  - 多种疾病和多模型设置使得结论具有一定普遍性。
  - 引入了随机基线进行统计显著性检验，方法对比公平。
  - 使用独立留出疾病（held-out diseases）评估模型排名与分类性能的关联，避免循环论证，设计较严谨。
  - 探索性分析提供生物学佐证，增强了解释性。

## 6. 论文的主要结论与发现

- 所有病理专用模型均能恢复疾病进展轨迹，且排序显著优于随机基线，证实**病理视觉基础模型能够隐式学习从独立静态观测中捕捉连续过程**。
- 仅视觉模型（vision-only）在轨迹保真度上表现最佳（如 CRC-Serrated 中 \(\tau > 0.78\)）。
- 模型在参考疾病上的轨迹保真度排名与在留出疾病上的少样本分类性能高度相关（\(\rho = 0.92\)），表明**轨迹保真度可作为超越下游任务性能的互补表征质量指标**。
- 推断轨迹上细胞类型组成平滑变化，与已知的基质重塑生物学过程一致，为潜在空间的生物学可解释性提供了证据。

## 7. 优点

- **跨领域方法迁移**：巧妙地将单细胞转录组学的伪时间分析引入计算机视觉和病理学，方法论新颖。
- **揭示隐式编码**：首次系统证明病理视觉基础模型可从静态图像中学习连续疾病进展，深化了对模型表征内涵的理解。
- **新的评估视角**：提出轨迹保真度作为表征质量的新维度，与下游分类性能互补，有助于筛选更符合生物过程的模型。
- **实验设计严谨**：多疾病、多模型对比，引入统计检验和留出疾病关联验证，结论可信度高。

## 8. 不足与局限

- **实验覆盖范围**：
  - 仅涉及四种癌症进展，是否适用于其他癌种或非癌疾病尚需验证。
  - 主要基于病理图像，框架虽声称可推广至其他领域（如连续过程通过静态快照观测），但未提供非病理领域的实证结果。
- **偏差风险**：
  - 已知疾病阶段标签用于评估伪时间排序，若标签本身定义存在模糊性或主观性，可能影响结论的客观性。
  - 伪时间方法依赖根节点选择，不同选择可能影响轨迹形态，文中处理方式未见详述。
- **应用限制**：
  - 轨迹保真度作为表征质量指标是否普遍适用于各类下游任务（如分割、检测）未加探讨。
  - 目前分析限于事后解释，尚未展示如何利用该发现主动改进模型训练或架构。

（完）
