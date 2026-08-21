---
title: "TopoCellGen: Generating Histopathology Cell Topology with a Diffusion Model"
title_zh: TopoCellGen：用扩散模型生成组织病理学细胞拓扑
authors: "Xu, Meilong, Gupta, Saumya, Hu, Xiaoling, Li, Chen, Abousamra, Shahira, Samaras, Dimitris, Prasanna, Prateek, Chen, Chao"
date: 2025-06-01
pdf: "https://openaccess.thecvf.com/content/CVPR2025/papers/Xu_TopoCellGen_Generating_Histopathology_Cell_Topology_with_a_Diffusion_Model_CVPR_2025_paper.pdf"
tags: ["query:cell-graph"]
score: 9.0
evidence: 生成多类细胞拓扑，直接建模细胞分布、相互作用和肿瘤微环境
tldr: 该论文针对数字病理学中多类细胞拓扑建模的挑战，提出TopoCellGen，一种将拓扑约束融入扩散模型的新方法，用于生成真实的细胞拓扑。该方法细化了细胞分布和相互作用的模拟，提高了精度和可解释性。生成的多类细胞拓扑可用于增强下游任务数据、模拟复杂组织环境，并为肿瘤微环境的控制和泛化提供新途径。这项工作对细胞图构建和空间细胞分析具有重要价值。
source: CVPR-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-xu-topocellgen-generating-histopathology-cell-topology-with-a-diffusion-model-cvpr-2025-paper/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 882, \"height\": 321}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-xu-topocellgen-generating-histopathology-cell-topology-with-a-diffusion-model-cvpr-2025-paper/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1805, \"height\": 766}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-xu-topocellgen-generating-histopathology-cell-topology-with-a-diffusion-model-cvpr-2025-paper/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 877, \"height\": 555}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-xu-topocellgen-generating-histopathology-cell-topology-with-a-diffusion-model-cvpr-2025-paper/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 879, \"height\": 355}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-xu-topocellgen-generating-histopathology-cell-topology-with-a-diffusion-model-cvpr-2025-paper/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1707, \"height\": 616}]"
tables_json: "[{\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-xu-topocellgen-generating-histopathology-cell-topology-with-a-diffusion-model-cvpr-2025-paper/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1645, \"height\": 301}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-xu-topocellgen-generating-histopathology-cell-topology-with-a-diffusion-model-cvpr-2025-paper/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1650, \"height\": 388}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-xu-topocellgen-generating-histopathology-cell-topology-with-a-diffusion-model-cvpr-2025-paper/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 688, \"height\": 321}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-xu-topocellgen-generating-histopathology-cell-topology-with-a-diffusion-model-cvpr-2025-paper/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 687, \"height\": 240}]"
motivation: 多类细胞拓扑的准确建模对理解组织结构至关重要，但现有方法缺乏对细胞分布和相互作用的精细模拟。
method: 提出将拓扑约束集成到扩散模型中，生成真实且上下文准确的细胞拓扑。
result: 改进了细胞分布和相互作用的模拟，提高了精度和可解释性。
conclusion: 为肿瘤微环境的模拟和下游任务增强提供了新机会。
---

## Abstract
Accurately modeling multi-class cell topology is crucial in digital pathology, as it provides critical insights into tissue structure and pathology. The synthetic generation of cell topology enables realistic simulations of complex tissue environments, enhances downstream tasks by augmenting training data, aligns more closely with pathologists' domain knowledge, and offers new opportunities for controlling and generalizing the tumor microenvironment. In this paper, we propose a novel approach that integrates topological constraints into a diffusion model to improve the generation of realistic, contextually accurate cell topologies. Our method refines the simulation of cell distributions and interactions, increasing the precision and interpretability of results in downstream tasks such as cell detection and classification. To assess the topological fidelity of generated layouts, we introduce a new metric, Topological Frechet Distance (TopoFD), which overcomes the limitations of traditional metrics like FID in evaluating topological structure. Experimental results demonstrate the effectiveness of our approach in generating multi-class cell layouts that capture intricate topological relationships. Code is available at https://github.com/Melon-Xu/TopoCellGen.

---

## 论文详细总结（自动生成）

# TopoCellGen 论文结构化总结

## 1. 论文的核心问题与整体含义

- **研究背景**：在数字病理学中，多类细胞的空间组织、聚集、混合和连接等拓扑关系，对理解组织结构、肿瘤微环境、疾病进展及预后具有重要价值。例如肿瘤浸润淋巴细胞（TILs）的分布、肿瘤出芽等均与临床结局相关。
- **现有问题**：
  - 主流生成模型（GAN、扩散模型）大多直接生成组织病理图像，视觉上逼真，但缺乏对细胞布局和细胞间拓扑关系的显式建模，难以与病理学家的领域知识对齐。
  - 少数面向细胞布局生成的方法（如 Spatial Diffusion）对细胞密度的控制较粗糙，不能精细保持类内空间分布与类间拓扑关系。
  - 常用评估指标如 FID 主要衡量视觉/特征分布相似性，不够敏感于拓扑结构差异。
- **本文整体含义**：提出首个面向数字病理学的细胞拓扑布局扩散模型 TopoCellGen，通过拓扑约束和细胞计数约束，生成更真实、更具生物学可解释性的多类细胞布局；并提出 TopoFD 指标，专门评估拓扑保真度。

---

## 2. 方法论：核心思想与关键技术细节

- **基础生成框架**：采用条件 DDPM 扩散模型，输入条件为各类细胞的计数向量 \(c=[c_1,c_2,\dots,c_n]\)，通过 UNet 逐步去噪生成多类细胞布局。
- **无噪布局估计**：在训练过程中，利用噪声调度参数从当前噪声状态 \(x_t\) 估计无噪布局 \(\hat{x}_t^0\)，方便后续施加约束。
- **三个核心损失函数**：
  - **细胞计数损失 \(L_{count}\)**：
    - 由于细胞计数不可微，使用 Straight-Through Estimator（STE）对预测布局进行二值化。
    - 逐通道比较预测布局与真实布局的细胞数量差异，其中单个细胞按 \(3\times 3\) 面积计算，实现对生成细胞密度的精确控制。
  - **类内空间一致性损失 \(L_{intra}\)**：
    - 对每个类别的二值布局分别计算距离变换图。
    - 提取 1 维持续同调持久图（persistence diagram）。
    - 将预测持久图与真实持久图进行 Wasserstein 最优匹配，并用匹配点之间的平方距离度量差异。
    - 对所有类别取平均，保持每一类细胞内部的空间分布和拓扑结构。
  - **类间结构正则化损失 \(L_{inter}\)**：
    - 将所有类别聚合为一个单通道聚合布局。
    - 同样计算距离变换、1 维持久图，并与真实聚合布局的持久图计算 Wasserstein 距离。
    - 目的是保持不同类别细胞之间的整体空间交互和结构关系。
- **总损失**：
  \[
  L_{total} = L_{simple} + \lambda_c L_{count} + \lambda_{intra} L_{intra} + \lambda_{inter} L_{inter}
  \]
  其中 \(\lambda_c,\lambda_{intra},\lambda_{inter}\) 为超参数。
- **Topological Fréchet Distance（TopoFD）指标**：
  - 对每一类细胞，提取细胞中心点云，计算 1 维持久图。
  - 在参考集和合成集内分别求 Wasserstein barycenter。
  - 将持久图转为 persistence landscapes 并向量化，得到均值向量和协方差矩阵。
  - 对每个类别计算 Fréchet 距离，再对所有类别取平均，得到最终 TopoFD。
  - 该指标比 FID 更能反映拓扑结构和空间配置差异。
- **布局到图像生成**：使用 guided diffusion 根据生成的细胞布局合成 H&E 病理图像，用于下游任务的数据增强。

---

## 3. 实验设计

- **数据集**：
  - **BRCA-M2C**：TCGA 乳腺癌细胞分类数据集，用于多类细胞检测和分类。
  - **Lizard**：结直肠核实例分割与分类大数据集。
- **对比方法**：
  - ADM [11]
  - TMCCG [2]
  - Spatial Diffusion / SpaDM [44]
- **生成质量评估指标**：
  - FID（使用针对各数据集自定义训练的特征提取器）
  - 每类细胞计数误差、总计数误差 TCE
  - 提出的 TopoFD
  - MMD（最大均值差异）
- **下游任务实验**：
  - 在 BRCA-M2C 上生成 2,000 对图像-布局作为增强数据。
  - 分别使用 UNet 和 MCSpatNet 进行细胞检测与分类。
  - 比较不使用合成数据、使用随机合成、TMCCG、SpaDM 和 TopoCellGen 合成数据时的 F1 分数。
- **生物合理性评估**：邀请一位具有 7 年以上经验的病理学家，对合成布局是否接近真实、是否保留良恶性特征进行评价。

---

## 4. 资源与算力

- **文中未明确给出算力信息**：
  - 主文和当前提取内容中未提及 GPU 型号、GPU 数量、训练时长、批次大小或具体训练轮数。
  - 仅提到实现细节在补充材料中，但从本提取文本无法获得具体算力信息。
  - 因此，无法从现有内容评估方法对算力的需求和可复现性。

---

## 5. 实验数量与充分性

- **主要实验组数**：
  - 生成质量对比实验：2 个数据集 × 4 种方法，包含多类计数

- 下游任务实验：在 BRCA-M2C 上，分别使用 UNet 和 MCSpatNet 两种检测模型，对比无合成数据、随机合成、TMCCG、SpaDM、TopoCellGen 五种数据增强条件，共 10 组实验，评估 F1 分数。
- 病理学家评估：邀请一位 7 年以上经验的病理学家对合成布局进行盲评，评价其接近真实程度以及是否保留良恶性结构特征；该评估属于定性验证，样本数量有限，但能提供生物学合理性支持。
- 消融实验：通过逐步移除细胞计数损失 \(L_{count}\)、类内拓扑损失 \(L_{intra}\)、类间正则化损失 \(L_{inter}\)，验证各模块对生成质量和拓扑保真度的贡献；消融组数通常为 4–6 组配置，具体数量未在提取文本中明确给出。
- **充分性评价**：实验覆盖生成质量、拓扑保真度、下游任务性能和专家主观评价，维度较为全面，能够支撑论文的主要结论；但病理学家评估样本量可能较小，且仅在一个或两个数据集上验证，外部有效性和可复现性仍有提升空间。总体而言，实验设计基本充分，但尚缺少更大规模多中心数据验证。

（完）
