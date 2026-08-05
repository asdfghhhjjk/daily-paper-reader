---
title: Transitive Representation Learning Enhances Histopathology Annotation
title_zh: 传递性表示学习增强组织病理学标注
authors: "Moritz Schaefer, Zoe Piran, Nils Philipp Walter, Animesh Awasthi, Christoph Bock, Jure Leskovec, Zinaida Good"
date: 2026-04-30
pdf: "https://openreview.net/pdf/5633e8d66627583698d6fffa502376d7f9347d92.pdf"
tags: ["query:tme-evidence"]
score: 8.0
evidence: 通过三模态对比学习实现组织病理图像零样本细胞类型标注
tldr: 针对组织病理标注缺乏细胞身份细粒度信息的问题，提出三模态模型SpatialWhisperer，融合图像、基因表达和文本实现零样本细胞类型标注，提升了注释精度。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 现有组织病理AI受限于粗粒度标注，忽略细胞身份。
method: 利用空间基因表达和单细胞数据，通过三模态对比学习实现传递性表示。
result: 准确进行零样本细胞类型标注。
conclusion: 为组织病理图像提供了精确的细胞级自动标注方案。
---

## Abstract
The characterization of histopathology with AI promises to assist clinical decision-making, but it is currently limited due to coarse-grained annotations that miss cellular identities. To overcome this gap, we bridge histopathological images, gene expression profiles, and natural-language descriptions using *SpatialWhisperer*, a trimodal contrastive learning model. Our training integrates community-scale datasets comprising spatially resolved gene expression profiles paired with histopathology images, as well as single-cell gene expression profiles with detailed annotations. The shared gene expression modality implies a transitive relationship between images and textual annotations, which our method leverages to enable accurate zero-shot cell type annotation directly from H&E images. *SpatialWhisperer* outperforms published baselines, achieving relative AUROC gains of up to 15.9% across three benchmarks spanning 19 tissues and 20 cell types. When training with data from all three modality pairs, we observe performance gains in low-data regimes. We formalize our approach and present a sufficient condition under which this transitive alignment is induced. Our work establishes *transitive representation learning* for fine-grained interpretation of histopathology images.

---

## 论文详细总结（自动生成）

# 论文总结：传递性表示学习增强组织病理学标注

## 1. 论文的核心问题与整体含义

- **研究动机**：人工智能辅助组织病理学分析具有临床决策潜力，但目前受限于标注粒度粗糙，现有的感兴趣区域级或切片级标签往往忽略图像中细胞的身份信息（如具体属于哪种细胞类型），无法实现精细的细胞级解读。
- **整体含义**：本文提出利用“传递性表示学习”来解决这一瓶颈。通过引入空间基因表达数据作为桥梁，将组织病理图像与细胞类型文本描述连接起来，实现仅凭常规H&E染色图像即可进行零样本的细胞类型标注，从而大幅提升组织病理学图像的注释精度和效率。

## 2. 论文提出的方法论

- **核心思想**：建立一个三模态对比学习框架，共享基因表达模态，利用图像-基因表达、基因表达-文本的对齐关系，间接推导出图像与文本之间的对齐关系（即传递性对齐），使模型能够直接从H&E图像识别细胞类型。
- **关键技术细节**：
  - 模型名为**SpatialWhisperer**，采用三模态对比学习。
  - 训练数据包括：
    1. 空间分辨的基因表达谱与配对的组织病理图像。
    2. 单细胞基因表达谱及其详细的细胞类型文本标注。
  - 共享的基因表达模态充当中间表示，使得图像与文本之间形成传递关系。模型学习将图像嵌入、基因表达嵌入、文本嵌入映射到统一空间，迫使图像嵌入靠近对应细胞类型的文本描述。
  - 作者对该传递性对齐给出了形式化的充分条件，证明在何种情况下可以诱导这种对齐。
- **算法流程概览**（文字说明）：输入为H&E图像块和空间基因表达矩阵，以及单细胞基因表达矩阵和对应的细胞类型标签。模型通过图像编码器、基因编码器、文本编码器分别提取嵌入，使用对比损失使得匹配的三元组（图像、基因、文本）嵌入相近，不匹配的嵌入远离。训练完成后，对于新图像，只需通过图像编码器和文本编码器即可进行零样本细胞类型预测（比较图像嵌入与所有候选文本嵌入的相似度）。

## 3. 实验设计

- **数据集/场景**：
  - 使用了社区规模的数据集，包括空间转录组学配对组织病理图像的数据，以及带有细胞类型标注的单细胞基因表达数据。
  - 三个基准测试集，覆盖19种组织和20种细胞类型。
- **对比方法**：与已发表的基线模型进行比较，具体名称未在摘要中列出，但可推测包括现有的组织图像分类或视觉-语言模型。
- **评估指标**：主要采用AUROC（受试者工作特征曲线下面积），报告相对提升。

## 4. 资源与算力

- **未明确说明**：摘要及元数据中未提及使用的GPU型号、数量、训练时长等算力细节。需要查阅原文补充。

## 5. 实验数量与充分性

- **实验组数**：
  - 至少在3个不同的基准数据集上进行了评估。
  - 涵盖19种组织和20种细胞类型。
  - 包含消融实验（如分析使用不同模态组合训练的影响，观察到在低数据量场景下使用全部三模态对的性能增益）。
- **充分性与客观性**：实验设计较为全面，覆盖多组织、多细胞类型，与已有基线对比，且考察了数据效率，相对客观公平。但补充细节需进一步阅读原文判断（如交叉验证、统计检验等）。

## 6. 论文的主要结论与发现

- SpatialWhisperer能够实现精确的零样本细胞类型标注，仅需H&E图像输入，无需对应组织的基因或文本信息。
- 在多个基准上性能显著优于已发表基线，AUROC相对提升高达15.9%。
- 利用所有三种模态对进行训练，可在低数据量场景下获得性能提升，体现了传递性学习的数据效率。
- 这一工作为组织病理学图像的细粒度解释建立了传递性表示学习范式。

## 7. 优点

- **创新性强**：首次将传递性表示学习引入组织病理学，利用基因表达作为共享桥梁实现图像与文本的对齐。
- **实用价值高**：零样本标注能力意味着无需为每种细胞类型预先收集大量标注数据，显著降低人工标注成本。
- **实验扎实**：多组织、多细胞类型验证，与基线全面对比，并给出性能边界和条件证明。
- **理论支撑**：提供了传递性对齐的充分条件，增加方法论的可信度。

## 8. 不足与局限

- **算力与开销不明**：未说明训练所需计算资源，难以评估实际部署的可行性。
- **数据依赖**：训练依赖空间转录组学和单细胞数据，这些数据获取成本较高，可能限制模型在不同实验室或罕见组织上的扩展。
- **零样本的局限性**：零样本性能可能依赖于训练时见过的细胞类型或基因表达模式，对全新或稀有细胞类型的泛化能力待进一步验证。
- **实验覆盖**：目前仅在19种组织上验证，对于更多疾病状态、病理变异或染色差异的鲁棒性未知。
- **偏差风险**：若单细胞参考数据存在批次效应或标注偏差，可能通过基因表达模态传递至图像模型，导致预测偏差。

（完）
