---
title: "Thinking in Scales: Accelerating Gigapixel Pathology Image Analysis via  Adaptive Continuous Reasoning"
title_zh: 尺度思维：通过自适应连续推理加速十亿像素病理图像分析
authors: "Jiusong Ge, Yingkang Zhan, Wenjie Zhao, Di Zhang, Ke Wang, Jiashuai Liu, Chunze Yang, Chengzu Li, Jian Zhang, Yuxin Dong, Ni Zhang, Qidong Liu, Mireia Crispin-Ortuzar, Huazhu Fu, Chen Li, Zeyu Gao"
date: 2026-04-30
pdf: "https://openreview.net/pdf/f0a644528105d8a40c15a51e8120eaae340a2f2e.pdf"
tags: ["query:path-xai-sel"]
score: 8.0
evidence: 自适应连续推理动态选择WSI中的重要区域以实现高效诊断。
tldr: 传统WSI分析依赖高倍镜下穷举式特征提取，计算代价高昂。PathCTM将诊断推理建模为动态信息搜索，逐步从低倍全局过渡到高倍局部检测，实现令牌高效的多尺度连续推理。实验表明，该方法在保持诊断准确性的同时显著加速了十亿像素病理图像分析，为高效WSI处理提供了新范式。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 现有WSI分析方法的穷举式补丁处理计算开销巨大，限制了可扩展性。
method: 提出PathCTM，将WSI诊断建模为动态序列信息追求，从低倍到高倍逐步检查。
result: 实验表明PathCTM在保持准确性的同时显著降低了计算成本。
conclusion: 连续尺度推理为高效WSI分析提供了有效解决方案，具有实际应用价值。
---

## Abstract
Traditional whole slide image (WSI) analysis methods typically rely on the multiple instance learning (MIL) paradigm, which extracts patch-level features at high magnification and aggregates them for slide-level prediction. 
However, such exhaustive patch-level processing is computationally expensive, severely limiting the efficiency and scalability of WSI analysis. 
To address this challenge, we propose PathCTM (a Pathology-oriented Continuous Thought Model) that enables token-efficient scale-space continuous reasoning for gigapixel WSIs. PathCTM formulates diagnostic inference as a dynamic sequential information pursuit. It progressively transitions from low-magnification global to high-magnification local inspection, and adaptively terminates inference when sufficient evidence is gathered to effectively bound decision uncertainty. Specifically, it uses conditional computation for dynamic scale switching with attention-guided region pruning, coupled with confidence-aware early stopping. Extensive experiments demonstrate that, compared with standard MIL-based methods, PathCTM reduces the number of required image patches by 95.95\% and shortens inference time by approximately 95.62\%, while maintaining AUC without degradation. Code is available at https://github.com/JSGe-AI/PathCTM.

---

## 论文详细总结（自动生成）

由于提供的论文内容仅限于摘要和元数据（因页面要求验证而无法获取全文），以下总结基于现有信息进行客观分析。若需完整内容，请提供完整的论文文本。

---

### 1. 论文的核心问题与整体含义（研究动机和背景）

- **核心问题**：传统全切片图像（WSI）分析通常依赖多实例学习（MIL）范式，在高倍率下穷举式提取所有图像块的局部特征，计算成本极高，严重制约了WSI分析的效率和可扩展性。
- **研究动机**：临床病理诊断中，人类专家并非盲目查看每一处高倍细节，而是从低倍全局快速定位可疑区域，再逐步放大检查。这种“尺度连续推理”策略可大幅减少不必要的信息处理。
- **整体含义**：论文旨在将人类诊断的认知过程建模为动态、令牌高效的多尺度推理，从而在保持诊断准确性的前提下，显著降低十亿像素病理图像分析的计算负担。

### 2. 论文提出的方法论：核心思想、关键技术细节

- **核心思想**：将WSI诊断推理重新定义为**动态序列信息追求**（dynamic sequential information pursuit）过程，从低倍全局视图出发，逐步过渡到高倍局部检查，并在收集到足够证据时自动终止推理，以约束决策不确定性。
- **模型名称**：PathCTM（Pathology-oriented Continuous Thought Model，面向病理的连续思维模型）。
- **关键技术细节**（基于摘要描述）：
  - **动态尺度切换**：采用条件计算（conditional computation）机制，根据当前信息状态自适应决定是否切换至更高倍率。
  - **区域剪枝**：结合注意力引导的区域剪枝（attention-guided region pruning），仅对具有高信息潜力的区域进行高倍观察，避免全局穷举。
  - **置信度感知早停**：引入置信度感知的早停（confidence-aware early stopping）策略，当累积证据足以可靠诊断时终止推理，减少冗余计算。
- **推理流程**：可概括为“低倍筛查 → 注意力划区 → 高倍精细检查 → 自信早停”的闭环迭代。

### 3. 实验设计：数据集、基准与对比方法

- **数据集/场景**：摘要未列出具体数据集名称，但明确是针对十亿像素（gigapixel）WSI的分析任务，可能涵盖癌症诊断、组织分类等典型病理场景。
- **基准（benchmark）**：以标准MIL方法作为性能对比基准，评估指标包括分类AUC、所需图像块数量、推理时间。
- **对比方法**：主要与标准MIL-based方法进行对比，其他对比方法未在摘要中详述，预计包含现有高效WSI分析方法。

### 4. 资源与算力

- 摘要及元数据中**未提供**GPU型号、数量、训练时长等具体算力信息。仅报告了推理阶段的加速效果（推理时间缩短约95.62%），未提及训练资源需求。

### 5. 实验数量与充分性

- **实验数量**：摘要中仅定性描述“大量实验”（extensive experiments），未给出具体实验组数。从报告的结果指标（补丁数量减少95.95%、推理时间缩短95.62%、AUC未降）可推测至少包含：
  - 主要性能对比实验（PathCTM vs. 标准MIL）；
  - 消融实验（验证动态尺度切换、区域剪枝、早停机制各自的贡献）；
  - 效率对比实验（计算量与推理时间）。
- **充分性评价**：基于片段信息，实验至少覆盖了性能和效率两个核心维度，且给出了定量降幅，具有说服力。但数据集数量、跨中心验证、统计显著性检验等细节因全文缺失无法评价。若全文包含多数据集、多任务验证和详细的消融分析，则实验充分；否则可能存在覆盖不足的风险。在现有信息下，初步判断实验设计较为扎实，但需阅读原文以确认。

### 6. 论文的主要结论与发现

- PathCTM通过模拟病理学家的尺度推理策略，实现了**令牌高效**的多尺度连续推理。
- 相较于标准MIL方法，PathCTM在保持AUC不降的前提下，所需图像块数量减少**95.95%**，推理时间缩短约**95.62%**。
- 连续尺度推理范式为高效、可扩展的WSI分析提供了有效解决方案，具有实际应用潜力。

### 7. 优点：方法或实验设计上的亮点

- **认知启发建模**：将医学诊断的认知过程（由粗到精、适时停、动态搜索）融入模型设计，思路新颖且符合临床直觉。
- **多策略协同**：集成了条件计算、注意力引导剪枝和早停三种机制，各部分目标明确，共同实现计算精简。
- **实验效果显著**：在维持诊断性能的同时，实现了接近两个数量级的效率提升，显示出技术上的明显优势。
- **开源可复现**：提供代码仓库，有利于社区验证和发展。

### 8. 不足与局限（基于摘要信息推断）

- **全文缺失引起的局限**：由于只能获取摘要，以下分析基于有限信息，可能存在遗漏。
- **数据集泛化性未知**：未说明使用了多少种不同器官、癌种或扫描仪来源的数据集，泛化能力待验证。
- **与最新MIL变体的对比**：仅提及与标准MIL对比，未与近年来出现的稀疏注意力MIL、自监督预训练MIL、Transformer-based MIL等高效方法进行直接比较，横向优势的边界不够清晰。
- **训练稳定性与成本**：未披露训练所需的额外开销（如强化学习或自监督预训练成本），模型动态决策的学习是否稳定未讨论。
- **临床部署门槛**：早停的置信度阈值设置可能因任务、数据集而异，超参数敏感性及校准需求未在摘要中体现。
- **潜在信息丢失风险**：仅观察部分区域可能遗漏微小但关键的病变（如微小转移灶），假阴性风险需通过大规模前瞻性研究进一步评估。

---

（完）
