---
title: "MUSE: Multi-Scale Dense Self-Distillation for Nucleus Detection and Classification"
title_zh: MUSE：用于细胞核检测与分类的多尺度稠密自蒸馏
authors: "Zijiang Yang, Hanqing Chao, Bokai Zhao, Yelin Yang, Yunshuo Zhang, Dongmei Fu, Junping Zhang, Le Lu, Ke Yan, Dakai Jin, Minfeng Xu, Yun Bian, Hui Jiang"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/38170/42132"
tags: ["query:cellseg"]
score: 10.0
evidence: 自监督方法同时完成细胞核检测与分类，直接解决实例分割与细胞类型分类联合建模的问题。
tldr: MUSE针对细胞核检测与分类任务中标注昂贵、无法充分利用无标注数据的问题，提出一种多尺度稠密自蒸馏的自监督学习方法。其核心NuLo模块基于预测的核位置进行局部自蒸馏，无需增强视图间的严格空间对齐，从而让模型可以灵活使用大量无标注病理图像。实验表明，MUSE在多个NDC基准上显著提升了检测和分类性能，证明了自监督学习在病理图像细胞分析中的巨大潜力。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38170/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 877, \"height\": 518, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38170/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 863, \"height\": 666, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38170/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 873, \"height\": 579, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38170/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1780, \"height\": 519, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38170/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 869, \"height\": 341, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38170/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1846, \"height\": 1133, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38170/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1846, \"height\": 1135, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38170/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 801, \"height\": 212, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38170/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 887, \"height\": 252, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38170/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1820, \"height\": 459, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38170/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 625, \"height\": 212, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38170/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 626, \"height\": 219, \"label\": \"Table\"}]"
motivation: 细胞核检测与分类依赖大量精细标注，现有方法难以利用海量无标注数据学习具有判别力的核表示。
method: 提出基于坐标引导的核位置局部自蒸馏的NuLo机制，结合多尺度特征实现稠密自监督学习。
result: 在多个公共病理数据集上，MUSE在核检测和分类任务上均取得领先性能，且标注需求大幅降低。
conclusion: MUSE通过自蒸馏有效地从无标注病理图像中学习核表示，为下游高级病理分析提供了准确的基础。
---

## Abstract
Nucleus detection and classification (NDC) in histopathology analysis is a fundamental task that underpins a wide range of high-level pathology applications. However, existing methods heavily rely on labor-intensive nucleus-level annotations and struggle to fully exploit large-scale unlabeled data for learning discriminative nucleus representations. In this work, we propose MUSE (MUlti-scale denSE self-distillation), a novel self-supervised learning method tailored for NDC. At its core is NuLo (Nucleus-based Local self-distillation), a coordinate-guided mechanism that enables flexible local self-distillation based on predicted nucleus positions. By removing the need for strict spatial alignment between augmented views, NuLo allows critical cross-scale alignment, thus unlocking the capacity of models for fine-grained nucleus-level representation. To support MUSE, we design a simple yet effective encoder-decoder architecture and a large field-of-view semi-supervised fine-tuning strategy that together maximize the value of unlabeled pathology images. Extensive experiments on three widely used benchmarks demonstrate that MUSE effectively addresses the core challenges of histopathological NDC. The resulting models not only surpass state-of-the-art supervised baselines but also outperform generic pathology foundation models.

---

## 论文详细总结（自动生成）

### 1. 论文核心问题与整体含义

- **研究背景**：细胞核检测与分类（NDC）是组织病理学诊断、生物标志物评估等高级应用的基础。精准识别细胞核类型需同时考虑核形态与周围组织结构。
- **核心痛点**：
  - 手工标注细胞核极其费时费力，且现有标注数据集多为小尺寸高倍视野（FoV）切片，难以覆盖组织架构、核形态及染色条件的全部多样性，导致监督模型泛化性不足。
  - 现有自监督学习（SSL）方法（如DINOv2）主要聚焦图像级表示，无法直接适配密集预测任务对细粒度核级特征的需求；且其要求增强视图间严格空间对齐，限制了尺度抖动等关键空间增强。
  - 通用病理基础模型受限于小视野输入（如256×256像素），缺乏对更广阔组织上下文的建模能力。
- **整体含义**：论文提出**MUSE（多尺度稠密自蒸馏）**，一种专为NDC设计的自监督学习方法，旨在高效利用大规模无标注病理图像，学习具有判别力的核级表示，从而突破标注瓶颈和视野限制。

### 2. 方法论

#### 核心思想
利用基于核位置坐标的局部自蒸馏（**NuLo**）机制，无需强制空间对齐即可进行跨尺度、核级别的语义对齐，模拟病理学家灵活关联核细节与组织上下文的能力。

#### 关键技术与流程
- **编码器-解码器主干架构**：
  - 编码器基于ViT，并引入重组层将多级特征转换为二维特征图。
  - 解码器融合多级特征图，输出统一稠密表示（`fmap`）用于核级预测，同时保留CLS token作为图像级表示。
  - 支持可变输入尺寸（96-1024像素），可实现大视野训练。
- **预训练策略（MUSE）**：
  - **ROI补丁生成**：从TCGA全切片图像中截取感兴趣区域，构建`TCGA_nu`数据集（约48.4万张补丁），核坐标通过自动检测获得。
  - **MPP-Based Cropping**：基于每像素微米（MPP）的精确裁剪，按指定物理分辨率生成多尺度成对视图，并建立跨视图的核索引，以便匹配同一细胞核。
  - **NuLo损失（\( \mathcal{L}_{nu} \)）**：在教师和学生网络的输出特征图上，通过坐标插值提取匹配核的特征，计算交叉熵损失。其核心优点是不受旋转、翻转、尺度变化等空间增强的限制。
  - **联合优化**：总损失 \( \mathcal{L}_{MUSE} = \lambda_{image}\mathcal{L}_{image} + \lambda_{nu}\mathcal{L}_{nu} \)，结合图像级自蒸馏（DINO）与核级自蒸馏。
  - **大视野预训练（LFoV）**：将全局视图和局部视图分辨率分别扩大至512和208像素，捕获更丰富的组织上下文。
- **下游微调**：
  - **大视野样本扩展**：将有标注的小切片自然扩展至更大视野（如1024×1024），引入周围无标注组织区域。
  - **半监督微调**：在标注区域内应用坐标回归损失（MSE）和类型分类损失（交叉熵）；在无标注区域基于置信度阈值生成伪标签，施加一致性正则化约束。

### 3. 实验设计

- **数据集与场景**：在三个广泛使用的公开基准上评估——**BRCAM2C**（乳腺癌）、**OCELOT**（多器官重叠细胞）、**PUMA**（黑色素瘤），覆盖不同组织和放大倍率（20倍/40倍）。
- **评估指标**：
  - **核分类**：KNN分类器、线性探测（LIN）、端到端微调（FT）的准确率（ACC）。
  - **核检测与分类**：按类别（淋巴细胞、肿瘤、其他）及平均F1分数。
- **对比方法**：
  - **通用预训练方法**：DINO、MAE、iBOT、DINOv2（基于ResNet和ViT）。
  - **病理基础模型**：MoCoV2 (病理版)、PathBench DINO、CHIEF、CTransPath、CONCH、UNI、Prov-GigaPath。
  - **监督NDC方法**：MCSpatNet、PointNu-Net、CellViT、SMILE、SENC、CGT、DPA-P2PNet。

### 4. 资源与算力

- 论文中未明确提及预训练所使用的GPU型号、数量及总训练时长。仅说明预训练数据集`TCGA_nu`包含约48.4万个ROI补丁。实验涉及多个不同规模模型的训练与测试，但具体算力消耗细节缺失。

### 5. 实验数量与充分性

- **丰富性**：实验覆盖3个下游数据集、3种评估协议（KNN、LIN、FT）、6种以上骨干网络（ResNet-50、ViT-S/B等）、多种预训练方法（通用与病理）及监督NDC模型。
- **消融研究**：系统性地分析了**解码器与多级上下文**的作用、**多尺度补丁**对放大倍率泛化的影响、**预训练损失权重**的重要性以及**大视野与半监督微调**的贡献。
- **公平性**：为公平比较，论文在相同`TCGA_nu`数据集上复现了DINOv2的预训练。对比实验采用统一的下游微调策略，结果客观、充分。

### 6. 主要结论与发现

- MUSE通过核级自蒸馏，在核分类任务上显著超越所有通用及病理基础模型，如**ViT-B/16版本在平均线性探测ACC上高出强基线CONCH约1.4%**，且仅使用约1/2的预训练数据。
- 大视野版本（LFoV-MUSE）进一步将性能推至新高，甚至**超越了参数量数倍于己的UNI和Prov-GigaPath**。
- 在下游NDC任务中，LFoV-MUSE [ViT-B/16] 以简洁的微调流程，**平均F1分数大幅领先现有最佳监督方法**（如在OCELOT上高出8.3个点），证明了自监督预训练的强大潜力。
- 方法有效解决了病理NDC中标注稀缺、视野受限的核心挑战，并展现出极高的数据效率。

### 7. 优点

- **任务特定性创新**：NuLo机制首次将自蒸馏从图像级精准下沉至核级，打破空间对齐桎梏，是SSL用于密集预测问题的精巧设计。
- **跨尺度对齐**：MPP裁剪与NuLo结合，成功建模核形态与组织上下文间的跨尺度关系，符合病理认知。
- **框架完整且灵活**：从预训练（大视野、多尺度）到微调（半监督扩展视野）形成完整闭环，骨干架构可适配不同编码器。
- **实验扎实全面**：在多个数据集、协议和模型规模上均取得一致优势，且与监督方法、超大基础模型的对比充分彰显其高效性。

### 8. 不足与局限

- **核检测器依赖**：预训练生成核坐标的检测器性能未详尽分析，其伪标签噪声可能影响预训练质量。
- **视野限制依然存在**：虽然扩展至512/1024像素，但仍为区域切片，尚未在全切片（WSI）尺度上进行上下文建模。
- **算力透明度不足**：未披露训练所需的具体算力、显存和时间成本，不利于评估实际落地门槛和复现性价比。
- **数据集泛化性**：仅在三个公开数据集上测试，组织类型和癌种覆盖有限，在更罕见肿瘤或不同染色平台上的鲁棒性待验证。
- **未完全无监督**：预训练依赖无监督检测器提供坐标，下游仍需少量标注进行微调，并非全流程免标注方案。
- **半监督策略简单**：伪标签置信度阈值过滤方式较基础，可能遗漏困难样本或引入错误标签，仍有优化空间。

（完）
