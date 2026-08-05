---
title: Transitive Representation Learning Enhances Histopathology Annotation
title_zh: 传导式表示学习增强组织病理学标注
authors: "Moritz Schaefer, Zoe Piran, Nils Philipp Walter, Animesh Awasthi, Christoph Bock, Jure Leskovec, Zinaida Good"
date: 2026-04-30
pdf: "https://openreview.net/pdf/5633e8d66627583698d6fffa502376d7f9347d92.pdf"
tags: ["query:cellseg"]
score: 9.0
evidence: 利用基因表达桥梁在组织病理图像中实现零样本细胞类型标注。
tldr: 组织病理学AI分析受限于粗粒度标注，缺乏细胞身份信息。本文提出三模态对比学习模型SpatialWhisperer，连接病理图像、基因表达和自然语言描述，利用共享的基因表达模态建立传递关系，实现零样本细胞类型标注，提升了解释性。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 组织病理学标注粗粒度，缺少细胞身份信息，限制了AI辅助临床决策。
method: 利用空间分辨基因表达和单细胞基因表达数据集，通过三模态对比学习建立图像和文本间的传递关系。
result: 实现准确的零样本细胞类型标注，提升了组织病理学表征能力。
conclusion: 传导式学习弥合了图像和文本标注间的模态鸿沟，为可解释AI病理提供了新途径。
---

## Abstract
The characterization of histopathology with AI promises to assist clinical decision-making, but it is currently limited due to coarse-grained annotations that miss cellular identities. To overcome this gap, we bridge histopathological images, gene expression profiles, and natural-language descriptions using *SpatialWhisperer*, a trimodal contrastive learning model. Our training integrates community-scale datasets comprising spatially resolved gene expression profiles paired with histopathology images, as well as single-cell gene expression profiles with detailed annotations. The shared gene expression modality implies a transitive relationship between images and textual annotations, which our method leverages to enable accurate zero-shot cell type annotation directly from H&E images. *SpatialWhisperer* outperforms published baselines, achieving relative AUROC gains of up to 15.9% across three benchmarks spanning 19 tissues and 20 cell types. When training with data from all three modality pairs, we observe performance gains in low-data regimes. We formalize our approach and present a sufficient condition under which this transitive alignment is induced. Our work establishes *transitive representation learning* for fine-grained interpretation of histopathology images.

---

## 论文详细总结（自动生成）

## 1. 论文的核心问题与整体含义

- **研究动机**：组织病理学的人工智能解析有望辅助临床决策，但目前的分析严重受限于粗粒度的标注（如整张切片级别的分类），这类标注缺失了关键的细胞身份信息。医生或模型无法知道图像中具体是哪种细胞，限制了 AI 的可解释性与临床价值。
- **整体含义**：本文试图通过“传导式表示学习”弥合病理图像与自然语言标注之间的模态鸿沟。将病理图像、基因表达谱和文本描述三种模态打通，使得模型能够直接从常规 H&E 染色图像中零样本地推断出精细的细胞类型，为可解释 AI 病理打开新通路。

## 2. 方法论

- **核心思想**：利用基因表达作为“桥梁”模态，隐式建立图像与文本之间的传递关系。具体而言：
  - 病理图像与空间分辨基因表达谱在空间上是配对的（共定位），可进行对齐学习。
  - 单细胞基因表达谱与细胞类型文本描述有详细标注，亦可进行对齐。
  - 由于这两条路径共享“基因表达”这一模态，模型通过对比学习能在联合嵌入空间中自动诱导出图像与文本的直接对齐，即**传递关系**。
- **关键模型**：提出三模态对比学习模型 **SpatialWhisperer**。
- **算法流程（文字描述）**：
  1. 构建三个编码器，分别处理图像、基因表达和自然语言描述。
  2. 训练时使用两类配对数据：病理图像-基因表达对（来自空间转录组学数据）、基因表达-文本对（来自单细胞数据集）。
  3. 采用对比学习损失，拉近配对样本的嵌入，推远非配对样本。
  4. 由于基因表达模态被两个对比学习任务共享，优化过程中图像嵌入与文本嵌入通过基因表达嵌入的中间约束逐步对齐，无需直接成对的图像-文本数据。
- **形式化保障**：论文给出了一个充分条件，证明在这种三模态传递设置下，对比学习确实会诱导出图像与文本的对齐。

## 3. 实验设计

- **数据集/场景**：
  - 融合社区规模的多个数据集：包括空间分辨基因表达与配对病理图像，以及带有详细细胞类型标注的单细胞基因表达谱。
  - 测试覆盖三个基准（benchmarks），共计 19 种组织和 20 种细胞类型。
- **核心任务**：零样本细胞类型标注——模型仅凭 H&E 图像，无需该组织/细胞类型的直接图像-文本对，预测图像区域对应的细胞类型。
- **对比方法**：与已发表的相关基线模型进行比较（具体名称未在元数据中展开），评估指标为 AUROC。
- **效果**：SpatialWhisperer 在所有基准上均超越基线，AUROC 相对提升最高达 15.9 %。进一步实验表明，在低数据场景下使用三种模态对联合训练可带来额外增益。

## 4. 资源与算力

- 所提供的元数据及摘要中**未明确说明**使用的 GPU 型号、数量、训练时长或总计算开销。需要查阅正文方可获知具体算力需求。

## 5. 实验数量与充分性

- **实验组数**：从摘要可窥见的实验维度包括：
  - 三个独立的组织/细胞类型基准测试。
  - 低数据模式下的训练实验（data regimes）。
  - 三模态联合训练与仅用两模态的对比实验。
  - 与多个已发表基线的全面比较。
- **充分性与公平性**：
  - 跨 19 个组织、20 种细胞类型的广泛评估，表明实验覆盖面较大。
  - 有相对提升指标和低数据场景分析，体现了一定深度。
  - 由于仅依据元数据，无法判断是否有完整的消融实验、统计检验或误差分析，但现有信息显示实验设计较为系统。
  - 对比对象是已发表方法，基准选择公平性在摘要中未受到质疑。

## 6. 主要结论与发现

- **零样本细胞类型标注可行且准确**：通过传导式学习，模型无需直接图像-文本对即可对 H&E 图像进行细粒度细胞分类。
- **表征能力增强**：SpatialWhisperer 学到的图像表征不仅对染色模式敏感，还与生物学意义的基因模块和细胞类型描述相关联，提升了可解释性。
- **传递对齐的理论成立**：形式化分析表明，共享桥接模态的对比学习确实能间接对齐图像与文本，为类似多模态问题提供一般性框架。
- **数据高效性**：尤其在低数据量时，利用多模态传递训练可提升性能，减少对大量图像-文本对的依赖。

## 7. 优点

- **创新的范式**：直接利用基因表达作为天然桥梁，巧妙绕过了病理图像-文本配对数据稀缺的难题，实现了零样本细胞级标注。
- **三模态联合嵌入**：与一般的图像-文本双模态模型不同，引入基因表达使学习到的表征具有分子层面的依据，增强了生物学可解释性。
- **理论与实践结合**：不仅给出了有效的模型，还提炼了传导式表示学习的充分条件，为后续研究提供理论参考。
- **效果显著**：在多个组织、多种细胞类型上的零样本性能一致超越已有基线，证明了方法的鲁棒性和通用性。

## 8. 不足与局限

- **对基因表达数据的依赖**：训练必须依赖高质量的空间转录组和单细胞基因表达数据，这类数据获取成本高、样本量有限，可能限制模型规模与覆盖的组织多样性。
- **跨组织的泛化细节未知**：虽然覆盖了 19 个组织，但元数据未说明训练/测试的划分方式（是否包含未见过组织或癌症类型），实际部署中可能遇到分布漂移。
- **实验细节透明性**：元数据显示对比了基线，但未列出具体方法名，且缺失算力、超参数敏感性等实验信息，无法判断复现的便利性和计算效率。
- **潜在的批次/平台偏差**：不同基因表达数据集（如不同单细胞测序平台）的批次效应可能影响传递关系，文中是否处理尚不清楚。
- **临床应用路径未论述**：零样本标注虽然惊艳，但转换为临床决策支持需要更严格的验证和解释性分析（如错误模式），该方面在现有提要中未深入涉及。

（完）
