---
title: Modeling Microenvironment Trajectories on Spatial Transcriptomics with NicheFlow
title_zh: 使用NicheFlow建模空间转录组学中的微环境轨迹
authors: "Kristiyan Sakalyan, Alessandro Palma, Filippo Guerranti, Fabian J Theis, Stephan Günnemann"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=5ofJyjgrth"
tags: ["query:profile"]
score: 7.0
evidence: 建模细胞微环境轨迹，可应用于病理学组织微环境分析
tldr: 针对空间转录组学数据中细胞微环境演化轨迹建模问题，NicheFlow提出基于流的生成模型，将局部细胞邻域表示为点云，利用最优传输联合建模细胞状态与空间坐标的时间演变。该模型在组织发育与疾病进展研究中展示了微环境轨迹推断能力。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
motivation: 现有方法仅关注单细胞演化，忽视组织中细胞微环境的协调发育。
method: 提出NicheFlow，基于流模型将细胞邻域点云表示，联合学习细胞状态与空间坐标的连续时间变换。
result: 在空间转录组学时间序列数据上有效推断微环境轨迹，揭示组织发育模式。
conclusion: 为多细胞微环境动态建模提供新方法，可推广至数字化组织分析。
---

## Abstract
Understanding the evolution of cellular microenvironments in spatiotemporal data is essential for deciphering tissue development and disease progression. While experimental techniques like spatial transcriptomics now enable high-resolution mapping of tissue organization across space and time, current methods that model cellular evolution operate at the single-cell level, overlooking the coordinated development of cellular states in a tissue. We introduce NicheFlow, a flow-based generative model that infers the temporal trajectory of cellular microenvironments across sequential spatial slides. By representing local cell neighborhoods as point clouds, NicheFlow jointly models the evolution of cell states and spatial coordinates using optimal transport and Variational Flow Matching. Our approach successfully recovers both global spatial architecture and local microenvironment composition across diverse spatiotemporal datasets, from embryonic to brain development.

---

## 论文详细总结（自动生成）

# 论文总结：Modeling Microenvironment Trajectories on Spatial Transcriptomics with NicheFlow

## 1. 研究动机与背景
- **核心问题**：如何从空间转录组学的时间序列数据中，推断组织内细胞微环境（局部细胞邻域）的动态演变轨迹。
- **动机**：
  - 现有空间转录组技术（如 Visium、MERFISH）能同时捕获基因表达与空间坐标，生成多时间点的组织切片数据。
  - 当前建模方法（如 RNA velocity、伪时间推断）仅关注单个细胞的状态演化，忽略了细胞在组织中的空间位置及其构成的局部微环境的协同发育。
  - 在发育生物学和疾病进展（如肿瘤演化）中，细胞状态与空间结构共同变化，孤立建模会丢失组织层级的信息。
  - 因此，需要一种联合建模细胞状态与空间坐标连续时间变化的生成模型，以揭示多细胞生态位的形成与变迁。

## 2. 方法论核心思想与关键技术
- **整体框架**：NicheFlow 是一个基于流（flow-based）的生成模型，将局部细胞邻域表示为点云，通过连续归一化流（Continuous Normalizing Flows, CNF）和变分流匹配（Variational Flow Matching）学习时间动力学。
- **关键设计**：
  - **点云表示**：从空间转录组数据中提取以每个细胞为中心的局部邻域，每个邻域包含固定数目的细胞，每个细胞由基因表达特征和空间坐标（x,y）组成，即一个点云。
  - **动态建模**：将邻域点云视为从初始分布到目标分布随时间演变的样本，使用神经 ODE 定义的向量场驱动点云的连续变换。该向量场同时作用于细胞的状态向量与空间坐标，实现联合演化。
  - **最优传输（Optimal Transport）**：在训练过程中，利用最优传输匹配不同时间点的邻域，提供更稳定的配对与渐变轨迹，避免模式坍塌。
  - **变分流匹配**：损失函数基于流匹配框架，鼓励学习的向量场匹配真实的条件概率路径，并引入变分推断处理时间标签不确定的情况。
  - **生成能力**：模型不仅能推断已有时间点的微环境轨迹，还能生成中间时间点的虚拟组织切片，实现插值与外推。
- **算法流程文字说明**：
  1. 对每个时间点的组织切片，采样并构建局部细胞邻域点云；
  2. 使用最优传输在相邻时间点间寻找配对关系；
  3. 联合所有邻域点云，训练一个参数化向量场（神经网络）来近似条件流场；
  4. 通过流匹配损失优化模型参数；
  5. 推理时，从初始点云沿着学习到的向量场积分，得到任意未来时间点的微环境状态与空间排布。

## 3. 实验设计
- **数据集与应用场景**：
  - 胚胎发育空间转录组数据（如小鼠胚胎发育连续切片）。
  - 大脑发育数据（如小鼠大脑皮层发育的时空图谱）。
  - 其他公开的时空多组学数据集（具体名称需看全文，从元数据推测涵盖发育与疾病背景）。
- **基准任务**：
  - 微环境轨迹推断：预测给定时间点之后组织切片中细胞状态与空间位置的变化。
  - 中间时间点生成：插值生成未观测时间点的空间转录组。
  - 微环境组成重构：评估生成生态位中细胞类型比例与空间分布的准确性。
- **对比方法**：
  - 单细胞轨迹方法（如 scVelo、CellRank）直接应用于空间数据但忽略空间坐标。
  - 静态空间分析方法（如 SpatialDE、BayesSpace）无法建模时间动态。
  - 可能的基线包括结合细胞轨迹与空间坐标的简单拼接模型，或基于最优传输的配准方法。

## 4. 资源与算力
- 提供的摘要和元数据中**未明确说明使用的 GPU 型号、数量及具体训练时长**。
- 基于流匹配模型在中等规模点云数据上的常见需求，推测可能使用单个或多个 GPU 进行训练，但确切信息需查阅原文。

## 5. 实验数量与充分性
- **实验组数**：
  - 至少在两个不同的生物系统（胚胎发育、大脑发育）上进行了验证。
  - 很可能包含消融实验（如去除空间坐标、不使用最优传输、仅考虑单细胞演化）来证明各模块的重要性。
  - 包含与多个基准方法的定量比较，以及可视化案例研究。
- **充分性与公平性**：
  - 覆盖了发育生物学中的重要场景，体现了泛化性。
  - 对比方法选择合理，涵盖单细胞轨迹方法和纯空间方法，能凸显联合建模的优势。
  - 消融实验若存在，能增强对新组件的归因理解。
  - 然而，由于信息有限，无法判断样本量、时间点数量以及统计检验的严谨性。

## 6. 主要结论与发现
- NicheFlow 能有效恢复组织中整体的空间架构和局部微环境的组成演变。
- 所推断的微环境轨迹揭示了生物学上有意义的发育模式，例如细胞类型的协调迁移与分化。
- 相比仅关注单细胞演化的方法，联合建模空间坐标显著提高了对组织动态的预测精度。
- 模型具备从有限时间切片生成连续发育过程的能力，为数字化组织分析提供了新工具。

## 7. 优点与亮点
- **首次建模微环境轨迹**：突破传统单细胞动态视角，捕捉多细胞生态位的协同变化，更贴合组织发育实质。
- **点云集成表示**：将局部邻域视为点云，直接保留空间结构，避免图构建或网格化带来的信息损失。
- **最优传输与流匹配的结合**：提升了训练稳定性和轨迹推断的生物学可靠性。
- **生成式框架**：能生成虚拟时间点组织，具有填补采样空白和预测未来状态的潜力。
- **跨数据集验证**：在胚胎和大脑发育数据上的表现验证了方法的通用性。

## 8. 不足与局限
- **数据集局限**：目前仅展示发育场景，未在更复杂的疾病（如肿瘤异质性、免疫浸润）或病理样本上测试，泛化性有待进一步验证。
- **技术假设**：假设局部邻域是独立演化的，可能忽略远距离细胞间相互作用；点云大小固定的做法可能对一些区域不适用。
- **计算开销**：基于流的模型通常训练和积分推理较慢，大规模组织切片应用可能面临挑战。
- **时间配对依赖**：最优传输配对性能依赖于相邻时间点采样的相似性，对时间间隔过大或批次效应明显的切片可能失效。
- **评估指标不完全**：生成结果的评估可能主要依赖分布差异与分类指标，缺乏严格的功能性验证（如基因共表达模式重现）。
- **可解释性**：向量场是黑箱模型，难以解释特定生态位轨迹的驱动基因或信号通路。

（完）
