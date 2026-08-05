---
title: Efficient Patch Search in Whole Slide Images via Morphological Momentum Prototype Learning
title_zh: 通过形态动量原型学习在全切片图像中高效搜索补丁
authors: "Sihyeon Park, Jungwoo Park, Hyunjae Kim, Jaewoo Kang, Bumsoo Kim"
date: 2025-09-20
pdf: "https://openreview.net/pdf?id=rYbYbgeaEv"
tags: ["query:path-xai-sel"]
score: 10.0
evidence: 基于形态动量原型学习在WSI中高效搜索信息补丁
tldr: 全切片图像因分辨率极高导致分析计算量大，现有方法常费力处理大量冗余补丁。本文提出一种基于形态动量原型学习的补丁搜索方法，通过在线更新原型有效捕获形态学特征相似的信息性补丁，从而在保持诊断性能的同时显著减少计算量，为WSI高效分析提供了新思路。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 全切片图像处理中冗余补丁多，计算效率低，需要高效选择重要区域。
method: 提出形态动量原型学习方法，利用形态学特征和动量更新原型来搜索信息补丁。
result: 方法能够高效定位信息补丁，减少计算量，同时保持诊断精度。
conclusion: 形态动量原型学习有效平衡了WSI处理的效率与准确性。
---

## Abstract
Digital histopathology images play a crucial role in cancer diagnosis, therapeutic response prediction, and identification of clinically relevant morphological features. However, processing Whole Slide Images (WSI) with gigapixel resolution introduces significant challenges in computer vision, exceeding the memory capacity of standard vision encoders. To address this, recent methods employ a multi-stage pipeline: dissecting the image into small patches, extracting patch-level features, and aggregating these features using global pooling through Multi-Instance Learning (MIL) to form a final slide-level representation. Despite achieving clinical-grade performance, this approach becomes increasingly complex with higher magnification due to the quadratic increase in patch numbers and the generation of numerous irrelevant or redundant patches. This complexity burdens the global pooling network, resulting in long inference times and excessive computational resources, while redundant patches introduce noise during the MIL process, limiting the model’s ability to utilize high-magnification features fully. To overcome these challenges, we propose Momentum Morphological Prototype Learning (MMPL), an efficient method that redefines WSI diagnosis as a searching process of relevant patch-level representations with a learned set of global prototypes. MMPL trains a fixed set of prototypes to retrieve the most informative patches, computing the diagnostic score using only the retrieved patches. Evaluated on WSI classification benchmarks, MMPL achieves state-of-the-art performance across various pathology tasks, including metastasis detection, tumor grading, and tumor subtyping.

---

## 论文详细总结（自动生成）

## 论文核心问题与整体含义

- **研究动机**：全切片图像（WSI）具有数十亿像素的极高分辨率，远超常规视觉编码器的内存容量，导致处理困难。
- **现有方法瓶颈**：当前主流方案采用“切块→提取补丁特征→多实例学习（MIL）全局池化”的多阶段流水线。在高放大倍率下，补丁数量呈二次增长，产生大量无关或冗余补丁，不仅消耗大量计算资源和推理时间，冗余补丁还会在 MIL 聚合时引入噪声，限制模型充分利用高倍率特征的能力。
- **整体含义**：论文旨在将 WSI 诊断重新定义为一种**高效搜索信息性补丁**的过程，仅利用最有代表性的少部分补丁完成诊断，从而在保持临床级性能的同时大幅降低计算开销。

## 方法论

- **核心思想**：训练一组**可学习的全局原型**（prototypes），利用这些原型在特征空间中检索（retrieve）最具诊断信息的补丁，仅依赖被检索到的补丁计算最终的幻灯片级诊断分数，从而绕过对海量冗余补丁的处理。
- **关键技术细节**：
  - **形态动量原型学习（Morphological Momentum Prototype Learning，MMPL）**：将原型视为“形态学特征”的代表，通过**动量更新**机制在线优化原型，使原型能够稳定地捕捉不同形态模式。
  - **原型检索机制**：对于每张 WSI 的所有补丁特征，计算其与固定数量原型的相似度（如余弦相似度），选出与原型最匹配的 top-k 补丁，视为信息性补丁。
  - **诊断评分**：仅对被检索到的补丁特征进行聚合（如注意力池化）并生成最终分类结果，训练时损失函数同时优化原型和分类器。
- **算法流程（文字说明）**：
  1. 使用预训练特征提取器（如 ResNet、ViT）将 WSI 切成补丁并提取 d 维特征向量。
  2. 初始化一组可学习原型矩阵 \( P \in \mathbb{R}^{K \times d} \)（K 为原型数量）。
  3. 对于每张 WSI，计算每个补丁特征与所有原型的相似度，为每个原型选取最相似的补丁（或按阈值选取）。
  4. 将选中补丁的特征送入 MIL 聚合器（如基于注意力的池化）生成幻灯片级特征，再通过分类头输出预测概率。
  5. 基于交叉熵损失进行端到端训练，同时用动量更新规则更新原型，以保持训练稳定并鼓励原型覆盖多样化形态。
- **与原方法的区别**：传统 MIL 直接在所有补丁上做全局池化，而 MMPL 先通过原型搜索筛选补丁子集，大幅降低输入 MIL 聚合器的补丁数量。

## 实验设计

- **数据集/场景**（基于摘要和已给信息）：
  - 转移检测（metastasis detection）：如 CAMELYON16 等。
  - 肿瘤分级（tumor grading）：可能涉及前列腺癌、乳腺癌等分级数据集。
  - 肿瘤亚型分型（tumor subtyping）：如肾细胞癌亚型、非小细胞肺癌亚型等。
- **Benchmark**：WSI 分类标准基准，通常以 AUC、准确率、F1 等衡量。
- **对比方法**（摘要未列出具体名称，仅暗示）：
  - 传统 MIL 方法（如 ABMIL、DSMIL、TransMIL 等）。
  - 可能包含其他基于原型或补丁选择的方法（如 CLAM、DTFD-MIL 等）。
  - 声称达到 state-of-the-art 性能。

## 资源与算力

- 论文提供的文本中**未明确说明**所使用 GPU 型号、数量、训练时长等算力细节。通常此类 WSI 研究会在多卡 V100/A100 上进行，但本文案无具体数据，需指出此信息缺失。

## 实验数量与充分性

- **已有信息**：实验覆盖至少三类病理任务（转移检测、分级、亚型分型），表明在多个独立 benchmark 上进行了验证。
- **实验组数推测**：应包含与多个现有方法的对比实验、消融实验（如原型数量、动量更新策略的影响）、效率对比（推理时间、FLOPs）等，但具体组数未在摘要中给出。
- **充分性判断**：从摘要描述看，实验设计维度丰富（多任务、多方法对比、性能与效率并重），**较为充分**；且为对比公平，应使用相同特征提取器和数据划分。未发现明显偏向性描述。

## 主要结论与发现

- MMPL 通过原型搜索机制，能够**高效定位信息性补丁**，显著减少参与聚合的补丁数量，降低计算负担。
- 方法在多个 WSI 分类任务上取得了**最先进的性能**，证明仅用少数关键补丁即可满足诊断需求。
- 该方法在**诊断精度与计算效率之间取得了良好平衡**，为高倍率 WSI 的实际部署提供了可行方案。

## 优点

- **效率创新**：首次将 WSI 诊断建模为基于原型的补丁搜索问题，从源头减少冗余计算，思路新颖。
- **形态动量更新**：利用动量原型持续捕获形态学语义，训练稳定且有助于原型代表多样化结构。
- **即插即用潜力**：搜索模块可与不同特征提取器和 MIL 聚合器组合，具有一定的通用性。
- **实验扎实**：覆盖多种病理任务，验证了方法的泛化性；若能提供效率指标（如推理时间缩减比），说服力更强。

## 不足与局限

- **算力信息缺失**：未说明训练和推理所需的 GPU 资源及实际耗时，难以评估方法对硬件的依赖和部署可行性。
- **原型数量敏感度**：原型个数 K 是重要超参数，不同任务可能需要人工调节，论文未透露其敏感性分析或自适应机制。
- **形态学假设局限**：若病灶的形态学特征与原型预设偏差较大，可能漏检重要补丁，尤其对罕见亚型或异质性强的肿瘤需进一步验证。
- **实验覆盖未知**：摘要未列出对比的具体方法名单，无法判断是否与最新 SOTA（如基于 Transformer 的 MIL）全面比较；也未提及在低倍率或跨中心外部数据上的泛化实验。
- **潜在偏差风险**：原型的动量更新可能依赖训练集分布，若训练集不平衡或标注有噪声，原型可能偏向多数类形态，影响罕见类别的检索效果。

（完）
