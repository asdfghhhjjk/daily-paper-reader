---
title: "PathVQ: Reforming Computational Pathology Foundation Model for Whole Slide Image Analysis via Vector Quantization"
title_zh: PathVQ：通过矢量量化改革计算病理基础模型用于全切片图像分析
authors: "Honglin Li, Zhongyi Shui, Yunlong Zhang, Chenglu Zhu, Lin Yang"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=Ekw6gjs5Y5"
tags: ["query:cell-path"]
score: 5.0
evidence: 基于矢量量化的计算病理全切片图像基础模型
tldr: 针对病理基础模型中视觉-语言模型依赖稀缺图文对、视觉模型效率受限的问题，本文提出PathVQ，一种基于矢量量化的计算病理基础模型，用于全切片图像分析。该方法通过矢量量化重构WSI表征，减少对图像-文本配对数据的依赖，并提升模型扩展性。实验结果显示，PathVQ在下游任务上表现优异，为WSI分析提供了高效可扩展的方案。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
motivation: 现有病理基础模型依赖图文对数据或仅用CLS标记，扩展性受限。
method: 提出基于矢量量化的视觉基础模型PathVQ，利用无标注WSI自监督学习表征。
result: 实验表明PathVQ提升下游任务性能并降低数据依赖。
conclusion: PathVQ为计算病理提供高效可扩展的全切片图像分析基础模型。
---

## Abstract
Pathology whole slide image (WSI) analysis is vital for disease diagnosis and understanding. While foundation models (FMs) have driven recent advances, their scalability in pathology remains a key challenge. In particular, vision-language (VL) pathology FMs align visual features with language annotation for downstream tasks, but they rely heavily on large-scale image-text paired data, which is scarce thus limiting generalization. On the other hand, vision-only pathology FMs can leverage abundant unlabeled data via self-supervised learning (SSL). However, current approaches often use the [CLS] token from tile-level ViTs as slide-level input for efficiency (a tile with 224×224 pixels composed of 196 patches with 16×16 pixels). This SSL pretrained [CLS] token lacks alignment with downstream objectives, limiting effectiveness. We find that spatial patch tokens retain a wealth of informative features beneficial for downstream tasks, but utilizing all of them incurs up to 200× higher computation and storage costs compared [CLS] token only (e.g., 196 tokens per ViT$_{224}$). This highlights a fundamental trade-off between efficiency and representational richness to build scalable pathology FMs. To address this, we propose a feature distillation framework via vector-quantization (VQ) that compresses patch tokens into discrete indices and reconstructs them via a decoder, achieving 64× compression (1024 → 16 dimensions) while preserving fidelity. We further introduce a multi-scale VQ (MSVQ) strategy, enhancing both reconstruction and providing SSL supervision for slide-level pretraining. Built upon MSVQ features and supervision signals, we design a progressive convolutional module and a slide-level SSL objective to learn spatially rich representations for downstream WSI tasks. Extensive experiments across multiple datasets demonstrate that our approach achieves state-of-the-art performance, offering a scalable and effective solution for high-performing pathology FMs in WSI analysis.

---

## 论文详细总结（自动生成）

# PathVQ 论文总结

## 1. 论文的核心问题与整体含义

- **研究背景**：病理全切片图像（WSI）分析对疾病诊断和理解至关重要。基础模型（Foundation Models, FMs）虽然推动了该领域进展，但在病理场景中的可扩展性仍是关键挑战。
- **现有方法的局限**：
  - **视觉-语言（VL）病理基础模型**：需要大量图像-文本配对数据进行视觉特征与语言标注的对齐。这类配对数据在病理领域非常稀缺，限制了模型泛化能力。
  - **纯视觉病理基础模型**：常借助自监督学习（SSL）利用大量无标注数据，但现有做法通常使用 tile 级 ViT 的 `[CLS]` token 作为 slide 级输入。该 `[CLS]` token 在 SSL 预训练后缺乏与下游任务目标的对齐，影响效果。
- **核心矛盾**：空间 patch tokens 包含丰富且对下游任务有益的信息，但全部使用会比仅用 `[CLS]` token 带来高达 200 倍的计算和存储开销（例如 ViT₂₂₄ 中每个 tile 有 196 个 patch tokens）。
- **整体含义**：需要在“计算效率”和“表征丰富度”之间取得平衡，构建可扩展的病理基础模型。论文提出 PathVQ 来解决这一权衡。

## 2. 论文提出的方法论

- **核心思想**：利用矢量量化（Vector Quantization, VQ）将 patch tokens 压缩为离散索引，再通过解码器重建，从而在保留关键信息的同时大幅降低维度。
- **关键技术细节**：
  - **VQ 特征蒸馏框架**：将 patch tokens 压缩为离散索引并重建，实现 **64 倍压缩**（维度从 1024 降至 16），同时保持重建保真度。
  - **多尺度 VQ（MSVQ）策略**：在多个尺度上进行矢量量化，既增强重建能力，又为 slide 级预训练提供自监督学习（SSL）监督信号。
  - **渐进卷积模块**：基于 MSVQ 特征和监督信号设计，用于学习空间丰富的 slide 级表示。
  - **slide 级 SSL 目标**：利用 MSVQ 提供的监督信号进行 slide 级自监督预训练，使学到的表示更契合下游 WSI 任务。
- **整体流程（文字描述）**：
  1. 从 tile 级 ViT 提取空间 patch tokens。
  2. 通过 VQ 将高维 patch tokens 映射为离散码本索引。
  3. 解码器根据索引重建原始 patch tokens，实现压缩与重建。
  4. 多尺度 VQ 在不同粒度上重复上述过程，产生多尺度特征和多尺度重建监督。
  5. 渐进卷积模块聚合多尺度离散特征，结合 slide 级 SSL 目标进行预训练，最终得到适用于下游任务的 slide 级表示。

## 3. 实验设计

- **数据集 / 场景**：摘要中仅提到“多个数据集”（multiple datasets），未给出具体数据集名称、数量或来源。
- **Benchmark**：下游任务为 WSI 分析相关任务，但具体 benchmark（如癌症分型、生存预测、分级等）未在摘要中列出。
- **对比方法**：摘要未列出具体对比的基线模型，仅表示“achieves state-of-the-art performance”，因此无法从现有信息判断与哪些方法进行了直接比较。

## 4. 资源与算力

- 提供的摘要和元数据中 **未明确说明** 所使用的 GPU 型号、数量、训练时长、批大小或显存消耗等算力信息。
- 需要查阅论文全文或附录才能获得相关细节。

## 5. 实验数量与充分性

- 根据摘要，作者声称进行了“extensive experiments across multiple datasets”（跨多个数据集的广泛实验），但 **未提供具体实验组数**、消融实验设置或统计检验结果。
- 从已有信息无法客观判断实验是否充分；但摘要中关于 64 倍压缩、多尺度 VQ、slide 级 SSL 等模块的描述暗示存在一定消融验证的可能，具体需查看全文。
- 公平性方面：未列出对比基线、数据集划分方式、评价指标等，因此无法评估对比实验的公平性与客观性。

## 6. 论文的主要结论与发现

- **主要结论**：PathVQ 通过矢量量化压缩 patch tokens，能够在保持表征丰富度的同时显著降低计算和存储成本，为病理 WSI 分析提供可扩展且有效的基础模型。
- **关键发现**：
  - 空间 patch tokens 包含对下游任务有益的信息，但直接使用代价过高；VQ 蒸馏可在 64 倍压缩下保留关键信息。
  - 多尺度 VQ 不仅增强重建，还能为 slide 级预训练提供有效的自监督信号。
  - 基于 MSVQ 的渐进卷积和 slide 级 SSL 目标能够学习到空间丰富的 slide 级表示，在多个数据集上取得 SOTA 性能。

## 7. 优点

- **不依赖稀缺图文对**：纯视觉自监督路线，可充分利用海量无标注病理切片数据，避免对图像-文本配对的强依赖。
- **高效压缩**：通过 VQ 实现 64 倍维度压缩，显著缓解 patch tokens 带来的计算与存储压力。
- **多尺度设计**：MSVQ 同时服务于重建和 slide 级 SSL 监督，提升了特征表达的丰富性和下游适应性。
- **针对性架构**：渐进卷积模块与 slide 级 SSL 目标专门为全切片级任务设计，更贴合病理 WSI 的特点。
- **可扩展性**：兼顾效率与表征质量，适合构建大规模病理基础模型。

## 8. 不足与局限

- **实验细节缺失**：摘要未提供具体数据集、基准任务、对比方法、评价指标和统计显著性，难以判断实验的全面性和结论的稳健性。
- **未报告算力开销**：虽然强调 64 倍压缩，但未给出实际训练/推理的 GPU 成本和训练时长，效率优势的量化证据不足。
- **潜在偏差风险**：
  - 仅从摘要看，未说明是否包含多中心、多扫描仪、多染色协议的外部验证，泛化性存疑。
  - 未提及罕见疾病亚型或长尾分布下的表现。
- **方法本身可能的局限**：矢量量化会引入离散化误差，重建保真度虽高但仍可能丢失细粒度信息；多尺度 VQ 和渐进卷积模块的复杂度未在摘要中交代。
- **可解释性**：未讨论离散码本是否具有病理语义可解释性，以及其对下游任务的具体贡献机制。

（完）
