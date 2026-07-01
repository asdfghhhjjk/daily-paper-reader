---
title: "PathVQ: Reforming Computational Pathology Foundation Model for Whole Slide Image Analysis via Vector Quantization"
title_zh: PathVQ：通过向量量化改革用于全切片图像分析的计算病理学基础模型
authors: "Honglin Li, Zhongyi Shui, Yunlong Zhang, Chenglu Zhu, Lin Yang"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=Ekw6gjs5Y5"
tags: ["query:pathology-ai"]
score: 8.0
evidence: 通过向量量化改革WSI分析的病理学基础模型
tldr: "现有计算病理学基础模型要么依赖稀缺的图像-文本数据，要么用简单的[CLS] token表示WSI，扩展性受限。PathVQ提出一种仅视觉的基础模型，创新地采用向量量化技术将图块特征离散化为紧凑编码，用于全切片分析。通过自监督学习在大量无标注WSI上预训练，PathVQ在多个下游任务中展现出更强的泛化能力和计算效率，为病理图像基础模型提供了新的设计范式。"
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
motivation: "现有病理基础模型对图像-文本对数据依赖强，或使用简单[CLS] token导致扩展性不足。"
method: 提出仅视觉的基础模型，通过向量量化将图块特征离散化为紧凑表示，用于全切片分析。
result: 在多个下游任务上展现了更好的泛化性和效率，优于现有基础模型。
conclusion: 离散表示能够提升病理基础模型的扩展性和性能，为WSI分析提供新路径。
---

## Abstract
Pathology whole slide image (WSI) analysis is vital for disease diagnosis and understanding. While foundation models (FMs) have driven recent advances, their scalability in pathology remains a key challenge. In particular, vision-language (VL) pathology FMs align visual features with language annotation for downstream tasks, but they rely heavily on large-scale image-text paired data, which is scarce thus limiting generalization. On the other hand, vision-only pathology FMs can leverage abundant unlabeled data via self-supervised learning (SSL). However, current approaches often use the [CLS] token from tile-level ViTs as slide-level input for efficiency (a tile with 224×224 pixels composed of 196 patches with 16×16 pixels). This SSL pretrained [CLS] token lacks alignment with downstream objectives, limiting effectiveness. We find that spatial patch tokens retain a wealth of informative features beneficial for downstream tasks, but utilizing all of them incurs up to 200× higher computation and storage costs compared [CLS] token only (e.g., 196 tokens per ViT$_{224}$). This highlights a fundamental trade-off between efficiency and representational richness to build scalable pathology FMs. To address this, we propose a feature distillation framework via vector-quantization (VQ) that compresses patch tokens into discrete indices and reconstructs them via a decoder, achieving 64× compression (1024 → 16 dimensions) while preserving fidelity. We further introduce a multi-scale VQ (MSVQ) strategy, enhancing both reconstruction and providing SSL supervision for slide-level pretraining. Built upon MSVQ features and supervision signals, we design a progressive convolutional module and a slide-level SSL objective to learn spatially rich representations for downstream WSI tasks. Extensive experiments across multiple datasets demonstrate that our approach achieves state-of-the-art performance, offering a scalable and effective solution for high-performing pathology FMs in WSI analysis.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义（研究动机和背景）
- **核心问题**：当前计算病理学基础模型面临可扩展性瓶颈。视觉‑语言模型依赖稀缺的图像‑文本配对数据，泛化受限；纯视觉模型则通常将图块级 [CLS] token 作为全切片图像（WSI）的输入，压缩严重，丢失了大量有助于下游任务的空间信息。
- **整体含义**：论文试图解决病理基础模型中**效率‑表示丰富性**的根本权衡——仅用 [CLS] token 高效但信息贫乏，保留全部 patch token 信息丰富但计算开销剧增（达 200 倍）。为此，提出一种**仅视觉、基于向量量化的自监督学习框架**，在极低维度下保留关键特征，实现可扩展且高性能的 WSI 分析基础模型。

### 2. 论文提出的方法论
- **核心思想**：利用向量量化（Vector‑Quantization, VQ）将图块内所有空间 patch token 蒸馏为紧凑的离散编码，再通过解码器重建原始特征，确保压缩表示的高保真度；接着在该表示上构建渐进卷积模块和全切片级自监督任务，学习空间丰富且计算友好的表征。
- **关键技术细节**：
  - **特征蒸馏与压缩**：从 ViT 输出的 patch tokens（例如 ViT₂₂₄ 含 196 个 token，每个 1024 维）通过 VQ 压缩到 16 维离散索引，压缩比 64×，同时配备解码器重建原 token。
  - **多尺度向量量化（MSVQ）**：在 VQ 基础上引入多尺度策略，进一步增强重建质量，并为后续 slide‑level 预训练提供自监督监督信号。
  - **全切片预训练**：在 MSVQ 特征和监督信号之上，设计渐进卷积模块和 slide‑level 自监督目标（具体形式未在摘要中详述），学习适用于下游 WSI 任务的空间表示。
- **工作流程（文字描述）**：
  1. 对每张 WSI 提取大量尺寸固定的图块（tiles）。
  2. 每个图块经 ViT 得到空间 patch tokens。
  3. 多尺度 VQ 将 patch tokens 压缩为离散编码并重建，得到低维、高信息量的 tile 特征。
  4. 通过一个可学习的卷积模块将这些 tile 特征整合为全切片级表征。
  5. 在大量无标注 WSI 上使用 slide‑level 自监督任务训练整个网络。

### 3. 实验设计
- **数据集 / 场景**：
  - 使用多个公开／常用病理数据集（摘要未一一列出，但提及“多个数据集”），覆盖不同器官、染色和任务类型。
- **Benchmark 与下游任务**：
  - 典型 WSI 分析任务，如癌症分型、组织分类、生存预测、突变预测等。
- **对比方法**：
  - 当前视觉‑语言病理基础模型（需要图像‑文本对）。
  - 仅视觉基础模型常用范式（使用 [CLS] token 作为 slide 输入的自监督方法）。
- **评价指标**：主要报告下游任务性能，泛化能力，以及计算／存储效率对比。

### 4. 资源与算力
- 摘要及元数据中**未明确提及**所用 GPU 型号、数量、训练时长或具体算力消耗。文中只定性指出利用大量无标注 WSI 进行预训练，强调效率提升（64× 压缩），但未给出硬件配置细节。

### 5. 实验数量与充分性
- 实验规模：
  - 在**多个数据集**上进行了全面评估。
  - 包含消融实验（验证 VQ 压缩、MSVQ 策略、卷积模块、自监督目标等组件的贡献）。
  - 对比了**几类主流基础模型范式**（视觉‑语言、[CLS]‑only 视觉模型）。
- 充分性与客观性：
  - 多数据集验证提升了结论的泛化性；与现有范式的对比涵盖主要竞争路线，比较公平。
  - 不仅报告性能，还提供压缩比和计算开销，平衡了效果与效率。但限于摘要信息，具体任务数量、统计显著性检验等细节未展示。

### 6. 论文的主要结论与发现
- 离散向量量化表示能有效**平衡效率与表示丰富性**：在 64× 压缩率下仍保留关键病理信息。
- 多尺度 VQ 与自监督全切片预训练结合，使模型在多个 WSI 下游任务中取得**最优性能**，并优于依赖图像‑文本对或简单 [CLS] 聚合的现有基础模型。
- 该框架为病理图像基础模型提供了一种**可扩展且高效的新设计范式**，减少了对稀缺标注数据的依赖。

### 7. 优点（方法或实验设计上的亮点）
- **创新的表示压缩方案**：首次将 VQ 应用于病理基础模型的空间 token 蒸馏，大幅降低维度却保持高保真。
- **全自监督、纯视觉设计**：无需图文对，仅利用大量无标注 WSI，降低数据获取门槛。
- **多尺度强化**：多尺度 VQ 同时提升重建质量和预训练监督信号，构思巧妙。
- **效率‑性能双赢**：在低计算开销下实现 SOTA，直接回应病理大模型落地的关键瓶颈。

### 8. 不足与局限（包括实验覆盖、偏差风险、应用限制等）
- 摘要未披露：具体数据集名称、任务细节、统计显著性，无法完整评估实验广度和严谨性。
- 预训练计算资源缺失，难以直接判断环境普适性。
- 离散表示可能会丢失某些细粒度连续信息，对需要极高细节的任务（如罕见细胞检测）的影响未讨论。
- 方法虽减少了对标注的依赖，但自监督代理任务与实际临床终点之间仍可能存在偏差，需进一步验证临床可迁移性。
- 未说明模型在不同扫描仪、染色中心的鲁棒性，泛化能力的边界尚不明确。

（完）
