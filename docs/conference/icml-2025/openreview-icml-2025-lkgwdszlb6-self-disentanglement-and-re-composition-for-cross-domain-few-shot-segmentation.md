---
title: Self-Disentanglement and Re-Composition for Cross-Domain Few-Shot Segmentation
title_zh: 自解缠与重组：跨域少样本分割
authors: "Jintao Tong, Yixiong Zou, Guangyao Chen, Yuhua Li, Ruixuan Li"
date: 2025-05-01
pdf: "https://openreview.net/pdf?id=LkgwdSzlb6"
tags: ["query:cellseg"]
score: 4.0
evidence: 可迁移至细胞实例分割的少样本分割方法
tldr: 针对跨域少样本分割中的特征纠缠问题，提出基于ViT结构分解的自解缠与重组方法，解绑源域特征模式以提升迁移性。在多个跨域分割任务上验证了有效性，为少样本细胞分割提供了可借鉴的通用方法。
source: ICML-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-icml-2025-lkgwdszlb6/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 857, \"height\": 525, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-lkgwdszlb6/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 850, \"height\": 293, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-lkgwdszlb6/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 865, \"height\": 363, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-lkgwdszlb6/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 865, \"height\": 293, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-lkgwdszlb6/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1674, \"height\": 870, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-lkgwdszlb6/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 783, \"height\": 559, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-lkgwdszlb6/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 864, \"height\": 501, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-lkgwdszlb6/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 853, \"height\": 387, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-lkgwdszlb6/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 862, \"height\": 536, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-lkgwdszlb6/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 772, \"height\": 548, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-lkgwdszlb6/fig-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1767, \"height\": 885, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-lkgwdszlb6/fig-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1759, \"height\": 918, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-icml-2025-lkgwdszlb6/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 847, \"height\": 232, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-lkgwdszlb6/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1770, \"height\": 652, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-lkgwdszlb6/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1771, \"height\": 309, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-lkgwdszlb6/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 854, \"height\": 292, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-lkgwdszlb6/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 837, \"height\": 216, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-lkgwdszlb6/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 850, \"height\": 290, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-lkgwdszlb6/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 787, \"height\": 155, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-lkgwdszlb6/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 857, \"height\": 164, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-lkgwdszlb6/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 857, \"height\": 134, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-lkgwdszlb6/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 859, \"height\": 149, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-lkgwdszlb6/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 691, \"height\": 135, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-lkgwdszlb6/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 859, \"height\": 284, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-lkgwdszlb6/table-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 856, \"height\": 301, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-lkgwdszlb6/table-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 856, \"height\": 229, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-lkgwdszlb6/table-015.webp\", \"caption\": \"\", \"page\": 0, \"index\": 15, \"width\": 857, \"height\": 171, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-lkgwdszlb6/table-016.webp\", \"caption\": \"\", \"page\": 0, \"index\": 16, \"width\": 857, \"height\": 134, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-lkgwdszlb6/table-017.webp\", \"caption\": \"\", \"page\": 0, \"index\": 17, \"width\": 859, \"height\": 193, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-lkgwdszlb6/table-018.webp\", \"caption\": \"\", \"page\": 0, \"index\": 18, \"width\": 770, \"height\": 178, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-lkgwdszlb6/table-019.webp\", \"caption\": \"\", \"page\": 0, \"index\": 19, \"width\": 407, \"height\": 154, \"label\": \"Table\"}]"
motivation: 现有跨域少样本分割方法存在特征纠缠问题，限制了模型向目标域的迁移能力。
method: 利用ViT的自然分解，通过自解缠与重组模块分离并重组特征，改善跨域迁移性。
result: 在多个跨域分割基准上取得了最优性能，验证了方法的有效性。
conclusion: 自解缠与重组策略能有效提升少样本分割模型的跨域泛化能力。
---

## Abstract
Cross-Domain Few-Shot Segmentation (CD-FSS) aims to transfer knowledge from a large-scale source-domain dataset to unseen target-domain datasets with limited annotated samples. Current methods typically compare the distance between training and testing samples for mask prediction. However, a problem of feature entanglement exists in this well-adopted method, which binds multiple patterns together and harms the transferability. However, we find an entanglement problem exists in this widely adopted method, which tends to bind source-domain patterns together and make each of them hard to transfer. In this paper, we aim to address this problem for the CD-FSS task. We first find a natural decomposition of the ViT structure, based on which we delve into the entanglement problem for an interpretation. We find the decomposed ViT components are crossly compared between images in distance calculation, where the rational comparisons are entangled with those meaningless ones by their equal importance, leading to the entanglement problem. Based on this interpretation, we further propose to address the entanglement problem by learning to weigh for all comparisons of ViT components, which learn disentangled features and re-compose them for the CD-FSS task, benefiting both the generalization and finetuning. 		Experiments show that our model outperforms the state-of-the-art CD-FSS method by 1.92% and 1.88% in average accuracy under 1-shot and 5-shot settings, respectively.

---

## 论文详细总结（自动生成）

# 论文总结：Self-Disentanglement and Re-Composition for Cross-Domain Few-Shot Segmentation

## 1. 核心问题与整体含义（研究动机和背景）

- **任务定义**：跨域少样本分割（CD-FSS）旨在将源域（如PASCAL VOC）中学习到的知识迁移到拥有极少量标注样本的未见目标域（如医疗影像、卫星图像等），且源域与目标域的数据分布和类别空间均不重叠。
- **现有方法瓶颈**：主流方法通过比较查询图像与支持图像在编码器输出特征上的距离（如余弦相似度）来预测分割掩码。然而，本文发现这种全局特征比较存在严重的**特征纠缠问题**——源域中的多种模式（如翅膀、身体）被捆绑在一起，导致单个模式难以独立迁移。例如，模型可能仅在翅膀和身体同时出现时才能检测到翅膀，当目标域中翅膀形状改变时则失效。
- **核心贡献**：首次从ViT结构的自然分解角度分析特征纠缠问题，并提出**自解缠（Self-Disentanglement）与重组（Re-Composition）** 的方法，通过为ViT各组件之间的比较赋予可学习权重来解绑并重组特征，从而提升跨域迁移能力。

## 2. 方法论：核心思想、关键技术细节

### 核心思想
- **基于ViT结构分解**：ViT的残差连接和一致的空间尺寸使得每一层（MSA/MLP）的输出位于同一特征空间。因此，ViT的最终输出可视为所有层输出（L层）的累加和：  
  `ViT(I) = Z0 + Σ_{l=1}^L MSA_l(Z_{l-1}) + Σ_{l=1}^L MLP_l(Ẑ_l) ≈ Z0 + Σ_{l=1}^L Layer_l`。
- **纠缠问题的根源**：在相似度计算中，每一层输出都被用来与所有其他层输出进行交叉比较，且所有比较被赋予同等权重。这导致有意义的比较（如翅膀与翅膀）与无意义的比较（如翅膀与身体）被纠缠在一起，造成特征过度拟合源域。
- **解决方案**：通过**学习比较权重**来区分有意义和无意义的交叉比较，实现特征的自解缠与重组。

### 关键技术细节

1. **正交空间解耦模块（OSD）**
   - 将来自L个ViT层的支持/查询特征沿通道维度拼接 → 通过一个全连接层`W_in`降维至低秩空间（r=8） → 经过一个卷积层`W_orth`施加正交约束 → 再通过全连接层`W_out`映射回原始空间并分裂为各层特征。
   - 正交正则化损失：`L_orth = ||F_orth F_orth^T - I||_F^2`，强制各层特征通道间低相关，促进语义解缠。
   - 源域训练时OSD与编码器联合训练；目标域微调时仅更新`W_orth`（轻量）。

2. **跨模式比较模块（CPC）**
   - 从OSD输出的解缠特征中，对支持特征通过掩膜平均池化得到L组前景/背景原型（`P_fg`, `P_bg`）。
   - 将L组查询特征与L组原型进行**交叉比较**，生成L×L×2×n×n的得分图（2代表前景/背景）。
   - 距离度量默认使用余弦相似度，也可替换为欧氏距离、点积、EMD等（实验表明方法通用）。

3. **自适应融合权重（AFW）**
   - **源域训练**：使用平均权重对L×L个得分图进行简单平均（避免小参数过拟合源域）。
   - **目标域微调**：引入一个小型参数矩阵`W_AFW`（形状L²×2，仅288个参数），对每个得分图按前景/背景动态加权融合。
   - 微调时不使用查询数据，而是将支持图像自身作为查询计算BCE损失和正交损失，实现无查询自适应。

4. **损失函数**：`L = L_BCE + λ L_orth`（λ=0.1）。

## 3. 实验设计

### 数据集与基准
- **源域**：PASCAL VOC 2012 + SBD增强（训练集）。
- **目标域**（4个跨域场景）：
  - **FSS-1000**：自然图像，1000类，240类测试。
  - **DeepGlobe**：卫星遥感图像，7类。
  - **ISIC2018**：皮肤镜病变图像。
  - **Chest X-ray**：胸部X光片（结核筛查）。
- **基准设定**：遵循PATNet [Lei et al., 2022] 的CD-FSS标准benchmark，采用1-way 1-shot和1-way 5-shot设置。

### 对比方法
- 基于ResNet-50的方法：PANet, RPMMs, PFENet, RePRI, HSNet, PATNet, APM, ABCDFSS, DRA。
- 基于ViT的方法：PATNet (ViT), PerSAM, APSeg, IFA（特殊批处理设置）。
- 传统解缠方法：InfoGAN, Disentangled-VAE, DFR。
- 特征融合方法：FPN, MEP3P, MMFuser。
- 槽注意力方法：Slot-Attention, DINOSAUR。
- 额外还验证了Swin Transformer上的有效性。

### 主要结果
- **SDRC（本文方法）** 在1-shot和5-shot平均mIoU上分别达到**63.22%**和**67.30%**，超越所有对比方法（包括SOTA APSeg的61.30%/65.09%）。
- 在四个目标域上均取得最优或次优结果，尤其在差距最大的Chest X-ray上提升显著（1-shot 82.86% vs. APSeg 84.10% 接近，平均更高）。

## 4. 资源与算力

- **未明确说明**：文中未提及使用的GPU型号、数量、训练时长。仅提到计算在“华中科技大学高性能计算平台”完成。但从方法轻量性推断，由于仅需ViT-B编码器+少量额外参数（OSD约12.4K，AFW 0.288K），训练和微调开销应远低于基于SAM的APSeg等方法。

## 5. 实验数量与充分性

- **实验数量丰富**：
  - 主实验：4个目标域 × 2种设定（1-shot/5-shot）= 8组对比，与15+种方法比较。
  - 消融实验：逐步验证CPC、AFW、OSD的贡献（表3）。
  - 距离度量实验：余弦、欧氏、点积、EMD共4种（表4）。
  - 交叉比较 vs. 逐层比较（表5）。
  - 超参数分析：正交损失权重（表9）、OSD秩r（表6）。
  - 多背景原型影响（表10）。
  - 计算效率：FLOPs对比（表11）。
  - 额外实验：Swin Transformer（表17）、特殊批处理设置IFA（表15）、域泛化/标准FSS（表18/19）、与解缠/融合/槽注意力方法比较（附录表12-14）。
- **充分性与客观性**：
  - 覆盖了不同域差距（自然→医疗、遥感）和多种骨干（ResNet、ViT、Swin）。
  - 控制基线一致（相同ViT-B编码器），消融设计清晰。
  - 统计上报告了多次实验的平均值（未提及标准差，但符合常见做法）。
  - 公平性：对比方法均取自原论文或公开结果，并注明代码未提供时的复现方式。

## 6. 主要结论与发现

- 特征纠缠是CD-FSS中阻碍跨域迁移的关键障碍，其根源是ViT各层输出之间的无意义交叉比较被赋予同等权重。
- 通过**解缠（利用ViT自然分解+正交约束）** 和**重组（可学习交叉比较权重+自适应融合）**，可以显著提升模型的泛化能力和目标域适配效率。
- 方法轻量高效（额外参数<13K），无需复杂分支网络，在4个完全不同域的目标集上均达到SOTA。
- 理论分析（第6节）从泛化误差上界角度解释了AFW和OSD如何降低源域风险与域散度。

## 7. 优点

- **新颖视角**：首次从ViT内部结构分解角度分析并解决特征纠缠，启发性强。
- **模型轻量**：仅需少量额外参数（OSD约12K、AFW 0.288K），计算开销低（FLOPs 18.86G，低于PATNet 22.63G）。
- **无需额外网络**：利用ViT固有层间特征空间一致性，避免了GAN/VAE等复杂生成式解缠方法。
- **通用性强**：适用于多种距离度量、多种骨干（ViT、Swin），并可在标准FSS和域泛化任务上受益。
- **理论支撑**：给出了泛化误差上界的理论分析，解释了方法为什么有效。
- **实验充分**：在多个专业领域（自然、卫星、皮肤镜、X光）验证，消融实验细致。

## 8. 不足与局限

- **实验覆盖有限**：仅测试了4个目标域，且均为二维图像。对于视频、点云等模态未涉及。细胞/病理图像等医学领域未直接包含（但方法理论上可迁移）。
- **未报告方差**：所有实验均为单次或平均结果，未给出标准差，不利于评估稳定性。
- **骨干依赖**：核心思路基于ViT的残差结构和一致特征空间，对无残差连接或不同架构（如纯CNN）需要额外适配（文中对Swin需上采样+映射层）。
- **微调策略限制**：目标域微调时仅使用支持图像进行自监督（支持当查询），可能无法完全利用目标域数据分布信息。
- **超参数敏感度分析不足**：仅评估了正交损失权重和秩r，但对其他设计（如层数L、原型数量）未深入探讨。
- **理论分析较初步**：第6节的理论推导较为简化（如忽略间接效应），缺乏严格的收敛性证明。
- **可复现性**：代码未公开（论文为ICML 2025收录，可能后续会开源，但当前无法验证）。

（完）
