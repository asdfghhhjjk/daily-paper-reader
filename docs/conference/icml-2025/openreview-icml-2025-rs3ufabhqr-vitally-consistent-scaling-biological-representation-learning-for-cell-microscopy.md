---
title: "ViTally Consistent: Scaling Biological Representation Learning for Cell Microscopy"
title_zh: ViTally一致：扩展细胞显微镜的生物学表示学习
authors: "Kian Kenyon-Dean, Zitong Jerry Wang, John Urbanik, Konstantin Donhauser, Jason Hartford, Saber Saberian, Nil Sahin, Ihab Bendidi, Safiye Celik, Juan Sebastián Rodríguez Vera, Marta Fay, Imran S Haque, Oren Kraus"
date: 2025-05-01
pdf: "https://openreview.net/pdf?id=rS3ufabhQr"
tags: ["query:pathology-ai"]
score: 8.0
evidence: 通过预训练基础模型进行细胞级显微镜图像分析
tldr: 细胞显微镜数据分析受限于随机和系统测量误差。本文提出一个三步预训练策略，包括构建自一致训练集、扩展模型规模、评估中间层表示。基于此，训练了迄今最大的19亿参数ViT细胞显微镜基础模型。该模型在下游任务中取得了最优性能，为细胞图像分析提供了强大的通用表示。
source: ICML-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-icml-2025-rs3ufabhqr/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 865, \"height\": 363, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-rs3ufabhqr/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 844, \"height\": 245, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-rs3ufabhqr/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 832, \"height\": 806, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-rs3ufabhqr/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1759, \"height\": 821, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-rs3ufabhqr/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1650, \"height\": 563, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-rs3ufabhqr/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 845, \"height\": 343, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-rs3ufabhqr/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 716, \"height\": 452, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-rs3ufabhqr/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 800, \"height\": 420, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-rs3ufabhqr/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 800, \"height\": 415, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-rs3ufabhqr/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 809, \"height\": 412, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-rs3ufabhqr/fig-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 801, \"height\": 405, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-rs3ufabhqr/fig-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 799, \"height\": 417, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-rs3ufabhqr/fig-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 797, \"height\": 415, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-rs3ufabhqr/fig-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 779, \"height\": 412, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-rs3ufabhqr/fig-015.webp\", \"caption\": \"\", \"page\": 0, \"index\": 15, \"width\": 784, \"height\": 417, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-icml-2025-rs3ufabhqr/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 867, \"height\": 965, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-rs3ufabhqr/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1465, \"height\": 281, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-rs3ufabhqr/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 864, \"height\": 451, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-rs3ufabhqr/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1242, \"height\": 602, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-rs3ufabhqr/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1453, \"height\": 454, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-rs3ufabhqr/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 788, \"height\": 194, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-rs3ufabhqr/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1780, \"height\": 1373, \"label\": \"Table\"}]"
motivation: 现有预训练方法无法有效消除测量误差对细胞显微镜表示学习的影响。
method: 提出包含数据筛选、模型扩缩和层评估的三阶段预训练框架，训练了19亿参数的ViT基础模型。
result: 模型在多种下游细胞分析任务中表现最优，并超越了此前所有显微镜表示学习模型。
conclusion: 该工作证明了大规模预训练可有效提取细胞显微镜图像的语义表示。
---

## Abstract
Deriving insights from experimentally generated datasets requires methods that can account for random and systematic measurement errors and remove them in order to accurately represent the underlying effects of the conditions being tested. Here we present a framework for pretraining on large-scale microscopy datasets that includes three steps: (1) curating a set of diverse and self-consistent training samples, (2) scaling training of an appropriate foundation model architecture on this dataset, (3) evaluating intermediate layers of the trained model to identify the best representation for downstream tasks. Using this strategy, we present the largest foundation model for cell microscopy data to our knowledge, a new 1.9 billion-parameter ViT-G/8 MAE trained on over 8 billion microscopy image crops. Compared to a previous published ViT-L/8 MAE, our new model achieves a 60\% improvement in linear separability of genetic perturbations and obtains the best overall performance on whole-genome relationship recall, batch correction replicate consistency, and compound-gene activity prediction benchmarks.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义（研究动机和背景）

- **核心问题**：细胞显微镜图像分析面临随机和系统测量误差，需要有效方法去除噪声并提取反映生物学效应的表征。现有自监督方法（如MAE）虽有效，但数据瓶颈限制缩放。如何更高效利用实验数据、进一步提升表示质量是关键。
- **整体含义**：本文提出一套系统框架，通过数据筛选、模型缩放、中间层选择三步策略，训练了迄今最大的细胞显微镜基础模型（1.9B参数ViT-G/8 MAE），在多种生物基准上显著优于先前最优模型，证明缩放定律在显微图像数据上的有效性。

### 2. 论文提出的方法论：核心思想、关键技术细节

- **核心思想**：三步策略：
  1. **数据筛选（Curated data）**：利用已有较强模型（MAE-L/8、WSL）评估扰动的表现一致性（非参数置换检验），仅保留诱导稳定形态变化的扰动，构建多样性更高、类别更平衡的数据集 **Phenoprints-16M**（从93M图像降至16M）。
  2. **模型缩放（Model scaling）**：基于Phenoprints-16M训练大规模MAE模型。采用ViT-Gigantic架构（1.9B参数，patch size 8×8），使用L2 + Fourier域重建损失，训练500 epochs。
  3. **块搜索（Block search）**：对ViT的每个Transformer block训练线性探针（logistic regression），预测基因ID或功能组，选择验证集上平衡准确率最高的中间block（\(b^*\)）作为特征提取层，替代默认的最后层。
- **关键技术细节**：
  - 数据筛选的扰动一致性检验：计算同扰动多重复的余弦相似度均值，与随机扰动对的null分布比较（permutation test），p值<0.01的扰动入选。
  - 训练MAE-G/8的掩码比例75%，Lion优化器，学习率3e-5，全局batch size 8192，stochastic depth 0.6。
  - 推理时采用TVN（Typical Variation Normalization）和染色体臂偏差校正进行后处理，再平均到基因级嵌入。
  - 代理任务（线性探针）与全基因组基准的Spearman秩相关≥0.91，说明可用廉价探针快速选择最优层。

### 3. 实验设计：数据集、基准、对比方法

- **数据集**：
  - **训练数据**：Phenoprints-16M（筛选自93M原始图像），RxRx3全基因组CRISPR筛选，6通道Cell Painting + 明场。
  - **线性探针数据集**：RxRx1（1138种siRNA + 对照，4种细胞系）；Anax（自建40类功能组，348个基因，包含多种通路/复合体）。
  - **全基因组评估数据集**：RxRx3（HUVEC细胞，17,063个基因×6 sgRNA）。
  - **外部验证**：JUMP-CP（独立实验室公开数据），RxRx3-core（公开基准，735基因+1674化合物）。
- **基准任务**：
  - 线性分离能力（平衡准确率）：RxRx1 siRNA分类、Anax功能组分类。
  - 生物学关系召回（Recall % at 0.05-0.95余弦阈值）在CORUM、hu.MAP、Reactome、StringDB上。
  - 技术复制一致性（KS统计量、Cramer-von Mises统计量）。
  - 化合物-基因活性预测（平均精度AP，z-score over random）。
- **对比方法**：
  - 基线ViT：未训练的ViT-S/16、DINOv2 ViT-S/L/G（自然图像）、ImageNet-21k MAE ViT-L/16。
  - 显微MAE：CA-MAE-S/16（RxRx3）、MAE-L/8（RPI-93M，之前SOTA）、MAE-L/8（Phenoprints-16M）、MAE-G/8（Phenoprints-16M）。
  - 手工特征：CellProfiler。
  - 消融：使用最后层 vs 最优中间层；使用RPI-93M vs Phenoprints-16M；不同模型规模。

### 4. 资源与算力

- **MAE-G/8**：256块H100 GPU，训练时长>1周，总计 **48,000 GPU-hours**。
- **MAE-L/8 (Phenoprints-16M)**：128块H100 GPU，15,360 GPU-hours。
- **CA-MAE-S/16**：16块A100 GPU，400 GPU-hours。
- **全基因组推理**（评估MAE-G/8的最后块）需约4,000 L4 GPU-hours。

### 5. 实验数量与充分性

- **实验数量**：覆盖**6个数据场景**（RxRx1, Anax, RxRx3全基因组, JUMP-CP, RxRx3-core, ARPE19/HUVEC+TNFα）、**8个骨干模型**（含变体）、**3个消融维度**（数据-模型-层）、**10项以上基准指标**（含多数据库关系召回、统计检验）。
- **充分性**：实验设计系统，从代理探针到全基因组验证；在多个独立数据集（内部RxRx系列+外部JUMP-CP）上验证；结果附标准差和z-score统计显著性（z=5.21提升）；消融实验清晰区分了数据筛选、模型缩放、层选择的贡献。对比自然图像预训练模型时公平（统一后处理、统一线性探针设置）。
- **客观性**：公开代码和部分模型权重（CA-MAE-S/16）；RxRx3-core为公开基准；线性探针性能与全基因组指标高度相关，降低了评估偏差风险。

### 6. 论文的主要结论与发现

1. **数据筛选显著提升效率**：Phenoprints-16M（仅16M图像）训练的MAE-L/8在相同模型下整体上优于93M数据集（RPI-93M）训练的SOTA模型。
2. **中间层比最后层更优**：对所有ViT（包括自然图像预训练），中间block的特征线性分离性更强，全基因组基准也更好（如MAE-G/8第38块优于48块）。线性探针可作为廉价代理来搜索最优层。
3. **缩放规律持续存在**：更大模型（1.9B参数）在更大训练计算下持续提升，MAE-G/8在所有任务上取得最佳（关系召回提升60%线性分离度、21% KS、48% CM）。
4. **跨域泛化能力**：在完全不同的JUMP-CP数据集上也保持趋势，MAE-G/8 trimmed优于CellProfiler和先前MAE。
5. **模式可迁移**：建议的“筛选-缩放-层选择”流程适用于其他实验数据丰富的领域。

### 7. 优点

- **方法创新性**：将数据一致性筛选（基于已有模型）引入显微镜预训练，而非简单随机采样或传统de-duplication。
- **层选择策略实用且高效**：通过廉价线性探针即可确定最优层，节省推理成本（MAE-G/8评估全基因组需4000 GPU-hours，探针仅需少量数据）。
- **大规模验证**：在1.9B参数级别验证了自监督学习的缩放律，并提供最直接的证据（FLOPS与性能几乎线性相关）。
- **开源与可复现**：公开推理、可视化和基准代码，以及小型模型权重，便于社区验证和扩展。
- **实验覆盖全面**：从代理任务到大规模全基因组评估再到外部数据集，形成闭环。

### 8. 不足与局限

- **DINO训练失败**：无法有效训练DINOv2在显微镜数据上（过拟合），未找到合适配方，因此仅探索了MAE一种SSL方法。
- **潜在偏差**：Phenoprints-16M的筛选依赖于MAE-L/8和WSL模型，可能引入模型偏好，遗漏弱但真实表型；迭代筛选虽建议但未验证。
- **计算资源要求高**：训练MAE-G/8需48K H100-hours，全基因组推理也耗费巨大，限制了可复现性。
- **细胞类型单一**：全基因组评估主要聚焦HUVEC细胞，结论向其他细胞系的泛化性未充分验证。
- **未进行微调**：所有下游评测均基于线性探针，未测试模型微调后的迁移能力。
- **对比基线有限**：未与近期其他自监督方法（如iBOT、MAE+对比学习变体）比较，也未与专为显微镜设计的U-Net风格模型比较。
- **损失函数细节不清**：Fourier损失实现与论文描述略有出入，可能影响结果重现。

（完）
