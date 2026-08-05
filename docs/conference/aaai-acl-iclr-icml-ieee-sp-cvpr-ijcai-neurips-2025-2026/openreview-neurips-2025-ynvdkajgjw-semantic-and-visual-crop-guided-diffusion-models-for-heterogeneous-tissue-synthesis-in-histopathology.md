---
title: Semantic and Visual Crop-Guided Diffusion Models for Heterogeneous Tissue Synthesis in Histopathology
title_zh: 基于语义和视觉裁剪引导的扩散模型用于病理组织异质性合成
authors: "Saghir Alfasly, Wataru Uegami, MD ENAMUL HOQ, Ghazal Alabtah, Hamid Tizhoosh"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=yNVDkAjGjw"
tags: ["query:profile"]
score: 6.0
evidence: 生成保留组织异质性和细胞形态细节的合成病理图像，以改进分割模型的训练。
tldr: 针对病理图像合成中组织异质性和细胞形态细节保持的挑战，该论文提出一种潜扩散模型，通过结合语义分割图和特定组织区域的视觉裁剪图像进行双重条件生成。方法能够从未标注数据中学习，在保持组织异质性的同时捕捉细微形态特征。生成的合成图像可作为数据增强，提升细胞分割等下游任务的性能，促进数字病理中形态学和微环境特征的利用。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
motivation: 现有病理图像合成方法难以保留组织异质性和细微形态特征。
method: 提出语义和视觉裁剪双重条件的潜扩散模型，结合语义分割图和组织图像块生成病理图像。
result: 成功生成具有组织异质性和形态细节的病理图像，可增强下游分割任务。
conclusion: 该合成方法为病理图像分析提供了有效的数据增强手段，提升了细胞形态分析和分割的鲁棒性。
---

## Abstract
Synthetic data generation in histopathology faces unique challenges: preserving tissue heterogeneity, capturing subtle morphological features, and scaling to unannotated datasets. We present a latent diffusion model that generates realistic heterogeneous histopathology images through a novel dual-conditioning approach combining semantic segmentation maps with tissue-specific visual crops. Unlike existing methods that rely on text prompts or abstract visual embeddings, our approach preserves critical morphological details by directly incorporating raw tissue crops from corresponding semantic regions. For annotated datasets (i.e., Camelyon16, Panda), we extract patches ensuring 20-80% tissue heterogeneity. For unannotated data (i.e., TCGA), we introduce a self-supervised extension that clusters whole-slide images into 100 tissue types using foundation model embeddings, automatically generating pseudo-semantic maps for training. Our method synthesizes high-fidelity images with precise region-wise annotations, achieving superior performance on downstream segmentation tasks. When evaluated on annotated datasets, models trained on our synthetic data show competitive performance to those trained on real data, demonstrating the utility of controlled heterogeneous tissue generation. In quantitative evaluation, prompt‐guided synthesis reduces Fréchet Distance by up to 6× on Camelyon16 (from 430.1 to 72.0) and yields 2–3× lower FD across Panda and TCGA. Downstream DeepLabv3+ models trained solely on synthetic data attain test IoU of 0.71 and 0.95 on Camelyon16 and Panda, within 1–2% of real‐data baselines (0.72 and 0.96). By scaling to 11,765 TCGA whole‐slide images without manual annotations, our framework offers a practical solution for an urgent need for generating diverse, annotated histopathology data, addressing a critical bottleneck in computational pathology.

---

## 论文详细总结（自动生成）

# 论文总结

## 1. 论文的核心问题与整体含义（研究动机和背景）

- **研究背景**：数字病理学中，深度学习模型需要大量带标注的组织病理图像进行训练，但获取高质量、多样性充足且带有像素级标注的病理数据极为困难且成本高昂。
- **核心问题**：现有的组织病理图像合成方法主要面临以下挑战：
  - 难以**保持组织异质性**（即一张图像中常同时存在多种组织类型，如肿瘤、基质、脂肪等）。
  - 难以**捕捉微小的细胞形态学细节**（如细胞核形状、染色质纹理等）。
  - **难以扩展到无标注数据集**，而真实世界中大量全切片图像（WSI）没有精细标注。
- **整体含义**：本文旨在提出一种能生成高保真、异质性组织病理图像的方法，且可在无标注数据上自监督运行，从而解决计算病理学中“多样化标注数据匮乏”的关键瓶颈，提升下游分割任务的性能。

## 2. 论文提出的方法论

### 2.1 核心思想
- 提出一种**双重条件引导的潜扩散模型（Latent Diffusion Model）**，同时利用：
  - **语义分割图**：提供区域级类别信息（如肿瘤区域、正常组织区域等）。
  - **视觉裁剪图像块（tissue-specific visual crops）**：直接从原始图像中裁剪出特定组织的实际图像片段，作为视觉参考，以保留微观形态细节。
- 与传统文本提示或抽象视觉嵌入不同，该方法通过直接注入真实组织碎片的图像内容，确保合成图像中细胞形态的逼真性。

### 2.2 关键技术细节
- **有标注数据集上的处理**（如Camelyon16、Panda）：
  - 从WSI中提取图像块时，确保每个图像块中**20%-80%的组织区域呈现异质性**（即非单一组织类别），从而让模型学习到不同组织的空间关系和过渡。
  - 将语义分割图和对应的组织裁剪图像一起输入扩散模型，作为生成条件。
- **无标注数据集的扩展**（如TCGA）：
  - 引入**自监督扩展**：使用基础模型的嵌入特征对WSI进行聚类，自动将组织划分为100种组织类型，生成伪语义分割图，用于训练。
  - 这种方式使得模型能够从11,765张无手工标注的TCGA全切片图像中学习，极大扩展了数据规模。
- **算法流程**（文字描述）：
  1. 对有标注数据集，提取异质性图像块及对应分割标签，同时截取特定组织的视觉裁剪图像。
  2. 对无标注数据集，通过特征聚类生成伪标签和视觉裁剪。
  3. 在潜空间中，以语义图和视觉裁剪为双条件，训练扩散模型进行去噪学习。
  4. 推理时，根据需要的语义布局和给定的组织参考图像，即可生成对应的高保真病理图像，并附带精确标注。

## 3. 实验设计

### 3.1 数据集与场景
- **Camelyon16**：乳腺癌淋巴结转移数据集，有详细的组织标注。
- **Panda**：前列腺癌分级数据集，有高级别分割标注。
- **TCGA**：泛癌全切片图像集合，在本工作中未经人工标注，用于自监督训练以测试方法对无标注数据的扩展能力。

### 3.2 评估基准（Benchmark）
- **生成质量**：
  - 使用 **Fréchet Distance（FD）** 衡量合成图像分布与真实图像分布的距离。
  - 在Camelyon16上，提示引导合成将FD降低了**6倍**（从430.1降至72.0）；在Panda和TCGA上也获得了2-3倍的FD降低。
- **下游任务**：
  - 采用 **DeepLabv3+** 分割模型，分别用**纯合成数据**训练和**真实数据**训练作对比。
  - 在Camelyon16上，合成数据训练的模型IoU达到0.71，真实数据基线为0.72（仅差1%）。
  - 在Panda上，合成数据训练的模型IoU为0.95，真实数据基线为0.96（仅差1%）。

### 3.3 对比方法
- 摘要虽未列出所有对比方法，但从问题描述可推断，主要对比对象可能包括：
  - 基于文本提示的合成方法。
  - 基于抽象视觉嵌入的扩散模型。
  - 使用纯分割图条件生成的模型。
- 本文方法通过直接引入视觉裁剪图像，在上述对比中展现了明显的形态学细节保留优势和更高的下游任务性能。

## 4. 资源与算力

- **文中是否提及算力**：根据提供的摘要及元数据，**未明确说明所使用的GPU型号、数量或训练时长**。
- 因原始PDF不可获取，仅能从摘要中推断：该工作处理了多达11,765张TCGA全切片图像，且采用了扩散模型训练，属于较大规模计算，但具体资源消耗需查阅正文。

## 5. 实验数量与充分性

### 5.1 实验组数
- 基于摘要可识别至少以下几种实验设置：
  - 在不同数据集上的独立实验（Camelyon16、Panda、TCGA）。
  - 对生成质量的评估实验（FD指标）。
  - 对下游分割任务的量化实验（DeepLabv3+的IoU）。
  - 自监督扩展实验（在TCGA上聚类得到伪标签训练）。
  - 可能还包含消融实验（验证双重条件的必要性），但摘要中未详细展开。

### 5.2 实验充分性评价
- **客观性**：采用标准的FD指标和真实数据基线进行对比，下游任务用统一的分割模型评估，较为客观。
- **公平性**：比较时合成数据训练与真实数据训练使用相同的模型和测试集，对比公平。
- **充分性**：涵盖多类癌症组织、有无标注两种情形，并验证了生成质量与下游任务收益，实验设计相对全面。但摘要缺乏消融研究细节，无法判断对双条件中每一项贡献的充分论证。

## 6. 论文的主要结论与发现

- 提出的**语义和视觉裁剪双重条件潜扩散模型**能够有效生成保留组织异质性和细微形态特征的病理图像。
- 在无标注情况下，基于基础模型嵌入的聚类方法可自动生成有意义的伪语义图，使模型能扩展到大规模未标注WSI数据集。
- 合成的图像不仅视觉质量逼真（FD显著降低），而且可直接作为数据增强，使下游分割模型性能接近甚至等同于用真实数据训练的效果。
- 该方法为计算病理学中缺乏多样化和带标注数据的问题提供了一种实用、可扩展的解决方案。

## 7. 优点

- **双重条件设计的创新性**：直接注入特定组织的原始图像裁剪作为视觉参考，是一种直接有效的形态学细节保持方法，优于仅用语义布局或文本描述。
- **良好的可扩展性**：通过自监督伪标注策略，轻松应用于无标注的大规模数据，大幅降低了对人工标注的依赖。
- **实用性显著**：合成的图像自带像素级标注，可直接用于训练下游模型，且已验证在多个组织的分割任务上效果接近真实数据。
- **定量结果突出**：FD改善倍数显著（Camelyon16降低6倍），下游IoU仅比真实数据少1-2%，证明了方法的高效性。

## 8. 不足与局限

- **算力与训练细节缺失**：从现有摘要无法获知计算资源要求，可能较大，不利于复现和实用性评估。
- **聚类可靠性质疑**：无标注数据的伪标签质量取决于聚类方法，若聚类不准确（如混入不同组织类型），可能引入噪声，影响生成质量。文中未探讨伪标签的精度及错误传播。
- **异质性区间限定**：人为设定20-80%的异质性比例，可能不适用于全部组织类型或任务，且未讨论不同阈值的敏感性。
- **下游任务单一**：仅评估了分割任务，未涉及检测、分类等其它病理学常用下游任务，泛化性证据不足。
- **组织类型有限**：虽覆盖乳腺、前列腺等，但未在更多组织亚型或罕见疾病上验证。
- **对比方法不明**：摘要中缺乏与同期相关工作的定量对比，难以判断相对提高幅度。

（完）
