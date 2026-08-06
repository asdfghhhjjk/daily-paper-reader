---
title: Multi-modal Topology-embedded Graph Learning for Spatially Resolved Genes Prediction from Pathology Images with Prior Gene Similarity Information
title_zh: 基于先验基因相似性信息的多模态拓扑嵌入图学习从病理图像预测空间分辨基因
authors: "Shi, Hang, Chi, Changxi, Wan, Peng, Zhang, Daoqiang, Shao, Wei"
date: 2025-06-01
pdf: "https://openaccess.thecvf.com/content/CVPR2025/papers/Shi_Multi-modal_Topology-embedded_Graph_Learning_for_Spatially_Resolved_Genes_Prediction_from_CVPR_2025_paper.pdf"
tags: ["query:immuno-topo"]
score: 7.0
evidence: 利用图学习从病理图像预测空间分辨基因表达
tldr: 该论文针对从H和E病理图像预测空间转录组基因表达时缺乏系统结合多模态特征和拓扑信息的问题，提出一种多模态拓扑嵌入图学习方法。通过结合预训练网络和手工特征，并利用图学习建模不同采样点的拓扑轮廓，实现了高精度的基因表达预测。这一方法打通了从常规病理切片推断分子信息的计算路径。
source: CVPR-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-shi-multi-modal-topology-embedded-graph-learning-for-spatially-resolved-genes-prediction-from-cvpr-2025-paper/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 863, \"height\": 597, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-shi-multi-modal-topology-embedded-graph-learning-for-spatially-resolved-genes-prediction-from-cvpr-2025-paper/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1443, \"height\": 616, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-shi-multi-modal-topology-embedded-graph-learning-for-spatially-resolved-genes-prediction-from-cvpr-2025-paper/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1619, \"height\": 741, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-shi-multi-modal-topology-embedded-graph-learning-for-spatially-resolved-genes-prediction-from-cvpr-2025-paper/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1369, \"height\": 745, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-shi-multi-modal-topology-embedded-graph-learning-for-spatially-resolved-genes-prediction-from-cvpr-2025-paper/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1354, \"height\": 244, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-shi-multi-modal-topology-embedded-graph-learning-for-spatially-resolved-genes-prediction-from-cvpr-2025-paper/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 871, \"height\": 242, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-shi-multi-modal-topology-embedded-graph-learning-for-spatially-resolved-genes-prediction-from-cvpr-2025-paper/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 868, \"height\": 185, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-shi-multi-modal-topology-embedded-graph-learning-for-spatially-resolved-genes-prediction-from-cvpr-2025-paper/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 876, \"height\": 212, \"label\": \"Table\"}]"
motivation: 现有方法难以系统结合病理图像特征和拓扑信息来准确预测空间基因表达。
method: 提出多模态拓扑嵌入图学习，融合预训练网络和手工特征并建模空间点的拓扑关系。
result: 在预测基因表达任务上取得高精度结果。
conclusion: 图学习能有效捕获病理图像中的拓扑信息用于基因预测。
---

## Abstract
The rapid development of spatial transcriptomics (ST) allows researchers to measure the spatial-level gene expression in tissues. Although powerful, the cost for collecting the ST data is expensive, and thus several studies aim to predict gene expression in ST by utilizing their corresponding H/E stained pathology images. The existing ST based gene expression prediction models either adopt the pre-trained networks or rely on the handcrafted features to describe the pathology images, which still lack a systematic way to combine them together to define a spot-level representation that can reflect the topological profiles of different spots. On the other hand, all the ST based gene prediction models treat the prediction task for each gene independently, which overlook the fact that the exploration of potential interrelationships among them can help improve the prediction performance for individual genes.To address the above issues, we propose a multi-modal topology-embedded graph learning algorithm guided by prior Gene Ontology similarity information (i.e., M2TGLGO) to predict the spatial resolved genes from pathology image. Specifically, M2TGLGO co-learns the image representation of different spots from both deep and handcrafted features by considering the within-modal and inter-modal interactions. Next, to keep the topological structure among different spots, a spatial-oriented ranking module is also incorporated to preserve their neighborhood similarity information. Finally, we present a Gene Ontology knowledge guided graph neural network for simultaneously predicting multiple gene expressions by considering their functional associations. We evaluate our method on three public available ST datasets, the experimental results show the effectiveness of our M2TGLGO in comparison with the existing studies.

---

## 论文详细总结（自动生成）

好的，作为一名资深学术论文分析助手，我将使用中文、以 Markdown 形式，对提供的论文进行结构化、深入、客观的总结。

### **1. 论文的核心问题与整体含义（研究动机和背景）**

- **核心问题**：如何从相对廉价且易获取的 H&E 染色病理图像中，准确预测昂贵的空间转录组学基因表达数据。
- **研究动机**：
    - **成本高昂**：空间转录组学技术虽然强大，但其数据采集成本过高，限制了其在临床上的广泛应用。
    - **表征方法单一**：现有方法要么使用预训练的深度网络提取特征，要么依赖手工设计的特征来描述病理图像，缺乏系统性的方法将二者融合，以形成能反映不同测量点（spot）之间拓扑结构的表征。
    - **忽视基因间关联**：几乎所有现有模型都将每个基因的预测任务视为独立的，完全忽略了基因之间功能相似性可能对提升个体基因预测性能的帮助。
- **整体含义**：该研究旨在通过计算手段建立病理图像组织形态与分子表达之间的桥梁，以更具成本效益和可扩展性的方式推断 ST 数据的分子信息，解决传统方法成本高、表征不全和忽视基因生物学关联的三大痛点。

### **2. 论文提出的方法论**

论文提出的 **M2TGLGO** 模型是一个多模态拓扑嵌入图学习算法，其核心思想是融合多模态图像特征，同时保持测量点间的拓扑结构，并利用基因本体论先验知识来指导多基因的联合预测。方法流程涵盖以下四个关键步骤：

- **多模态病理图像特征提取**：
    - **深度特征**：使用预训练的 ResNet-101 网络从每个测量点图像中提取。
    - **手工特征**：聚焦于细胞核的形态学信息（如面积、长度、形状等14个特征）和拓扑学信息（通过 Delaunay 三角剖分计算细胞核间的平均、最大和最小距离，共3个特征）。细胞核通过预训练的 HoVer-Net 进行分割。

- **多模态图嵌入模块 (MMGE)**：
    - **核心思想**：通过图注意力网络 (GAT) 协同学习由手工特征和深度特征构成的测量点表征，同时考虑模态内和模态间的交互。
    - **模态内交互建模**：对每种模态(m)的特征，使用 GAT 聚合其空间邻居节点的信息，得到模态内嵌入 \( H^{WI}_m \)。
    - **模态间交互建模**：通过计算不同模态特征间的相似度，生成注意力权重 \( \beta_{m,n} \) 来加权聚合其他模态的特征，得到模态间嵌入 \( H^{IT}_m \)。
    - **融合与生成**：通过一个可学习的参数 \( \gamma \) 将每种模态的模态内和模态间嵌入进行加权融合，最后将所有模态的融合特征拼接起来，生成最终的测量点表征 \( H \)。

- **空间导向的邻域排序模块 (SONRM)**：
    - **核心思想**：为了缓解图学习中的过平滑问题并保持测量点间的拓扑结构，该模块强制使空间上距离更远的节点（如3-hop邻居）具有比距离更近的节点（如1-hop邻居）更低的表征相似性。
    - **实现方式**：除了最小化原始空间邻接矩阵 \( A \) 与从表征 \( H \) 重建的相似性矩阵 \( A' \) 之间的重建损失 \( L_{recon} \) 之外，还引入了一个排序损失 \( L_s \)。
    - **排序损失 \( L_s \)**：对于一个目标测量点，分别计算其与 1-hop、2-hop、3-hop 邻居的表征相似度，并将其划分为四分位数。该损失函数项会惩罚违反“跳数越大，相似度分位数应越低”这一规则的情况。

- **基因本体论知识引导的图神经网络预测**：
    - **核心思想**：首次利用基因本体论（GO）知识来显式建模基因间的功能关联，并引导多基因表达水平的协同预测。
    - **基因相似性网络构建**：根据 GO 的有向无环图结构，计算基因对之间的语义相似度 \( S_{g} \)，并以此为据构建基因关联图 \( G_g \)。
    - **基因表达预测**：使用 GAT 层处理预训练的 Gene2Vec 基因表征，得到基因预测器 \( P \)。最终，通过 \( \hat{Z} = H P^{T} \) 一次性预测出所有基因在所有测量点上的表达水平，并最小化预测值 \( \hat{Z} \) 与真实值 \( Z \) 之间的均方误差 \( L_{gene} \)。
- **总目标函数**：\( L_{total} = L_{gene} + L_s + L_{recon} \)。

### **3. 实验设计**

- **数据集**：使用了三个公开可用的空间转录组学数据集：
    - **DLPFC**: 人脑背外侧前额叶皮层样本，包含12个组织切片。
    - **BC**: 乳腺癌样本，包含12个组织切片。
    - **ccRCC**: 肾透明细胞癌样本，包含12个样本及配对的高分辨率病理图像。
- **评估基准**：
    - **基因预测结果**：评估对 **前50个高变基因 (HVG)** 和 **前50个高表达基因 (HEG)** 的预测性能。
    - **评估指标**：主要采用皮尔逊相关系数 (PCC)，均值平方误差 (MSE) 的结果在补充材料中，结论一致。
- **对比方法**:
    - **空间基因预测方法 (7种)**: Hist2ST, HisToGene, THItoGene, ST-Net, BLEEP, TRIPLEX, TG-GATEs。这是核心对比。
    - **病理图像表征方法 (6种)**: IGI-DL, SI-MIL, TMEGL, MGNN, GECMC, TSIEN。用于验证 M2TGLGO 表征模块的优越性。

### **4. 资源与算力**

- 论文**未明确提及**具体使用的 GPU 型号、数量及训练总时长。
- 文中提到优化器为 AdamW，学习率为 \( 1 \times 10^{-4} \)，训练轮次为 500 个 epoch，批次大小设置为 1。

### **5. 实验数量与充分性**

论文设计的实验较为全面和充分，体现了客观性和公平性：

- **主实验结果**：在 3 个数据集上，与 7 种 SOTA 的基因预测方法在 HVG 和 HEG 两个指标上进行了全面对比（共 \( 3 \times 2 \times 7 = 42 \) 组核心对比结果），均取得显著提升。
- **下游任务验证**：通过对预测的基因表达做空间可视化、基因-基因相关性分析，多角度验证了方法的生物学合理性。
- **消融实验**：系统性地移除了 MMGE（含模态内和模态间交互）、SONRM 和 GO 知识引导等核心组件，验证了每个模块的有效性。
- **超参数敏感性分析**：探讨了模块融合参数 \( \gamma \) 和 SONRM 中四分位数设定对模型性能的影响，证明模型具有较好的鲁棒性。
- **模态组合实验**：（在补充材料中）对比了不同模态特征组合对最终结果的影响，证实了多模态融合的优越性。

### **6. 论文的主要结论与发现**

- **性能提升显著**：所提出的 M2TGLGO 模型在三个公开 ST 数据集上，均能显著优于所有对比方法，在基因表达预测任务上取得了最高的 PCC 和最低的 MSE。
- **多模态与拓扑信息的有效性**：通过系统性地融合深度和手工特征，并结合空间拓扑结构，能够比单一模态或忽视空间关系的方法生成更具判别力的测量点表征。
- **基因关联知识的重要性**：引入基因本体论（GO）来建模基因间的功能相似性，能有效提升单个基因的预测性能，证明了挖掘基因内在关联的必要性。
- **生物学意义的恢复**：通过空间可视化和基因-基因相关性分析，验证了 M2TGLGO 不仅能准确预测数值，还能更好地恢复基因的原始空间分布模式和共表达关系。

### **7. 优点**

- **方法创新性强**：首次系统性地将多模态图像特征（深度+手工形态学+手工拓扑学）融合与空间拓扑结保持结合用于基因预测，并提出 GO 知识引导的多基因协同预测框架。
- **问题导向清晰**：设计上针对现有方法的“表征单一”、“过平滑”和“忽视基因关联”三个痛点提出精准解决方案（MMGE, SONRM, GO-GNN），逻辑链条完整。
- **实验设计扎实**：对比方法丰富、评估指标全面、数据集多样，并辅以可视化、相关性分析和详尽的消融实验，有力地支撑了核心主张。
- **生物学可解释性强**：利用 GO 知识库和手工特征（形态学、拓扑学）增强了模型的生物学可解释性，并非纯“黑箱”操作。

### **8. 不足与局限**

- **算力与时间成本未披露**：缺乏对模型训练所需计算资源（GPU型号、显存、时间）的说明，难以评估其实际应用中的硬件门槛和时间成本。
- **基因数限制**：模型主要评估了对前 50 个 HVG/HEG 的预测性能，虽然这是领域内常见做法，但在预测全转录组数万个基因时的性能及计算开销仍是挑战。
- **空间图构建的敏感性**：K-近邻图构建时的K值（文中设为6）对模型性能可能有影响，但文中未对此进行敏感性分析。
- **泛化性与偏差风险**：实验仅在脑组织和肿瘤组织上进行，对其它正常器官或疾病类型的泛化能力有待验证。此外，模型直接预测特定癌型的基因表达，可能隐式地引入了数据集的特定偏差。
- **依赖外部工具**：方法流程依赖于多种外部预训练模型和工具（ResNet-101, HoVer-Net, Gene2Vec, GO 数据库），这些组件的性能和版本更新可能会影响最终的预测结果。

（完）
