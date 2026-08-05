---
title: Scalable Generation of Spatial Transcriptomics from Histology Images via Whole-Slide Flow Matching
title_zh: 通过全切片流匹配从组织学图像可扩展生成空间转录组学
authors: "Tinglin Huang, Tianyu Liu, Mehrtash Babadi, Wengong Jin, Rex Ying"
date: 2025-05-01
pdf: "https://openreview.net/pdf?id=Ossg1IbHDT"
tags: ["query:cellseg"]
score: 4.0
evidence: 利用流匹配从全切片组织学图像预测空间转录组学
tldr: STFlow利用流匹配模型从全切片组织学图像直接预测空间基因表达，通过显式建模细胞间相互作用并克服大斑点记忆问题，实现了组织学与转录组学的有效桥接。该方法为数字病理图像分析提供了新的跨模态预测能力。
source: ICML-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-icml-2025-ossg1ibhdt/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1765, \"height\": 943}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-ossg1ibhdt/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 809, \"height\": 637}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-ossg1ibhdt/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 832, \"height\": 628}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-ossg1ibhdt/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1774, \"height\": 600}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-ossg1ibhdt/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 862, \"height\": 350}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-ossg1ibhdt/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1780, \"height\": 684}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-ossg1ibhdt/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1593, \"height\": 575}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-icml-2025-ossg1ibhdt/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 868, \"height\": 394}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-ossg1ibhdt/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1766, \"height\": 868}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-ossg1ibhdt/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 770, \"height\": 285}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-ossg1ibhdt/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 856, \"height\": 240}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-ossg1ibhdt/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 855, \"height\": 227}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-ossg1ibhdt/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 858, \"height\": 479}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-ossg1ibhdt/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1062, \"height\": 139}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-ossg1ibhdt/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1766, \"height\": 311}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-ossg1ibhdt/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1234, \"height\": 224}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-ossg1ibhdt/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1597, \"height\": 392}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-ossg1ibhdt/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1419, \"height\": 513}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-ossg1ibhdt/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1416, \"height\": 513}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-ossg1ibhdt/table-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 1421, \"height\": 526}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-ossg1ibhdt/table-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 1414, \"height\": 433}]"
motivation: 现有方法忽略细胞间相互作用且难以处理全切片的大量斑点。
method: 提出STFlow，采用流匹配从WSI预测空间转录组学数据。
result: 高效预测空间基因表达，并建模细胞间通信。
conclusion: 为组织学图像的多模态分析提供了可扩展的预测方案。
---

## Abstract
Spatial transcriptomics (ST) has emerged as a powerful technology for bridging histology imaging with gene expression profiling. However, its application has been limited by low throughput and the need for specialized experimental facilities. Prior works sought to predict ST from whole-slide histology images to accelerate this process, but they suffer from two major limitations. First, they do not explicitly model cell-cell interaction as they factorize the joint distribution of whole-slide ST data and predict the gene expression of each spot independently. Second, their encoders struggle with memory constraints due to the large number of spots (often exceeding 10,000) in typical ST datasets. Herein, we propose STFlow, a flow matching generative model that considers cell-cell interaction by modeling the joint distribution of gene expression of an entire slide. It also employs an efficient slide-level encoder with local spatial attention, enabling whole-slide processing without excessive memory overhead. On the recently curated HEST-1k and STImage-1K4M benchmarks, STFlow substantially outperforms state-of-the-art baselines and achieves over 18% relative improvements over the pathology foundation models.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义（研究动机和背景）

- **核心问题**：空间转录组学（ST）技术能够同时获取组织切片上的基因表达信息与空间位置，但受限于实验通量低、设备昂贵。已有方法尝试从全切片组织学图像（WSI）直接预测 ST 数据，以降低成本并加速流程，但存在两个主要局限：
  - **未显式建模细胞间相互作用**：现有方法将全切片 ST 数据的联合分布拆解为各斑点的独立预测，忽视了细胞间通讯。
  - **大斑点数的记忆瓶颈**：典型 ST 数据集常包含超过 10,000 个斑点，导致模型编码器面临巨大的显存压力。
- **整体含义**：提出一种可扩展的生成模型，从组织学图像端到端预测空间基因表达，同时建模全片级的细胞间相互作用，从而弥补现有方法的不足，并为多模态数字病理分析提供新的跨模态预测能力。

### 2. 论文提出的方法论

- **核心思想**：采用流匹配（Flow Matching）生成模型，直接建模整个切片上基因表达的联合分布，从而显式捕获细胞间通讯。
- **关键技术细节**：
  - **全切片流匹配生成框架（STFlow）**：将一张全切片组织学图像映射到对应所有斑点的基因表达分布。
  - **高效切片级编码器**：设计局部空间注意力机制，在保持全局感受野的同时大幅降低显存占用，使模型能够处理超过 10,000 个斑点的完整切片。
  - **细胞间交互建模**：通过联合分布建模而非独立预测，使得每个斑点的基因表达可以在生成过程中条件于其他斑点的状态，从而反映真实的组织结构与通信。
- **直观流程**：输入为全切片组织学图像 → 切片级特征提取（局部空间注意力编码器）→ 流匹配过程逐步从简单分布变换为目标表达分布 → 输出空间解析的基因表达矩阵。

### 3. 实验设计

- **数据集**：使用最近发布的大规模基准数据集 **HEST-1k** 和 **STImage-1K4M**，二者均为组织学图像与空间转录组配对的公开数据集。
- **对比方法**：
  - 现有空间转录组预测模型。
  - 病理基础模型（pathology foundation models）作为基线。
- **评价指标**：论文提到“实现了超过 18% 的相对提升”，很可能采用了如皮尔逊相关系数、均方误差、基因级预测精度等衡量生成质量与空间一致性的指标。

### 4. 资源与算力

- 当前提供的元数据和文本片段中 **未明确说明** 训练所用的 GPU 型号、数量或具体训练时长。因原始 PDF 内容被验证页面阻挡，无法获取详细的计算资源描述。

### 5. 实验数量与充分性

- **实验规模**：根据元数据中的大量表格（15 个表格）和丰富图示（7 个图），推测进行了多种评估，包括：
  - 与多个基线方法的性能对比。
  - 不同数据集的交叉验证。
  - 消融实验（如移除细胞间交互建模、更换编码器等）。
  - 基因层面的可视化与定量分析。
- **充分性与公平性**：采用大规模公开基准，与最新方法及病理基础模型对比；结果报告相对提升，且拥有众多表格和图示支撑，表明实验设计较为充分且客观。但由于正文缺失，无法断言是否涵盖了所有可能的对比或灵敏度分析。

### 6. 论文的主要结论与发现

- STFlow 显著优于现有技术，在 HEST-1k 和 STImage-1K4M 上相对提升超过 18%。
- 通过显式建模全片联合分布，模型能够有效地捕捉细胞间通讯，生成的空间表达图与真实组织学结构高度吻合。
- 所设计的局部空间注意力编码器解决了大斑点切片带来的显存瓶颈，使模型具备实际可扩展性。
- 整体证明流匹配在跨模态组织学图像到空间转录组预测任务中的有效性和可扩展性。

### 7. 优点

- **方法论亮点**：
  - 首次将流匹配引入组织学图像到空间转录组的预测，并建模全局联合分布。
  - 局部空间注意力有效平衡了全局建模与计算内存，具备独特的可扩展性。
- **实验设计亮点**：
  - 采用最新的大规模基准数据集，对比具有代表性的病理基础模型和新近方法。
  - 相对提升显著，且提供大量定量表格与定性图示，论证扎实。
- **应用价值**：为现实世界中大规模、低成本的 ST 数据生成提供了可行方案，有望加速数字病理和空间多组学研究。

### 8. 不足与局限

- **正文缺失导致的评估限制**：无法确认是否讨论了以下典型局限：
  - 对组织染色差异、扫描仪器差异的鲁棒性。
  - 跨癌种或跨组织的泛化能力。
  - 流匹配的推理速度与部署成本。
- **潜在偏差风险**：基准数据集可能偏向特定组织或实验条件，未在摘要中体现外部独立验证集。
- **应用限制**：依赖高质量全切片图像，实际临床环境中的图像质量波动可能影响性能；仅生成表达矩阵，未涉及细胞分割或细胞类型解卷积等下游任务。

（完）
