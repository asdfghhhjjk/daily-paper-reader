---
title: "FedSDA: Federated Stain Distribution Alignment for Non-IID Histopathological Image Classification"
title_zh: FedSDA：面向非独立同分布组织病理图像分类的联邦染色分布对齐
authors: "Cheng-Chang Tsai, Kai-Wen Cheng, Chun-Shien Lu"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/37918/41880"
tags: ["query:path-xai-sel"]
score: 7.0
evidence: 联邦学习结合染色分布对齐用于组织病理图像分类
tldr: 解决联邦组织病理学中染色分布偏移导致的非独立同分布问题，提出通过染色分离和扩散模型对齐客户端数据分布，提升分类模型性能。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-37918/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 576, \"height\": 727}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-37918/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 859, \"height\": 298}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-37918/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1812, \"height\": 489}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-37918/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 784, \"height\": 358}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-37918/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 871, \"height\": 418}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-37918/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 858, \"height\": 341}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-37918/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 867, \"height\": 381}]"
tables_json: "[{\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-37918/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 783, \"height\": 168}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-37918/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 787, \"height\": 599}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-37918/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1149, \"height\": 303}]"
motivation: 联邦学习中不同站点染色差异造成数据分布偏移，阻碍模型训练。
method: 利用染色分离与扩散模型调整客户端数据分布，实现分布对齐。
result: 在多个组织病理分类任务上有效缓解非独立同分布影响。
conclusion: 为隐私保护下的组织病理图像分类提供了染色归一化新思路。
---

## Abstract
Federated learning (FL) has shown success in collaboratively training a model among decentralized data resources without directly sharing privacy-sensitive training data. Despite recent advances, non-IID (non-independent and identically distributed) data poses an inevitable challenge that hinders the use of FL. In this work, we address the issue of non-IID histopathological images with feature distribution shifts from an intuitive perspective that has only received limited attention. Specifically, we address this issue from the perspective of data distribution by solely adjusting the data distributions of all clients. Building on the success of diffusion models in fitting data distributions and leveraging stain separation to extract the pivotal features that are closely related to the non-IID properties of histopathological images, we propose a Federated Stain Distribution Alignment (FedSDA) method. FedSDA aligns the stain distribution of each client with a target distribution in an FL framework to mitigate distribution shifts among clients. Furthermore, considering that training diffusion models on raw data in FL has been shown to be susceptible to privacy leakage risks, we circumvent this problem while still effectively achieving alignment. Extensive experimental results show that FedSDA is not only effective in improving baselines that focus on mitigating disparities across clients’ model updates but also outperforms baselines that address the non-IID data issues from the perspective of data distribution. We show that FedSDA provides valuable and practical insights for the computational pathology community.

---

## 论文详细总结（自动生成）

## 1. 论文的核心问题与整体含义

- **核心问题**：在联邦学习（FL）框架下，各参与方（如不同医疗中心）的组织病理图像存在显著的非独立同分布（non‑IID）特性，主要表现为因染色协议、扫描设备差异导致的**特征分布偏移**（feature distribution shifts）。这种偏移严重损害了全局分类模型的性能与泛化能力。
- **研究动机**：现有工作大多从**优化**（如 FedProx、FedSAM）或**归一化**（如 FedBN、HarmoFL）角度缓解 non‑IID 问题，但极少直接调整各客户端的数据分布本身。少量从数据分布切入的方法（如 CCST）会丢失图像的结构信息，不利于肿瘤分类。因此，需要一种**在保护结构信息的前提下，对齐各客户端染色分布**的联邦学习方法。
- **整体含义**：FedSDA 旨在通过**染色分离**和**扩散模型**，在不直接共享原始数据的前提下，对齐各客户端的染色分布，从而缓解特征分布偏移，提升分类模型在 non‑IID 组织病理图像上的性能。

## 2. 方法论

### 核心思想
- 将组织病理图像分解为**颜色相关**的染色矩阵（stain matrix）和**结构相关**的染色密度图（stain density map），仅调整染色矩阵，保全结构信息。
- 在联邦框架下训练一个条件扩散模型，用于**拟合所有客户端的染色矩阵联合分布**（目标分布），使每个客户端能生成其他客户端的染色矩阵。
- 利用生成的染色矩阵与自身的染色密度图重构图像，实现**染色分布对齐**，从而消除各客户端数据分布差异。

### 关键技术细节
1. **染色分离**（Stain Separation）  
   - 采用 Vahadane 等人的稀疏染色分离方法，将 H&E 染色图像 \(x\) 分解为染色矩阵 \(w \in \mathbb{R}^{3\times r}\) 和染色密度图 \(h \in \mathbb{R}^{r\times N}\)，满足 \(x \approx I_0 \exp(-wh)\)。  
   - 分离过程通过优化问题 \(\arg\min_{w,h} \frac{1}{2}\|-\log(x/I_0)-wh\|_F^2 + \lambda\|h\|_1\) 实现，约束 \(w\ge 0, h\ge 0\) 且每列 \(w\) 的二范数为 1。

2. **目标分布拟合**  
   - 采用单层 Transformer 作为扩散模型骨干（表 1 显示其 FD 分数显著优于 MLP，仅需少量参数）。  
   - 在联邦平均（FedAvg）框架下训练条件扩散模型：每个客户端以其 ID 为条件，仅用本地染色矩阵训练扩散模型，上传梯度/权重，由中心服务器聚合。  
   - 扩散模型在低维染色矩阵上训练，避免原始图像隐私泄露风险，且通信开销低。

3. **染色对齐**  
   - 每个客户端下载训练好的扩散模型 \(G\)，将本地图像均匀划分 \(K\) 份（\(K\) 为客户端数）。  
   - 对第 \(j\) 份图像，用染色分离得到染色密度图 \(\{h_{i,j,k}\}\)，再用扩散模型生成第 \(j\) 个客户端的染色矩阵 \(G(j)\)，按下式重构图像：  
     \[
     \hat{x}_{i,j,k} = R(G(j), h_{i,j,k})
     \]  
     从而获得对齐后的数据集 \(\hat{X}_i\)。  
   - 该过程无需访问其他客户端的原始图像或染色矩阵，仅依赖联邦训练的扩散模型。

### 算法流程
- **第一阶段**：所有客户端在中心服务器协调下，用本地染色矩阵共同训练一个条件扩散模型（FedAvg 方式）。  
- **第二阶段**：各客户端下载扩散模型，独立完成本地图像的染色对齐，生成分布对齐的新数据集。  
- **第三阶段**：在对齐后的数据集上，用任意 FL 分类算法（如 FedAvg、FedProx 等）训练肿瘤分类模型。

## 3. 实验设计

- **数据集**：  
  - Mitos & Atypia 14 (MA14)  
  - CAMELYON17 (C17)  
  - AGGC22 (A22)  
  所有数据集均为 H&E 染色的全切片组织病理图像，从中提取图像块进行 patch‑level 分类。各数据集按采集医院或扫描仪差异天然划分为多个域（每个域为一个客户端）。
- **对比方法**：  
  - **优化类基线**：FedAvg、FedProx、FedSAM、FedLESAM、FedFA。  
  - **数据分布类基线**：CCST（跨客户端风格迁移）、amp‑norm（HarmoFL 中的振幅归一化）。  
  - FedSDA 作为即插即用模块，嵌入到上述优化类基线中测试性能提升；同时与 CCST 和 amp‑norm 直接比较。
- **评价指标**：  
  - 分类性能：AUROC（所有数据集）、AUPRC（A22 数据集）。  
  - 图像质量：SSIM（结构保持度）、FID/KID（分布距离）、WD（颜色差异）。

## 4. 资源与算力

- 论文明确提到实验使用**单块 NVIDIA Tesla V100 GPU** 进行。  
- 扩散模型训练配置：3 个通信轮次，每轮本地 300 个 epoch，批次大小 65,536，使用 AdamW 优化器。  
- 分类器训练：100 个通信轮次，每轮 1 个本地 epoch，批次大小 128，SGD 优化器。  
- 未给出详细的耗时（小时/天）数据，但指出扩散模型因处理低维染色矩阵且采用单层网络，开销极小。

## 5. 实验数量与充分性

- **主实验**：  
  - 在 C17 和 A22 两个数据集上，将 FedSDA 嵌入 5 种优化类基线，共 10 组对比实验（表 2）。  
  - 同时对比 FedSDA 与 CCST、amp‑norm 在相同数据集上的分类性能与图像质量，涵盖 MA14、C17、A22 三个数据集（表 3 及正文描述）。  
  - 提供收敛曲线对比（图 5）和 t‑SNE 特征可视化（图 6 及附录）。
- **消融实验**：  
  - 扩散模型通信轮次 vs. 本地 epoch 的影响（图 7）。  
  - 扩散模型网络架构（Transformer vs. MLP）对比（表 1）。  
- **补充实验**：  
  - 附录中包含染色矩阵可视化（图 14‑16）、CCST 与 FedSDA 结构保持效果对比（图 17‑18）等。  
- 实验设计公平：所有基线使用相同分类网络（DenseNet-121）、优化器和超参数；FedSDA 仅作为数据预处理步骤，不改变下游分类器训练流程。总体实验数量较丰富，消融分析充分，支撑核心结论。

## 6. 主要结论与发现

- FedSDA 能**显著提升**各类基于优化的 FL 方法的分类性能（如 C17 上 FedAvg 的 AUROC 从 90.97% 提升至 93.84%，A22 上 AUROC 从 78.99% 提升至 90.38%）。  
- 相比专门从数据分布角度设计的 CCST 和 amp‑norm，FedSDA 在分类效果和图像结构保真度（SSIM）上取得明显优势，且不需要在测试时进行额外归一化处理。  
- 在扩散模型训练阶段，使用低维染色矩阵（而非原始图像）进行联邦学习，既能有效拟合目标分布，又能规避针对扩散模型的隐私攻击（如 DataStealing）。  
- 增大本地 epoch 数（如 300）可大幅减少通信轮次（仅需 3 轮），使联邦扩散模型训练具有更好的通信效率。

## 7. 优点

- **数据分布层面的创新**：首次在联邦学习中结合染色分离与扩散模型，从根源上缓解组织病理图像的特征分布偏移，区别于优化或归一化方法。  
- **结构信息保全**：通过染色分离，仅修改染色矩阵而保留密度图，避免风格迁移中常见的结构失真问题（如表 3 中 SSIM=0.9969，远高于 CCST 的 0.2462）。  
- **隐私保护设计**：扩散模型在染色矩阵而非原始图像上训练，降低了梯度泄露等隐私风险。  
- **即插即用**：FedSDA 作为预处理步骤，可与任何下游 FL 算法无缝结合，实验证明对多种方法均有增益。  
- **轻量高效**：扩散模型使用单层 Transformer，训练只需 3 轮通信，推理时仅进行染色矩阵生成和图像重构，开销可控。

## 8. 不足与局限

- **染色分离假设**：方法依赖 H&E 染色图像的两染色模型，对于不属于此染色模式的其他病理图像（如 IHC 染色）或非标准染色的扫描仪，适用性可能受限。  
- **扩散模型泛化性**：扩散模型训练依赖于所有客户端的染色矩阵，若新增客户端且其染色分布与训练时差异过大，可能需要重新训练或微调。  
- **隐私风险未完全消除**：尽管在染色矩阵上训练降低了泄露风险，但梯度反演、成员推理攻击等威胁未进行系统验证，仅列举相关工作，缺乏直接防护措施。  
- **实验场景单一**：仅在三个公开组织病理数据集上验证，未在更多样化的医学图像或更大规模跨中心数据上测试。  
- **资源消耗细节缺失**：未报告训练总时长、内存占用等具体开销数据，实际部署中的成本难以评估。

（完）
