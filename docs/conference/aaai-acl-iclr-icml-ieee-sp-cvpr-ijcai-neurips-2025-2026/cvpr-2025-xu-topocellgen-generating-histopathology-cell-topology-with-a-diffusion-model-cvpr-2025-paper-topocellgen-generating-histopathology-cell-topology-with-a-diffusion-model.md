---
title: "TopoCellGen: Generating Histopathology Cell Topology with a Diffusion Model"
title_zh: TopoCellGen：利用扩散模型生成组织病理细胞拓扑
authors: "Xu, Meilong, Gupta, Saumya, Hu, Xiaoling, Li, Chen, Abousamra, Shahira, Samaras, Dimitris, Prasanna, Prateek, Chen, Chao"
date: 2025-06-01
pdf: "https://openaccess.thecvf.com/content/CVPR2025/papers/Xu_TopoCellGen_Generating_Histopathology_Cell_Topology_with_a_Diffusion_Model_CVPR_2025_paper.pdf"
tags: ["query:cellseg"]
score: 9.0
evidence: 生成数字病理中的逼真多类细胞拓扑，增强肿瘤微环境模拟
tldr: 针对数字病理中多类细胞拓扑建模需求，提出融合拓扑约束的扩散模型TopoCellGen，生成逼真且上下文准确的细胞拓扑分布，可用于数据增强和肿瘤微环境控制与泛化。
source: CVPR-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-xu-topocellgen-generating-histopathology-cell-topology-with-a-diffusion-model-cvpr-2025-paper/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 882, \"height\": 321, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-xu-topocellgen-generating-histopathology-cell-topology-with-a-diffusion-model-cvpr-2025-paper/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1805, \"height\": 766, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-xu-topocellgen-generating-histopathology-cell-topology-with-a-diffusion-model-cvpr-2025-paper/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 877, \"height\": 555, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-xu-topocellgen-generating-histopathology-cell-topology-with-a-diffusion-model-cvpr-2025-paper/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 879, \"height\": 355, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-xu-topocellgen-generating-histopathology-cell-topology-with-a-diffusion-model-cvpr-2025-paper/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1707, \"height\": 616, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-xu-topocellgen-generating-histopathology-cell-topology-with-a-diffusion-model-cvpr-2025-paper/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1645, \"height\": 301, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-xu-topocellgen-generating-histopathology-cell-topology-with-a-diffusion-model-cvpr-2025-paper/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1650, \"height\": 388, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-xu-topocellgen-generating-histopathology-cell-topology-with-a-diffusion-model-cvpr-2025-paper/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 688, \"height\": 321, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-xu-topocellgen-generating-histopathology-cell-topology-with-a-diffusion-model-cvpr-2025-paper/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 687, \"height\": 240, \"label\": \"Table\"}]"
motivation: 准确的多类细胞拓扑对理解组织结构和病理至关重要。
method: 将拓扑约束集成到扩散模型中，生成逼真细胞拓扑。
result: 生成拓扑在精度和可解释性上优于基线方法。
conclusion: 为肿瘤微环境模拟和下游任务增强提供新途径。
---

## Abstract
Accurately modeling multi-class cell topology is crucial in digital pathology, as it provides critical insights into tissue structure and pathology. The synthetic generation of cell topology enables realistic simulations of complex tissue environments, enhances downstream tasks by augmenting training data, aligns more closely with pathologists' domain knowledge, and offers new opportunities for controlling and generalizing the tumor microenvironment. In this paper, we propose a novel approach that integrates topological constraints into a diffusion model to improve the generation of realistic, contextually accurate cell topologies. Our method refines the simulation of cell distributions and interactions, increasing the precision and interpretability of results in downstream tasks such as cell detection and classification. To assess the topological fidelity of generated layouts, we introduce a new metric, Topological Frechet Distance (TopoFD), which overcomes the limitations of traditional metrics like FID in evaluating topological structure. Experimental results demonstrate the effectiveness of our approach in generating multi-class cell layouts that capture intricate topological relationships. Code is available at https://github.com/Melon-Xu/TopoCellGen.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义
- **研究动机**：数字病理中多类细胞（如淋巴细胞、上皮细胞、基质细胞等）的空间组织（拓扑结构）对理解组织结构、疾病进展与肿瘤微环境至关重要。但人工标注多类细胞布局困难，现有生成模型（如GAN、扩散模型）多直接生成病理图像，忽略了对细胞本身及其空间交互的显式建模，难以融入病理学家的领域知识，也难以验证、泛化或控制生成结果。
- **核心问题**：如何生成**具有真实拓扑结构的多类细胞空间布局**（cell topology），使得生成的布局不仅在视觉上相似，更在细胞密度、空间分布、细胞类型间的拓扑关系上忠实于真实组织？
- **整体含义**：通过将拓扑约束（持续同源性，persistent homology）引入扩散模型，直接生成细胞布局，使其同时满足计数准确、空间一致、跨类交互合理，从而为肿瘤微环境模拟、下游任务（细胞检测/分类）数据增强提供更可信的合成数据，并引入一个专用于评估拓扑保真度的新指标 TopoFD。

### 2. 论文提出的方法论
- **核心思想**：在条件扩散模型（DDPM）的基础上，引入**三个专门的损失项**，分别强化细胞数量、类内空间分布、类间结构关系。条件向量为各类细胞计数 `c = [c1, c2, ..., cn]`。前向过程加噪，逆向过程预测噪声。从噪声状态 `x_t` 通过式子（2）近似还原出无噪布局 `\hat{x}_t^0`，并对其施加约束。
- **关键技术细节**：
  - **细胞计数损失（L_count）**：对 `\hat{x}_t^0` 进行硬阈值二值化，使用 Straight‑Through Estimator（STE）使操作可微，然后计算预测与真实各类细胞点总数的绝对误差。
  - **类内空间一致性（L_intra）**：对每种细胞类型单独计算距离变换图，获得 1‑维持续同源图（persistence diagrams）；计算预测图与真实图之间的 Wasserstein 距离，并求和。
  - **类间结构正则化（L_inter）**：将所有细胞类型合并为单通道聚合布局，计算距离变换图，同样用 1‑维持续同源图的 Wasserstein 距离约束整体空间关系。
  - **总损失**：`L_total = L_simple + λ_c * L_count + λ_intra * L_intra + λ_inter * L_inter`（L_simple 为标准扩散噪声预测损失）。
  - **拓扑保真度评估新指标 TopoFD**：对每个细胞类型，分别从真实布局和生成布局提取细胞中心点云，计算各自的 1‑维持续同源图；用重心（barycenter）和 persistence landscape 向量化，计算 Fréchet 距离，再对所有细胞类型取平均。相比 FID 或计数误差，更敏感地反映拓扑结构的相似性。
- **算法流程**：
  1. 训练 DDPM，条件为细胞计数向量。
  2. 在每个去噪时间步，估计 `\hat{x}_t^0`，计算 `L_count`、`L_intra`、`L_inter`，联合优化。
  3. 推理时，从噪声出发，逐步去噪生成多类细胞布局。
  4. 还可将生成的布局作为条件，用引导扩散模型合成对应的 H&E 染色病理图像。

### 3. 实验设计
- **数据集**：
  - **BRCA‑M2C**（TCGA 乳腺癌细胞分类数据集）：含淋巴细胞、上皮/肿瘤细胞、基质细胞等 3 类。
  - **Lizard**（结肠组织核分割与分类数据集）：含多种细胞类型（如上皮、淋巴细胞、中性粒细胞、浆细胞、嗜酸性粒细胞、连接细胞等）。
- **基线方法**：ADM（基础扩散模型）、TMCCG（拓扑引导的多类细胞上下文生成，基于 GAN）、Spatial Diffusion（基于密度图的空间扩散模型）。
- **评估指标**：
  - **样本质量**：FID（对每个数据集定制训练特征提取器）、各类细胞计数误差、总计数误差（TCE）、TopoFD、MMD（最大均值差异）。
  - **下游任务**：细胞检测与分类（框架：UNet 和 MCSpatNet），以 F1‑score 衡量。
- **对比方式**：生成 2000 个合成样本作为额外训练数据，与仅用真实数据、随机合成样本、其他方法生成样本进行数据增强的效果对比。同时通过病理学家评估生成布局的生物学合理性。

### 4. 资源与算力
- 论文的正文及附录中**未明确提及**使用的 GPU 型号、数量、训练时长或具体算力配置。仅部分实现细节提到使用 FastGeodis 库在 GPU 上并行计算距离变换，但未给出硬件详细信息。

### 5. 实验数量与充分性
- **实验数量**：
  - 在 **2 个多组织数据集**（BRCA‑M2C、Lizard）上与 **3 种基线**对比，评估样本质量（表格 1）。
  - 在 BRCA‑M2C 上评估下游任务（细胞检测/分类），结合两种分割框架，展示数据增强效果（表格 2）。
  - **消融实验**：在 BRCA‑M2C 上逐个移除/组合损失组件（L_count、L_intra、L_inter），验证各自贡献（表格 3）。
  - **损失权重敏感性**：在 BRCA‑M2C 上测试不同权重组合的影响（表格 4）。
  - 定性可视化（图 5）和病理学家主观评估。
- **充分性与公平性**：
  - 对比对象覆盖了近期代表性的布局生成方法，指标从视觉质量、计数精度、拓扑保真度到下游任务性能，全面合理。
  - 消融和权重实验说明了各模块的必要性。
  - 但实验仅局限在两个特定癌种/组织类型的数据集，对有更多类别或不同组织类型的泛化性未做验证；且仅进行了二维布局生成，未讨论三维扩展或更大组织尺度下的表现。

### 6. 论文的主要结论与发现
- 将**持续同源性**集成到扩散模型中可有效生成**拓扑逼真**的多类细胞布局，同时控制细胞数量。
- 提出的 **TopoFD** 指标比传统 FID 或简单的计数误差更能捕捉拓扑结构的差异。
- 生成的合成数据作为训练增强，显著提升了细胞检测与分类的下游任务性能，尤其在 F1‑score 上超越 TMCCG、Spatial Diffusion 等方法。
- 病理学家评价显示，生成的细胞布局在良/恶性特征上几乎与真实布局不可区分。

### 7. 优点
- **创新性**：首次将扩散模型与多类细胞拓扑生成结合，并用持续同源性显式约束空间结构。
- **多面约束**：计数损失、类内空间一致性、类间结构正则化三者互补，使生成的可控性和真实性大幅提升。
- **专用评估指标**：TopoFD 弥补了现有指标（如 FID）忽略拓扑相似性的不足，可推广至其他生成任务。
- **实用性强**：生成的细胞布局可作为中间表征，指导病理图像合成，为下游任务数据增强提供精准的“免费”标注。
- **实验设计扎实**：多数据集、多基线、消融与权重分析，辅以病理学家评估。

### 8. 不足与局限
- **泛化性验证有限**：仅在两种癌症组织数据集上测试，未涉及其他脏器或更复杂的病理状态。
- **计算开销**：持续同源性的计算（尤其是大规模点云）可能较慢，文中未给出推理/训练的时间对比，可能影响实际部署。
- **固定数量的局限**：条件依赖于预先给定的细胞计数向量，未讨论如何从图像或其他模态自动估计该向量，限制了端到端自动化。
- **布局引导图像生成部分**：论文仅提及使用现有引导扩散模型，未深入优化或对比不同的图像生成策略，且未评估生成病理图像的视觉质量或对临床诊断的影响。
- **未讨论罕见拓扑**：例如极特殊的肿瘤出芽模式或炎症浸润模式，生成的多样性是否足够未做专门分析。
- **偏差风险**：训练数据来自特定医院或公共数据集，可能存在人群偏倚；评价虽有病理学家参与，但仅为单人，主观性可能影响结论的强度。

（完）
