---
title: "MUSE: Multi-Scale Dense Self-Distillation for Nucleus Detection and Classification"
title_zh: "MUSE: 用于核检测与分类的多尺度稠密自蒸馏"
authors: "Zijiang Yang, Hanqing Chao, Bokai Zhao, Yelin Yang, Yunshuo Zhang, Dongmei Fu, Junping Zhang, Le Lu, Ke Yan, Dakai Jin, Minfeng Xu, Yun Bian, Hui Jiang"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/38170/42132"
tags: ["query:immuno-topo"]
score: 10.0
evidence: 通过多尺度稠密自蒸馏实现组织病理学中的自监督核检测与分类
tldr: 针对组织病理学中核检测与分类依赖大量标注的问题，MUSE提出多尺度稠密自蒸馏方法，利用基于预测核位置的局部自蒸馏机制，无需严格空间对齐即可从无标注数据学习判别性核表示。实验证明，MUSE在有限标注下显著提升核检测与分类性能。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38170/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 877, \"height\": 518}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38170/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 863, \"height\": 666}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38170/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 873, \"height\": 579}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38170/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1780, \"height\": 519}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38170/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 869, \"height\": 341}]"
tables_json: "[{\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38170/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1846, \"height\": 1133}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38170/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1846, \"height\": 1135}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38170/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 801, \"height\": 212}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38170/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 887, \"height\": 252}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38170/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1820, \"height\": 459}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38170/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 625, \"height\": 212}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38170/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 626, \"height\": 219}]"
motivation: 组织病理核检测与分类依赖高昂的核级标注。
method: 设计基于核位置的局部自蒸馏机制，实现从无标注数据中学习。
result: 在多个基准上相比于有监督方法显著提高了检测与分类精度。
conclusion: MUSE为利用大量无标注病理数据提升核分析性能提供了有效途径。
---

## Abstract
Nucleus detection and classification (NDC) in histopathology analysis is a fundamental task that underpins a wide range of high-level pathology applications. However, existing methods heavily rely on labor-intensive nucleus-level annotations and struggle to fully exploit large-scale unlabeled data for learning discriminative nucleus representations. In this work, we propose MUSE (MUlti-scale denSE self-distillation), a novel self-supervised learning method tailored for NDC. At its core is NuLo (Nucleus-based Local self-distillation), a coordinate-guided mechanism that enables flexible local self-distillation based on predicted nucleus positions. By removing the need for strict spatial alignment between augmented views, NuLo allows critical cross-scale alignment, thus unlocking the capacity of models for fine-grained nucleus-level representation. To support MUSE, we design a simple yet effective encoder-decoder architecture and a large field-of-view semi-supervised fine-tuning strategy that together maximize the value of unlabeled pathology images. Extensive experiments on three widely used benchmarks demonstrate that MUSE effectively addresses the core challenges of histopathological NDC. The resulting models not only surpass state-of-the-art supervised baselines but also outperform generic pathology foundation models.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义
- **核心问题**：组织病理学中的细胞核检测与分类（NDC）是许多下游任务的基础，但现有方法严重依赖人工标注细胞核，无法有效利用大规模无标注数据学习有区分力的细胞核表征。
- **整体含义**：提出一种专门针对NDC的自监督学习方法MUSE，通过基于细胞核的局部自蒸馏机制，无需严格空间对齐即可实现多尺度细胞核表征学习，从而大幅降低标注依赖，提升在小标注样本下的性能。

### 2. 论文提出的方法论
- **核心思想**：基于教师‑学生网络的自我蒸馏框架，在图像级蒸馏基础上，增加基于细胞核坐标引导的局部自蒸馏（NuLo），使得不同增强视图间无需空间对齐即可学习跨尺度的细胞核一致性表征。
- **关键技术细节**：
  - **MPP‑Based Cropping**：按照物理分辨率（微米/像素）裁剪多尺度视图，保证视图间细胞核的空间对应关系。
  - **NuLo**：通过一个轻量的核检测器预先估计细胞核坐标，在特征图上利用双线性插值提取每个核的特征，然后对匹配的核做特征蒸馏（交叉熵损失），从而在不要求视图空间对齐的条件下实现局部‑全局对齐。
  - **编解码架构**：基于ViT的编码器配合重装配层和残差解码器，输出多级特征图，支持图像级和核级蒸馏。
  - **大视野半监督微调**：将标注区域扩展为更大视野的样本，在标注区域施加有监督损失，在无标注区域施加伪标签一致性正则化。
- **损失函数**：总损失 \( \mathcal{L}_{\text{MUSE}} = \lambda_{\text{image}}\mathcal{L}_{\text{image}} + \lambda_{\text{nu}}\mathcal{L}_{\text{nu}} \)，其中 \(\mathcal{L}_{\text{image}}\) 为图像级DINO损失，\(\mathcal{L}_{\text{nu}}\) 为核级蒸馏损失。

### 3. 实验设计
- **数据集/场景**：
  - 预训练数据集：从TCGA中构建的483,627个ROI片（TCGA_nu）。
  - 下游测试基准：BRCAM2C（乳腺癌，20×/40×）、OCELOT（多种组织，20×/40×）、PUMA（黑色素瘤，20×）。
  - 任务评价：细胞核分类（KNN、线性探测、微调准确率）和细胞核检测+分类（F1分数）。
- **对比方法**：
  - 通用自监督模型（DINO、MAE、iBOT、DINOv2）及其病理领域微调版。
  - 病理基础模型（CHIEF、CTransPath、CONCH、UNI、Prov‑GigaPath）。
  - 有监督NDC方法（MCSpatNet、PointNu‑Net、SMILE、SENC、CGT、CellViT、DPA‑P2PNet）。
- **benchmark**：均在统一的数据集划分和指标下对比，部分方法使用其公开预训练权重或复现结果。

### 4. 资源与算力
- 论文未明确说明预训练所使用的GPU型号、数量及训练时长，仅提供了用于预训练的样本数量（约48万ROI）和模型参数量（如ViT‑S/16 31M，ViT‑B/16 123M）。推断训练在商用多GPU集群上进行，但确切算力信息缺失。

### 5. 实验数量与充分性
- **实验组数**：
  - 细胞核分类实验：涵盖6个数据集/放大倍数组合，3种评估协议（KNN、线性探测、微调），对比超过15种方法。
  - 核检测+分类实验：在3个数据集上对比7种有监督方法。
  - 消融实验：包括解码器与多级上下文、多尺度裁剪、预训练损失权重、大视野微调与一致性正则化等，每组至少汇报3种指标。
- **充分性**：对比基线全面，覆盖通用视觉预训练、病理专用预训练和有监督NDC方法；消融设计合理，能够验证各组件贡献。实验设定公平，使用相同数据集和统一评价指标。

### 6. 论文的主要结论与发现
- MUSE的跨尺度局部自蒸馏显著提升了细胞核表征质量，在有限标注下获得远超有监督方法和通用病理基础模型的性能。
- 即使模型参数量和预训练数据量更小（如ViT‑B参数量远小于UNI、Prov‑GigaPath），MUSE仍能在细胞核分类和检测任务上取得最优成绩。
- 大视野预训练和半监督微调进一步利用组织上下文信息，带来额外性能增益。
- 多尺度裁剪让模型能够适应不同放大倍率，表现出较强的倍率泛化能力。

### 7. 优点
- 首次将坐标引导的局部自蒸馏引入病理细胞核分析，消除了严格空间对齐的限制。
- 从预训练到微调的全流程设计简洁且有效，组件可插拔。
- 在数据效率和模型参数量上具有明显优势，对比公平且有说服力。
- 在三个公开 benchmark 上均取得显著提升，展现较强的泛化性。

### 8. 不足与局限
- 预训练依赖自动核检测器生成的伪坐标，其准确性会影响NuLo的训练质量，文中未深入分析该影响。
- 未提供预训练的计算开销和收敛时间，限制了可复现性和资源评估。
- 实验主要集中在常见癌种和固定放大倍率（20×、40×），不同染色、扫描仪以及更极端的组织形态泛化性有待验证。
- 半监督微调中的伪标签阈值和损失权重可能需要针对不同数据集调整，超参数敏感性未充分探索。
- 对于极端小目标或严重遮挡的细胞核，特征插值可能引入噪声，文中未讨论鲁棒性。

（完）
