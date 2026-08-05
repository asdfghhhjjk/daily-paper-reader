---
title: "MUSE: Multi-Scale Dense Self-Distillation for Nucleus Detection and Classification"
title_zh: "MUSE: 面向细胞核检测与分类的多尺度稠密自蒸馏"
authors: "Zijiang Yang, Hanqing Chao, Bokai Zhao, Yelin Yang, Yunshuo Zhang, Dongmei Fu, Junping Zhang, Le Lu, Ke Yan, Dakai Jin, Minfeng Xu, Yun Bian, Hui Jiang"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/38170/42132"
tags: ["query:cellseg"]
score: 9.0
evidence: 提出自监督学习方法，用于组织病理图像中的细胞核检测与分类
tldr: 针对细胞核检测与分类任务中需要大量标注的问题，提出MUSE自监督学习框架，通过核心组件NuLo实现基于预测核位置的灵活局部自蒸馏，无需严格空间对齐，从而有效利用无标注数据学习判别性核表示，显著提升分类与检测性能。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38170/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 877, \"height\": 518}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38170/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 863, \"height\": 666}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38170/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 873, \"height\": 579}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38170/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1780, \"height\": 519}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38170/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 869, \"height\": 341}]"
tables_json: "[{\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38170/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1846, \"height\": 1133}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38170/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1846, \"height\": 1135}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38170/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 801, \"height\": 212}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38170/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 887, \"height\": 252}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38170/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1820, \"height\": 459}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38170/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 625, \"height\": 212}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38170/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 626, \"height\": 219}]"
motivation: 现有细胞核检测分类方法依赖大量像素级标注，无法充分利用大规模无标注数据。
method: 提出多尺度稠密自蒸馏方法，利用坐标引导的核局部自蒸馏机制学习细胞核表示。
result: 在多个组织病理数据集上，取得了领先的细胞核检测与分类精度。
conclusion: MUSE为细胞核分析提供了有效的自监督学习方案，降低了对人工标注的依赖。
---

## Abstract
Nucleus detection and classification (NDC) in histopathology analysis is a fundamental task that underpins a wide range of high-level pathology applications. However, existing methods heavily rely on labor-intensive nucleus-level annotations and struggle to fully exploit large-scale unlabeled data for learning discriminative nucleus representations. In this work, we propose MUSE (MUlti-scale denSE self-distillation), a novel self-supervised learning method tailored for NDC. At its core is NuLo (Nucleus-based Local self-distillation), a coordinate-guided mechanism that enables flexible local self-distillation based on predicted nucleus positions. By removing the need for strict spatial alignment between augmented views, NuLo allows critical cross-scale alignment, thus unlocking the capacity of models for fine-grained nucleus-level representation. To support MUSE, we design a simple yet effective encoder-decoder architecture and a large field-of-view semi-supervised fine-tuning strategy that together maximize the value of unlabeled pathology images. Extensive experiments on three widely used benchmarks demonstrate that MUSE effectively addresses the core challenges of histopathological NDC. The resulting models not only surpass state-of-the-art supervised baselines but also outperform generic pathology foundation models.

---

## 论文详细总结（自动生成）

## 1. 论文的核心问题与整体含义
- **研究背景**：组织病理图像中的细胞核检测与分类（Nucleus Detection and Classification, NDC）是疾病诊断、生物标志物评估、预后预测等下游任务的基础，准确识别依赖核形态与周围组织结构。
- **现有问题**：
  - 依赖昂贵的像素级核标注，标注区域小（约128μm），难以捕获组织结构的完整变异。
  - 自监督预训练方法（如DINOv2、iBOT等病理基础模型）偏重图像级表示，且需要增强视图之间严格的空间对齐，限制了多尺度/翻转等关键增强，不利于学习细粒度的核级特征。
  - 半监督方法假设标注与未标注数据同分布，难以利用大规模异质病理图像。
- **整体含义**：提出一种专为NDC设计的自监督学习框架MUSE，通过引入基于核坐标引导的局部自蒸馏（NuLo），在无需严格空间对齐的前提下实现跨尺度核表示学习，并配合大视野半监督微调，大幅提高无标注数据的利用效率，在多个数据集上超越现有监督方法和通用病理基础模型。

## 2. 论文提出的方法论
- **整体框架**：基于编码器-解码器的ViT架构，采用教师-学生自蒸馏范式，损失由图像级CLS token蒸馏和核级特征蒸馏共同组成。
- **核心机制——NuLo（核级局部自蒸馏）**：
  - 使用轻量级核检测器在未标注数据上自动获取核坐标，并分配全局唯一索引。
  - 基于MPP（微米/像素）的裁剪操作生成不同物理尺度的多视图图像对，保留核索引用于跨视图匹配。
  - 从解码器输出的稠密特征图中，通过双线性插值提取每个核的特征向量。
  - 对匹配的核对进行交叉熵自蒸馏损失（仅匹配区域参与），使学生网络学习跨尺度一致的核表示，解除了传统方法对空间对齐的依赖。
- **多尺度稠密自蒸馏**：
  - 图像级损失：教师/学生编码器的CLS token输出进行交叉熵损失。
  - 核级损失：教师/学生网络提取的匹配核特征计算交叉熵损失。总损失为两者加权和（权重均为1）。
  - 支持多尺度MPP裁剪（如在20x和40x放大倍率之间随机采样），生成全局视图（如224/512像素）和局部视图（96/208像素），实现跨尺度局部到全局的学习。
- **编码器-解码器架构**：
  - 编码器由ViT和重组合层组成，从ViT的多个等距层提取特征图，并将编码器输出的序列重排为2D特征图。
  - 解码器由残差块组成，逐步融合多级特征图，最终拼接形成统一的稠密特征图用于核插值；同时保留CLS token作为图像级表示。
- **预训练与微调策略**：
  - **预训练**：使用TCGA nu数据集（~48万ROI patch，自动生成核坐标），可选用大视野（LFoV）预训练（如512像素）以捕获更多组织上下文。
  - **下游微调**：将标注的小视野样本向外扩展（随机偏移）形成大视野样本，标注区域内进行标准回归和分类监督（MSE + 交叉熵），未标注区域通过高置信度伪标签进行一致性正则化，实现简易的半监督精细化训练。

## 3. 实验设计
- **数据集与场景**：
  - BRCA-M2C（乳腺癌，20x/40x），OCELOT（重叠细胞组织，20x/40x），PUMA（黑色素瘤，20x/40x）。
  - 核分类任务：给定真实核坐标预测核类型，使用KNN、线性探测和微调后的准确率（ACC）评估。
  - 核检测与分类任务：直接输出预测框与类别，采用F1分数（淋巴细胞、肿瘤细胞、其他细胞及平均）。
- **对比方法**：
  - 通用自监督预训练：DINO (ResNet-50/ViT-S/16/ViT-B/16)，MAE，iBOT，DINOv2。
  - 病理专用预训练：MoCoV2，DINO在TCGA上训练的ViT-S/16，以及病理基础模型CHIEF、CTransPath、CONCH、UNI、Prov-GigaPath。
  - 监督NDC方法：MCSpatNet，PointNu-Net，SMILE，SENC，CGT，CellViT，DPA-P2PNet。
- **实验协议**：所有方法在相同数据集上训练下游任务，公平比较。预训练数据量：MUSE仅使用约48万TCGA nu patch，远少于UNI（1亿）等大模型。

## 4. 资源与算力
- 论文未明确说明使用GPU型号、数量或训练时长等计算资源细节，作者仅在实现细节中指向补充材料（arXiv版），因此**本文未给出具体算力信息**。

## 5. 实验数量与充分性
- **实验组数**：
  - 三张大型表格比较核分类性能（KNN、线性探测、微调下的准确率），涵盖6个评价子集（三数据集 × 两倍率）。
  - 一张表格展示核检测与分类的F1对比。
  - 四组消融实验：解码器与多级上下文的影响（KNN/LIN/FT）、多尺度裁剪模式（固定倍率 vs 混合倍率）、预训练损失成分（有无图像级、核级损失）、大视野与一致性正则化对微调的影响。
- **充分性与公平性**：
  - 对比了通用预训练、病理预训练、任务专用模型的广泛基线，并统一评价协议。
  - 对多种架构（ResNet-50, ViT-S/16, ViT-B/16）均进行了实验，验证方法的通用性。
  - 消融研究拆解了每一关键组件的贡献，结论有充分支撑。
  - 总体实验量较大，设计合理，评价指标全面，较为客观公正。

## 6. 论文的主要结论与发现
- 提出的MUSE方法在三个公开NDC基准上一致超越现有监督方法和病理基础模型，且使用更少的参数量和预训练样本。
- NuLo机制有效解耦空间对齐限制，实现跨尺度核表示学习，大幅提升核分类性能（例如，ViT-B/16 LFoV-MUSE在FT准确率比CONCH高1.7%，比UNI高1.0%）。
- 编码器-解码器架构与多级特征融合、大视野预训练和半监督微调进一步放大性能，在核检测与分类任务上比现有最佳方法平均F1提升3.5~7.2点。
- 结论：面向密集预测的任务专用自监督预训练能极大弥补通用病理模型的不足，提供高效、可扩展的NDC解决方案。

## 7. 优点
- **创新性**：NuLo设计巧妙，利用核坐标插值实现跨视图的局部自蒸馏，从根本上避开了空间对齐约束，支持多尺度、翻转等关键增强。
- **任务针对性**：整个框架从模型结构、预训练损失到微调策略均为NDC任务量身定制，而非简单迁移通用SSL。
- **高效数据利用**：仅用约48万patch达到甚至超越需要在数百万/数十亿样本上预训练的大模型，数据效率极高。
- **简单有效的微调**：大视野半监督管道大幅提升性能，无需复杂图表构建或密度统计。
- **实验充分**：多数据集、多倍率、多评价指标、多类基线对比，加上细致的消融，结论可靠。

## 8. 不足与局限
- **算力透明度**：未提供GPU型号、训练时间等关键资源消耗信息，难以评估实际经济成本。
- **伪核坐标依赖**：NuLo依赖自动检测的核坐标，可能存在漏检、错检噪声，尤其对密集或重叠核场景的鲁棒性未做分析。
- **预训练组织代表性**：预训练数据仅来自TCGA（多为肿瘤组织），在非肿瘤或罕见组织类型上的泛化能力尚需验证。
- **伪标签阈值敏感**：微调阶段使用置信度阈值生成伪标签，其最佳阈值可能因数据集而异，论文未讨论该超参数影响。
- **仅方形区域扩展**：大视野扩展假定标注区为方形，处理任意形状ROI时的适应性未说明。
- **对比模型限制**：虽然对比了多个基础模型，但部分模型（如CONCH、UNI）在原始任务中可能使用了不同微调策略，性能潜力未必完全释放。

（完）
