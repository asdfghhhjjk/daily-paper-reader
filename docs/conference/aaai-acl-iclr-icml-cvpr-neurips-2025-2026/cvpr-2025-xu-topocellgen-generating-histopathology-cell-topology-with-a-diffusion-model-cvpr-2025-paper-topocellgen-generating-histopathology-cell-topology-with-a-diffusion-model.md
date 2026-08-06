---
title: "TopoCellGen: Generating Histopathology Cell Topology with a Diffusion Model"
title_zh: "TopoCellGen: 用扩散模型生成组织病理细胞拓扑"
authors: "Xu, Meilong, Gupta, Saumya, Hu, Xiaoling, Li, Chen, Abousamra, Shahira, Samaras, Dimitris, Prasanna, Prateek, Chen, Chao"
date: 2025-06-01
pdf: "https://openaccess.thecvf.com/content/CVPR2025/papers/Xu_TopoCellGen_Generating_Histopathology_Cell_Topology_with_a_Diffusion_Model_CVPR_2025_paper.pdf"
tags: ["query:immuno-topo"]
score: 9.0
evidence: 生成多类细胞拓扑用于组织病理，增强微环境建模。
tldr: 针对组织病理中多类细胞拓扑建模问题，本文提出TopoCellGen，将拓扑约束融入扩散模型，生成逼真且上下文准确的细胞拓扑。该方法改进了细胞分布与相互作用的仿真，提高了数字病理下游任务的性能，并为肿瘤微环境的可控生成与泛化提供了新工具。
source: CVPR-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-xu-topocellgen-generating-histopathology-cell-topology-with-a-diffusion-model-cvpr-2025-paper/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 882, \"height\": 321}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-xu-topocellgen-generating-histopathology-cell-topology-with-a-diffusion-model-cvpr-2025-paper/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1805, \"height\": 766}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-xu-topocellgen-generating-histopathology-cell-topology-with-a-diffusion-model-cvpr-2025-paper/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 877, \"height\": 555}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-xu-topocellgen-generating-histopathology-cell-topology-with-a-diffusion-model-cvpr-2025-paper/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 879, \"height\": 355}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-xu-topocellgen-generating-histopathology-cell-topology-with-a-diffusion-model-cvpr-2025-paper/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1707, \"height\": 616}]"
tables_json: "[{\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-xu-topocellgen-generating-histopathology-cell-topology-with-a-diffusion-model-cvpr-2025-paper/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1645, \"height\": 301}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-xu-topocellgen-generating-histopathology-cell-topology-with-a-diffusion-model-cvpr-2025-paper/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1650, \"height\": 388}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-xu-topocellgen-generating-histopathology-cell-topology-with-a-diffusion-model-cvpr-2025-paper/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 688, \"height\": 321}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-xu-topocellgen-generating-histopathology-cell-topology-with-a-diffusion-model-cvpr-2025-paper/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 687, \"height\": 240}]"
motivation: 精确建模多类细胞拓扑对数字病理中组织结构和微环境理解至关重要。
method: 提出将拓扑约束集成到扩散模型中，生成逼真且上下文准确的细胞拓扑。
result: 方法精化了细胞分布和相互作用的模拟，提升了精度和可解释性。
conclusion: 生成的细胞拓扑可增强下游任务，并为肿瘤微环境的控制和泛化提供新途径。
---

## Abstract
Accurately modeling multi-class cell topology is crucial in digital pathology, as it provides critical insights into tissue structure and pathology. The synthetic generation of cell topology enables realistic simulations of complex tissue environments, enhances downstream tasks by augmenting training data, aligns more closely with pathologists' domain knowledge, and offers new opportunities for controlling and generalizing the tumor microenvironment. In this paper, we propose a novel approach that integrates topological constraints into a diffusion model to improve the generation of realistic, contextually accurate cell topologies. Our method refines the simulation of cell distributions and interactions, increasing the precision and interpretability of results in downstream tasks such as cell detection and classification. To assess the topological fidelity of generated layouts, we introduce a new metric, Topological Frechet Distance (TopoFD), which overcomes the limitations of traditional metrics like FID in evaluating topological structure. Experimental results demonstrate the effectiveness of our approach in generating multi-class cell layouts that capture intricate topological relationships. Code is available at https://github.com/Melon-Xu/TopoCellGen.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义
*   **核心问题**：当前病理图像生成模型（如扩散模型）通常直接生成整张图像，缺乏对细胞空间布局和细胞间相互作用的显式建模，难以与病理医生的领域知识对齐，也无法灵活控制或泛化肿瘤微环境。
*   **研究动机**：多类细胞拓扑（细胞的聚类、混合、连通性等空间组织关系）对理解组织结构和疾病进展至关重要。生成准确的细胞拓扑布局，不仅能提供符合生物学先验的合成数据，还能作为条件指导病理图像生成，增强下游任务（如细胞检测、分类）的训练数据。
*   **整体含义**：本文首次提出显式生成细胞拓扑的扩散模型，通过引入拓扑约束和细胞计数控制，使生成的细胞布局在类内分布和类间关系上均高度逼真，从而推动合成病理数据向更具生物学可解释性和可控性的方向发展。

### 2. 论文提出的方法论
*   **核心思想**：以去噪扩散概率模型（DDPM）为基础，在反向去噪过程中附加三种损失，迫使生成器同时保持正确的细胞数量、类内的空间结构（0维拓扑特征：连通分量）以及类间的空间关系（1维拓扑特征：环/空洞）。
*   **关键技术细节**：
    *   **条件生成**：将多类细胞计数向量 $c=[c_1,\dots,c_n]$ 作为条件输入，控制每类细胞数量。
    *   **细胞计数损失（$L_{count}$）**：利用直通估计器（STE）对从预测的干净布局 $\hat{x}_t^0$ 二值化后的结果进行可微细胞计数，与真实布局 $x_0$ 的计数求差，确保生成数量准确。
    *   **类内空间一致性损失（$L_{intra}$）**：
        *   对真实布局和预测布局的每一类通道分别计算距离变换图。
        *   计算距离变换图的1维持久同调图（持久图）。
        *   使用Wasserstein距离度量两张持久图间的差异，并通过最优匹配公式化损失项（式6），最后对各类取平均（式7）。
    *   **类间结构正则化损失（$L_{inter}$）**：
        *   将所有细胞类型合并为单通道聚合布局。
        *   计算聚合布局的距离变换图及其1维持久图。
        *   同样以Wasserstein距离损失（式8）约束真实与预测聚合布局的拓扑相似性。
    *   **总目标**：
        $L_{total} = L_{simple} + \lambda_c L_{count} + \lambda_{intra} L_{intra} + \lambda_{inter} L_{inter}$。
    *   **拓扑弗雷歇距离（TopoFD）**：新提出的评估指标，分别对真实和生成布局集合提取每类细胞的点云，计算1维持久图的巴里中心，将其转化为持久景观后计算弗雷歇距离，克服了FID无法评估空间拓扑结构的缺陷。
    *   **布局到图像的生成**：用生成的细胞布局作为条件，通过引导扩散模型合成对应的H&E染色病理图像。

### 3. 实验设计
*   **数据集**：
    *   BRCA-M2C（TCGA乳腺癌细胞分类数据集），包含淋巴细胞（Lym.）、肿瘤/上皮（Epi.）、间质细胞（Stro.）等类别。
    *   Lizard（结肠核分割与分类数据集），包含上皮、淋巴细胞、中性粒细胞、浆细胞、嗜酸性粒细胞、结缔组织细胞等类别。
*   **Benchmark指标**：
    *   **样本质量**：FID、各类型细胞计数误差、总计数误差（TCE）、TopoFD、最大均值差异（MMD）。
    *   **下游任务**：以2,000对合成图像‑布局作为增强数据，训练UNet和MCSpatNet进行细胞检测与分类，报告F1‑score。
*   **对比方法**：ADM（消融扩散模型）、TMCCG（基于GAN的拓扑引导多类上下文生成）、Spatial Diffusion（空间密度图引导的扩散布局生成）。

### 4. 资源与算力
*   论文正文及提供的元数据中**未明确说明**使用的GPU型号、数量或具体训练时长。相关实现细节可能包含在补充材料或代码仓库中，但主文未提及。

### 5. 实验数量与充分性
*   **主要实验组数**：
    *   2个多类病理数据集上的样本质量与下游任务性能对比（与3个baseline比较）。
    *   消融实验1：针对三种损失函数（$L_{count}, L_{intra}, L_{inter}$）的七种组合，在BRCA‑M2C上评估FID、TCE和TopoFD。
    *   消融实验2：针对损失权重 $\lambda_c, \lambda_{intra}, \lambda_{inter}$ 的五种设置进行对比。
    *   生物合理性评估：邀请资深病理医生对生成布局进行定性盲评。
*   **充分性评价**：
    *   实验覆盖了两种不同组织来源的数据集，兼顾了不同类别数量的场景。
    *   消融实验清晰展示了各个损失项和权重的作用，验证了拓扑约束的有效性。
    *   对比方法包含了扩散模型、GAN和当前最佳的细胞布局生成模型，基准较为全面。
    *   下游任务评估展示了生成数据对实际应用的增益，实验设计具有较好的客观性和公平性。

### 6. 论文的主要结论与发现
*   **生成效果**：TopoCellGen生成的细胞布局在视觉逼真度（最低FID）、拓扑准确性（最低TopoFD）和细胞数量精度（最低TCE）上全面优于现有方法。
*   **拓扑约束的重要性**：类内和类间拓扑损失是保证多类细胞空间分布合理性的关键，仅靠细胞计数或单纯扩散模型无法捕捉细胞间的结构关系。
*   **对下游任务的增强**：用TopoCellGen合成的图像‑标注对进行数据增强，能有效提升细胞检测和分类的平均F1分数，优于其他合成数据增强方法。
*   **新指标TopoFD的有效性**：TopoFD能够捕捉到传统FID忽略的空间结构差异，更贴合实际生物学空间保真度的评估需求。

### 7. 优点
*   **首创性**：首次将扩散模型应用于多类细胞拓扑布局的显式生成，将领域知识（细胞间拓扑关系）直接融入生成过程。
*   **双重拓扑约束**：分别设计类内和类间拓扑损失，从0维和1维持久同调层面同时约束，是方法上的精巧设计。
*   **可微分的计数控制**：通过STE实现二值计数损失，解决了细胞数量不可微控制的难题，保证生成布局的密度准确性。
*   **评价指标创新**：提出TopoFD，弥补了FID在评估拓扑结构时的不足，为后续相关研究提供了更全面的量化工具。
*   **完整的生成管线**：从布局生成到条件图像合成再到下游任务验证，形成闭环，实用性较强。

### 8. 不足与局限
*   **算力信息缺失**：未报告训练所需的硬件与时间成本，影响可复现性的评估。
*   **泛化性限**：仅在两个公开数据集上验证，且细胞类别数有限，对于包含更多稀有细胞类型或更复杂组织来源的场景，效果未知。
*   **拓扑损失依赖于距离变换**：方法先将细胞点转化为距离变换图再计算拓扑，可能对细胞形状（设为单位正方形）和分布尺度敏感，实际应用中可能需要自适应阈值调整。
*   **下游任务评估有限**：仅验证了分类和检测，未评估生成布局在分割、预后预测等其他病理任务上的增益。
*   **生物合理性评估单一**：仅依赖一位病理医生的定性判断，缺乏多中心、多人评分及定量生物学指标（如TILs密度、肿瘤出芽数等）的对比验证。
*   **布局只是中间表示**：最终生成图像仍需另一个条件扩散模型，图像质量受限于该图像生成模型的能力，且未探讨布局到图像生成过程中的拓扑保真度传递。

（完）
