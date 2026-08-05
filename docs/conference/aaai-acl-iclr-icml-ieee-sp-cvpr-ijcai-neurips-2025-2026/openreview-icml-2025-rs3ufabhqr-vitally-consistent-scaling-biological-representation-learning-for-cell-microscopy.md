---
title: "ViTally Consistent: Scaling Biological Representation Learning for Cell Microscopy"
title_zh: "ViTally Consistent: 面向细胞显微镜的大规模生物表示学习"
authors: "Kian Kenyon-Dean, Zitong Jerry Wang, John Urbanik, Konstantin Donhauser, Jason Hartford, Saber Saberian, Nil Sahin, Ihab Bendidi, Safiye Celik, Juan Sebastián Rodríguez Vera, Marta Fay, Imran S Haque, Oren Kraus"
date: 2025-05-01
pdf: "https://openreview.net/pdf?id=rS3ufabhQr"
tags: ["query:profile"]
score: 6.0
evidence: 在大规模细胞显微镜数据集上预训练视觉Transformer，为下游细胞分析提供表示
tldr: 针对细胞显微镜实验中测量误差问题，提出一个包含数据筛选、大规模预训练和层选择的三步框架，训练出19亿参数视觉Transformer基础模型，为细胞图像分析提供抗干扰的通用表示，可提升多种下游任务性能。
source: ICML-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-icml-2025-rs3ufabhqr/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 865, \"height\": 363}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-rs3ufabhqr/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 844, \"height\": 245}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-rs3ufabhqr/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 832, \"height\": 806}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-rs3ufabhqr/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1759, \"height\": 821}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-rs3ufabhqr/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1650, \"height\": 563}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-rs3ufabhqr/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 845, \"height\": 343}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-rs3ufabhqr/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 716, \"height\": 452}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-rs3ufabhqr/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 800, \"height\": 420}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-rs3ufabhqr/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 800, \"height\": 415}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-rs3ufabhqr/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 809, \"height\": 412}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-rs3ufabhqr/fig-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 801, \"height\": 405}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-rs3ufabhqr/fig-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 799, \"height\": 417}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-rs3ufabhqr/fig-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 797, \"height\": 415}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-rs3ufabhqr/fig-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 779, \"height\": 412}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-rs3ufabhqr/fig-015.webp\", \"caption\": \"\", \"page\": 0, \"index\": 15, \"width\": 784, \"height\": 417}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-icml-2025-rs3ufabhqr/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 867, \"height\": 965}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-rs3ufabhqr/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1465, \"height\": 281}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-rs3ufabhqr/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 864, \"height\": 451}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-rs3ufabhqr/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1242, \"height\": 602}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-rs3ufabhqr/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1453, \"height\": 454}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-rs3ufabhqr/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 788, \"height\": 194}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-rs3ufabhqr/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1780, \"height\": 1373}]"
motivation: 细胞显微镜数据常受随机和系统误差影响，阻碍下游分析。
method: 通过数据筛选、规模化预训练和中间层评估，训练出大规模视觉Transformer基础模型。
result: 获得目前规模最大的细胞显微镜基础模型，可实现稳健表征。
conclusion: 大规模预训练为细胞图像分析提供了更准确的表示，有潜力推动多种生物学应用。
---

## Abstract
Deriving insights from experimentally generated datasets requires methods that can account for random and systematic measurement errors and remove them in order to accurately represent the underlying effects of the conditions being tested. Here we present a framework for pretraining on large-scale microscopy datasets that includes three steps: (1) curating a set of diverse and self-consistent training samples, (2) scaling training of an appropriate foundation model architecture on this dataset, (3) evaluating intermediate layers of the trained model to identify the best representation for downstream tasks. Using this strategy, we present the largest foundation model for cell microscopy data to our knowledge, a new 1.9 billion-parameter ViT-G/8 MAE trained on over 8 billion microscopy image crops. Compared to a previous published ViT-L/8 MAE, our new model achieves a 60\% improvement in linear separability of genetic perturbations and obtains the best overall performance on whole-genome relationship recall, batch correction replicate consistency, and compound-gene activity prediction benchmarks.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义
- **研究动机**：细胞显微镜实验普遍存在随机误差和系统误差（如批次效应、技术偏差），这些噪声会掩盖真实的生物学效应，严重影响下游分析（如基因功能鉴定、药物活性评估）的准确性。
- **核心目标**：通过大规模预训练构建一个对测量误差具有鲁棒性的通用细胞图像基础模型，使其能够提供“抗干扰”的生物表示，从而提升多种下游任务的性能。
- **整体含义**：该工作表明，在巨型、精心筛选的数据集上扩展视觉Transformer（ViT）的规模，并结合合理的层选择策略，可以为细胞显微分析带来质的飞跃，推动基础模型在生命科学中的应用。

### 2. 论文提出的方法论
- **整体框架**：一个三步流程，统一解决数据、模型与表示选择问题。
  - **第一步：数据筛选（Curation）**
    - 从大量显微图像中筛选出“多样化且自洽”的训练样本，目的可能包括剔除技术离群值、平衡不同实验条件、保证重复之间的内在一致性。
  - **第二步：规模化预训练（Scaling Training）**
    - 采用掩码自编码器（Masked Autoencoder, MAE）作为自监督学习目标。
    - 架构为ViT-G/8（Vision Transformer, Giant规模, patch size=8），参数量高达**19亿**。
    - 训练数据量：超过**80亿**张显微图像裁剪块（crops）。
  - **第三步：中间层评估与层选择（Intermediate Layer Evaluation）**
    - 并非直接使用最后一层输出，而是系统地评估不同中间层生成的特征在下游任务上的表现，选出最优表示层。这一策略有助于保留更通用的信号，避免高层特征过度拟合预训练任务。
- **关键设计**：通过规模扩展（模型+数据）和层选择来隐式地实现去噪与鲁棒表示学习。

### 3. 实验设计
- **主要数据集与场景**：大规模显微镜图像集合（具体名称未在摘要中指明），涵盖多种细胞类型、扰动条件（遗传扰动、化合物处理等）。
- **Baselines 与对比方法**：
  - 与先前已发表的 ViT-L/8 MAE（较小规模基础模型）进行头对头比较。
- **评测基准（Benchmarks）**：
  - 遗传扰动线性可分性（Linear separability of genetic perturbations）
  - 全基因组关系召回（Whole-genome relationship recall）
  - 批次校正重复一致性（Batch correction replicate consistency）
  - 化合物-基因活性预测（Compound-gene activity prediction）

### 4. 资源与算力
- **论文中未明确说明**具体的 GPU 型号、数量及训练时长。鉴于训练的是 19 亿参数 ViT-G/8，且处理超过 80 亿张图像块，所需算力必然极为庞大（通常需数百至数千张高端 GPU 训练数周）。然而，摘要与提供的元数据中均未披露这些细节，读者无法从中估算资源消耗。

### 5. 实验数量与充分性
- **实验覆盖范围**：
  - 至少覆盖了四类具有代表性的下游任务基准，跨越遗传功能表征、批次效应校正、药物活性预测等多个维度。
  - 包含与先前的 ViT-L/8 MAE 模型的直接比较。
  - 框架内含中间层评估，说明可能进行了层选择消融实验（尽管未列出具体消融项）。
- **充分性与公平性**：
  - 从任务多样性看，实验设计较为全面，能够验证模型的通用鲁棒性。
  - 对比对象明确，但仅与一种早期架构比较，缺少与其他同期大规模细胞显微镜模型（如 CellViT、Cytotype 等）的横向对比。
  - 摘要未提供统计检验或误差条信息，无法判断结果稳定性和显著性。
  - 整体上，实验方向合理，但因论文完整内容缺失，无法确认内部消融和解剖实验是否充分。

### 6. 论文的主要结论与发现
- 成功训练出截至目前**规模最大的细胞显微镜基础模型**——1.9B 参数的 ViT-G/8 MAE。
- 新模型相较先前的 ViT-L/8 MAE，在遗传扰动线性可分性上获得 **60% 的相对提升**。
- 在全部四项核心基准（基因组关系召回、批次一致性、化合物-基因预测等）上均取得**综合最优性能**。
- 验证了“数据筛选 + 极大模型 + 中间层选择”这一框架能有效克服显微实验中的测量误差，为下游分析提供更准确的表示。

### 7. 优点
- **规模突破**：首次将细胞显微模型参数扩展至近 20 亿，数据量推至 80 亿图块，展现了规模带来的显著增益。
- **实用框架**：提出的三步流程（数据清洗、大规模预训练、层选择）清晰可操作，对领域有方法论指导意义。
- **抗噪能力**：显式针对测量误差问题设计，并通过基准（如批次校正一致性）证明了鲁棒性的提升。
- **任务广泛性**：评测覆盖多样化的生物学问题，增强了结论的泛化可信度。
- **中间层利用**：评估中间层而非只用最后一层，是简单有效且常被忽略的表示选择技巧，被实验证实有其价值。

### 8. 不足与局限
- **信息缺失严重**：由于仅获取摘要，无法得知数据组成、训练细节、消融实验、失败案例分析等关键内容，极大限制了对结论可靠性的判断。
- **基线单一**：仅与 ViT-L/8 MAE 对比，未与更近期的细胞基础模型（如 scGPT 的图像版本、 Cell-Transformer 等）或监督学习方法相比，无法声称全面领先。
- **可复现性与资源门槛**：未公布算力需求、模型检查点或训练代码（可能涉及数据隐私），其他人难以复现或适配。
- **应用限制**：尽管在基准上表现优异，但缺乏真实世界生物学发现的验证（如基因功能预测命中率、药物筛选湿实验验证），其“实用性”尚止于数值指标。
- **误差去除非完全透明**：论文框架对“自洽样本”的筛选标准未在摘要中阐明，可能引入数据偏差，影响模型公平性。
- **解读泛化性**：在以单细胞显微镜为对象的研究中，扩展到其他成像模态（如组织病理）的有效性未知。

（完）
