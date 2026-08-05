---
title: "PathVQ: Reforming Computational Pathology Foundation Model for Whole Slide Image Analysis via Vector Quantization"
title_zh: PathVQ：通过向量量化改革计算病理学基础模型用于全切片图像分析
authors: "Honglin Li, Zhongyi Shui, Yunlong Zhang, Chenglu Zhu, Lin Yang"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=Ekw6gjs5Y5"
tags: ["query:cellseg"]
score: 7.0
evidence: 改革计算病理学基础模型用于全切片图像分析
tldr: PathVQ针对病理基础模型依赖大量图文配对数据和计算效率低的难题，创新地采用向量量化技术，将视觉-语言模型与视觉自监督学习结合，无需大规模配对数据即可训练，并通过离散编码实现高效全切片表示，在多个下游任务和稀缺数据场景下均取得有竞争力的性能，为计算病理学提供了一种可扩展的基础模型新方案。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
motivation: 计算病理基础模型依赖大规模图文配对数据，泛化性受限。
method: 通过向量量化改革视觉-语言病理基础模型，融合视觉自监督学习。
result: 在有限配对数据下实现高效全切片分析，提高下游任务性能。
conclusion: 为病理WSI分析提供更具可扩展性和泛化能力的基础模型。
---

## Abstract
Pathology whole slide image (WSI) analysis is vital for disease diagnosis and understanding. While foundation models (FMs) have driven recent advances, their scalability in pathology remains a key challenge. In particular, vision-language (VL) pathology FMs align visual features with language annotation for downstream tasks, but they rely heavily on large-scale image-text paired data, which is scarce thus limiting generalization. On the other hand, vision-only pathology FMs can leverage abundant unlabeled data via self-supervised learning (SSL). However, current approaches often use the [CLS] token from tile-level ViTs as slide-level input for efficiency (a tile with 224×224 pixels composed of 196 patches with 16×16 pixels). This SSL pretrained [CLS] token lacks alignment with downstream objectives, limiting effectiveness. We find that spatial patch tokens retain a wealth of informative features beneficial for downstream tasks, but utilizing all of them incurs up to 200× higher computation and storage costs compared [CLS] token only (e.g., 196 tokens per ViT$_{224}$). This highlights a fundamental trade-off between efficiency and representational richness to build scalable pathology FMs. To address this, we propose a feature distillation framework via vector-quantization (VQ) that compresses patch tokens into discrete indices and reconstructs them via a decoder, achieving 64× compression (1024 → 16 dimensions) while preserving fidelity. We further introduce a multi-scale VQ (MSVQ) strategy, enhancing both reconstruction and providing SSL supervision for slide-level pretraining. Built upon MSVQ features and supervision signals, we design a progressive convolutional module and a slide-level SSL objective to learn spatially rich representations for downstream WSI tasks. Extensive experiments across multiple datasets demonstrate that our approach achieves state-of-the-art performance, offering a scalable and effective solution for high-performing pathology FMs in WSI analysis.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义（研究动机和背景）
- **核心问题**：当前计算病理学基础模型面临可扩展性困境，难以同时兼顾**表示丰富性**与**计算效率**。
  - **视觉-语言 (VL) 模型**虽然表现好，但严重依赖大规模图文配对数据，而此类数据在病理领域极为稀缺，限制了其泛化能力。
  - **纯视觉自监督模型**可利用海量无标注数据，但主流做法为追求效率仅使用每张 tile 的全局特征（如 ViT 的 `[CLS]` token），这丢弃了空间 patch token 中蕴含的丰富局部信息。若使用所有 patch token（如 196 个），则计算与存储开销会暴增约 **200 倍**。
- **整体含义**：论文旨在打破这一僵局，通过引入**向量量化 (VQ)** 技术，在不依赖大规模图文对的前提下，高效压缩并利用空间局部特征，从而构建一个更可扩展、性能更强的全切片图像分析基础模型。

### 2. 论文提出的方法论
- **核心思想**：采用**向量量化**作为特征蒸馏手段，将大量的、高维的视觉 patch tokens 压缩为紧凑的离散索引序列，再通过解码器恢复其语义信息。这样既能保留空间丰富性，又大幅降低维度。
- **关键技术细节与流程**：
  1.  **特征压缩与重建基础框架**：设计一个 VQ 自编码器，将 ViT 输出的所有 patch tokens 映射到码本中的离散索引（压缩比为 **64×**，如 1024 维 → 16 维），随后通过解码器在语义空间中进行重建，确保压缩过程保持高保真度。
  2.  **多尺度向量量化 (MSVQ)**：为了解决单一尺度压缩可能损失细节的问题，提出多尺度 VQ 策略。该策略在不同语义尺度上进行量化和重建，既增强了重建质量，又为后续的切片级预训练提供了额外的自监督信号。
  3.  **切片级渐进式网络**：基于 MSVQ 生成的紧凑特征图和提供的监督信号，设计了一个**渐进式卷积模块**和一个**切片级自监督学习目标**。该模块能够在全切片尺度上高效地融合空间信息，学习到适用于下游任务的丰富空间表征。

### 3. 实验设计
- **数据集与场景**：论文摘要仅提及在“多个数据集”上进行了“广泛实验”，涵盖了多种下游任务（推测为常见的癌症分型、生存预测等全切片分析任务）。**文中未给出具体的数据集名称或规模。**
- **基准与对比方法**：摘要指出，其方法在性能和可扩展性上达到了 state-of-the-art (SOTA) 水平，但没有列出对比的具体模型名称。可合理推断，其对比的基准应包括主流的视觉-语言病理模型和纯视觉自监督病理模型。

### 4. 资源与算力
- **摘要中未明确说明任何算力细节。** 文中没有提及所使用 GPU 的型号、数量、训练时长等任何与计算资源开销相关的信息。

### 5. 实验数量与充分性
- **实验覆盖面**：摘要使用了“广泛实验（extensive experiments）”来描述验证工作，暗示可能包含了多任务、多数据集下的性能评估，以及消融实验（如验证 VQ 压缩、MSVQ 策略等模块的有效性）。然而，**具体的实验组数（如消融实验项数、数据集数量）及详细设置并未在摘要中提供。**
- **充分性与客观性**：由于缺乏具体实验细节，无法从摘要层面评判实验是否足够充分或公平。但文章已被 NeurIPS-2025 接收（评分为 7.0），可以认为其通过了严苛的同行评审，实验设计在完整论文中大概率是充分且令人信服的。

### 6. 论文的主要结论与发现
- PathVQ 成功地将**向量量化技术**应用于病理学基础模型，有效解决了视觉 token 的压缩难题。
- 提出的**多尺度 VQ 策略**不仅能高质量地重建被压缩的特征，还能同时为下游任务提供有价值的自监督学习信号。
- 整套方法在无需依赖大规模图文配对数据的前提下，实现了**高效的计算**与**丰富的空间表示**，在多个全切片图像分析任务上取得了当时最先进的性能，为构建可扩展的病理学基础模型提供了新范式。

### 7. 优点
- **创新性的问题突破**：精准定位并优雅地打破了“效率-表示丰富性”的固有权衡，角度新颖。
- **技术融合巧妙**：将向量量化从图像生成领域跨界用于特征压缩和蒸馏，并与自监督学习有机结合，一箭双雕（压缩+监督信号）。
- **可扩展性强**：摆脱了对稀缺图文配对数据的依赖，并能高效处理全切片尺度的数据，为大规模临床部署提供了可能。
- **架构设计完整**：从 patch 级压缩（MSVQ）到切片级聚合（渐进式卷积模块），形成了一套端到端的完整解决方案。

### 8. 不足与局限
- **信息缺失严重**：摘要未提供任何具体数据集、基准模型、算力开销和详细实验结果，导致难以客观评估其实际应用门槛和泛化边界。
- **潜在局限**（基于方法论的合理推测）：
  - **码本崩溃风险**：向量量化模型在训练中容易出现码本利用率低的问题，可能影响最终表示的信息量。
  - **压缩损失**：尽管声称保持高保真度，从 1024 维到 16 维的高度压缩仍可能丢失关键的精细细胞形态学信息，这一点在极细粒度任务上可能是瓶颈。
  - **多尺度复杂性和超参数**：MSVQ 和渐进式网络引入了更多设计选择和超参数，可能增加在不同中心、不同染色制片条件下的训练和调参难度。
  - **偏倚风险**：未详尽报告实验设置，无法评估其在不同种族或扫描仪来源数据上的稳健性与公平性。

（完）
