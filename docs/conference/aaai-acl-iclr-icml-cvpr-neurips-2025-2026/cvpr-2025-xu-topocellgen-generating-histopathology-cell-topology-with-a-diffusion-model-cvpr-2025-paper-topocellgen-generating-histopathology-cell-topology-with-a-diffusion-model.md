---
title: "TopoCellGen: Generating Histopathology Cell Topology with a Diffusion Model"
title_zh: TopoCellGen：利用扩散模型生成组织病理细胞拓扑
authors: "Xu, Meilong, Gupta, Saumya, Hu, Xiaoling, Li, Chen, Abousamra, Shahira, Samaras, Dimitris, Prasanna, Prateek, Chen, Chao"
date: 2025-06-01
pdf: "https://openaccess.thecvf.com/content/CVPR2025/papers/Xu_TopoCellGen_Generating_Histopathology_Cell_Topology_with_a_Diffusion_Model_CVPR_2025_paper.pdf"
tags: ["query:immuno-topo"]
score: 9.0
evidence: 通过在扩散模型中集成拓扑约束，直接生成组织病理多类细胞拓扑图
tldr: 针对数字病理中细胞拓扑建模需求，提出整合拓扑约束的扩散模型 TopoCellGen，生成逼真、上下文准确的多类细胞拓扑结构，用于增强下游任务和模拟肿瘤微环境，提升了细胞分布与交互的模拟精度。
source: CVPR-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-xu-topocellgen-generating-histopathology-cell-topology-with-a-diffusion-model-cvpr-2025-paper/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 882, \"height\": 321}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-xu-topocellgen-generating-histopathology-cell-topology-with-a-diffusion-model-cvpr-2025-paper/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1805, \"height\": 766}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-xu-topocellgen-generating-histopathology-cell-topology-with-a-diffusion-model-cvpr-2025-paper/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 877, \"height\": 555}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-xu-topocellgen-generating-histopathology-cell-topology-with-a-diffusion-model-cvpr-2025-paper/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 879, \"height\": 355}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-xu-topocellgen-generating-histopathology-cell-topology-with-a-diffusion-model-cvpr-2025-paper/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1707, \"height\": 616}]"
tables_json: "[{\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-xu-topocellgen-generating-histopathology-cell-topology-with-a-diffusion-model-cvpr-2025-paper/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1645, \"height\": 301}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-xu-topocellgen-generating-histopathology-cell-topology-with-a-diffusion-model-cvpr-2025-paper/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1650, \"height\": 388}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-xu-topocellgen-generating-histopathology-cell-topology-with-a-diffusion-model-cvpr-2025-paper/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 688, \"height\": 321}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-xu-topocellgen-generating-histopathology-cell-topology-with-a-diffusion-model-cvpr-2025-paper/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 687, \"height\": 240}]"
motivation: 现有方法难以模拟真实复杂的多类细胞空间分布和交互，限制了肿瘤微环境的泛化。
method: 在扩散模型中嵌入拓扑约束，精细优化细胞分布的生成，提高真实性和可解释性。
result: 生成的细胞拓扑在结构保真度和上下文准确性上显著优于现有方法。
conclusion: 拓扑引导的生成模型为数据增强和微环境控制提供了新方向。
---

## Abstract
Accurately modeling multi-class cell topology is crucial in digital pathology, as it provides critical insights into tissue structure and pathology. The synthetic generation of cell topology enables realistic simulations of complex tissue environments, enhances downstream tasks by augmenting training data, aligns more closely with pathologists' domain knowledge, and offers new opportunities for controlling and generalizing the tumor microenvironment. In this paper, we propose a novel approach that integrates topological constraints into a diffusion model to improve the generation of realistic, contextually accurate cell topologies. Our method refines the simulation of cell distributions and interactions, increasing the precision and interpretability of results in downstream tasks such as cell detection and classification. To assess the topological fidelity of generated layouts, we introduce a new metric, Topological Frechet Distance (TopoFD), which overcomes the limitations of traditional metrics like FID in evaluating topological structure. Experimental results demonstrate the effectiveness of our approach in generating multi-class cell layouts that capture intricate topological relationships. Code is available at https://github.com/Melon-Xu/TopoCellGen.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义（研究动机和背景）

- **核心问题**：在数字病理中，精确的多类细胞空间布局生成难度极高。现有扩散模型虽能生成整张病理图像，却无法显式地模拟细胞的空间排列、类型间拓扑关系及细胞密度，导致难以与病理学家的领域知识对齐、难以验证、不易泛化。
- **研究动机**：
  - 细胞的空间组织（如肿瘤浸润淋巴细胞的密度、肿瘤出芽等）对诊断和预后至关重要，直接生成细胞布局能贴合人类专家知识。
  - 拓扑关系（细胞的聚类、混合、连通性、空洞/环状结构）是理解组织结构功能的关键，但现有方法极少为此建模。
  - 需要一种方法，既能生成高度逼真的细胞布局，又能精确控制细胞数量，并保留细胞内和细胞间的拓扑模式。
- **整体含义**：提出首个专门针对组织病理细胞拓扑的扩散模型，通过拓扑约束和计数损失使生成布局更符合真实组织微环境，进而作为数据增强提升下游细胞检测和分类性能，并向可控、可泛化的肿瘤微环境模拟迈进一步。

### 2. 论文提出的方法论

**核心思想**：在去噪扩散概率模型（DDPM）的基础上，引入基于持续同调的拓扑损失与细胞计数损失，引导生成布局同时保持单类细胞的空间分布一致性及多类细胞间的结构关系。

**关键技术细节**：

- **细胞计数损失（L_count）**：通过直通估计器（STE）将预测的去噪布局二值化，并对每个细胞类别的细胞数进行约束，使生成布局的细胞总数与真实数据一致，避免模型偏向过高或过低的细胞数。
- **类内空间一致性损失（L_intra）**：对每一类细胞的二值布局计算距离变换图，再分别计算其 1-维持续图（persistence diagram），使用 Wasserstein 距离匹配预测布局与真实布局的持续点，强制单类细胞的空间分布模式（如聚簇、孔洞）相似。
- **类间结构正则化损失（L_inter）**：将所有细胞类型合并为一幅聚合布局，同样计算其距离变换图的持续图，并与真实聚合布局的持续图进行 Wasserstein 距离匹配，从而跨类型约束细胞集体的空间排布（如免疫细胞环绕肿瘤细胞的“环”结构）。
- **整体训练目标**：将简单去噪损失 L_simple 与上述三个损失加权组合。

**生成流程**：先用 DDPM 从噪声生成细胞多类布局，再以此布局为条件，利用引导扩散模型合成对应的 H&E 染色组织图像。

**新指标**：提出拓扑 Fréchet 距离（TopoFD），将真实与生成布局的各类型细胞点云分别计算持续图，再通过持续景观向量化并计算 Fréchet 距离，比 FID 更能捕捉空间拓扑差异。

### 3. 实验设计

- **数据集**：
  - BRCA-M2C：TCGA 乳腺癌多类细胞分类数据集（3 类：淋巴细胞、上皮/肿瘤细胞、基质细胞）。
  - Lizard：结肠组织核实例分割与分类数据集（6 类：淋巴细胞、上皮细胞、基质细胞、嗜中性粒细胞、浆细胞、嗜酸性粒细胞、结缔组织细胞）。
- **对比方法**：
  - ADM（标准扩散模型）
  - TMCCG（拓扑引导的 GAN 方法）
  - Spatial Diffusion（基于密度图的扩散布局生成方法）
- **评估基准**：生成质量通过 FID、各类细胞计数误差、总计数误差（TCE）、TopoFD、最大平均差异（MMD）评估；下游任务通过 F1-score（细胞检测和分类）在 UNet 和 MCSpatNet 上进行评估。
- **实验设置**：分别生成布局后进一步合成图像，将 2000 组图像-布局对作为增强数据训练下游模型，与仅用真实数据、随机增强及另外两种基线方法进行对比。

### 4. 资源与算力

- 论文**未明确说明**训练所用的 GPU 型号、数量及具体训练时长。仅提及使用 FastGeodis 库在 GPU 上计算可微距离变换，但计算资源详情缺失。

### 5. 实验数量与充分性

- **实验组数**：
  - 在两个公开数据集（BRCA-M2C 和 Lizard）上进行了完整的生成质量评估和下游任务评估。
  - 对损失分量（L_count, L_intra, L_inter）进行了消融实验（8 种组合，BRCA-M2C）。
  - 对三个损失权重进行了消融实验（5 种参数组合，BRCA-M2C）。
  - 还定性展示了生成布局的视觉效果，并与病理学家进行生物学合理性验证（文中提及，但未详述实验细节）。
- **充分性与公平性**：
  - 对比的方法覆盖经典扩散、基于拓扑的 GAN 和基于密度的扩散模型，具有代表性。
  - 评估指标全面，既包括生成质量（FID），也包括拓扑特异性指标（TopoFD、MMD）和下游应用性能，保证多方面比较。
  - 消融实验清晰证明每个损失项的必要性和权重敏感性，但权重搜索范围有限（仅 5 个离散值），可能存在调优不充分。
  - 所有对比方法在相同的任务框架下进行（生成 2000 个样本，相同下游模型），确保公平。

### 6. 论文的主要结论与发现

- 提出的 TopoCellGen 能在两个数据集上生成视觉逼真、计数精确、拓扑一致的多类细胞布局，FID、计数误差、TopoFD 均显著优于现有方法。
- 引入的细胞计数损失成功解决了扩散模型计数偏差问题；类内拓扑损失提升了单类空间分布的真实性；类间拓扑损失改善了跨细胞类型的结构交互。
- 用 TopoCellGen 生成的布局合成图像进行数据增强，在细胞检测与分类任务上获得了最佳 F1 分数，证明其生物学合理性和对下游任务的增益。
- 新提出的 TopoFD 指标能比 FID 更敏感地区分拓扑布局差异（如图 3 示例），更适合评估空间结构保真度。

### 7. 优点

- **方法开创性**：首次在扩散模型中显式引入多尺度的持续同调损失（0 维和 1 维）来同时约束细胞的空间聚类与孔洞/环状结构，填补了细胞拓扑生成的空间。
- **多类型空间关系建模**：类内和类间拓扑损失分别保障了个体细胞分布和集体结构模式的真实性，避免了仅使用简单密度图或计数条件的局限。
- **拓扑评价指标创新**：TopoFD 解决了传统 FID 对结构不敏感的问题，为拓扑生成任务提供了更科学的评价手段。
- **端到端可微**：通过 STE 与可微距离变换，将离散拓扑结构纳入梯度优化，训练过程稳定。
- **下游任务增益明显**：生成的合成数据直接提升了细胞检测和分类性能，实用性强。

### 8. 不足与局限

- **计算成本未明**：未报告训练时间和显存需求，限制了其可复现性与部署可行性评估。
- **肿瘤类型/组织泛化性**：只在乳腺癌和结肠组织上验证，对其他器官、其他肿瘤微环境模式（如纤维化、炎症不同阶段）的泛化能力尚待探究。
- **拓扑维度限制**：仅使用了 0 维和 1 维同调（连通分量和环），未涉及 2 维空洞等高阶特征，可能不足以全面刻画复杂组织三维拓扑（文中布局实际上仍是 2D 伪三维平铺）。
- **下游任务有限**：仅测试了细胞检测和分类，未探究生成布局对预后预测、基因关联等高级任务的影响。
- **布局到图像的合成依赖性**：生成最终病理图像需要额外的条件扩散模型，整个流程的误差可能层层累积。
- **潜在偏差**：细胞计数损失基于直通估计器，虽可微但梯度估计可能引入噪声；距离变换阈值固定为中位数，可能对不同密度分布适应性不足。

（完）
