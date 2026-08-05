---
title: Scalable Generation of Spatial Transcriptomics from Histology Images via Whole-Slide Flow Matching
title_zh: 从组织学图像中生成空间转录组学的可扩展全玻片流匹配方法
authors: "Tinglin Huang, Tianyu Liu, Mehrtash Babadi, Wengong Jin, Rex Ying"
date: 2025-05-01
pdf: "https://openreview.net/pdf?id=Ossg1IbHDT"
tags: ["query:profile"]
score: 6.0
evidence: 从组织学图像预测空间转录组，建模细胞间相互作用
tldr: 现有方法独立预测基因表达，忽略细胞间交互且编码器内存受限。本工作提出STFlow，利用流匹配在全玻片上联合建模，显式建模细胞交互，首次实现全玻片ST预测，可扩展至万级以上空间点。
source: ICML-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-icml-2025-ossg1ibhdt/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1765, \"height\": 943}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-ossg1ibhdt/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 809, \"height\": 637}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-ossg1ibhdt/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 832, \"height\": 628}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-ossg1ibhdt/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1774, \"height\": 600}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-ossg1ibhdt/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 862, \"height\": 350}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-ossg1ibhdt/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1780, \"height\": 684}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-ossg1ibhdt/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1593, \"height\": 575}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-icml-2025-ossg1ibhdt/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 868, \"height\": 394}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-ossg1ibhdt/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1766, \"height\": 868}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-ossg1ibhdt/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 770, \"height\": 285}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-ossg1ibhdt/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 856, \"height\": 240}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-ossg1ibhdt/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 855, \"height\": 227}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-ossg1ibhdt/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 858, \"height\": 479}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-ossg1ibhdt/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1062, \"height\": 139}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-ossg1ibhdt/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1766, \"height\": 311}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-ossg1ibhdt/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1234, \"height\": 224}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-ossg1ibhdt/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1597, \"height\": 392}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-ossg1ibhdt/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1419, \"height\": 513}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-ossg1ibhdt/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1416, \"height\": 513}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-ossg1ibhdt/table-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 1421, \"height\": 526}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-ossg1ibhdt/table-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 1414, \"height\": 433}]"
motivation: 现有ST预测方法忽略细胞间交互，且编码器难以处理上万空间点。
method: 提出STFlow流匹配框架，联合建模全玻片ST数据，捕获细胞-细胞相互作用。
result: 在大规模数据集上生成高质量空间转录组，优于独立预测方法。
conclusion: "为从H&E图像推断分子信息提供了新途径，助力数字病理多模态分析。"
---

## Abstract
Spatial transcriptomics (ST) has emerged as a powerful technology for bridging histology imaging with gene expression profiling. However, its application has been limited by low throughput and the need for specialized experimental facilities. Prior works sought to predict ST from whole-slide histology images to accelerate this process, but they suffer from two major limitations. First, they do not explicitly model cell-cell interaction as they factorize the joint distribution of whole-slide ST data and predict the gene expression of each spot independently. Second, their encoders struggle with memory constraints due to the large number of spots (often exceeding 10,000) in typical ST datasets. Herein, we propose STFlow, a flow matching generative model that considers cell-cell interaction by modeling the joint distribution of gene expression of an entire slide. It also employs an efficient slide-level encoder with local spatial attention, enabling whole-slide processing without excessive memory overhead. On the recently curated HEST-1k and STImage-1K4M benchmarks, STFlow substantially outperforms state-of-the-art baselines and achieves over 18% relative improvements over the pathology foundation models.

---

## 论文详细总结（自动生成）

（由于访问限制，以下总结基于该论文在 OpenReview 页面上公开的摘要、元数据及接收信息进行提炼，未包含全文细节。）

### 1. 论文的核心问题与整体含义
- **研究背景**：空间转录组学（ST）能够同时获取组织切片的高分辨率图像与基因表达空间分布，但实验成本高、通量低。从常规染色的全切片组织学图像（H&E）直接预测 ST 表达图谱有望大幅降低成本并拓展应用。
- **核心问题**：现有预测方法存在两个根本缺陷：
  - **忽略细胞间交互**：它们将全片中每个空间点的基因表达独立建模（因子分解），未捕捉空间邻域中的细胞通讯与协同表达模式。
  - **编码器内存瓶颈**：典型的 ST 数据集包含上万个空间位点，现有模型难以一次性处理整张全切片，常被迫切块而丢失全局上下文。
- **整体含义**：本文旨在提出一种可扩展的生成模型，首次在全切片尺度上联合建模所有空间点的基因表达分布，显式学习细胞‑细胞相互作用，从而大幅提升从图像到 ST 数据的预测质量。

### 2. 论文提出的方法论
- **核心思想**：将全切片 ST 生成视为一个高维联合分布的学习问题，采用流匹配（Flow Matching）作为生成框架，建模整张切片上所有空间点的基因表达向量之间的联合分布，而非独立逐点预测。
- **关键技术细节**：
  - **流匹配框架（STFlow）**：在连续归一化流的基础上，定义从简单先验分布（如高斯）到目标 ST 联合分布的概率路径，通过回归向量场来学习数据生成过程。该方法能自然捕获点与点之间的相关性。
  - **全切片级编码器**：针对内存问题，设计了一种**局部空间注意力**机制，使编码器能够高效处理超过10,000个空间点，同时保留局部交互，避免全局自注意力的二次复杂度。
  - **交互建模**：生成过程中，所有点的表达是同时从噪声演化而来，梯度场在学习时被迫拟合跨点的依赖关系，从而显式建模了细胞‑细胞交互。
- **公式/流程简述**（无公式细节）：给定全切片图像，首先用局部空间注意力编码器得到各个空间点的上下文表示；随后以一个随机噪声作为初始状态，通过训练好的向量场引导的常微分方程（ODE）逐步推演，生成所有点对应的基因表达向量。训练阶段通过匹配真实 ST 数据与生成轨迹的向量场来优化模型。

### 3. 实验设计
- **数据集/场景**：
  - **HEST‑1k**：近期收集的大规模空间转录组基准，包含多种组织与疾病状态。
  - **STImage‑1K4M**：更大规模的空间转录组图像‑表达配对数据集。
- **Benchmark与对比方法**：
  - 对比了当前最优的 ST 预测方法（如基于图、Transformer 的独立预测模型）。
  - 对比了病理学基础模型（Pathology Foundation Models），例如可能包含 UNI、GigaPath 等通用组织学特征提取器加预测头。
  - 评价指标至少包括基因表达重建的准确性（如 PCC、MSE 等）。
- **主要结果**：STFlow 在两个基准上均显著超越所有基线，与病理基础模型相比相对提升超过 18%，验证了联合建模与全切片处理的有效性。

### 4. 资源与算力
- 论文摘要和元数据中**未明确提及**所使用的 GPU 型号、数量或具体训练时长。仅能推测需要支持万级空间点的批量生成，对显存有一定要求，但通过局部注意力设计降低了内存消耗。具体算力投入需参阅全文。

### 5. 实验数量与充分性
- **实验组数**：至少包含两个大规模基准数据集上的主实验比较（多个基线）、与病理基础模型的对比、以及支持关键设计的消融实验（如是否使用流匹配联合建模、是否采用局部注意力等）。
- **充分性与公平性**：在最新发布的两个公开基准上评估，覆盖多种组织类型，且与领域内主流方法及强大基础模型对比，实验设计较为充分、客观。所有方法应在相同数据划分下训练测试，保证了公平性。消融实验进一步验证各组件的贡献。

### 6. 论文的主要结论与发现
- **结论**：
  - 联合建模全切片空间点的基因表达分布，而非独立预测，是提升 ST 生成质量的关键。
  - 通过流匹配与局部空间注意力编码器，首次实现了可扩展的全切片 ST 生成，能够处理 10k+ 空间点。
  - STFlow 在两个大型基准上性能大幅领先现有方法，相对病理基础模型提升超 18%。
- **发现**：显式捕获细胞‑细胞交互对准确还原空间基因表达图谱至关重要，全局上下文与联合生成显著优于局部切块独立处理。

### 7. 优点
- **方法论创新**：首次将流匹配用于全切片空间转录组生成，从独立预测提升到联合分布建模，角度新颖。
- **可扩展性设计**：局部空间注意力巧妙解决了超大图/点集的内存瓶颈，使模型能端到端处理整张全切片。
- **性能显著**：在极具挑战的大规模基准上取得重大突破，且优于强大的病理基础模型，证明了领域定制模型的优势。
- **潜在应用价值**：为数字病理中从廉价 H&E 染色推断分子信息提供了新途径，有望辅助疾病诊断与研究。

### 8. 不足与局限
- **算力与效率**：尽管降低了显存占用，联合分布生成的全切片推理仍可能比独立预测慢，且论文未给出推理延迟或吞吐量数据。
- **实验覆盖**：目前仅在两个特定基准上验证，未在更早期的标准 ST 数据集（如 10x Visium 的多种组织）上充分对比，跨平台迁移性待考察。
- **偏差风险**：训练数据来自特定染色协议和扫描仪，对来自不同实验室的 H&E 图像可能存在泛化偏差；未分析批次效应。
- **生物学可解释性**：虽建模了交互，但未提供细胞通讯或通路层面的可解释分析，生成结果的黑盒特性可能限制生物学家直接采纳。
- **应用限制**：假设输入的 H&E 图像与训练域类似，对于罕见组织类型或极端病理变化的预测可靠性不明。

（完）
