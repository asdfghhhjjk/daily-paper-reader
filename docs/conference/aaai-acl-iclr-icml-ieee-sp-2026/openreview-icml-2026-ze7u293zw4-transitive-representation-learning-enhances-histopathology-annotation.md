---
title: Transitive Representation Learning Enhances Histopathology Annotation
title_zh: 传递表示学习增强组织病理学注释
authors: "Moritz Schaefer, Zoe Piran, Nils Philipp Walter, Animesh Awasthi, Christoph Bock, Jure Leskovec, Zinaida Good"
date: 2026-04-30
pdf: "https://openreview.net/pdf/5633e8d66627583698d6fffa502376d7f9347d92.pdf"
tags: ["query:immuno-topo"]
score: 10.0
evidence: 通过图像、基因表达和文本之间的传递学习实现零样本细胞类型注释。
tldr: 针对组织病理学中细胞身份注释粗糙的问题，SpatialWhisperer利用空间分辨基因表达数据作为桥梁，通过三模态对比学习对齐图像、基因表达与文本描述。该方法实现了无需微调的零样本细胞类型注释，显著提升了注释效率和准确性，为稀缺标注场景下的计算病理学提供了有效工具。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 现有组织病理学AI受限于粗粒度注释，无法识别细胞身份。
method: 提出三模态对比学习模型SpatialWhisperer，利用基因表达传递关系实现跨模态对齐。
result: 模型实现了准确的零样本细胞类型注释，无需额外微调。
conclusion: 传递表示学习为组织病理学细胞注释提供了高效解决方案，推动了精准诊断。
---

## Abstract
The characterization of histopathology with AI promises to assist clinical decision-making, but it is currently limited due to coarse-grained annotations that miss cellular identities. To overcome this gap, we bridge histopathological images, gene expression profiles, and natural-language descriptions using *SpatialWhisperer*, a trimodal contrastive learning model. Our training integrates community-scale datasets comprising spatially resolved gene expression profiles paired with histopathology images, as well as single-cell gene expression profiles with detailed annotations. The shared gene expression modality implies a transitive relationship between images and textual annotations, which our method leverages to enable accurate zero-shot cell type annotation directly from H&E images. *SpatialWhisperer* outperforms published baselines, achieving relative AUROC gains of up to 15.9% across three benchmarks spanning 19 tissues and 20 cell types. When training with data from all three modality pairs, we observe performance gains in low-data regimes. We formalize our approach and present a sufficient condition under which this transitive alignment is induced. Our work establishes *transitive representation learning* for fine-grained interpretation of histopathology images.

---

## 论文详细总结（自动生成）

# 论文总结：Transitive Representation Learning Enhances Histopathology Annotation

## 1. 论文的核心问题与整体含义

- **研究动机**：组织病理学图像的 AI 分析有望辅助临床决策，但现有的监督学习方法受限于粗粒度的标注，无法识别图像中细胞的精确身份（例如无法区分不同的免疫细胞亚型或肿瘤异质性细胞）。
- **整体含义**：作者提出利用“传递表示学习”（transitive representation learning）来解决这一问题。通过将图像、基因表达谱和自然语言描述三种模态对齐，使模型能够在仅有 H&E 染色图像且无额外微调的情况下，零样本地预测图像区域的细胞类型注释，从而为精细化的计算病理学提供通用工具。

## 2. 论文提出的方法论

- **核心思想**：利用空间分辨的基因表达数据作为“桥梁”，建立图像与文本注释之间的传递关系。由于空间转录组数据同时配对组织图像和基因表达，而单细胞转录组数据又包含详尽的文本注释，因此基因表达模态使得图像与文本可间接对齐。
- **关键技术细节**：
  - 提出三模态对比学习模型 **SpatialWhisperer**。
  - 训练整合两个社区规模的数据集：① 空间分辨基因表达谱及其配对的 H&E 图像；② 带详细注释的单细胞基因表达谱。
  - 对比目标：在不同模态的对齐中拉近匹配样本的表示，推远不匹配样本。形式化条件保证了传递对齐的成立。
  - 推理阶段：输入 H&E 图像，通过模型提取表示，与文本描述的表示计算相似度，实现零样本细胞类型分类。
- **公式或算法流程**（文字说明）：
  - 三个编码器分别处理图像、基因表达和文本，输出归一化的嵌入向量。
  - 训练时使用两个配对的模态对（图像-基因、基因-文本）进行对比损失优化，使得基因嵌入作为中间表示强制图像与文本嵌入空间对齐。
  - 作者给出一个充分条件，确保这种间接训练能诱导出直接的图像-文本映射。

## 3. 实验设计

- **使用数据集**：
  - 社区规模的空间转录组数据集（包含多种组织、多组织切片配对图像与基因表达）。
  - 单细胞基因表达数据集（具详细细胞类型标注）。
- **Benchmark**：
  - 在 **3 个基准测试** 上评估，覆盖 **19 种组织** 和 **20 种细胞类型**。
- **对比方法**：
  - 与已发表的基线方法（published baselines）进行比较，具体方法名称未列出，但包括可能已有的图像到文本的对齐模型或监督方法。
- **评估指标**：采用相对 AUROC 提升作为主要指标，并考察低数据条件下的性能增益。

## 4. 资源与算力

- 摘要及元数据中 **未明确说明** 使用的 GPU 型号、数量及训练时长等算力细节。如果需要精确信息，需查阅原论文正文。

## 5. 实验数量与充分性

- **实验组数**：至少包含 3 个基准数据集上的主实验对比，以及与多个 published baselines 的比较；还有消融研究（如训练使用不同模态配对数据）以及低数据场景分析。整体实验覆盖组织类型广泛（19 种组织），细胞类型 20 种，体现了一定的充分性。
- **客观与公平性**：采用公开数据集和标准化指标 AUROC，对比已发表方法，增益显著（相对 AUROC 最高提升 15.9%），实验设计合理。但缺少更细致的样本量和统计检验细节，在该摘要中无法判断是否完全避免了偏差。

## 6. 论文的主要结论与发现

- SpatialWhisperer 成功地实现了无害微调、直接基于 H&E 图像的零样本细胞类型注释。
- 在所有三个基准测试上均超越现有基线，取得显著的 AUROC 提升。
- 当训练使用全部三种模态配对的数据时，在低数据体制下仍可获得性能增益。
- 传递表示学习为组织病理学图像的细粒度解释提供了理论支撑与实践方案，有望推动精准诊断。

## 7. 优点

- **方法创新性**：首次将三模态（图像-基因-文本）的传递学习引入组织病理学，无需配对图像-文本标注，降低了对昂贵专家标注的依赖。
- **零样本能力**：模型通用性强，可在未见过的组织或细胞类型上直接推理，实用性高。
- **性能突出**：相对 AUROC 提升高达 15.9%，优势明显。
- **理论完备**：给出了传递对齐成立的充分条件，增强了方法的可解释性与可靠性。
- **数据利用高效**：巧妙利用了两类公开的大规模数据（空间组学与单细胞组学），避免了耗时耗力的图像-文本配对标注。

## 8. 不足与局限

- **实验细节不详**：摘要及元数据未提供具体数据集名称、样本量、对比方法的详细列表，难以独立复现或评判基准线的强度。
- **算力信息缺失**：无法评估其训练成本与可扩展性。
- **可能的应用偏差**：传递对齐假设基因表达模态能完美桥接图像与文本，但在实际中，基因表达可能会丢失部分组织形态信息，零样本性能在某些罕见细胞类型上可能下降。
- **评估局限**：目前仅报告了 20 种细胞类型，真实临床场景中细胞类型更为多样且存在连续过渡状态，方法泛化能力待进一步验证。
- **文本模态的覆盖范围**：自然语言描述的质量和覆盖面直接影响分类边界，未说明如何处理文本标注的歧义或不一致。

（完）
