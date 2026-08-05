---
title: Transitive Representation Learning Enhances Histopathology Annotation
title_zh: 传递表示学习增强组织病理学注释
authors: "Moritz Schaefer, Zoe Piran, Nils Philipp Walter, Animesh Awasthi, Christoph Bock, Jure Leskovec, Zinaida Good"
date: 2026-04-30
pdf: "https://openreview.net/pdf/5633e8d66627583698d6fffa502376d7f9347d92.pdf"
tags: ["query:cellseg"]
score: 9.0
evidence: 在组织病理图像上实现零样本细胞类型注释，无需直接标签进行细胞分类。
tldr: 该论文提出SpatialWhisperer模型，通过三模态对比学习桥接组织病理图像、基因表达谱和自然语言描述，利用传递关系实现组织病理图像的零样本细胞类型注释。模型在没有任何细胞级标签的情况下，准确地识别细胞身份，为精细组织病理分析提供了新范式。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 当前组织病理学AI受限于粗糙的注释，缺失细胞身份信息。
method: 利用空间转录组和单细胞基因表达数据，通过三模态对比学习实现图像到文本的传递表示。
result: 模型在零样本条件下准确注释细胞类型，超越现有方法。
conclusion: 传递学习为组织病理图像提供精确的细胞级注释，推动临床辅助诊断。
---

## Abstract
The characterization of histopathology with AI promises to assist clinical decision-making, but it is currently limited due to coarse-grained annotations that miss cellular identities. To overcome this gap, we bridge histopathological images, gene expression profiles, and natural-language descriptions using *SpatialWhisperer*, a trimodal contrastive learning model. Our training integrates community-scale datasets comprising spatially resolved gene expression profiles paired with histopathology images, as well as single-cell gene expression profiles with detailed annotations. The shared gene expression modality implies a transitive relationship between images and textual annotations, which our method leverages to enable accurate zero-shot cell type annotation directly from H&E images. *SpatialWhisperer* outperforms published baselines, achieving relative AUROC gains of up to 15.9% across three benchmarks spanning 19 tissues and 20 cell types. When training with data from all three modality pairs, we observe performance gains in low-data regimes. We formalize our approach and present a sufficient condition under which this transitive alignment is induced. Our work establishes *transitive representation learning* for fine-grained interpretation of histopathology images.

---

## 论文详细总结（自动生成）

# 论文详细总结：传递表示学习增强组织病理学注释

## 1. 论文的核心问题与整体含义
- **核心问题**：当前组织病理学人工智能分析受限于粗略的注释（如组织区域标签），无法获取精确的细胞身份信息（例如“肿瘤细胞”、“T细胞”），这限制了辅助临床决策的能力。
- **整体含义**：作者提出利用一种**传递表示学习**方法，通过共享的基因表达模态桥接组织病理图像与自然语言描述，实现在没有直接细胞级标签的情况下对H&E染色图像进行零样本细胞类型注释，从而为组织病理提供更精细的解读。

## 2. 论文提出的方法论
- **核心思想**：构建一个三模态对比学习模型——**SpatialWhisperer**，通过整合三类数据来学习统一表示：
  - 空间分辨的基因表达谱与配对的H&E组织病理图像；
  - 带有详细细胞类型注释的单细胞基因表达谱；
  - 自然语言描述（如细胞类型名称）。
  - 由于图像与单细胞数据都共享基因表达这一模态，便自然形成“图像 ↔ 表达谱 ↔ 文本”的**传递关系**，使模型无需图像-文本直接配对即可对齐图像与文本。
- **关键技术细节**：
  - 使用对比学习将三个模态分别映射到共享嵌入空间。
  - 训练时利用成对的（图像，基因表达）和（基因表达，文本）数据。
  - 推理时，直接计算图像嵌入与文本嵌入的相似度，实现零样本细胞类型识别。
- **理论贡献**：给出这种传递对齐成立的充分条件。

## 3. 实验设计
- **数据集/场景**：使用了社区规模的公开数据集：
  - 空间转录组学数据（包含H&E图像与基因表达）；
  - 单细胞基因表达数据集（带有细胞类型注释）。
- **基准评测**：在三个基准测试上进行评估，覆盖**19种组织**和**20种细胞类型**。
- **对比方法**：与已发表的基线方法对比（具体方法名称未在摘要中列出，但提及“published baselines”），SpatialWhisperer取得了高达15.9%的相对AUROC增益。
- **消融分析**：考察了使用全部三种模态对训练时的性能提升，尤其是在数据量较少的情况下。

## 4. 资源与算力
- **未明确说明**：提供的摘要中未提及所使用的GPU型号、数量或训练时长。元数据及摘要部分均无相关描述。

## 5. 实验数量与充分性
- **实验数量**：摘要提到在**三个基准测试**上进行了评估，涉及多组织、多细胞类型；同时进行了低数据条件下的性能对比。从描述推断，至少包含了跨多种组织、多种细胞类型的全面对比以及数据效率分析，但具体实验总数未给出。
- **充分性与公平性**：与已发表基线进行对比，并报告了相对AUROC提升，对比看似公平；但缺乏对基线的具体描述，无法判断是否涵盖了最相关的方法。跨组织、跨细胞类型的范围较广，有助于验证泛化性。在无完整论文的情况下，只能认为实验设计较为充分。

## 6. 论文的主要结论与发现
- SpatialWhisperer能够**在没有细胞级标签的情况下**实现准确的细胞类型注释，性能优于现有基线。
- 利用多模态配对数据训练时，**低数据量场景下性能提升明显**。
- 通过形式化分析，给出传递对齐成立的充分条件，从理论上支持该方法。
- 传递表示学习为组织病理图像的细粒度解读开辟了新范式。

## 7. 优点
- **新颖的模态桥接方式**：通过基因表达作为中间模态实现图像与文本的零样本对齐，摆脱了对昂贵细胞级标注的依赖。
- **理论支撑**：不仅提出方法，还给出对齐成立的充分条件，增加方法可信度。
- **广泛的验证**：跨多种组织、多种细胞类型评估，且与已发表方法对比，结果显著。
- **数据高效**：在少量数据下仍可受益于多模态训练。

## 8. 不足与局限
- **实验覆盖的细节缺失**：摘要未提供基线方法的具体名称、每个数据集的具体规模、消融实验的详细结果，难以独立评判实验的严格程度。
- **可能的偏差风险**：依赖空间转录组和单细胞数据的质量与代表性；跨数据集的分布偏移可能影响零样本性能。
- **应用限制**：目前仅在H&E图像上验证；实际临床部署还需要考虑染色变异、扫描仪差异等因素。
- **算力需求不明**：未报告资源消耗，不利于复现或成本评估。

（完）
