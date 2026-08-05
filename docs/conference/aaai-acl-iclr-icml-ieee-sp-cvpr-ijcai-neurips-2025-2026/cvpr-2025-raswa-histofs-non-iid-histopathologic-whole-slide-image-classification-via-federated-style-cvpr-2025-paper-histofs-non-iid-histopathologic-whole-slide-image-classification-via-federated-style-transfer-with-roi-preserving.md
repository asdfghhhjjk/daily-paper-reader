---
title: "HistoFS: Non-IID Histopathologic Whole Slide Image Classification via Federated Style Transfer with RoI-Preserving"
title_zh: HistoFS：面向非独立同分布病理全切片图像分类的联邦风格迁移与感兴趣区域保留
authors: "Raswa, Farchan Hakim, Lu, Chun-Shien, Wang, Jia-Ching"
date: 2025-06-01
pdf: "https://openaccess.thecvf.com/content/CVPR2025/papers/Raswa_HistoFS_Non-IID_Histopathologic_Whole_Slide_Image_Classification_via_Federated_Style_CVPR_2025_paper.pdf"
tags: ["query:cellseg"]
score: 5.0
evidence: 数字病理中的联邦全切片图像分类
tldr: 针对联邦学习在病理全切片图像分类中面临的特征分布偏移问题，提出HistoFS框架，通过感兴趣区域保留的风格迁移增强非独立同分布数据的训练，在保护隐私的同时提升分类性能。
source: CVPR-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-raswa-histofs-non-iid-histopathologic-whole-slide-image-classification-via-federated-style-cvpr-2025-paper/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 829, \"height\": 448, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-raswa-histofs-non-iid-histopathologic-whole-slide-image-classification-via-federated-style-cvpr-2025-paper/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1548, \"height\": 692, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-raswa-histofs-non-iid-histopathologic-whole-slide-image-classification-via-federated-style-cvpr-2025-paper/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1631, \"height\": 493, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-raswa-histofs-non-iid-histopathologic-whole-slide-image-classification-via-federated-style-cvpr-2025-paper/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 648, \"height\": 350, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-raswa-histofs-non-iid-histopathologic-whole-slide-image-classification-via-federated-style-cvpr-2025-paper/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 826, \"height\": 251, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-raswa-histofs-non-iid-histopathologic-whole-slide-image-classification-via-federated-style-cvpr-2025-paper/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1725, \"height\": 590, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-raswa-histofs-non-iid-histopathologic-whole-slide-image-classification-via-federated-style-cvpr-2025-paper/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1724, \"height\": 562, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-raswa-histofs-non-iid-histopathologic-whole-slide-image-classification-via-federated-style-cvpr-2025-paper/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 869, \"height\": 293, \"label\": \"Table\"}]"
motivation: 解决联邦学习中病理WSI分类的非独立同分布特征偏移问题。
method: 提出一种感兴趣区域保留的风格迁移方法用于联邦学习。
result: 在非独立同分布数据上提升了WSI分类准确率。
conclusion: 该方法为隐私保护下的多中心病理WSI分类提供了有效方案。
---

## Abstract
Federated learning for pathological whole slide image (WSI) classification allows multiple clients to train a global multiple instance learning (MIL) model without sharing their privacy-sensitive WSIs. To accommodate the non-independent and identically distributed (non-i.i.d.) feature shifts, cross-client style transfer has been popularly used but is subject to two fundamental issues: (1) WSI contains multiple morphological structures, each corresponding to a distinct style. (2) Performing style transfer may potentially shift the region of interests (RoIs) in the augmented WSIs. To address these challenges, we propose HistoFS, a federated learning framework for computational pathology on non-i.i.d. feature shifts in WSI classification. Specifically, we introduce pseudo bag styles that capture multiple style variations within a single WSI. In addition, an authenticity module is introduced to ensure that RoIs are preserved, allowing local models to learn WSIs with diverse styles while maintaining essential RoIs. Extensive experiments validate the superiority of HistoFS over state-of-the-art methods on three clinical datasets. Our code is available at https://lalakitchen.github.io/HistoFS/.

---

## 论文详细总结（自动生成）

好的，以下是对论文《HistoFS: Non-IID Histopathologic Whole Slide Image Classification via Federated Style Transfer with RoI-Preserving》的结构化深度总结。

### 1. 论文的核心问题与整体含义
- **研究背景**：病理全切片图像（WSI）分类是计算病理学中的关键任务。由于WSI尺寸巨大，通常采用多实例学习（MIL）方法，将一张WSI视为一个“包”，其中包含数千个“补丁”。
- **核心问题**：在联邦学习（FL）框架下，多个机构协作训练全局MIL模型，但不同机构的WSI数据往往呈现非独立同分布（non-i.i.d.）的特性。这主要是由于扫描仪、染色协议等差异导致的数据异质性，即“特征偏移”。
- **现有方法的局限**：目前缓解特征偏移的跨客户端风格迁移方法存在两个根本性问题：
    1.  **多形态结构**：WSI包含多种组织形态（如颜色、纹理、细胞模式），每种形态对应不同的风格，而现有方法仅使用单一风格表示一张图像，不足以准确增强WSI。
    2.  **感兴趣区域（RoI）偏移**：风格迁移可能会改变增强后WSI中的关键诊断区域（RoI），导致全局模型性能次优。
- **整体含义**：本研究旨在解决联邦病理WSI分类中，因数据非独立同分布导致的特征偏移问题，同时克服现有多形态风格表示缺失和RoI偏移的风险。

### 2. 论文提出的方法论
论文提出了名为 **HistoFS** 的联邦学习框架，其核心思想是**在保护RoI的前提下，利用多伪包风格迁移来增强本地WSI数据**，从而使本地模型能够学习多样化的风格，避免偏向特定机构风格。

关键技术细节与流程如下：
- **伪包风格构建（Pseudo Bag Styles Construction）**：
    - **动机**：一个WSI内包含多种形态，对应非均匀的统计特性（风格）。需要对一个WSI内的补丁特征进行聚类，以提取多个具有代表性的“伪风格”。
    - **流程**：首先，将每个补丁特征的局部分布建模为高斯分布 \( \mathcal{N}(\mu, \sigma^2) \)。然后，采用K-means聚类，并使用2-Wasserstein距离（公式5）作为分布间的度量，将WSI内的补丁特征分布划分为K个簇。每个簇的质心（公式6）即代表一种“伪风格”。最终，一个WSI由K个伪风格组成的集合（伪包风格）来表示，而非单一风格或全部补丁风格。这不仅捕获了多形态结构，也极大降低了联邦通信成本。
- **服务器端广播**：各机构仅需上传其WSI的少量伪包风格至服务器。服务器收集后，以非重叠方式（机构不接收自己的风格）将其他机构的伪包风格广播给各机构。
- **本地伪包风格迁移（Local Pseudo Bag Styles Transfer）**：
    - 各机构接收到来自其他机构的伪包风格后，使用自适应实例归一化（AdaIN）（公式7）将接收到的风格应用到自己的WSI的每个补丁特征上，生成增强后的WSI（\(X^{\text{aug}}\)）。其标签与原WSI保持一致。
- **真实性模块（Authenticity Module）**：
    - **动机**：风格迁移可能导致增强后WSI的RoI发生偏移。
    - **流程**：该模块通过测量和比对原始WSI和增强后WSI的**注意力权重**（由MIL聚合器输出的，标识补丁对分类贡献的权重）来工作。计算两个注意力权重向量的余弦相似度，得到“真实性得分”（公式8）。得分越高，表示RoI偏移风险越大。然后，利用该得分对增强后WSI的注意力权重进行标量乘法校准（公式9），从而对齐RoI。最终，使用原始、增强和对齐后的数据共同训练本地MIL模型。

### 3. 实验设计
- **数据集与场景**：
    - **HER2**：乳腺癌HER2状态的二分类任务。包含来自3个机构的884张WSI，存在不平衡分布。
    - **RCC**：肾细胞癌的三个亚型分类任务（CCRCC, PRCC, CHRCC）。包含来自3个机构的937张WSI，存在类别和机构间的不平衡。
    - **Camelyon17**：用于评估模型对未见客户端的泛化能力。包含来自5个机构的500张WSI的肿瘤二元分类任务。实验用前3个机构训练，后2个未见过的机构评估。
- **Benchmark与对比方法**：
    - **MIL基线方法**：HistoFL， DTFD-MIL， FRMIL。
    - **局部风格迁移**：MixStyle， DSU。
    - **联邦风格迁移**：CCST， DACS。
- **评估指标**：主要采用AUC，同时使用平衡准确率（bACC）、F1-score，并独创性地采用**熵分数**来衡量跨机构性能的公平性（性能差异程度，分数越低越公平）。

### 4. 资源与算力
- **硬件**：论文明确指出，实验在**单个NVIDIA-GTX 3050 GPU**上采用混合精度训练完成。
- **训练时长**：未明确提及时钟总时长，但报告了每轮全局通信的平均训练时间（例如，在HER2数据集上HistoFS约为720秒，显著低于对比方法）。

### 5. 实验数量与充分性
- **实验组数**：实验设计全面且充分，主要包括：
    1.  **与最先进方法对比**：在HER2、RCC两个数据集上，对比了6种基线方法，并展示了AUC和熵分数。
    2.  **未见客户端泛化评估**：在Camelyon17数据集上，对比了6种方法在未见机构上的bACC、F1和AUC表现。
    3.  **通信与效率分析**：比较了HistoFS、CCST和DACS在通信负载（MB）和平均训练时间上的差异。
    4.  **消融研究**：设计了仅使用“伪包风格”模块、“伪包风格+真实性模块”的自身模块消融实验，以及将HistoFS框架与不同MIL骨干（DTFD-MIL, FRMIL）结合的兼容性实验。
    5.  **附录中的补充实验**：论文在附录中提供了更多实验，包括：以bACC和F1-score为指标的对比、与其它聚合型FL方法的比较、缩短本地迭代轮次的影响、不同特征提取器的影响、伪包风格构建的替代策略、以及关键超参数K和λ的敏感性分析。
- **公平性与客观性**：对比方法均使用原始论文推荐的超参数，并针对WSI场景（如风格迁移方法应用于随机补丁特征）做了合理适配。实验设置公平。

### 6. 论文的主要结论与发现
- **性能领先**：HistoFS在三个临床数据集上均取得了最先进的性能，显著优于现有MIL、局部和联邦风格迁移方法。
- **公平性提升**：HistoFS在所有数据集中都取得了最低的熵分数，表明它能够有效缓解机构间的性能差异，实现更公平的联邦学习。
- **有效性验证**：消融研究证明，“伪包风格”模块和“真实性模块”对性能提升均有贡献，且两者结合效果最佳。该方法能有效兼容不同的MIL聚合器。
- **效率优势**：与CCST和DACS相比，HistoFS在取得更高AUC的同时，通信负载更低，训练时间更短。

### 7. 优点
- **创新性强**：首次在联邦WSI分类中，同时解决了多形态结构风格表示和增强后RoI偏移两个关键且被忽视的问题。
- **方法设计精妙**：引入基于Wasserstein距离的伪包风格概念，既捕获了WSI内多样性，又降低了通信成本；设计的真实性模块利用MIL自身的注意力机制来校准RoI，巧妙且无需额外标注。
- **实验扎实全面**：涵盖了多中心、多任务、不均衡数据、未见域泛化、效率和多种消融，评估指标也考虑了模型性能的公平性。
- **实用性高**：计算资源需求低（单个3050 GPU即可复现），通信开销小，有潜力应用于真实世界的多中心协作场景。

### 8. 不足与局限
- **应用泛化性**：实验局限于两个诊断任务和三个病理数据集。在更广泛的组织类型、疾病或染色协议上的有效性有待进一步验证。
- **隐私攻击风险未评估**：论文传输了伪包风格（风格的统计量），虽然不含原始图像，但未分析其是否可能泄露原始数据的某些分布信息，或是否容易受到隐私攻击。
- **风格构建的局限性**：伪包风格构建依赖预定义的聚类数目K，且用均值和标准差来表示一种“风格”是统计层面的简化，可能无法完全捕获复杂的病理组织纹理语义。
- **对比方法有限**：虽然对比了主流的联邦域泛化和风格迁移方法，但一些发表于同时期的、针对联邦病理图像的工作可能未被纳入比较。

（完）
