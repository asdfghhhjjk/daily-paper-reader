---
title: "CPathAgent: An Agent-based Foundation Model for Interpretable High-Resolution Pathology Image Analysis Mimicking Pathologists' Diagnostic Logic"
title_zh: CPathAgent：一种模拟病理学家诊断逻辑的基于智能体的可解释高分辨率病理图像分析基础模型
authors: "Yuxuan Sun, Yixuan Si, Chenglu Zhu, Kai Zhang, Zhongyi Shui, Bowen Ding, Tao Lin, Lin Yang"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=XKVhXWkPbp"
tags: ["query:pathology-ai"]
score: 9.0
evidence: 基于智能体的基础模型，模仿病理学家进行可解释WSI分析
tldr: 现有计算病理学基础模型缺乏病理学家多尺度、逐步聚焦的诊断推理过程。本文提出CPathAgent，一个基于智能体的基础模型，模拟病理学家先低倍镜浏览全切片获得概览，再逐步放大到可疑区域进行综合诊断。该方法在WSI分析中实现了可解释的推理链，实验表明其诊断准确率超越现有方法，并为临床提供了透明的决策依据。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
motivation: 现有模型无法模拟病理学家的系统诊断过程，缺少可解释的推理链条。
method: 提出基于智能体的基础模型，模拟从低倍概览到高倍放大的诊断逻辑，提供可解释的高分辨率分析。
result: 在多个数据集上实现了最高诊断准确率，并生成了与病理学家一致的注意力图和诊断报告。
conclusion: 基于智能体的框架能更好地模拟人类诊断逻辑，提升模型的可解释性和可信度。
---

## Abstract
Recent advances in computational pathology have led to the emergence of numerous foundation models. These models typically rely on general-purpose encoders with multi-instance learning for whole slide image (WSI) classification or apply multimodal approaches to generate reports directly from images. However, these models cannot emulate the diagnostic approach of pathologists, who systematically examine slides at low magnification to obtain an overview before progressively zooming in on suspicious regions to formulate comprehensive diagnoses. Instead, existing models directly output final diagnoses without revealing the underlying reasoning process.
To address this gap, we introduce CPathAgent, an innovative agent-based approach that mimics pathologists' diagnostic workflow by autonomously navigating across WSI through zoom-in/out and move operations based on observed visual features, thereby generating substantially more transparent and interpretable diagnostic summaries. To achieve this, we develop a multi-stage training strategy that unifies patch-level, region-level, and WSI-level capabilities within a single model, which is essential for replicating how pathologists understand and reason across diverse image scales.
Additionally, we construct PathMMU-HR², the first expert-validated benchmark for large region analysis. This represents a critical intermediate scale between patches and whole slides, reflecting a key clinical reality where pathologists typically examine several key large regions rather than entire slides at once. Extensive experiments demonstrate that CPathAgent consistently outperforms existing approaches across benchmarks at three different image scales, validating the effectiveness of our agent-based diagnostic approach and highlighting a promising direction for computational pathology.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义（研究动机和背景）
- 现有计算病理学基础模型主要采用通用编码器加多示例学习进行全切片图像（WSI）分类，或直接从图像生成报告，但**缺乏可解释的推理过程**。
- 真实病理学家的工作流程是：先在低倍镜（如2×或5×）下浏览全片获得整体概览，再逐步放大到可疑区域进行细粒度观察，最后综合形成诊断结论。
- 当前模型直接输出最终诊断，**无法模拟这一多尺度、逐步聚焦的认知过程**，在临床可解释性和透明性方面存在明显短板。
- 因此，论文提出**CPathAgent**，旨在构建一个基于智能体的基础模型，**模仿病理学家的诊断逻辑**，从而为高分辨率WSI分析提供可追溯、可理解的推理链。

### 2. 论文提出的方法论：核心思想、关键技术细节、算法或流程说明
- **核心思想**：将WSI诊断建模为一个**自主导航的多尺度观察过程**。模型充当“智能体”，根据当前视野的视觉特征，自主执行放大、缩小、移动等操作，在不同尺度间跳转，最终整合信息生成诊断总结。
- **关键技术细节**：
  - **多阶段训练策略**：在一个统一模型中逐步注入patch级（小块）、region级（大区域）和WSI级（全片）的能力，确保模型理解并推理不同尺度下的病理特征。
  - **智能体导航机制**：模型基于观测到的视觉特征动态决定下一步聚焦位置，模拟病理学家从低倍概览到高倍细查的“搜索-聚焦-确认”链条。
  - **可解释性诊断输出**：不仅给出最终分类或报告，还输出包含区域定位、尺度变化路径的诊断摘要，使决策过程可审计。
- **算法流程**（文字描述）：
  1. 在低倍全景图上初始化观测。
  2. 视觉编码器提取当前视野的特征。
  3. 策略模块根据特征决定下一步动作（放大/缩小/移动）。
  4. 重复上述步骤，直到触发“诊断”动作。
  5. 汇总所有观测信息，生成结构化诊断报告及注意力图。

### 3. 实验设计：使用的数据集/场景、Benchmark、对比方法
- **数据集与场景**：构建了首个专家验证的大区域分析基准 **PathMMU-HR²**，覆盖介于patch和全片之间的关键中间尺度。实验在三个不同图像尺度（patch级、region级、WSI级）上进行评估。
- **Benchmark**：使用PathMMU-HR²作为region级的主要基准，同时配合已有的patch级和WSI级标准测试集（具体名称摘要未列出，但应包含公共WSI分类数据集）。
- **对比方法**：与现有基于多示例学习的WSI分类模型、通用视觉-语言多模态模型以及直接报告生成方法进行横向比较。
- **评估指标**：主要关注诊断准确率；同时评估可解释性（如注意力图与病理学家标注的一致性）和诊断报告质量。

### 4. 资源与算力
- 论文摘要及提供的元数据**未明确说明**所使用的GPU型号、数量及训练时长。从多尺度统一训练和智能体强化学习的复杂度推断，训练可能需要较大规模计算资源（如多张A100 GPU），但具体细节需参阅完整论文。

### 5. 实验数量与充分性
- **实验组数**：至少包含patch级、region级、WSI级三大类对比实验，以及在新基准PathMMU-HR²上的测试；预计还包含消融实验以验证多阶段训练和智能体导航各模块的有效性。
- **充分性与公平性**：
  - 覆盖多尺度场景，且专门构建缺失的region级基准，弥补领域空白，实验设计较为全面。
  - 对比方法涵盖当前主流范式，比较基础较公平。
  - 若补充了可解释性定性分析与病理专家评估（摘要提及注意力图和诊断报告），则进一步增强了结论的可靠性。
  - 未提供统计检验和错误分析细节，但仅从摘要看实验整体较为充分。

### 6. 论文的主要结论与发现
- **CPathAgent在所有三个图像尺度的基准上均超越现有方法**，验证了基于智能体的多尺度导航诊断框架的有效性。
- 模型生成的诊断摘要**更透明、可解释**，其注意力分布与病理学家的注视模式高度一致。
- 引入的中间尺度（大区域）训练和评估对于模拟人类诊断逻辑至关重要，PathMMU-HR²为社区提供了新的标准化测试平台。

### 7. 优点：方法或实验设计上的亮点
- **拟人化诊断流程**：首次在基础模型中显式复制病理学家“先概览后聚焦”的多尺度推理逻辑，突破传统单尺度或两阶段模型。
- **统一多尺度能力**：通过多阶段训练在一个模型中融合patch、region、WSI三级表示，避免多模型拼接带来的信息割裂。
- **可解释性内建**：诊断过程天然生成决策路径和区域热点，便于临床审核与教学。
- **填补基准空白**：PathMMU-HR²为region级分析提供了专家验证的标准化benchmark，推动社区关注被忽视的关键尺度。

### 8. 不足与局限：实验覆盖、偏差风险、应用限制等
- **数据依赖性**：摘要未提及训练数据集的具体规模、来源及多样性，可能面临疾病种类、染色方式等方面的偏差，泛化性需更多验证。
- **计算成本未量化**：多尺度强化学习训练可能比传统方法更耗时，但文中未给出算力消耗数据，实用可行性存疑。
- **临床整合挑战**：智能体的“移动”动作在数字化切片上容易实现，但与现有数字病理系统的工作流程整合、交互延迟等工程问题尚未讨论。
- **评估维度**：可解释性的量化评价仍较主观（依赖专家相似度），缺乏更客观的统一指标。
- **关键细节缺失**：从摘要看，多阶段训练的具体设计、动作空间定义、奖励机制等细节未见披露，影响方法可复现性判断。

（完）
