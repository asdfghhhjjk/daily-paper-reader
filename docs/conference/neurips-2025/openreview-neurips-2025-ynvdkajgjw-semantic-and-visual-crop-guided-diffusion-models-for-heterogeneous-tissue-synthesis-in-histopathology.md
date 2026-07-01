---
title: Semantic and Visual Crop-Guided Diffusion Models for Heterogeneous Tissue Synthesis in Histopathology
title_zh: 语义与视觉裁剪引导的扩散模型用于组织病理学异质性组织合成
authors: "Saghir Alfasly, Wataru Uegami, MD ENAMUL HOQ, Ghazal Alabtah, Hamid Tizhoosh"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=yNVDkAjGjw"
tags: ["query:profile"]
score: 8.0
evidence: 生成保持组织异质性和形态特征的真实组织病理图像
tldr: 该论文针对组织病理学合成数据生成中保持组织异质性和细微形态特征的挑战，提出双条件潜扩散模型，结合语义分割图和区域组织块视觉引导。该方法在Camelyon16等数据集上生成了具有丰富组织结构和细胞形态的真实图像，为下游任务提供了高质量训练数据。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
motivation: 组织病理合成需保留组织异质性和细微形态特征，现有方法难以兼顾。
method: 提出双条件潜扩散模型，同时使用语义分割图和对应区域的组织块作为视觉引导，直接在原图中提取。
result: 在Camelyon16和Panda数据集上生成高度异质且保留形态细节的组织病理图像。
conclusion: 该方法为利用未标注数据生成形态保留的病理图像提供了有效途径，助力下游任务。
---

## Abstract
Synthetic data generation in histopathology faces unique challenges: preserving tissue heterogeneity, capturing subtle morphological features, and scaling to unannotated datasets. We present a latent diffusion model that generates realistic heterogeneous histopathology images through a novel dual-conditioning approach combining semantic segmentation maps with tissue-specific visual crops. Unlike existing methods that rely on text prompts or abstract visual embeddings, our approach preserves critical morphological details by directly incorporating raw tissue crops from corresponding semantic regions. For annotated datasets (i.e., Camelyon16, Panda), we extract patches ensuring 20-80% tissue heterogeneity. For unannotated data (i.e., TCGA), we introduce a self-supervised extension that clusters whole-slide images into 100 tissue types using foundation model embeddings, automatically generating pseudo-semantic maps for training. Our method synthesizes high-fidelity images with precise region-wise annotations, achieving superior performance on downstream segmentation tasks. When evaluated on annotated datasets, models trained on our synthetic data show competitive performance to those trained on real data, demonstrating the utility of controlled heterogeneous tissue generation. In quantitative evaluation, prompt‐guided synthesis reduces Fréchet Distance by up to 6× on Camelyon16 (from 430.1 to 72.0) and yields 2–3× lower FD across Panda and TCGA. Downstream DeepLabv3+ models trained solely on synthetic data attain test IoU of 0.71 and 0.95 on Camelyon16 and Panda, within 1–2% of real‐data baselines (0.72 and 0.96). By scaling to 11,765 TCGA whole‐slide images without manual annotations, our framework offers a practical solution for an urgent need for generating diverse, annotated histopathology data, addressing a critical bottleneck in computational pathology.

---

## 论文详细总结（自动生成）

# 论文核心问题与整体含义

- **研究动机**：组织病理学中合成数据生成面临独特挑战：需要保留组织异质性（不同组织区域的混合）、捕获细微的细胞形态特征，并能扩展到大规模未标注数据集。
- **核心问题**：现有方法（如文本提示或抽象视觉嵌入引导）难以兼顾异质性保持与细节形态保留，限制了合成病理图像在下游任务中的实用性。该论文旨在解决在生成过程中同时保留组织异质性和细微形态特征的问题，并为未标注数据提供可扩展的合成方案。
- **整体含义**：提出一种可控制、高保真的异质性组织合成方法，为计算病理学中标注数据匮乏的瓶颈提供实用解决方案。

# 方法论

- **核心思想**：采用双条件潜扩散模型，同时用语义分割图和对应区域的组织图像块作为引导，直接融合原始组织块的视觉细节以保持形态特征。
- **技术细节**：
  - **双条件机制**：条件一为语义分割图（提供区域类别信息）；条件二为从对应语义区域提取的原始组织块（提供视觉细节），直接作为视觉引导输入模型。
  - **有标注数据集处理**：从Camelyon16、Panda等数据集中提取图像块，确保每个块包含20‑80%的组织异质性。
  - **无标注数据集处理**（自监督扩展）：针对TCGA等未标注的全切片图像，利用基础模型嵌入对图像进行聚类（分为100种组织类型），自动生成伪语义图用于训练。
  - **模型基底**：基于潜在扩散模型（LDM），在潜在空间进行生成，并结合条件控制。
  - **下游应用**：生成图像带有精确的区域标注，可直接用于训练语义分割模型（如DeepLabv3+）。
- **算法流程**：
  1. 对有标注数据：提取异质性丰富的图像块，获得语义分割图和对应的组织块对。
  2. 对无标注数据：通过自监督聚类获得聚类伪标签，构建伪语义图和组织块对。
  3. 将语义图和组织块对作为条件，训练条件扩散模型。
  4. 利用训练后的模型合成高质量带标注的组织病理图像。
  5. 用合成数据训练下游分割模型。

# 实验设计

- **数据集与场景**：
  - 有标注数据集：Camelyon16（乳腺癌转移检测）、Panda（前列腺癌分级）。
  - 无标注数据集：TCGA（大规模全切片图像，11,765张）。
- **基准对比**：
  - 定量评估生成质量：采用Fréchet Distance (FD) 等指标。
  - 下游任务：用合成数据训练DeepLabv3+分割模型，评估在Camelyon16和Panda测试集上的IoU，并与真实数据训练的模型对比。
- **对比方法**：
  - 虽然摘要未详列，但提到与现有依赖文本提示或抽象视觉嵌入的方法对比，并展示了FD大幅降低（在Camelyon16上从430.1降至72.0，降低最多6倍；Panda和TCGA上降低2‑3倍）。

# 资源与算力

- 论文摘要中**未明确说明**所使用的GPU型号、数量及训练时长等具体算力信息。推测完整论文中可能包含相关细节，但基于提供的内容无法获取。

# 实验数量与充分性

- **实验组数**：
  - 至少涵盖三个大型数据集（两个有标注，一个无标注）的生成实验。
  - 多指标定量评估（FD的降幅对比）。
  - 下游分割任务的对比实验（仅用合成数据训练的模型与真实数据训练的模型对比）。
- **充分性与客观性**：
  - 实验覆盖有标注和无标注场景，体现了方法的可扩展性。
  - 评估指标兼具生成质量（FD）与下游任务实用性（分割IoU），且报告了具体数值（如Camelyon16上合成数据训练分割IoU达0.71，真实数据0.72；Panda上0.95 vs 0.96），差距仅1‑2%，较为客观。
  - 未提供消融实验的细节，无法判断对双条件各成分的剥离分析是否充分。整体实验设计看似合理且具有说服力，但在有限信息下，消融实验的充分性无法确认。

# 主要结论与发现

- 提出的双条件扩散模型能够生成高度异质且保留细微形态细节的组织病理图像。
- 语义图与组织块视觉引导的结合显著提升了合成图像的真实性和下游任务性能。
- 在无标注数据集上，自监督聚类生成的伪语义图可有效驱动模型训练，展示了方法向大规模未标注数据扩展的能力。
- 仅用合成数据训练的分割模型，在Camelyon16和Panda上的性能与真实数据训练的基线极为接近（IoU差距在1‑2%以内），体现了可控异质组织生成的实用性。

# 优点

- **双条件设计创新**：同时利用语义类别和原始视觉块，直接保留关键的形态细节，比只用文本或抽象嵌入的方法更具病理学针对性。
- **兼顾异质性与细节**：强制提取20‑80%异质性的图像块进行训练，主动保证生成图像的组织多样性。
- **自监督扩展**：通过基础模型嵌入聚类，将方法无缝应用于大规模无标注全切片图像，无需额外人工标注，极大提升了方法的可及性和数据覆盖范围。
- **下游任务验证扎实**：不仅在生成指标上大幅超越现有方法，还通过分割任务实际证明了合成数据的效用，研究闭环完整。
- **性能突出**：FD降低最多6倍，下游分割IoU接近真实数据训练的模型，效果显著。

# 不足与局限

- **算力与实施细节缺失**：从摘要无法得知训练资源需求、时间成本等，可能限制其实际部署的可行性评估。
- **无标注聚类的可靠性**：自监督阶段聚类得到的100种组织类型可能无法精准对应临床含义，伪语义图的质量可能影响某些精细任务；对聚类数目的选择缺乏探讨。
- **实验对比有限**：未明确列出与多种最新生成模型（如其他条件扩散模型、GAN等）的直接对比，只与“文本提示或抽象视觉嵌入”方法比较。
- **消融分析未知**：未提供双条件中单一条件的消融实验结果，无法确定各成分的贡献度。
- **泛化性验证不足**：仅在三种数据（两种肿瘤类型）上验证，对其他器官、染色平台、罕见病种的适用性尚不明确。
- **评估指标局限性**：Fréchet Distance和下游IoU虽常用，但未能涵盖病理医生主观评分，对形态学细节保留的评估可能不够充分。
- **应用偏差风险**：合成数据可能继承原始数据中的偏见（如特定机构染色风格），若不加控制，可能在下游任务中引入偏差。

（完）
