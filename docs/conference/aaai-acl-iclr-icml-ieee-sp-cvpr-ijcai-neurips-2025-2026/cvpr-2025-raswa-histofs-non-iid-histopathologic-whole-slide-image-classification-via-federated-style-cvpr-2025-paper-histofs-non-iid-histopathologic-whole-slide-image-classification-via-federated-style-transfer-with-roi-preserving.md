---
title: "HistoFS: Non-IID Histopathologic Whole Slide Image Classification via Federated Style Transfer with RoI-Preserving"
title_zh: HistoFS：通过保留感兴趣区域的联邦风格迁移实现非IID组织病理全切片图像分类
authors: "Raswa, Farchan Hakim, Lu, Chun-Shien, Wang, Jia-Ching"
date: 2025-06-01
pdf: "https://openaccess.thecvf.com/content/CVPR2025/papers/Raswa_HistoFS_Non-IID_Histopathologic_Whole_Slide_Image_Classification_via_Federated_Style_CVPR_2025_paper.pdf"
tags: ["query:profile"]
score: 6.0
evidence: 通过多实例学习聚合跨patch信息的联邦全切片分类
tldr: 针对全切片图像分类中联邦学习的非独立同分布特征偏移问题，提出保留感兴趣区域的风格迁移方法HistoFS，提升联邦多实例学习模型的性能。
source: CVPR-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-raswa-histofs-non-iid-histopathologic-whole-slide-image-classification-via-federated-style-cvpr-2025-paper/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 829, \"height\": 448, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-raswa-histofs-non-iid-histopathologic-whole-slide-image-classification-via-federated-style-cvpr-2025-paper/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1548, \"height\": 692, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-raswa-histofs-non-iid-histopathologic-whole-slide-image-classification-via-federated-style-cvpr-2025-paper/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1631, \"height\": 493, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-raswa-histofs-non-iid-histopathologic-whole-slide-image-classification-via-federated-style-cvpr-2025-paper/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 648, \"height\": 350, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-raswa-histofs-non-iid-histopathologic-whole-slide-image-classification-via-federated-style-cvpr-2025-paper/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 826, \"height\": 251, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-raswa-histofs-non-iid-histopathologic-whole-slide-image-classification-via-federated-style-cvpr-2025-paper/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1725, \"height\": 590, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-raswa-histofs-non-iid-histopathologic-whole-slide-image-classification-via-federated-style-cvpr-2025-paper/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1724, \"height\": 562, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-raswa-histofs-non-iid-histopathologic-whole-slide-image-classification-via-federated-style-cvpr-2025-paper/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 869, \"height\": 293, \"label\": \"Table\"}]"
motivation: 联邦WSI分类面临多客户端非i.i.d.特征分布偏移和风格迁移可能改变关键区域的问题。
method: 提出HistoFS框架，采用保留感兴趣区域的风格迁移来对齐跨客户端的特征分布。
result: 在非i.i.d.的WSI分类任务上优于已有联邦学习方法。
conclusion: 为分布偏移下的联邦病理图像分析提供了有效解决方案。
---

## Abstract
Federated learning for pathological whole slide image (WSI) classification allows multiple clients to train a global multiple instance learning (MIL) model without sharing their privacy-sensitive WSIs. To accommodate the non-independent and identically distributed (non-i.i.d.) feature shifts, cross-client style transfer has been popularly used but is subject to two fundamental issues: (1) WSI contains multiple morphological structures, each corresponding to a distinct style. (2) Performing style transfer may potentially shift the region of interests (RoIs) in the augmented WSIs. To address these challenges, we propose HistoFS, a federated learning framework for computational pathology on non-i.i.d. feature shifts in WSI classification. Specifically, we introduce pseudo bag styles that capture multiple style variations within a single WSI. In addition, an authenticity module is introduced to ensure that RoIs are preserved, allowing local models to learn WSIs with diverse styles while maintaining essential RoIs. Extensive experiments validate the superiority of HistoFS over state-of-the-art methods on three clinical datasets. Our code is available at https://lalakitchen.github.io/HistoFS/.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义
- **研究背景**：病理全切片图像（WSI）分类依赖多实例学习（MIL），因其千兆像素级尺寸，一张WSI被视为由数千个小图块（patch）组成的“包”。联邦学习（FL）允许多家机构在不共享隐私数据的前提下协同训练一个全局MIL模型。
- **核心问题**：不同机构的WSI由于扫描设备、染色协议等差异，导致提取的patch特征呈非独立同分布（non-i.i.d.），即特征空间存在偏移。这种偏移会损害全局模型的性能。
- **现有方法局限**：现有跨客户端风格迁移方法用于对齐特征分布，但面临两个关键缺陷：
  1. 一张WSI包含多种形态结构（如不同组织纹理），单一风格不足以描述其统计特性，而传输每个patch的风格又带来高昂通信开销。
  2. 风格迁移可能改变WSI中的关键感兴趣区域（RoI），导致加入风格增强的样本丢失原始病灶相关的重要上下文，降低分类精度。

### 2. 论文提出的方法论
- **整体框架**：HistoFS在联邦MIL框架中引入“伪包风格迁移”和“真实性模块”，在保护隐私的前提下对齐各客户端特征分布。
- **关键技术细节**：
  - **伪包风格构建**：对每个WSI，计算各patch特征的均值和标准差作为其统计风格，然后将这些patch风格分布用2-Wasserstein距离通过K-means聚类成K个簇，簇中心即为“伪包风格”。这用少量风格（如K=5）概括了单张WSI的多种形态特征，降低通信量。
  - **服务器端广播**：各客户端将本地选定WSI的伪包风格上传至服务器，服务器汇总后再广播给其他客户端（避免自身风格冗余）。
  - **局部伪包风格迁移**：客户端利用接收到的其他客户端风格，通过自适应实例归一化（AdaIN）对本地的patch特征进行风格变换，生成增强WSI，连同原始WSI一起训练本地模型。
  - **真实性模块**：为解决风格迁移导致RoI偏移的问题，计算原始WSI与增强WSI在MIL聚合器产生的注意力权重之间的余弦相似度，得到一个真实性得分，通过该得分对增强WSI的注意力权重进行标量乘法校准（似重新标定），从而强制对齐RoI区域，使模型在多样化风格下仍关注关键病灶区域。
  - **损失目标**：全局损失函数为各机构局部损失的加权和，局部损失采用交叉熵等分类损失，并加入注意力对齐的强约束（隐含在注意力权重校准中）。

### 3. 实验设计
- **数据集**：
  - **HER2**：乳腺癌HER2状态二分类（HER2+/HER2-），来自三个机构（HEROHE GC、Yale HER2、TCGA-BRCA），共884张WSI。
  - **RCC**：肾细胞癌三类分类（透明、乳头、嫌色细胞），来自TCGA的937张WSI，按组织来源随机划分为三个不重叠的客户端。
  - **Camelyon17**：用于测试未见客户端泛化性能，包含五个机构的500张WSI，取前三个机构训练，剩余两个评估。
- **对比方法**：包括MIL基线（HistoFL、DTFD-MIL、FRMIL）、局部风格迁移（MixStyle、DSU）、联邦风格迁移（CCST、DACS）。评估指标使用AUC、平衡准确率（bACC）、F1分数，并引入熵分数衡量客户端性能差异（越低越公平）。
- **实验设定**：所有方法采用SSL-ViT作为特征提取器，全局50轮通信，每轮本地训练20个epoch。HistoFS设伪包风格数K=5，真实性系数λ=0.4。

### 4. 资源与算力
- 文中明确提到实验使用“NVIDIA-GTX 3050 GPU”进行混合精度训练。
- 未说明GPU数量，从表格6的平均训练时间看，RCC和HER2每轮全局训练时间分别为760秒和720秒，共50轮，总时长合理，未使用大规模分布式算力。

### 5. 实验数量与充分性
- **主要对比实验**：在两个诊断数据集（RCC, HER2）上与6种方法比较，分别报告AUC、bACC、F1和熵分数，共2×7组核心结果。
- **未见客户端泛化实验**：在Camelyon17上与相同方法比较，统计bACC、F1、AUC和熵分数，进一步验证泛化性。
- **消融实验**：分析伪包风格模块和真实性模块的贡献（分步添加），验证HistoFS与不同MIL模型（DTFD-MIL、FRMIL）的兼容性。
- **超参数敏感性**：在附录中讨论K（伪包风格数）和λ（真实性权重）的影响。
- **其他分析**：对比通信开销与平均训练时间，与CCST、DACS相较更低；检查特征提取器的影响（附录中可能对比ResNet-50）、不同聚类策略等。
- 实验覆盖了不同分类难度、数据分布、客户端设置，对比公平，消融充分，结论可信。

### 6. 论文的主要结论与发现
- HistoFS在非i.i.d.的联邦WSI分类任务上以显著优势超越已有方法，在HER2和RCC上平均AUC分别达到86.07%和98.11%，并有效降低客户端间性能熵（更公平）。
- 伪包风格传输能以低通信代价概括WSI的多形态风格，真实性模块通过注意力对齐成功保留RoI，两者协同让本地模型学到鲁棒且病灶相关的表征。
- 在未见客户端（Camelyon17）测试中同样取得最优，表明模型具备良好泛化能力，对真实世界部署有参考价值。

### 7. 优点
- **创新性强**：首次在联邦MIL中同时处理WSI的多种形态风格和风格迁移造成的RoI偏移，思路新颖。
- **通信高效**：利用聚类生成少量伪包风格，避免了逐patch风格传输的高昂开销。
- **设计合理**：真实性模块通过注意力权重校准（而非像素级重建）对齐RoI，与MIL聚合器无缝结合。
- **实验扎实**：评测数据集多样（二类/多类/多客户端），与多种SOTA对比，消融充分，且评估了泛化性与公平性。

### 8. 不足与局限
- **算力描述不完整**：仅提及GPU型号，未说明显存大小、训练总时长等资源细节，复现成本评估不足。
- **隐私分析欠缺**：伪包风格的交换是否泄漏患者个体信息、是否满足差分隐私等未讨论，隐私保护深度有待扩展。
- **超参数敏感度**：K和λ需在实验中固定，对不同数据分布可能需要额外调优，文中未提供自动化选择策略。
- **任务范围有限**：仅验证了分类任务，未拓展到WSI分割、预后预测等更复杂场景，方法的普适性待检验。
- **对比方法版本**：部分联邦风格迁移方法（如StableFDG）因兼容性问题未纳入比较，同时未与基于生成模型的WSI增强方法（如PseMix）直接对比公平性可能受影响。

（完）
