---
title: "TopoCellGen: Generating Histopathology Cell Topology with a Diffusion Model"
title_zh: TopoCellGen：利用扩散模型生成组织病理学细胞拓扑
authors: "Xu, Meilong, Gupta, Saumya, Hu, Xiaoling, Li, Chen, Abousamra, Shahira, Samaras, Dimitris, Prasanna, Prateek, Chen, Chao"
date: 2025-06-01
pdf: "https://openaccess.thecvf.com/content/CVPR2025/papers/Xu_TopoCellGen_Generating_Histopathology_Cell_Topology_with_a_Diffusion_Model_CVPR_2025_paper.pdf"
tags: ["query:cellseg"]
score: 9.0
evidence: 生成真实的多类细胞拓扑用于肿瘤微环境建模
tldr: 针对数字病理中多类细胞拓扑建模问题，提出TopoCellGen，将拓扑约束融入扩散模型生成逼真的细胞分布与交互，为下游任务提供高质量合成数据，增强肿瘤微环境的模拟与控制能力。
source: CVPR-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-xu-topocellgen-generating-histopathology-cell-topology-with-a-diffusion-model-cvpr-2025-paper/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 882, \"height\": 321, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-xu-topocellgen-generating-histopathology-cell-topology-with-a-diffusion-model-cvpr-2025-paper/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1805, \"height\": 766, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-xu-topocellgen-generating-histopathology-cell-topology-with-a-diffusion-model-cvpr-2025-paper/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 877, \"height\": 555, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-xu-topocellgen-generating-histopathology-cell-topology-with-a-diffusion-model-cvpr-2025-paper/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 879, \"height\": 355, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-xu-topocellgen-generating-histopathology-cell-topology-with-a-diffusion-model-cvpr-2025-paper/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1707, \"height\": 616, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-xu-topocellgen-generating-histopathology-cell-topology-with-a-diffusion-model-cvpr-2025-paper/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1645, \"height\": 301, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-xu-topocellgen-generating-histopathology-cell-topology-with-a-diffusion-model-cvpr-2025-paper/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1650, \"height\": 388, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-xu-topocellgen-generating-histopathology-cell-topology-with-a-diffusion-model-cvpr-2025-paper/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 688, \"height\": 321, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-xu-topocellgen-generating-histopathology-cell-topology-with-a-diffusion-model-cvpr-2025-paper/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 687, \"height\": 240, \"label\": \"Table\"}]"
motivation: 准确建模多类细胞拓扑对理解组织结构和肿瘤微环境至关重要。
method: 提出将拓扑约束集成到扩散模型中以生成细胞拓扑。
result: 提高了细胞拓扑生成的现实性和下游任务性能。
conclusion: 该工作为病理图像分析提供了可扩展的细胞拓扑生成方法。
---

## Abstract
Accurately modeling multi-class cell topology is crucial in digital pathology, as it provides critical insights into tissue structure and pathology. The synthetic generation of cell topology enables realistic simulations of complex tissue environments, enhances downstream tasks by augmenting training data, aligns more closely with pathologists' domain knowledge, and offers new opportunities for controlling and generalizing the tumor microenvironment. In this paper, we propose a novel approach that integrates topological constraints into a diffusion model to improve the generation of realistic, contextually accurate cell topologies. Our method refines the simulation of cell distributions and interactions, increasing the precision and interpretability of results in downstream tasks such as cell detection and classification. To assess the topological fidelity of generated layouts, we introduce a new metric, Topological Frechet Distance (TopoFD), which overcomes the limitations of traditional metrics like FID in evaluating topological structure. Experimental results demonstrate the effectiveness of our approach in generating multi-class cell layouts that capture intricate topological relationships. Code is available at https://github.com/Melon-Xu/TopoCellGen.

---

## 论文详细总结（自动生成）

# 论文总结：TopoCellGen: Generating Histopathology Cell Topology with a Diffusion Model

## 1. 核心问题与研究动机
- **问题**：数字病理中多类细胞空间布局（细胞拓扑）的精确建模对理解组织结构和肿瘤微环境至关重要，但手动标注多类细胞耗时且需领域专家。
- **含义**：现有病理图像生成模型（如GAN、扩散模型）虽能生成视觉逼真的图像，但缺少对细胞位置和细胞间相互作用的显式建模，难以与病理学家的领域知识对齐，且难以控制或泛化。
- **动机**：提出直接生成多类细胞布局，并在此基础上通过拓扑约束（使用持久同调）来保持类内空间模式和类间结构关系，从而增强生成布局的生物学真实性，并引入新评价指标弥补FID无法评估拓扑结构的不足。

## 2. 方法论
### 2.1 核心思想
- 将拓扑特征（0维连通分量、1维环/空洞）作为生成约束，融入去噪扩散概率模型（DDPM），生成既满足类内空间分布、又保持类间结构交互的多类细胞布局。
- 提出可微的**细胞计数损失**、**类内空间一致性损失**和**类间结构正则化损失**，分别控制细胞数量、单类分布和跨类拓扑。
- 设计**拓扑弗雷歇距离（TopoFD）**作为评估生成布局拓扑相似性的新指标。

### 2.2 关键技术细节
- **基础模型**：DDPM，输入为多通道细胞布局（每个通道一种细胞类型，二值图），条件向量为每类细胞计数。
- **细胞计数损失** \( L_{count} \)：对预测的去噪布局进行硬阈值二值化（使用直通估计器STE保证可微），计算每通道细胞数与真实布局的绝对误差。
- **类内空间一致性损失** \( L_{intra} \)：
  1. 对真实布局和预测布局的每类二值图分别计算欧氏距离变换图。
  2. 对距离变换图提取1维持久同调图中的特征点（出生-死亡对）。
  3. 用Wasserstein距离度量两个持久图之间的差异，逐通道求和后平均。
- **类间结构正则化损失** \( L_{inter} \)：
  - 将所有类合并为单通道的聚合布局，计算距离变换图，同样用持久图和Wasserstein距离度量，捕捉多类细胞混合形成的环状结构。
- **总损失**：\( L_{total} = L_{simple} + \lambda_c L_{count} + \lambda_{intra} L_{intra} + \lambda_{inter} L_{inter} \)，其中 \( L_{simple} \) 为DDPM的噪声预测损失。
- **TopoFD** 计算流程：
  - 从真实和生成布局中提取每类细胞的点云（细胞中心坐标），计算每类的1维持久图。
  - 分别计算真实集和生成集的持久图重心（barycenter），转换为持久景观（landscape）向量。
  - 用弗雷歇距离度量两类向量间的分布差异，再对所有类取平均。
- **布局到图像的生成**：使用布局引导的扩散模型，将生成的细胞布局作为条件，合成对应的H&E病理图像，用于下游训练数据增强。

## 3. 实验设计
### 3.1 数据集
- **BRCA-M2C**：TCGA乳腺癌细胞分类数据集，包含淋巴细胞、上皮细胞、间质细胞等。
- **Lizard**：结肠细胞核实例分割与分类数据集，包含淋巴细胞、上皮细胞、中性粒细胞、浆细胞、嗜酸性粒细胞、结缔组织细胞等。

### 3.2 Benchmark与对比方法
- **对比基线**：
  - ADM（经典的分类器引导扩散模型）
  - TMCCG（基于GAN的多类细胞上下文生成）
  - Spatial Diffusion（基于空间密度图的扩散模型，但计数均为粗粒度类别条件）
- **评价指标**：
  - 视觉质量与计数准确性：FID（针对布局数据）、每类细胞的计数误差、总计数误差（TCE）
  - 拓扑相似性：**TopoFD**、MMD（最大均值差异）
  - 下游任务性能：在细胞检测与分类任务上，用生成的图像-布局对增强后，测试UNet和MCSpatNet的F1分数。

### 3.3 下游任务实验
- 在每个数据集上，生成2000张图像-布局对作为增强数据，和原始真实数据混合训练，比较仅用真实数据、真实+随机增强、真实+各方法生成数据的效果。

### 3.4 消融实验
- **损失组件消融**：逐一移除 \( L_{count} \)、\( L_{intra} \)、\( L_{inter} \)，观察FID、TCE、TopoFD的变化。
- **损失权重消融**：测试不同 \( \lambda \) 组合（0.005, 0.001, 1e-4, 5e-5, 5e-4）的影响。

### 3.5 生物合理性评估
- 请一位有7年以上经验的认证病理学家盲评，评价生成布局是否与真实布局难以区分及是否保存了良/恶性特征。

## 4. 资源与算力
- **文中未明确说明**使用的GPU型号、数量、训练时长等信息，仅提供代码仓库，可能需从官方代码获取算力细节。

## 5. 实验数量与充分性
- **实验项**：两个公开数据集 × 三个baseline + 该文方法，质量评估12项指标，下游任务2个框架，消融实验两个（组件8组、权重5组），生物合理性评估1项。
- **充分性**：实验覆盖了与前沿方法的全面对比、不同损失贡献的消融、参数敏感性，以及实际增强下游模型的表现，并通过专家评估增强可信度，实验设计较为充分、客观、公平。

## 6. 主要结论与发现
- TopoCellGen 生成的细胞布局在视觉质量（FID）和拓扑准确性（TopoFD）上均显著优于现有方法，同时细胞计数误差大幅降低。
- 结合拓扑约束后，类内空间分布和类间结构关系得以精准保持，生成的布局与真实组织微环境高度相似。
- 使用该布局生成的图像增强训练，可使细胞检测与分类模型（UNet、MCSpatNet）的F1分数获得一致且显著的提升。
- TopoFD 能有效捕获传统FID无法反映的拓扑结构差异，是一种对空间组织更敏感的评估指标。

## 7. 优点
- **首次**将持久同调引入扩散模型以生成多类细胞拓扑，显式建模类内和类间几何。
- **新损失函数**：细胞计数损失利用STE实现可微二值化，使生成细胞数高度可控；L_intra、L_inter 通过距离变换+持久同调保持拓扑结构。
- **提出TopoFD**：可直接量化生成布局的拓扑相似性，弥补FID不足。
- **实验全面**：在多个数据集、多重指标、多种下游框架上验证，并包含专家评估，结果说服力强。
- **实用性**：生成的布局可进一步生成带标注的病理图像，缓解标注稀缺问题。

## 8. 不足与局限
- **算力未提及**：缺少训练计算成本信息，难以评估部署需求。
- **场景扩展验证不足**：仅在两套组织切片数据集（乳腺、结肠）上测试，泛化到其他组织、不同癌种或更大WSI全景图的能力未验证。
- **持久同调计算开销**：训练中反复计算距离变换和持久图可能增加额外负担，论文未讨论效率或加速方法。
- **生物评估仅一人**：虽邀请病理专家，但样本量和评估者数量有限，可能存在主观偏差。
- **病种多样性**：实验中仅包含相对常见的细胞类型分布，对极端密度、特殊细胞排列或罕见亚型可能不够鲁棒。
- **无不确定性量化**：生成过程未提供对布局置信度的评估，可能限制其在风险敏感场景的应用。

（完）
