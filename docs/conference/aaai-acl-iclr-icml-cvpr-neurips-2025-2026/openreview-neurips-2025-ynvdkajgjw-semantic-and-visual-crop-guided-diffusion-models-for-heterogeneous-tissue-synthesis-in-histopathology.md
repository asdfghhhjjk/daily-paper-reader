---
title: Semantic and Visual Crop-Guided Diffusion Models for Heterogeneous Tissue Synthesis in Histopathology
title_zh: 语义与视觉裁剪引导的扩散模型用于组织病理异质组织合成
authors: "Saghir Alfasly, Wataru Uegami, MD ENAMUL HOQ, Ghazal Alabtah, Hamid Tizhoosh"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=yNVDkAjGjw"
tags: ["query:immuno-topo"]
score: 6.0
evidence: 使用深度学习与语义视觉引导合成异质组织病理图像。
tldr: 针对组织病理图像合成中异质性和形态保留的挑战，提出一种语义与视觉裁剪双条件引导的潜在扩散模型。通过语义分割图和原始组织裁剪区域，方法在Camelyon16等数据集上生成保留细微形态特征的异质组织图像，可扩展至无标注数据，为病理学下游任务提供高质量合成数据。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
motivation: 组织病理合成需保留组织异质性和细微形态特征，现有方法难以兼顾。
method: 提出双条件潜在扩散模型，结合语义分割图和组织特异性视觉裁剪引导合成。
result: 在标注和未标注数据集上生成逼真的异质组织图像，保留关键形态细节。
conclusion: 方法支持大规模无标注数据扩展，提升病理合成数据多样性和真实性。
---

## Abstract
Synthetic data generation in histopathology faces unique challenges: preserving tissue heterogeneity, capturing subtle morphological features, and scaling to unannotated datasets. We present a latent diffusion model that generates realistic heterogeneous histopathology images through a novel dual-conditioning approach combining semantic segmentation maps with tissue-specific visual crops. Unlike existing methods that rely on text prompts or abstract visual embeddings, our approach preserves critical morphological details by directly incorporating raw tissue crops from corresponding semantic regions. For annotated datasets (i.e., Camelyon16, Panda), we extract patches ensuring 20-80% tissue heterogeneity. For unannotated data (i.e., TCGA), we introduce a self-supervised extension that clusters whole-slide images into 100 tissue types using foundation model embeddings, automatically generating pseudo-semantic maps for training. Our method synthesizes high-fidelity images with precise region-wise annotations, achieving superior performance on downstream segmentation tasks. When evaluated on annotated datasets, models trained on our synthetic data show competitive performance to those trained on real data, demonstrating the utility of controlled heterogeneous tissue generation. In quantitative evaluation, prompt‐guided synthesis reduces Fréchet Distance by up to 6× on Camelyon16 (from 430.1 to 72.0) and yields 2–3× lower FD across Panda and TCGA. Downstream DeepLabv3+ models trained solely on synthetic data attain test IoU of 0.71 and 0.95 on Camelyon16 and Panda, within 1–2% of real‐data baselines (0.72 and 0.96). By scaling to 11,765 TCGA whole‐slide images without manual annotations, our framework offers a practical solution for an urgent need for generating diverse, annotated histopathology data, addressing a critical bottleneck in computational pathology.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义
- **研究背景**：计算病理学中，高质量标注数据稀缺是核心瓶颈，而合成数据生成面临三大挑战：
  1. 组织异质性（不同组织成分混合）的保留；
  2. 细微形态特征（细胞核形状、纹理等）的准确捕捉；
  3. 向无标注大规模数据集的扩展能力。
- **整体含义**：提出一种语义与视觉双条件引导的潜在扩散模型，生成带有精确区域标注的逼真异质组织病理图像，既能利用有标注数据，也能通过自监督方式利用无标注数据，从而缓解标注瓶颈并提升下游分割任务的性能。

### 2. 论文提出的方法论
- **核心思想**：在潜在扩散模型中引入两条并行的条件信号：
  - **语义条件**：使用组织的语义分割图（如肿瘤区域 vs 正常区域），保证生成图像的组织构成符合指定异质比例（如20%-80%异质性）。
  - **视觉条件**：直接从对应语义区域裁剪的原始组织小块（raw tissue crops），保留局部形态细节和纹理特征，避免纯语义条件导致的细节模糊。
- **关键技术细节**：
  - 对有标注数据集（如Camelyon16、Panda），提取图像块并确保组织异质性在20%-80%之间。
  - 对无标注数据集（如TCGA），提出自监督扩展方法：
    1. 使用基础模型（foundation model）的嵌入向量对全切片图像（WSI）进行聚类，得到100种组织类型；
    2. 自动生成伪语义分割图（pseudo-semantic maps），用于训练。
  - 模型架构为潜在扩散模型，条件机制将语义图和视觉裁剪特征同时注入去噪过程，生成高保真图像，同时产出精确的区域级别标注。
- **流程（文字说明）**：输入语义分割图与从各语义区域提取的真实组织裁剪 → 将裁剪编码为特征并与语义图融合为条件 → 扩散模型在潜在空间进行去噪生成 → 输出与输入语义一致的异质组织图像及相关标注。

### 3. 实验设计
- **数据集/场景**：
  - **标注数据集**：Camelyon16（乳腺癌转移检测）、Panda（前列腺癌分级）。
  - **未标注数据集**：TCGA（多种癌种的全切片图像），规模达11,765张WSI。
- **Benchmark与评估指标**：
  - **生成质量**：Fréchet Distance（FD，越低越好），在Camelyon16上FD从430.1降至72.0（降低约6倍），在Panda和TCGA上降低2~3倍。
  - **下游任务**：在Camelyon16和Panda上训练DeepLabv3+分割模型，仅用合成数据训练，测试IoU分别为0.71和0.95，而真实数据基线分别为0.72和0.96（差距仅1~2%）。
- **对比方法**：未在摘要中详列具体对比方法名称，但提及“prompt-guided synthesis”等现有方法依赖文本提示或抽象视觉嵌入，本方法在FD指标上明显优于它们，并且在无标注数据集上展示了可扩展性。

### 4. 资源与算力
- 摘要及提供材料中**未明确提及**使用的GPU型号、数量、训练时长等算力信息。由于论文仅以摘要形式给出，可能全文中有详细说明，但此处无法提供。

### 5. 实验数量与充分性
- **实验组数**：至少覆盖三个大型数据集（Camelyon16、Panda、TCGA），其中TCGA涉及自监督聚类和伪标注生成，实验广度较大。
- **定量评估**：生成质量指标（FD）在三个数据集上均有量化和显著提升；下游分割任务在两种标注数据集上有对照组（合成数据 vs. 真实数据），显示接近性能。
- **消融实验**：摘要未明确提到消融实验，但推理双条件设计的有效性可能可通过FD的显著降低间接体现（从430到72），全文可能包含更细致的消融对比。
- **充分性与公平性**：基于有限信息，实验覆盖有标注和无标注场景，指标多元，分割任务对比真实数据基线，较为客观。但未列出具体对比方法名称，可能需参看全文。

### 6. 论文的主要结论与发现
- 提出的双条件（语义+视觉裁剪）扩散模型能有效合成保留组织异质性和细微形态的病理图像，并附带精准语义标注。
- 该方法在有标注数据上生成的合成数据用于训练分割模型，效果接近真实数据（IoU差距1~2%），且无需额外人工标注。
- 自监督聚类扩展使方法能利用大规模无标注WSI（如TCGA），扩展性强，为计算病理学提供了实际可用的多样化标注数据生成方案。

### 7. 优点
- **新颖的双条件设计**：直接融合真实组织裁剪作为视觉条件，优于抽象文本或嵌入，保留形态细节。
- **异质性可控**：明确保证20-80%的组织异质比例，生成更符合临床实际的组织混合图像。
- **无标注数据利用**：通过自监督聚类生成伪语义图，突破对人工标注的依赖，可直接适用于超大规模WSI数据集。
- **下游任务验证**：不仅评估生成质量，还通过分割任务证实合成数据的实际效用，指标接近真实数据，说服力强。
- **跨数据集泛化**：在乳腺癌、前列腺癌和TCGA多种癌症类型上验证，展示通用性。

### 8. 不足与局限
- **算力未明**：摘要未提供计算资源需求，可能对复现造成障碍。
- **对比方法模糊**：未具体列出所有对比的现有合成方法，无法评估改进的确切幅度是否全面。
- **伪标注质量风险**：自监督聚类得到的100种组织类型伪标签可能噪声较大，其对最终生成质量的下游影响缺乏分析（摘要未提）。
- **真实数据差距**：合成数据训练的分割模型仍与真实数据有1~2%的IoU差距，对于某些高精度临床场景仍可能不足。
- **实验覆盖局限**：摘要中仅展示分割任务，是否对其他病理任务（如分类、检测）有效未知；生成图像的病理学保真度未经病理学家主观评测。

（完）
