---
title: "HistoFS: Non-IID Histopathologic Whole Slide Image Classification via Federated Style Transfer with RoI-Preserving"
title_zh: HistoFS：通过保留ROI的联邦风格迁移实现非独立同分布组织病理学全切片图像分类
authors: "Raswa, Farchan Hakim, Lu, Chun-Shien, Wang, Jia-Ching"
date: 2025-06-01
pdf: "https://openaccess.thecvf.com/content/CVPR2025/papers/Raswa_HistoFS_Non-IID_Histopathologic_Whole_Slide_Image_Classification_via_Federated_Style_CVPR_2025_paper.pdf"
tags: ["query:immuno-topo"]
score: 8.0
evidence: 联邦学习框架应用于WSI分类，采用保留感兴趣区域的风格迁移
tldr: 针对联邦学习场景下WSI分类中的非独立同分布特征漂移，提出HistoFS，通过带有ROI保留的客户端风格迁移，既适应多重形态风格又保护感兴趣区域，实现隐私安全的全局病理分类模型。
source: CVPR-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-raswa-histofs-non-iid-histopathologic-whole-slide-image-classification-via-federated-style-cvpr-2025-paper/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 829, \"height\": 448}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-raswa-histofs-non-iid-histopathologic-whole-slide-image-classification-via-federated-style-cvpr-2025-paper/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1548, \"height\": 692}]"
tables_json: "[{\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-raswa-histofs-non-iid-histopathologic-whole-slide-image-classification-via-federated-style-cvpr-2025-paper/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1631, \"height\": 493}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-raswa-histofs-non-iid-histopathologic-whole-slide-image-classification-via-federated-style-cvpr-2025-paper/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 648, \"height\": 350}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-raswa-histofs-non-iid-histopathologic-whole-slide-image-classification-via-federated-style-cvpr-2025-paper/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 826, \"height\": 251}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-raswa-histofs-non-iid-histopathologic-whole-slide-image-classification-via-federated-style-cvpr-2025-paper/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1725, \"height\": 590}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-raswa-histofs-non-iid-histopathologic-whole-slide-image-classification-via-federated-style-cvpr-2025-paper/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1724, \"height\": 562}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-raswa-histofs-non-iid-histopathologic-whole-slide-image-classification-via-federated-style-cvpr-2025-paper/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 869, \"height\": 293}]"
motivation: 病理WSI包含多种风格，联邦学习中风格迁移可能破坏诊断关键区域。
method: 设计HistoFS框架，在联邦学习中实施ROI保留的跨客户端风格迁移，以应对非独立同分布特征。
result: 在多个数据集上有效提升了非独立同分布条件下的WSI分类精度。
conclusion: HistoFS实现了隐私保护下可靠的WSI分类，证明了风格迁移在联邦病理学中的有效性。
---

## Abstract
Federated learning for pathological whole slide image (WSI) classification allows multiple clients to train a global multiple instance learning (MIL) model without sharing their privacy-sensitive WSIs. To accommodate the non-independent and identically distributed (non-i.i.d.) feature shifts, cross-client style transfer has been popularly used but is subject to two fundamental issues: (1) WSI contains multiple morphological structures, each corresponding to a distinct style. (2) Performing style transfer may potentially shift the region of interests (RoIs) in the augmented WSIs. To address these challenges, we propose HistoFS, a federated learning framework for computational pathology on non-i.i.d. feature shifts in WSI classification. Specifically, we introduce pseudo bag styles that capture multiple style variations within a single WSI. In addition, an authenticity module is introduced to ensure that RoIs are preserved, allowing local models to learn WSIs with diverse styles while maintaining essential RoIs. Extensive experiments validate the superiority of HistoFS over state-of-the-art methods on three clinical datasets. Our code is available at https://lalakitchen.github.io/HistoFS/.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义（研究动机和背景）
*   **核心问题**：在联邦学习（FL）框架下进行全切片图像（WSI）分类时，不同机构（客户端）的数据因扫描仪、染色协议等差异呈现**非独立同分布（non-IID）**的特征漂移，严重影响了全局模型的性能。
*   **研究动机**：
    *   现有联邦病理方法（如 HistoFL）主要关注模型聚合，**忽略了跨机构的非 IID 特征偏移**。
    *   用于缓解特征偏移的跨客户端风格迁移方法存在两个根本性缺陷：
        1.  **单一风格假设失效**：一张 WSI 包含成百上千个形态结构（如不同细胞/组织区域），对应多种不同的风格统计特性，无法用单一风格表示。
        2.  **感兴趣区域（RoI）可能被破坏**：经典风格迁移在改变图像统计量时，可能无意中改变或模糊了对诊断至关重要的病理区域（RoI），导致模型性能下降。
*   **整体含义**：论文旨在提出一种**保留 RoI 的联邦风格迁移框架**，使本地模型能学习到多样化的跨机构风格，同时确保关键病理区域不会在增强过程中丢失，从而训练出更鲁棒、公平且隐私安全的 WSI 分类模型。

### 2. 论文提出的方法论：核心思想、关键技术细节
*   **核心思想**：通过“**伪包风格**”捕捉每张 WSI 的多重形态风格，并利用“**真实性模块**”在对齐风格的过程中保护 RoI，实现非 IID 场景下的高效联邦多实例学习（MIL）。
*   **关键技术细节与流程**：
    *   **伪包风格构建（Pseudo Bag Styles）**
        *   对每个 WSI 的 patch 特征，计算其局部统计量（均值 `μ` 和标准差 `σ`）作为该 patch 的风格向量。
        *   将每个 patch 的风格建模为高斯分布，并采用 **2-Wasserstein 距离**作为分布间距离度量，进行 **K-means 聚类**。
        *   将得到的 `K` 个聚类中心作为该 WSI 的“伪包风格”（Pseudo Bag Styles），从而用少量代表风格捕获 WSI 内部的多形态特性，大幅降低后续通信开销。
    *   **服务器端广播与风格迁移**
        *   客户端将本地部分 WSI 的伪包风格上传至服务器；服务器收集后，将**除请求方自己的风格之外**的所有风格广播给各个客户端。
        *   客户端接收到多样化的伪包风格后，对本地每个 patch 特征用 **自适应实例归一化（AdaIN）** 进行风格迁移，生成风格增强的 WSI 特征包。公式为：`x_augment = σ_k * ((x - μ(x)) / σ(x)) + μ_k`。
    *   **真实性模块（Authenticity Module）**：保护 RoI 不被风格扭曲
        *   分别计算原始 WSI 和增强 WSI 经过注意力聚合器产生的**注意力权重向量** `A` 和 `A(aug)`。
        *   通过**余弦相似度**计算真实性分数 `Auth_score = 1 - λ * cosine_similarity(A, A(aug))`，该分数越高代表 RoI 偏移越大。
        *   然后利用该分数对增强 WSI 的注意力权重进行**标量乘法重标定**：`A(align) = Auth_score * A(aug)`，使模型在更新时更关注与原始 WSI 一致的 RoI，确保关键区域信息不丢失。

### 3. 实验设计：数据集、基准与对比方法
*   **数据集与场景**：
    *   **HER2 数据集**：来自 3 家机构（TCGA-BRCA等），共 884 张 WSI，二分类（HER2+/HER2-），用于评估联邦下特征偏移问题。
    *   **RCC 数据集**：来自 TCGA，按组织来源随机划分为 3 个不重叠机构，共 937 张 WSI，三分类（透明细胞癌、乳头状、嫌色细胞癌）。
    *   **Camelyon17 数据集**：包含 5 家机构的 500 张 WSI，二分类（良/恶性）。使用前 3 家机构数据进行训练，后 2 家机构作为 **未见客户端** 评估模型泛化能力。
*   **基准与对比方法**：
    *   **MIL 方法**：HistoFL、DTFD-MIL、FRMIL。
    *   **本地风格迁移方法**：MixStyle、DSU。
    *   **联邦风格迁移方法**：CCST、DACS。
*   **评价指标**：AUC、平衡准确率（bACC）、F1 分数；并专门引入 **熵得分（Entropy Score）** 量化机构间性能的公平性/分歧度。

### 4. 资源与算力
*   **所用 GPU**：明确提及实验在一张 **NVIDIA GTX 3050** GPU 上完成。
*   **训练设置**：采用混合精度训练。通信轮次共 50 轮，每轮本地训练 20 个 epoch。
*   **训练时长**：论文表 6 给出了平均每全局轮的训练时间（秒）。在 RCC 数据集上，HistoFS 约为 **760 秒**；在 HER2 数据集上约为 **720 秒**，均显著低于对比方法（CCST 约 1485/1590 秒）。

### 5. 实验数量与充分性
*   **实验数量丰富**：覆盖 **3 个** 临床多样数据集，进行了 **2 大组** 对比实验（已知机构内部、未见机构泛化）。
*   **消融研究充分**：
    *   分离测试了“仅伪包风格”与“添加真实性模块”的效果，验证了两个组件的贡献。
    *   将 HistoFS 与 **另两种主流 MIL 模型（DTFD-MIL, FRMIL）** 相结合，验证了方法的兼容性。
    *   附录中进一步涵盖：不同指标（bACC/F1）、与聚合型 FL 方法对比、不同本地迭代次数、不同特征提取器、替代构建策略、关键超参数 `K` 和 `λ` 的敏感性分析等多组实验。
*   **客观公平性**：对比方法均采用原论文推荐超参数；所有方法在同一特征提取器和实验配置下进行；采用多指标（包括公平性熵得分）评估，实验设计标准、客观。

### 6. 论文的主要结论与发现
*   **SOTA 性能**：HistoFS 在所有评估数据集上均取得了最优的平均 AUC（如 RCC 达 98.11%，HER2 达 86.07%），并在未见客户端场景下展现了最强的泛化能力（如 Camelyon17 上平均 AUC 84.67%）。
*   **性能公平性**：HistoFS 的熵得分始终最低，说明它有效地**缩小了不同机构间的性能差距**，实现了更公平的联邦学习。
*   **组件有效性**：伪包风格构建和真实性模块两者都对性能提升有独立且累积的贡献。真实性模块能有效保护 RoI，防止增强带来的性能退化。
*   **高效通信**：通过只传输每个 WSI 的 `K=5` 个伪风格，HistoFS 在保证高精度的同时，**显著降低了通信负载和本地训练耗时**。

### 7. 优点：方法或实验设计上的亮点
*   **问题洞察深刻**：明确指出了 WSI 多形态风格和 RoI 保护两个被忽视的关键痛点，并首次在联邦风格迁移框架中同时解决。
*   **方法设计精巧**：
    *   “伪包风格”利用聚类高效表征复杂组织形态，既避免了传输巨量风格，又捕获了 WSI 内部的风格多样性。
    *   “真实性模块”巧妙地通过**对齐注意力权重**来保护 RoI，无需额外的像素级约束，将病理诊断知识隐含地融入增强过程。
*   **实验全面严谨**：不仅关注模型精度，还考察了**泛化性（未见客户端）** 和**公平性（熵得分）**；充分的消融实验论证了每个设计的有效性。
*   **实用性强**：方法即插即用，可兼容不同的 MIL 聚合器，且通信与计算开销低，适合真实医疗联邦环境。

### 8. 不足与局限
*   **对预训练特征提取器的依赖**：方法构建于预训练的 SSL-ViT 特征之上，若特征提取器本身对机构风格敏感或质量不佳，可能会影响伪风格聚类和下游性能。
*   **注意力机制的局限性**：真实性模块假设注意力权重能准确反映 RoI，但若当 WSI 类别与微小的组织形态有关，注意力可能本身就不够精确或无法定位关键区域，此时真实性模块的保护效果可能有限。
*   **对比方法范围可扩展**：部分联邦风格方法（如 StableFDG）因声称的“不兼容”被排除，虽然作者给出了理由，但仍可能遗漏了潜在的可比基线，对比的全面性略受限制。
*   **隐私保护分析较浅**：除了添加高斯噪声外，论文未对风格信息本身可能泄露的隐私风险进行深入分析（如风格反演攻击），也未与差分隐私等机制结合。
*   **数据集局限**：实验涉及 3 个公开数据集，尚未在更大规模的、疾病种类更丰富的真实联邦网络中进行验证，其泛化至极端标签不平衡或罕见病的鲁棒性有待考证。

（完）
