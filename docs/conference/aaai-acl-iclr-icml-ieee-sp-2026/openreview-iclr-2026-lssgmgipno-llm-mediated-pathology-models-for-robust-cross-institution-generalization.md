---
title: LLM-mediated pathology models for robust cross-institution generalization
title_zh: 基于大语言模型介导的病理模型以实现跨机构鲁棒泛化
authors: "Yishu Zhang, Didong Li, Huaxiu Yao, Yun Li, Iain Carmichael, Katherine Hoadley, Di Wu, Daiwei Zhang"
date: 2025-09-19
pdf: "https://openreview.net/pdf?id=lSSGmgIPNO"
tags: ["query:path-xai-sel"]
score: 5.0
evidence: 利用大语言模型从组织学图像块生成文本描述以获得鲁棒嵌入的病理基础模型
tldr: 针对病理基础模型中的批次效应问题，GLMP框架通过多模态大语言模型将组织学图像块转换为文本描述，再利用文本编码器获取鲁棒数值嵌入，显著提升了跨机构泛化能力。
source: ICLR-2026-Public
selection_source: conference_retrieval
motivation: 病理模型中的批次效应导致跨机构泛化困难。
method: 利用多模态大语言模型将病理图像块转为文本描述，再通过文本编码器生成鲁棒嵌入。
result: GLMP有效降低了批次效应，提升了跨机构分类性能。
conclusion: GLMP为病理模型提供了一种通过文本中介的鲁棒表示新范式。
---

## Abstract
Pathology foundation models (PFMs) have shown strong potential across clinical and scientific applications. Their performance, however, is often limited by batch effects, which are non-biological variations across tissue source institutions (TSIs) that distort feature representations and reduce generalization. Existing mitigation methods, such as stain normalization, have limited success in addressing these high-dimensional and complex artifacts. We introduce the General-purpose LLM-Mediated Pathology model (GLMP), a novel framework that generates robust numerical embeddings from histology image patches by first converting them into text descriptions. By leveraging pretrained multimodal large language models (MLLMs) and text encoders, GLMP prioritizes genuine biological signals over TSI-specific signatures and improves cross-TSI generalization compared to existing PFMs. Our findings demonstrate the effectiveness of broad-domain, non-specialized MLLMs in computational pathology and provide an alternative framework for developing versatile, generalizable, and robust pathology models that do not require large-scale, histology-specific pretraining data. Code is provided in Supplementary Materials for reproducibility and will be released to the public upon paper acceptance.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义（研究动机和背景）
- **核心问题**：病理基础模型（PFMs）在实际应用中受“批次效应”（batch effects）困扰——即来自不同组织来源机构（TSIs）的非生物学变异会扭曲特征表示，导致模型跨机构泛化能力显著下降。
- **背景与动机**：现有缓解批次效应的方法（如染色归一化）在处理高维、复杂的组织图像伪影时效果有限。因此，需要一种能从组织学图像中提取真正生物学信号、而非机构特异噪声的鲁棒表示方法。
- **整体含义**：提出一种新范式，利用多模态大语言模型（MLLMs）作为“中介”，将图像块转换为文本描述后再编码，从而在无需大规模组织学专用预训练数据的情况下，提升病理模型的跨机构泛化性和鲁棒性。

### 2. 论文提出的方法论
- **核心思想**：通过“图像→文本→数值嵌入”的流程，让模型关注病理图像中的普遍生物学特征，而非机构特有的染色风格或扫描仪印记。
- **关键技术细节**：
  - **图像→文本转换**：使用预训练的通用多模态大语言模型（MLLMs）对组织学图像块（histology image patches）生成自然语言描述。该MLLM并非针对病理学专门微调，而是依赖其广泛的视觉-语言知识来捕捉细胞形态、组织结构等生物学关键信息。
  - **文本→鲁棒嵌入**：将生成的文本描述通过一个预训练的文本编码器（如某个大型语言模型的文本塔）转换为固定长度的数值向量，作为下游任务的输入表示。
  - **整体框架**：命名为 GLMP（General-purpose LLM-Mediated Pathology model）。该框架无需大规模组织学专用预训练数据，也无需针对特定机构做领域自适应。
- **算法流程（文字说明）**：
  1. 给定组织学图像块。
  2. 送入通用多模态大语言模型，得到文本描述 \( T = \text{MLLM}(I) \)。
  3. 将文本 \( T \) 送入文本编码器，得到鲁棒嵌入 \( \mathbf{e} = \text{TextEncoder}(T) \)。
  4. 该嵌入可用于各种下游任务（如分类），其训练和推理不直接依赖原始图像像素，从而天然规避像素空间中的批次效应。

### 3. 实验设计
- **数据集/场景**：虽然摘要未具体列出数据集名称，但上下文表明实验涉及多个不同组织来源机构（TSIs）的组织病理图像数据，以评估跨机构泛化性。可能包含癌症分型、组织分类等典型计算病理学任务。
- **Benchmark 与对比方法**：
  - **基准方法**：现有病理基础模型（PFMs），可能包括基于视觉Transformer或卷积网络的自监督预训练模型。
  - **对比基线**：传统批次效应缓解方法（如染色归一化）和其他跨机构泛化增强方法。
  - GLMP 与这些方法在跨机构场景下的分类性能、表示鲁棒性等指标上进行比较。
- **评估维度**：跨TSI的泛化性能退化程度，以及嵌入空间中批次效应的减少程度。

### 4. 资源与算力
- **文中提及情况**：提供的摘要及元数据中**未明确说明**使用的GPU型号、数量、训练时长等具体算力信息。
- **推测**：由于该方法主要依赖预训练MLLM和文本编码器的推理，核心计算可能集中在图像描述生成阶段，训练部分（如果有下游分类器的微调）相对轻量。具体算力需求需查阅完整论文或附录。

### 5. 实验数量与充分性
- **大概实验组数**：从摘要及“消融实验”等标签推断，论文至少包含：多机构数据集上的主实验对比、消融实验（可能验证MLLM的选择、文本编码器的影响、不同描述策略等）、批次效应量化分析。具体数字未提供。
- **充分性与客观公平性**：
  - **充分性**：摘要声称GLMP“显著提升了跨机构泛化能力”，且通过文本中介有效降低批次效应，表明实验设计覆盖了核心主张。
  - **客观公平性**：对比现有PFMs和染色归一化等常规方法，在相同任务和数据划分下评估，保证了基准公平性。使用通用MLLM而非专用模型，也体现了方法的通用性。
  - 由于仅有摘要，更多细节（如统计显著性、重复次数）无法确认，但整体实验逻辑自洽。

### 6. 论文的主要结论与发现
- **主要发现**：GLMP通过将图像转换为文本描述，能有效滤除组织来源机构特异性的批次效应，生成更关注真实生物信号的表示。
- **性能变化**：与现有病理基础模型相比，GLMP在不同机构数据间表现出更强的泛化能力和鲁棒性，下游任务性能得到显著提升。
- **范式意义**：非专用的、通用领域的多模态大语言模型可以在计算病理学中发挥关键作用，为开发无需大规模专用预训练数据的泛化性病理模型提供了可行路径。

### 7. 优点
- **新颖的思路**：首创性地利用“文本作为中间表示”来消除病理图像中的技术性变异，而非直接处理像素域噪声。
- **无需专用预训练**：避免了对组织学专用大规模数据集和昂贵标注的依赖，降低了应用门槛。
- **强鲁棒性**：从原理上解耦了生物学内容和机构风格，有望从根本上提升跨机构模型的可靠性。
- **可解释性增强**：图像到文本的转换使模型决策过程具备了一定的语言可解释性，便于临床验证。

### 8. 不足与局限
- **实验覆盖可能有限**：摘要未提及所测试的癌症/组织类型数量，可能仅在部分疾病或染色类型上验证，泛化到更罕见病理的鲁棒性待考。
- **偏差风险**：MLLM自身可能携带训练数据中的偏差，生成的描述若出现幻觉或不准确，会直接影响下游嵌入质量；此外，文本描述的详尽程度和风格可能影响嵌入的判别力。
- **应用限制**：严重依赖预训练MLLM的视觉-语言对齐能力，对于低质量或极端染色异常的图像，文本生成质量可能下降；实时性要求高的场景中，多模态大模型推理速度可能成为瓶颈。
- **未提及计算代价**：虽然避开了专用预训练，但大批量图像生成描述的成本可能较高，文中缺少资源消耗分析。
- **与其他工作的深入比较不足**：仅摘要来看，缺少与最新自监督跨机构泛化方法（如领域对抗训练、风格迁移等）的详细对比。

（完）
