---
title: "LangDAug: Langevin Data Augmentation for Multi-Source Domain Generalization in Medical Image Segmentation"
title_zh: "LangDAug: 用于医学图像分割多源领域泛化的Langevin数据增强"
authors: "Piyush Tiwary, Kinjawl Bhattacharyya, Prathosh AP"
date: 2025-05-01
pdf: "https://openreview.net/pdf?id=LB5F02kwAv"
tags: ["query:cellseg"]
score: 4.0
evidence: 医学图像分割，领域泛化，数据增强
tldr: 针对医学图像分割模型在不同域之间泛化能力差的问题，提出LangDAug方法，利用基于能量的模型通过Langevin动力学生成增强样本，提升多源领域泛化性能。在多个分割基准上验证了其有效性，尤其对病理图像等复杂场景具有潜力。
source: ICML-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-icml-2025-lb5f02kwav/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1736, \"height\": 934, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-lb5f02kwav/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 831, \"height\": 324, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-lb5f02kwav/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 852, \"height\": 523, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-lb5f02kwav/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 847, \"height\": 751, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-lb5f02kwav/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1809, \"height\": 2058, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-lb5f02kwav/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1648, \"height\": 2095, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-lb5f02kwav/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1647, \"height\": 2101, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-lb5f02kwav/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1647, \"height\": 2109, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-lb5f02kwav/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1645, \"height\": 2103, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-lb5f02kwav/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1646, \"height\": 2094, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-lb5f02kwav/fig-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1649, \"height\": 1371, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-lb5f02kwav/fig-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1645, \"height\": 2100, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-lb5f02kwav/fig-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 1649, \"height\": 1371, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-lb5f02kwav/fig-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 1647, \"height\": 2095, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-lb5f02kwav/fig-015.webp\", \"caption\": \"\", \"page\": 0, \"index\": 15, \"width\": 1648, \"height\": 1371, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-lb5f02kwav/fig-016.webp\", \"caption\": \"\", \"page\": 0, \"index\": 16, \"width\": 1647, \"height\": 2091, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-lb5f02kwav/fig-017.webp\", \"caption\": \"\", \"page\": 0, \"index\": 17, \"width\": 1646, \"height\": 1370, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-lb5f02kwav/fig-018.webp\", \"caption\": \"\", \"page\": 0, \"index\": 18, \"width\": 1646, \"height\": 2093, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-lb5f02kwav/fig-019.webp\", \"caption\": \"\", \"page\": 0, \"index\": 19, \"width\": 1649, \"height\": 1369, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-lb5f02kwav/fig-020.webp\", \"caption\": \"\", \"page\": 0, \"index\": 20, \"width\": 1646, \"height\": 2096, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-lb5f02kwav/fig-021.webp\", \"caption\": \"\", \"page\": 0, \"index\": 21, \"width\": 1650, \"height\": 1371, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-icml-2025-lb5f02kwav/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1775, \"height\": 405, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-lb5f02kwav/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1429, \"height\": 501, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-lb5f02kwav/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1773, \"height\": 236, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-lb5f02kwav/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 862, \"height\": 224, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-lb5f02kwav/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1432, \"height\": 174, \"label\": \"Table\"}]"
motivation: 医学图像分割模型在不同域间泛化困难，现有数据增强方法缺乏理论保障。
method: 利用能量模型通过Langevin动力学生成合成样本，用于多源领域泛化的数据增强。
result: 在多个医学图像分割数据集上达到领先的泛化性能。
conclusion: Langevin数据增强能有效提升分割模型对域变化的鲁棒性。
---

## Abstract
Medical image segmentation models often struggle to generalize across different domains due to various reasons. Domain Generalization (DG) methods overcome this either through representation learning or data augmentation (DA). While representation learning methods seek domain-invariant features, they often rely on ad-hoc techniques and lack formal guarantees. DA methods, which enrich model representations through synthetic samples, have shown comparable or superior performance to representation learning approaches. We propose LangDAug, a novel **Lang**evin **D**ata **Aug**mentation for multi-source domain generalization in 2D medical image segmentation. LangDAug leverages Energy-Based Models (EBMs) trained via contrastive divergence to traverse between source domains, generating intermediate samples through Langevin dynamics. Theoretical analysis shows that LangDAug induces a regularization effect, and for GLMs, it upper-bounds the Rademacher complexity by the intrinsic dimensionality of the data manifold. Through extensive experiments on Fundus segmentation and 2D MRI prostate segmentation benchmarks, we show that LangDAug outperforms state-of-the-art domain generalization methods and effectively complements existing domain-randomization approaches. The codebase for our method is available at https://github.com/backpropagator/LangDAug.

---

## 论文详细总结（自动生成）

# LangDAug: 详细中文总结

## 1. 论文的核心问题与整体含义（研究动机和背景）

- **核心问题**：医学图像分割模型在不同数据分布（域）之间泛化能力差。由于成像协议、设备规格、患者属性等差异，训练集（源域）与测试集（目标域）之间存在域偏移，导致基于经验风险最小化（ERM）的模型在未见过的域上性能严重下降。
- **研究背景**：现有领域泛化（DG）方法主要分为表示学习和数据增强两类。表示学习方法追求域不变特征，但往往依赖启发式技术且缺乏理论保证；数据增强方法通过合成样本来丰富模型表示，已展示出与表示学习相当或更优的性能。论文旨在提出一种新的数据增强方法，既能提升泛化性，又具有理论支撑。

## 2. 论文提出的方法论：核心思想、关键技术细节

- **核心思想**：利用能量模型（EBM）通过Langevin动力学在源域之间遍历，生成连接不同域的中间样本（称为“Langevin样本”），并将这些样本作为数据增强加入到ERM训练中，从而让模型学习到更广阔的域空间。
- **关键技术细节**：
  - **EBM训练**：对每对源域 \(D_i\) 和 \(D_j\)（\(i \neq j\)）训练一个EBM \(E_{\theta_{ij}}\)，使用对比散度损失。损失梯度为：\(\nabla_{\theta} L_{CD} = \mathbb{E}_{P_{D_j}}[\nabla_{\theta} E_\theta(x)] - \mathbb{E}_{P_\theta}[\nabla_{\theta} E_\theta(x)]\)。其中从 \(P_\theta\) 采样通过Langevin动力学近似：从 \(D_i\) 的样本初始化，运行K步LD：\(x_{t+1} = x_t - \frac{\alpha^2}{2} \nabla_{x_t} E_\theta(x_t) + \alpha \epsilon\)。
  - **Langevin数据增强**：对每个源域样本 \(x_j \in D_i\)，运行LD从 \(D_i\) 向 \(D_j\) 遍历，保存中间步骤的子集（例如每3步或5步保存一个），形成新域 \(D^k_{ij}\)。这些样本保持原始标签不变（经验发现内容结构保持良好）。
  - **训练**：原始域样本加上所有生成的Langevin样本一起训练分割网络。
- **理论分析**：
  - 定理4.1：对于形式为 \(h(f_\theta(x)) - y f_\theta(x)\) 的损失函数，LangDAug的增强风险可展开为标准风险加上三个正则化项（\(R_1, R_2, R_3\)），分别与梯度、Hessian等有关，具有Hessian平滑和寻找平缓最小值的效果。
  - 对广义线性模型（GLM），正则化项简化为 \(R_{GLM} = \frac{\beta^2}{2n} \sum_i [A''(\theta^T x_i) \theta^T \theta - A'(\theta^T x_i) \theta^T s(x_i)]\)，其中 \(s(x_i)=\nabla \log p(x_i)\) 为Stein得分。
  - 定理4.3和推论4.4：LangDAug的Rademacher复杂度上界由数据流形的内在维度 \(\text{rank}(\Sigma_x)\) 决定，而非输入数据的全维度，这对高维医学图像特别有利。

## 3. 实验设计：数据集、基准、对比方法

- **数据集**：
  - **Retinal Fundus Segmentation (RFS)**：来自4个临床站点（域A、B、C、D），分割视杯（OC）和视盘（OD）。使用留一域协议评估。
  - **Prostate MRI Segmentation**：来自6个临床站点（域A–F），116个T2加权MRI扫描，处理为2D轴向切片。评估2D的Dice和3D体积的平均表面距离（ASD）。
- **基准协议**：在RFS上报告IoU和Dice（OC和OD分开），在Prostate上报告DSC和ASD。所有结果均为三次独立运行的平均值。
- **对比方法**：
  - DomainBed基准方法：Hutchinson、Fish、Fishr。
  - 医学图像分割专用DG方法：RandConv、MixStyle、FedDG、RAM、TriD。
  - 额外对比：CORAL、RSC、SagNet、SWAD。
  - 所有方法使用相同骨干网络ResNet34。

## 4. 资源与算力

- **文中明确告知**：实验在单张NVIDIA A6000 GPU（48GB内存）上进行。
- **训练时间**（Table 5）：ERM约1.51小时；LangDAug约3.14小时；TriD约5.53小时；TriD+Ours约7.49小时。EBM平均训练时间约0.357小时/每对域；Langevin链推理时间约2秒/链。
- **峰值内存**：LangDAug约19.41 GB，TriD+Ours约30.11 GB。
- **说明**：训练成本增加是生成合成样本的固有代价，未来可通过选择性采样和共享EBM架构优化。

## 5. 实验数量与充分性

- **主要实验**：
  - RFS上的4个域留一法测试（共4种目标域设置）。
  - Prostate MRI上的6个域留一法测试（共6种设置）。
  - 与域随机化方法结合：将LangDAug应用于FedDG、RAM、TriD，观察性能提升（共3×2=6组，两个数据集）。
- **消融实验**（附录C.1）：在RFS上对Langevin步数K（20,40,60,80）、步长β（0.1,1,10）、EBM复杂度（卷积块数1,4,7）、每链样本数（2,13,40）进行消融，每个超参数改变下比较mIoU和mDSC。
- **充分性评估**：实验覆盖两个数据集、多种先进基线、显式消融，且结果具有统计稳定性（三次运行均值）。公平性方面，所有方法使用相同骨干和训练设置。总体而言实验充分、客观、公平。

## 6. 论文的主要结论与发现

- 在RFS上，LangDAug在所有域平均mIoU（78.84%）和mDSC（87.61%）上均优于所有对比方法，且标准偏差最小（±2.43和±1.89），表明一致性强。
- 在Prostate MRI上，LangDAug在平均ASD（0.81 mm）和DSC（89.16%）上为最优，尤其在域D上DSC提升超过4%。
- LangDAug能够有效提升现有域随机化方法（FedDG、RAM、TriD）的性能，如TriD+Ours在RFS上mIoU提升3.05百分点、DSC提升2.21百分点；在Prostate上ASD降低0.14 mm、DSC提升2.90百分点。
- 理论分析揭示了LangDAug的正则化本质，且泛化界依赖于数据流形的内在维度，而非输入的全维度。

## 7. 优点：方法或实验设计上的亮点

- **理论严谨性**：给出了正则化效应的精确分解，并对GLM提供了Rademacher复杂度上界，连接数据流形内在维度与泛化能力。
- **方法简洁有效**：基于EBM和Langevin动力学，直接生成图像级增强样本，可即插即用于现有分割框架。
- **实验全面**：在两种不同模态（视网膜眼底图像和MRI）上验证，包含多个域和多种指标，且与SOTA方法公平对比。
- **兼容性**：LangDAug可自然地与域随机化方法结合，进一步提升性能，展示出通用性。
- **可视化验证**：t-SNE图显示Langevin样本填补了域间空隙；附录展示了域遍历过程的可视化，直观证明语义内容保持。

## 8. 不足与局限

- **计算开销**：训练时间显著增加（约ERM的2倍），且需存储大量中间样本（13×或5×数据量）。
- **EBM数量随域数平方增长**：对n个源域需训练\(\binom{n}{2}\)个EBM，当域数很多时（如>10）可能不可扩展。未来可通过共享架构和域条件缓解。
- **2D处理限制**：处理3D MRI时仅按切片处理，忽略了跨切片上下文。未来可探索直接训练3D EBM。
- **标签保持假设**：论文称Langevin样本内容结构不变，但未提供严格证明，仅在可视化中观察。对某些剧烈域偏移可能不保真。
- **超参数敏感性**：消融实验显示步数K、步长β、样本数等需要手工调节，未提供自适应策略。
- **实验覆盖**：仅评价了两种医学图像分割任务，未在自然图像或其他医学模态（如CT、超声）上验证，泛化性需进一步考察。
- **理论假设较强**：定理4.1要求损失函数和预测函数二阶可导，实际深度网络满足，但GLM假设简化了分析。

（完）
