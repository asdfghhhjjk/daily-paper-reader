---
title: "FedSDA: Federated Stain Distribution Alignment for Non-IID Histopathological Image Classification"
title_zh: FedSDA：针对非独立同分布组织病理学图像分类的联邦染色分布对齐
authors: "Cheng-Chang Tsai, Kai-Wen Cheng, Chun-Shien Lu"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/37918/41880"
tags: ["query:tme-evidence"]
score: 8.0
evidence: 联邦学习结合染色分布对齐用于组织病理学图像分类
tldr: 针对联邦学习环境下组织病理学图像的非独立同分布问题，提出通过调整各客户端数据分布的方法，利用扩散模型和染色分离技术实现染色分布对齐，从而提升分类性能，为隐私保护下的多中心病理诊断提供新途径。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-37918/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 576, \"height\": 727, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-37918/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 859, \"height\": 298, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-37918/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1812, \"height\": 489, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-37918/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 784, \"height\": 358, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-37918/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 871, \"height\": 418, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-37918/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 858, \"height\": 341, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-37918/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 867, \"height\": 381, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-37918/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 783, \"height\": 168, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-37918/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 787, \"height\": 599, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-37918/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1149, \"height\": 303, \"label\": \"Table\"}]"
motivation: 联邦学习中非独立同分布的组织病理学图像存在特征分布偏移，影响分类性能。
method: 提出FedSDA，仅通过调整数据分布，利用扩散模型和染色分离技术对齐各客户端的染色分布。
result: 在多个组织病理学图像分类数据集上验证，有效减轻分布偏移，提高分类准确率。
conclusion: 染色分布对齐策略能缓解非独立同分布问题，增强联邦学习在病理分类中的实用性。
---

## Abstract
Federated learning (FL) has shown success in collaboratively training a model among decentralized data resources without directly sharing privacy-sensitive training data. Despite recent advances, non-IID (non-independent and identically distributed) data poses an inevitable challenge that hinders the use of FL. In this work, we address the issue of non-IID histopathological images with feature distribution shifts from an intuitive perspective that has only received limited attention. Specifically, we address this issue from the perspective of data distribution by solely adjusting the data distributions of all clients. Building on the success of diffusion models in fitting data distributions and leveraging stain separation to extract the pivotal features that are closely related to the non-IID properties of histopathological images, we propose a Federated Stain Distribution Alignment (FedSDA) method. FedSDA aligns the stain distribution of each client with a target distribution in an FL framework to mitigate distribution shifts among clients. Furthermore, considering that training diffusion models on raw data in FL has been shown to be susceptible to privacy leakage risks, we circumvent this problem while still effectively achieving alignment. Extensive experimental results show that FedSDA is not only effective in improving baselines that focus on mitigating disparities across clients’ model updates but also outperforms baselines that address the non-IID data issues from the perspective of data distribution. We show that FedSDA provides valuable and practical insights for the computational pathology community.

---

## 论文详细总结（自动生成）

## 1. 研究背景与核心问题  
- **背景**：联邦学习（FL）允许多个机构在不共享隐私数据的前提下协同训练模型，在组织病理图像诊断中具有广阔前景。然而，不同医疗中心的染色协议、扫描仪品牌等差异会导致图像出现明显的颜色/特征分布偏移，造成典型的**非独立同分布（non‑IID）**问题，严重削弱联邦模型的性能。  
- **核心问题与动机**：现有工作大多从**优化**（如 FedProx、FedSAM、SCAFFOLD）或**归一化**（如 FedBN、HarmoFL）角度缓解模型更新差异或特征偏移，而**直接调整各客户端数据分布**的纯数据驱动思路尚未得到充分挖掘。少数数据分布方法（如 CCST）会严重破坏图像结构信息（SSIM 仅 0.25），因此本文旨在设计一种**仅通过对齐数据分布**来消除非独立同分布偏差的联邦学习方法，同时**保持图像结构**，并在隐私约束下实现。

## 2. 提出的方法论  
### 核心思想  
利用**染色分离**提取组织病理图像中与颜色/染色相关的关键特征，通过**扩散模型**在联邦框架下聚合所有客户端的染色矩阵，生成**目标分布**，进而**对齐每个客户端的染色分布**，从而弥合特征分布偏移。整个过程**不直接在原始图像上训练扩散模型**，以降低隐私泄露风险。

### 关键技术细节  
- **染色分离（Stain Separation）**：采用 Vahadane 等人的方法，将 H&E 染色的组织病理图像 \( x \) 分解为**染色矩阵 \( w \)（3×2，代表染色基色）和**染色密度图 \( h \)（2×N，代表染色浓度）**。  
  - 公式：\(\{w, h\} = S(x)\)，重构：\(\hat{x} = R(w, h) = I_0 \exp(-wh)\)。  
  - 通过优化目标：\[ \arg\min_{w,h} \tfrac12 \| -\log(x/I_0) - wh \|_F^2 + \lambda \|h\|_1 \] 以及非负和柱范数约束求解。

- **目标分布拟合**：每个客户端基于自己的染色矩阵 \( w \) 训练一个条件扩散模型（条件 \( c \) 为客户索引），并通过 FedAvg 聚合得到全局扩散模型 \( G(c) \)，该模型可生成任意客户的染色矩阵。  
  - 扩散模型采用**单层 Transformer**，将染色矩阵的每个元素视为一个 token，条件 \( c \) 和时间步 \( t \) 拼接后输入。  
  - 训练配置：3 轮通信、300 个本地 epoch、batch size 65 536，AdamW 优化器。该轻量网络保证额外开销极小。

- **染色对齐（Stain Alignment）**：  
  1. 客户 \( C_i \) 将其本地图像集随机等分成 \( K \) 份（\( K \) 为客户数）。  
  2. 对第 \( j \) 份图像，提取染色密度图 \( h_{i,j,k} \)，并使用全局扩散模型 \( G(j) \) 生成属于客户 \( C_j \) 的染色矩阵。  
  3. 通过 \( R(G(j), h_{i,j,k}) \) 重构图像，得到染色来自 \( C_j \) 但结构保留的图像。  
  4. 合并各份对齐后的图像，构成新的本地数据集 \( \hat{X}_i \)。  
  该过程使所有客户的数据分布趋同，且无需测试时额外处理。

### 总流程  
1. 各客户端用本地染色矩阵训练扩散模型并 FedAvg 聚合。  
2. 各客户端下载全局扩散模型，对自己的图像进行染色对齐。  
3. 在对齐后的数据集上训练肿瘤分类器（如 DenseNet-121），标准联邦学习。

## 3. 实验设计  
- **数据集**：  
  - Mitos & Atypia 14 (MA14)：乳腺癌有丝分裂和异型性分类。  
  - CAMELYON17 (C17)：前哨淋巴结转移检测（平衡数据集）。  
  - AGGC22 (A22)：前列腺 Gleason 分级（类别不平衡）。  
  每个数据集包含多个来自不同医院的域，每个域视为一个客户端，因染色差异产生自然的 non-IID。

- **评价指标**：  
  - 分类：AUROC（所有数据集）、AUPRC（仅 A22，针对不平衡）。  
  - 图像质量：SSIM（结构保持）、Wasserstein Distance、FID、KID。

- **对比基线**：  
  - **优化角度**：FedAvg（基础）、FedProx、FedSAM、FedLESAM、FedFA。  
  - **数据分布角度**：CCST（跨客户端风格迁移）、HarmoFL 中的振幅归一化（amp-norm）。  
  所有基线方法都分别测试了**不应用 FedSDA** 和 **应用 FedSDA** 时的分类性能。

## 4. 资源与算力  
- **硬件**：单块 NVIDIA Tesla V100 GPU（根据“conducted experiments on an NVIDIA Tesla V100 GPU”）。  
- **训练时间**：未明确给出训练时长，但提到扩散模型仅用 3 轮通信、300 本地 epoch 即可收敛；分类器训练 100 轮通信，每轮 1 个本地 epoch。  

## 5. 实验数量与充分性  
- **主要实验**：  
  - 表 2：在 C17 和 A22 上，5 种基线（FedAvg、FedProx、FedSAM、FedLESAM、FedFA）应用 FedSDA 前后的 AUROC/AUPRC 对比（共 10 行结果）。  
  - 表 3：FedAvg 上嵌入 CCST、amp-norm、FedSDA 的分类与图像质量对比（在 C17、A22、MA14&C17&A22 综合指标）。  
  - 图 5：A22 上各方法收敛曲线。  
  - 图 6：C17 的 t-SNE 可视化，展示对齐前后特征分布变化。

- **消融实验**：  
  - 扩散模型通信轮次 vs. 本地 epoch（图 7），发现增加本地 epoch（300）可大幅减少通信轮次（3 轮即收敛）。  
  - 扩散模型网络结构对比（表 1）：单层 Transformer vs. 单层 MLP，FD 指标显示 MLP 性能严重下降。  

- **评估充分性**：  
  - 涵盖多个数据集、类不平衡情况、多种优化类和数据分布类基线，指标兼顾分类性能和图像结构保持。  
  - 消融实验验证了本地 epoch 和网络结构对扩散模型收敛性和质量的影响。  
  - 实验设计相对公平：所有对比均在相同数据划分下进行，使用标准联邦设定，并且基线代码与 FedSDA 集成简单（每个基线仅需应用数据对齐模块）。  

## 6. 主要结论与发现  
- FedSDA 能够**显著提升**多种优化类联邦方法（如 FedAvg）在 non-IID 组织病理图像上的分类性能，甚至让 vanilla FedAvg 超越更复杂的方法。  
- 在数据分布调整类方法中，FedSDA 在保持图像结构（高 SSIM）的同时，分类准确率和图像分布距离均优于 CCST 和振幅归一化。  
- 通过特征可视化证实，FedSDA 拉近了各客户端数据在特征空间的距离，有效缓解了特征漂移。  
- 训练扩散模型时采用染色矩阵而非原始图像，既实现了全客户端染色分布共享，又规避了原始数据梯度泄露等隐私风险。

## 7. 方法优点  
- **思路新颖**：直接调整数据分布应对非独立同分布，并通过染色分离精准操作与偏移高度相关的成分，不影响组织结构信息。  
- **隐私友好**：不在原始图像上训练生成模型，降低窃取风险；整个对齐过程在本地完成，不共享原始像素。  
- **实用性强**：测试时无需任何额外归一化或处理，对齐后的图像可直接送入任何分类器，易于集成。  
- **实验扎实**：在三个公开病理数据集上验证，覆盖手术淋巴结、乳腺、前列腺等多种组织，对比范围广，消融实验充分。

## 8. 不足与局限  
- **生成模型开销**：虽然扩散模型网络很轻量，但仍需要额外的训练和对齐过程，可能在某些计算资源极度受限的场景中成为负担。  
- **染色类型限制**：染色分离和扩散模型均基于 H&E 双染色假设，不能直接拓展到免疫组化（IHC）或其他染色方式。  
- **客户端数量敏感**：扩散模型的条件是客户端索引，当客户端数量动态变化或较多时，可能需要重新训练或条件扩展。  
- **隐私攻击评估不完整**：仅讨论了数据窃取风险，未评估更高级的成员推断或重构攻击在染色矩阵训练下的实际威胁；且依赖 FedAvg 聚合，仍可能面临模型反演风险。  
- **类别不平衡处理**：虽然 A22 采用 AUPRC 评估，但 FedSDA 本身未专门设计处理标签偏移的措施，可能无法应对极端标签分布偏移。  
- **实验范围限制**：仅在三个病理数据集上测试，且分类器统一为 DenseNet-121，未考察与其他骨干网络或更细粒度任务的兼容性；对比基线中也缺少近期的一些强联邦学习正则化方法（如 MOON、FCCL 等）。

（完）
