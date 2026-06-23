---
title: "ConceptAttention: Diffusion Transformers Learn Highly Interpretable Features"
title_zh: "ConceptAttention: 扩散变换器学习高度可解释的特征"
authors: "Alec Helbling, Tuna Han Salih Meral, Benjamin Hoover, Pinar Yanardag, Duen Horng Chau"
date: 2025-05-01
pdf: "https://openreview.net/pdf?id=Rc7y9HFC34"
tags: ["query:pathology-ai"]
score: 5.0
evidence: 来自扩散变换器的可解释显著性图
tldr: ConceptAttention利用扩散变换器的注意力层生成高质量显著性图，精确定位图像中的文本概念，无需额外训练。该方法在可解释性任务上达到最优，可应用于病理图像中概念定位的可解释分析。
source: ICML-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-icml-2025-rc7y9hfc34/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 845, \"height\": 1139, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-rc7y9hfc34/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1681, \"height\": 538, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-rc7y9hfc34/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1775, \"height\": 464, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-rc7y9hfc34/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1752, \"height\": 398, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-rc7y9hfc34/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 815, \"height\": 758, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-rc7y9hfc34/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1698, \"height\": 527, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-rc7y9hfc34/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 817, \"height\": 535, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-rc7y9hfc34/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 815, \"height\": 533, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-rc7y9hfc34/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1706, \"height\": 766, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-rc7y9hfc34/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1775, \"height\": 542, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-rc7y9hfc34/fig-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1751, \"height\": 853, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-rc7y9hfc34/fig-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1495, \"height\": 922, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-rc7y9hfc34/fig-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 1505, \"height\": 925, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-rc7y9hfc34/fig-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 1786, \"height\": 385, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-rc7y9hfc34/fig-015.webp\", \"caption\": \"\", \"page\": 0, \"index\": 15, \"width\": 1782, \"height\": 382, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-rc7y9hfc34/fig-016.webp\", \"caption\": \"\", \"page\": 0, \"index\": 16, \"width\": 1680, \"height\": 683, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-rc7y9hfc34/fig-017.webp\", \"caption\": \"\", \"page\": 0, \"index\": 17, \"width\": 1622, \"height\": 2016, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-rc7y9hfc34/fig-018.webp\", \"caption\": \"\", \"page\": 0, \"index\": 18, \"width\": 1622, \"height\": 2018, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-icml-2025-rc7y9hfc34/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1699, \"height\": 822, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-rc7y9hfc34/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 627, \"height\": 243, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-rc7y9hfc34/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 739, \"height\": 311, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-rc7y9hfc34/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 658, \"height\": 244, \"label\": \"Table\"}]"
motivation: 扩散变换器的丰富表示是否具有独特的可解释性特性尚不清楚。
method: 重用DiT注意力层参数生成概念嵌入，通过线性投影获得清晰显著性图。
result: 在多个基准上取得最先进的可解释性性能。
conclusion: ConceptAttention展示了扩散变换器在可解释AI中的潜力，可迁移至医学图像。
---

## Abstract
Do the rich representations of multi-modal diffusion transformers (DiTs) exhibit unique properties that enhance their interpretability? We introduce ConceptAttention, a novel method that leverages the expressive power of DiT attention layers to generate high-quality saliency maps that precisely locate textual concepts within images. Without requiring additional training, ConceptAttention repurposes the parameters of DiT attention layers to produce highly contextualized *concept embeddings*, contributing the major discovery that performing linear projections in the output space of DiT attention layers yields significantly sharper saliency maps compared to commonly used cross-attention maps. ConceptAttention even achieves state-of-the-art performance on zero-shot image segmentation benchmarks, outperforming 15 other zero-shot interpretability methods on the ImageNet-Segmentation dataset. ConceptAttention works for popular image models and even seamlessly generalizes to video generation. Our work contributes the first evidence that the representations of multi-modal DiTs are highly transferable to vision tasks like segmentation.

---

## 论文详细总结（自动生成）

# ConceptAttention：扩散变换器学习高度可解释的特征 —— 中文详细总结

## 1. 核心问题与整体含义

- **研究动机**：多模态扩散变换器（DiTs）在文本到图像生成中取得了突破，但其内部工作机制仍不透明，缺乏有效的可解释性工具。现有解释方法大多针对UNet架构，而对DiT的潜力挖掘不足。
- **整体含义**：本文首次系统性地探索了DiT注意力层表示的可解释性，并提出无需额外训练的方法生成高质量显著性图，揭示了DiT特征在视觉任务（如零样本分割）中的强迁移能力。

## 2. 方法论

- **核心思想**：通过在DiT的多模态注意力层中注入一组“概念嵌入”（concept embeddings），并利用单向注意力机制（仅概念关注图像和其他概念，但图像不影响概念），在不改变生成结果的前提下获取与文本概念高度对应的上下文特征。
- **关键技术细节**：
  - **概念嵌入初始化**：用户指定的若干单token概念（如“cat”、“sky”）经T5编码器获得初始嵌入，并作为独立残差流与图像、文本流并行。
  - **单向注意力操作**：使用文本提示的投影矩阵（Query、Key、Value）对概念嵌入进行投影，然后让概念查询图像token和概念token自身（自注意力和交叉注意力混合），但图像/文本流完全忽略概念token，保证原始生成不变。
  - **显著性图生成**：取各层概念的输出向量与图像输出向量的点积相似度，经softmax得到每层显著性图，最后对所有层取平均。该“输出空间”方法显著优于传统的交叉注意力图。
- **算法流程**（文字说明）：
  - 输入图像、文本提示、概念列表。
  - 前向传播时，在每个多模态注意力层中：
    - 计算图像和文本的 K、Q、V。
    - 使用文本投影矩阵计算概念的 K、Q、V。
    - 图像和文本进行标准自注意力。
    - 概念与图像/概念拼接后的序列进行注意力（概念查询），得到更新后的概念输出。
    - 应用残差连接、调制层和MLP。
  - 缓存所有层的图像输出和概念输出。
  - 逐层计算点积相似度并平均，得到最终显著性图。

## 3. 实验设计

- **数据集与场景**：
  - **ImageNet-Segmentation**（4276张图像，445个类别，每图主要单对象）。
  - **PascalVOC 2012**：单类子集（930张图像）和多类子集（1449张图像）。
- **基准与评估指标**：像素级准确率（Acc）、平均交并比（mIoU）、平均精度（mAP）。
- **对比方法**（共15种以上）：
  - **CLIP ViT系列**：LRP、Partial-LRP、Rollout、Raw Attention、GradCAM、TextSpan、TransInterp、CLIPasRNN。
  - **DINO系列**：DINOv1、DINOv2、DINOv2 with registers、iBOT。
  - **UNet扩散模型**：DAAM（SDXL、SD2）、OVAM。
  - **DiT基线**：Flux/SD3.5原生交叉注意力。
- **额外验证**：在CogVideoX视频生成DiT模型上进行了定性比较。

## 4. 资源与算力

- **文中未明确说明**：论文没有提及训练所需的具体GPU型号、数量或训练时长（因为ConceptAttention本身无需训练，仅推理阶段使用预训练DiT模型）。实验基于Flux-Schnell、SD3.5 Turbo和CogVideoX等公开模型，推理在单GPU上即可完成，但未提供详细硬件规格。致谢中提到了NSF、Cisco、Google、Amazon、Meta、NVIDIA等支持，但未量化算力。

## 5. 实验数量与充分性

- **大量定量实验**：
  - 主要对比15+方法在两个数据集上的三个指标，包含单类和多种类分割。
  - 消融实验：不同层深度（图7）、不同扩散时间步（图7）、不同注意力操作（仅交叉/仅自/两者，表4）、不同表示空间（交叉注意力、值空间、输出空间，表3）、是否应用softmax（表3）。
  - 额外定性结果：多概念同时定位（图3、图11-14）、视频帧级显著性（图8、16-17）。
- **充分性与公平性**：实验设置遵循已有工作（TextSpan、TransInterp）的标准协议，对比方法覆盖主流可解释性基线，且所有基线均采用相同的数据集划分和预处理。消融实验系统性地拆解了各组件贡献，结论可靠。

## 6. 主要结论与发现

- **发现1**：DiT注意力层的输出空间（而非交叉注意力图）可生成更清晰、更准确的显著性图，这一特性是UNet架构所不具备的。
- **发现2**：ConceptAttention在零样本分割任务上全面超越15种现有可解释方法，在ImageNet-Segmentation上达到Acc 83.07%、mIoU 71.04%、mAP 90.45%，在PascalVOC多类场景下优势更显著（**表1、表2**）。
- **发现3**：中层（而非最深层）扩散时间步和深层（而非浅层）注意力层贡献最大，融合所有层效果最佳（**图7**）。
- **发现4**：方法无缝推广至视频生成模型（CogVideoX），生成帧级显著性图优于原生交叉注意力。
- **核心贡献**：提供首个强有力证据表明多模态DiT的表示高度可迁移至视觉分割任务，并开辟了无需训练的可解释性新路径。

## 7. 优点

- **无需训练**：完全重用预训练DiT参数，零额外训练成本，推理开销极小。
- **架构通用**：适用于Flux、SD3.5、CogVideoX等多种MMDiT架构。
- **开集支持**：可对任意文本概念生成显著性图，不受限于原始提示。
- **高质量显著性图**：视觉效果清晰，在多重语义边界模糊时仍能精准定位（图4、10-14）。
- **方法论创新**：提出“输出空间投影”替代“注意力图”，并验证自+交叉联合注意力的优势。
- **全面评估**：涵盖单类、多类、视频场景，消融实验系统，对比方法多样，结论稳健。

## 8. 不足与局限

- **语义重叠困难**：对于高度相似的概念（如“太阳”与“天空”），难以精确分割边界，会产生模糊的“光晕”效应（图6）。
- **负样本处理**：当图像中不包含任何目标概念时，模型仍会选最相似的概念，导致误检（图15）。
- **依赖单token概念**：论文使用简化的单token概念名称（如“dog”），对于需要多token描述的精细类别（如“golden retriever”）效果可能下降。
- **计算资源未公开**：虽无需训练，但推理时需缓存所有层的输出，对于高分辨率或长视频可能增加内存开销。
- **仅评估分割任务**：虽展示了可解释性，但未验证在其他下游任务（如编辑、反事实解释）上的有效性。
- **可迁移性边界**：结论主要基于Flux和SD3.5架构，是否适用于其他MMDiT变体（如PixArt-α）有待验证。

（完）
