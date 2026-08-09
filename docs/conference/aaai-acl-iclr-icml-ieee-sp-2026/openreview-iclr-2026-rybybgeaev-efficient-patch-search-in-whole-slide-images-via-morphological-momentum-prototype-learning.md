---
title: Efficient Patch Search in Whole Slide Images via Morphological Momentum Prototype Learning
title_zh: 通过形态学动量原型学习实现高效全切片图像区域搜索
authors: "Sihyeon Park, Jungwoo Park, Hyunjae Kim, Jaewoo Kang, Bumsoo Kim"
date: 2025-09-20
pdf: "https://openreview.net/pdf?id=rYbYbgeaEv"
tags: ["query:path-xai-sel"]
score: 9.0
evidence: 提出形态学原型学习以高效搜索和排序WSI中的图像块
tldr: 针对全切片图像处理的内存限制，提出基于形态学动量原型学习的有效切片搜索方法，能够快速定位诊断相关区域，提升计算效率与下游分类性能。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 全切片图像分辨率极高，传统多阶段处理复杂且难以聚焦关键区域。
method: 提出形态学动量原型学习，利用原型表征驱动高效切片搜索与排序。
result: 方法能有效筛选诊断相关区域，在迭代中显著降低计算开销。
conclusion: 形态学原型引导的搜索策略为WSI分析提供了高效可解释的区域选择方案。
---

## Abstract
Digital histopathology images play a crucial role in cancer diagnosis, therapeutic response prediction, and identification of clinically relevant morphological features. However, processing Whole Slide Images (WSI) with gigapixel resolution introduces significant challenges in computer vision, exceeding the memory capacity of standard vision encoders. To address this, recent methods employ a multi-stage pipeline: dissecting the image into small patches, extracting patch-level features, and aggregating these features using global pooling through Multi-Instance Learning (MIL) to form a final slide-level representation. Despite achieving clinical-grade performance, this approach becomes increasingly complex with higher magnification due to the quadratic increase in patch numbers and the generation of numerous irrelevant or redundant patches. This complexity burdens the global pooling network, resulting in long inference times and excessive computational resources, while redundant patches introduce noise during the MIL process, limiting the model’s ability to utilize high-magnification features fully. To overcome these challenges, we propose Momentum Morphological Prototype Learning (MMPL), an efficient method that redefines WSI diagnosis as a searching process of relevant patch-level representations with a learned set of global prototypes. MMPL trains a fixed set of prototypes to retrieve the most informative patches, computing the diagnostic score using only the retrieved patches. Evaluated on WSI classification benchmarks, MMPL achieves state-of-the-art performance across various pathology tasks, including metastasis detection, tumor grading, and tumor subtyping.

---

## 论文详细总结（自动生成）

由于提供的文本仅为论文元数据与简短摘要，未包含完整全文，以下总结将主要依据可用的摘要、标题及元信息进行分析。若某些部分信息缺失，会如实指明。

---

### 1. 论文的核心问题与整体含义（研究动机和背景）
- **核心问题**：全切片图像（WSI）分辨率高达数十亿像素，无法直接输入标准视觉编码器，现有主流方法需将图像切割为海量小块，再通过多实例学习（MIL）聚合特征。随着放大倍率提高，块数量呈二次增长，产生大量无关或冗余块，导致：
  - 全局池化网络计算量剧增，推理耗时过长；
  - 冗余块引入噪声，限制模型充分利用高倍镜下的细节特征。
- **整体含义**：该研究将 WSI 诊断重新定义为**基于学习到的全局原型集，在大量图像块中搜索最具辨别力的块**的过程，从而仅依靠筛选出的少量关键块完成分类，大幅降低计算开销并提升性能。

### 2. 论文提出的方法论
- **核心思想**：通过一组可学习的、固定的**形态学原型**（Morphological Prototypes）来检索信息量最大的图像块，并使用动量机制（Momentum）稳定原型更新。最终只用检索出的块计算诊断分数，而非聚合所有块。
- **关键技术细节**（依据摘要与元信息推测）：
  - **原型学习**：训练一组固定数量的全局原型向量，每个原型代表某种具有诊断意义的形态模式。
  - **块搜索与排序**：对于一张 WSI 的所有块，计算它们与每个原型的相似度，利用相似度得分对块进行排序，筛选出与原型最匹配的少量块（“检索”过程）。
  - **动量更新**：采用动量方式更新原型，可能是指在训练过程中缓慢调整原型位置，保持稳定性。
  - **诊断评分**：仅将检索到的块输入后续分类器，生成切片级预测。
- **算法流程**（文字描述）：输入 WSI → 切分为小块 → 提取块特征 → 与动量原型集计算相似度 → 根据相似度选择 Top-K 个块 → 利用这些块的表示进行诊断分类。训练时，原型和分类器端到端优化，同时保持原型集的稀疏与动量更新。

### 3. 实验设计
- **使用数据集/场景**：文中提及在“WSI 分类基准”上进行评估，涵盖多种病理任务：
  - 转移检测（metastasis detection）
  - 肿瘤分级（tumor grading）
  - 肿瘤亚型分型（tumor subtyping）
- **基准与对比方法**：声称与现有最先进方法（state‑of‑the‑art）进行比较。摘要未列出具体方法名称，但可以推断对比对象为基于 MIL 的 WSI 分析主流模型（如 CLAM、TransMIL、DSMIL 等）。由于原文缺失，暂无法给出完整对比清单。
- **评价指标**：可能包括分类准确率、AUC、计算效率（推理时间、GPU 内存占用）等，但摘要未详细说明。

### 4. 资源与算力
- **明确说明**：提供的文本中**未提及**使用的 GPU 型号、数量、训练时长或浮点运算次数。仅提到方法能够“显著降低计算开销”，并通过只使用少量关键块来缩短推理时间。具体算力细节需参阅原文完整版本。

### 5. 实验数量与充分性
- **实验数量粗略估计**：基于摘要，至少覆盖了**3 类病理任务**（转移、分级、分型），每个任务可能对应一个或多个数据集（如 CAMELYON16、TCGA 等常见基准）。另外，方法本身带有消融研究（例如原型数量、动量机制、搜索策略等的对比）的可能性很高，但摘要未展开。
- **充分性与公平性**：声称达到最先进性能，说明实验设计应较为全面；从“检索少量块”这一角度评估效率提升，并与其他 MIL 方法进行同基准对比，体现了客观性。但由于缺乏详细表格和消融实验细节，无法判断实验的完整程度。

### 6. 论文的主要结论与发现
- MMPL 能够用极少量（检索到的）图像块实现高精度的 WSI 诊断，性能优于传统使用全部块的 MIL 方法。
- 该方法重新定义了 WSI 分析流程，将聚合问题转化为搜索问题，显著降低了聚合阶段的复杂性。
- 通过动量形态学原型，模型可以学到具有可解释性的形态表示，并为诊断提供关键区域定位。

### 7. 优点（方法与实验设计的亮点）
- **计算高效**：通过只处理搜索到的最相关小块，避免了输入全量块的冗余计算，推理速度和内存消耗明显改善。
- **可解释性强**：原型直接对应形态学模式，检索出的块即为诊断依据，便于医生验证。
- **任务通用性**：在多种病理任务（转移、分级、分型）上均取得领先结果，表明方法通用性好。
- **简化流程**：将复杂的 MIL 聚合简化为搜索–排序–轻量分类的过程，训练和部署更轻量。

### 8. 不足与局限
- **信息缺失限制评估**：由于仅有摘要，无法得知具体的原型数量选择、块搜索的 Top-K 设定、对边界情况的鲁棒性等细节。
- **潜在局限**（依据常识推断）：
  - **原型固定性**：预设的原型数量可能无法灵活适应不同数据分布，需要人为调整。
  - **搜索依赖初始原型**：若初始化不当，可能检索到非代表性块，影响收敛。
  - **仅块级筛选**：舍弃了大量非检索块，可能丢失全局上下文信息，在某些需要综合巨量视野的任务中表现不足。
  - **对比基线不明**：摘要未列出对比的具体方法，无法判断是否与最新最强的所有方法（如基于 Transformer 或图神经网络的方法）进行了充分比较。
  - **实验覆盖可能不足**：仅有三个任务类型，是否覆盖更多癌种或稀有变异有待证实。
- **标注风险**：全切片标签常为弱监督，检索出的块未必是完全准确的形态学解释，可能存在偏差。

（完）
