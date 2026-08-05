---
title: "RPMIL: Rethinking Uncertainty-Aware Probabilistic Multiple Instance Learning for Whole Slide Pathology Diagnosis"
title_zh: RPMIL：重新思考面向全切片病理诊断的不确定性感知概率多实例学习
authors: "(PDF |   Details)"
date: 2025-08-01
pdf: "https://www.ijcai.org/proceedings/2025/0275.pdf"
tags: ["query:cellseg"]
score: 4.0
evidence: 概率MIL用于全切片病理诊断，属于数字病理分析范畴
tldr: 针对全切片图像诊断中的不确定性，提出概率多实例学习方法；引入不确定性感知机制，在WSI级别预测中增强可靠性；实验显示在病理诊断任务上提升了性能和可解释性。
source: IJCAI-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/ijcai-2025-accepted/ijcai-2025-275/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 888, \"height\": 659, \"label\": \"Figure\"}, {\"url\": \"assets/figures/ijcai-2025-accepted/ijcai-2025-275/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1809, \"height\": 721, \"label\": \"Figure\"}, {\"url\": \"assets/figures/ijcai-2025-accepted/ijcai-2025-275/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1763, \"height\": 481, \"label\": \"Figure\"}, {\"url\": \"assets/figures/ijcai-2025-accepted/ijcai-2025-275/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1748, \"height\": 486, \"label\": \"Figure\"}, {\"url\": \"assets/figures/ijcai-2025-accepted/ijcai-2025-275/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1770, \"height\": 444, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/ijcai-2025-accepted/ijcai-2025-275/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1827, \"height\": 715, \"label\": \"Table\"}, {\"url\": \"assets/tables/ijcai-2025-accepted/ijcai-2025-275/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 899, \"height\": 364, \"label\": \"Table\"}, {\"url\": \"assets/tables/ijcai-2025-accepted/ijcai-2025-275/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 891, \"height\": 439, \"label\": \"Table\"}, {\"url\": \"assets/tables/ijcai-2025-accepted/ijcai-2025-275/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 893, \"height\": 341, \"label\": \"Table\"}]"
motivation: 解决WSI诊断中MIL预测的不确定性问题。
method: 提出不确定性感知的概率多实例学习框架。
result: 在病理诊断任务上提升了预测可靠性和性能。
conclusion: 为WSI诊断提供了一种考虑不确定性的概率MIL方法。
---

## Abstract
No abstract is available.

---

## 论文详细总结（自动生成）

## 1. 论文的核心问题与整体含义

- **研究背景**：全切片图像（WSI）是千兆像素级的病理切片数字扫描，常用于癌症诊断。现有方法多遵循多实例学习（MIL）范式，将 WSI（包）划分为大量小块（实例），通过聚合实例特征得到固定的包特征（确定性嵌入）进行分类。
- **核心问题**：传统 MIL 方法是 **点估计（point estimation）**，每个包映射为一个确定性向量，难以捕捉数据的完整变异性，尤其在训练包数量有限时容易过拟合，导致分类器鲁棒性不足。
- **整体含义**：论文从不确定性估计的角度重新思考 MIL，提出 **不确定性感知的概率 MIL 方法（RPMIL）**，将包特征建模为概率分布而非固定值，并联合实例分布与包分布进行预测，以更好地描述数据多样性、提升诊断可靠性。

## 2. 方法论

- **核心思想**：将传统的确定性聚合器改为 **概率聚合器**，学习包特征的分布（均值 μ 和方差 σ²），并通过重参数化采样获得多个包特征表示；预测时不仅使用包分布，还结合实例特征的分布。
- **关键技术细节**：
  - **包分布构建**：利用变分自编码器（VAE）将所有实例特征压缩为低维潜在空间的两个向量（μ 和 σ），形成正态分布 \( P(z|x) = \mathcal{N}(\mu, \sigma^2) \)。
  - **采样与近似**：通过重参数化技巧对分布进行采样（采样数 K 可取 1, 10, 100, 1000），使用 MCMC 近似积分 \( \int_z P(z|x)P(y|z) dz \)。
  - **联合分布预测**：最终预测概率为 \( P(y|x) = \int_z P(z|x) \int_x P(y|x,z) P(x|z) dx dz \)，实现上引入交叉注意力模块，以采样的 z 作 Query，实例特征 x 作 Key/Value，融合后经池化送入分类器。
- **损失函数**：
  \[
  \mathcal{L} = \lambda_1 \text{CE}(y, \hat{y}) + \lambda_2 \text{KL}\big(P(z|x)\|Q(z)\big) + \lambda_3 \text{MSE}(\bar{z}, z')
  \]
  - CE：分类交叉熵；KL：使得包分布靠近标准正态先验，正则化特征空间；MSE：限制采样均值与点估计特征 \( z' \) 的差异，防止分布漂移。超参数 \( \lambda_1=1 \)，\( \lambda_2=\lambda_3=0.5 \)。

## 3. 实验设计

- **数据集**：
  - **Camelyon16**：乳腺癌淋巴结转移检测，官方分割：270 个 WSI 训练，129 个测试。肿瘤区域平均仅约 10%，正负样本不均衡。
  - **TCGA-NSCLC**：包含肺腺癌（LUAD）和肺鳞癌（LUSC）共 1053 个 WSI，按 6:1.5:2.5 划分训练/验证/测试，肿瘤区域平均约 80%，类别更均衡。
- **预处理**：在 20× 放大倍率下将 WSI 切割为 256×256 不重叠的补丁；用 ImageNet 预训练的 ResNet-50（1024 维）或病理图像预训练的 PLIP（512 维）提取实例特征。
- **对比方法**：Mean-pooling、Max-pooling、ABMIL、CLAM（SB/MB）、TransMIL、DGMIL、DTFD（MaxS/MaxMinS/AFS）、MMIL、DGR-MIL。评估指标为 ACC、F1-score、AUC，所有实验重复 5 次取均值±标准差。

## 4. 资源与算力

- **硬件**：1 块 NVIDIA GeForce RTX 3090。
- **训练设置**：优化器 Adam，初始学习率 1e-4，权重衰减 1e-5，采用余弦退火调整学习率。Batch size = 1，总训练轮数 100。论文未明确给出单次训练耗时。

## 5. 实验数量与充分性

- **主要对比实验**：在两个数据集上，与 10 余种主流 MIL 方法进行比较（表 1），涵盖两种特征提取器（ResNet-50 和 PLIP）。
- **消融/分析实验**：
  - 采样数量影响（1、10、100、1000）对 ACC/F1/AUC 的影响（图 3）；
  - 方差重要性验证：按方差大小删除部分测试样本观察性能变化（图 4）；
  - 损失函数消融（w/o MSE、w/o KL、w/o both）（表 3）；
  - 不同聚合器（均值、最大、注意力）与池化方式的组合效果（表 4）；
  - 点估计与不确定性估计的对比、仅用包分布与联合分布的性能对比（表 2）。
- **充分性评价**：实验设计较为全面，从主结果、消融到可视化均有覆盖，对比方法包含同期 SOTA，评估指标多样，统计分析（五折重复）增强了可靠性。

## 6. 主要结论与发现

- **不确定性估计优于点估计**：在相同的注意力聚合器下，基于包分布的预测大幅超越确定性嵌入方法。
- **联合分布显著提升性能**：同时利用实例分布和包分布（\( P(y|x,z) \)）比仅用包分布（\( P(y|z) \)）带来明显增益，这符合病理学家通过瘤区判断整张 WSI 的逻辑。
- **采样数量越多结果越好**：增加采样次数（至 1000）能更准确反映分布，提升并稳定模型性能。
- **方差可作为不确定性度量**：删除高方差样本后分类指标提升，证明方差与预测可靠性相关。

## 7. 优点

- **方法新颖**：首次在袋级 MIL 中引入显式的概率聚合器，将点估计转化为分布估计，为该领域提供新思路。
- **双重分布利用**：巧妙融合实例分布与包分布，通过交叉注意力实现信息交互，有效利用了 MIL 中被忽视的实例整体统计特性。
- **理论支撑与实现严谨**：推导了概率预测公式，并结合 VAE、重参数化、MCMC 等技术形成端到端框架；损失函数设计考虑了分布约束。
- **实验性能突出**：在两个公开数据集上达到 SOTA，且对不平衡的小肿瘤区域（Camelyon16）表现优越，鲁棒性强。
- **可视化可解释性**：注意力热图显示模型能规避污染区，关注真正病灶，更符合临床预期。

## 8. 不足与局限

- **计算成本增加**：采样过程（尤其是较大 K 值）会显著增加推理时间，论文未报告推理延迟或资源消耗对比，可能限制实时或大规模部署。
- **癌症类型有限**：仅在乳腺癌和肺癌两个数据集上验证，未涉及更多癌种或罕见病，普适性有待进一步检验。
- **采样稳定性**：小样本时样本均值可能偏离分布中心，影响性能，虽然大 K 值缓解了该问题，但本质上是一种近似。
- **依赖特征提取器**：方法基于预提取的固定特征，未对特征提取器进行联合优化，若特征本身噪声较大，分布建模可能受到影响。
- **超参数敏感**：λ2 和 λ3 均设 0.5，缺乏关于这些权重对性能影响的讨论，不同数据集可能需要调优。

（完）
