---
title: "Cello: A Universal Cell-wise Feature Aggregation framework for  Reliable  Pathology Images Analysis"
title_zh: "Cello: 面向可靠病理图像分析的通用细胞级特征聚合框架"
authors: "Hengrui Lou, Weihan Li, Jiazhen Yang, Lingxiang Jia, Shengxuming Zhang, Linyun Zhou, Xiuming Zhang, Zhenyang Wang, Mingli Song, Zunlei Feng"
date: 2026-04-30
pdf: "https://openreview.net/pdf/0fac7f88f69a8fee60081cbee4e3d07d13b48f75.pdf"
tags: ["query:profile"]
score: 9.0
evidence: 面向WSI级病理任务的细胞级特征聚合，整合细胞形态与微环境
tldr: Cello提出一种通用的细胞级特征聚合框架，通过蛋白质信号监督的细胞学习将细胞表示集成到全切片图像建模中，弥补了现有patch级流程与病理学家细胞中心推理之间的鸿沟。该方法在千兆像素约束下保留精细的细胞线索，支持局部和全局任务并提供可信证据，为数字病理学分析提供了更可靠的细胞形态与微环境特征利用途径。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 现有数字病理分析依赖patch级特征，忽略了细胞中心的病理学推理，限制了微小病变和细微变化的检测。
method: 提出Cello框架，通过蛋白质信号监督学习实现细胞级特征表示，并聚合到WSI建模中。
result: 实验表明Cello在局部和全局任务上均能提供可信证据，提升了病理图像分析的可靠性。
conclusion: Cello为数字病理学提供了一种统一的细胞级特征聚合方案，有助于更精细的诊断和预后预测。
---

## Abstract
Computational pathology has made progress in diagnosis and prognosis prediction from whole slide images (WSIs), yet pipelines still rely on patch-level feature extraction and aggregation, departing from the cell-centric reasoning used by pathologists.
This gap limits sensitivity to micro-lesions and subtle changes, and current methods rarely provide a unified solution that supports both local and global tasks with trustworthy evidence. We propose Cello, a universal cell-wise feature aggregation framework for reliable pathology image analysis. Cello integrates cell-level representations into WSI modeling via protein-signal–supervised cell-wise learning, preserving fine-grained cellular cues under gigapixel constraints. For local tasks, Cello introduces a flexible prototype-based contrastive module for scalable, task-adaptive representation learning. For global tasks, Cello adopts a weakly supervised gated aggregation that can widely leverage WSI labels. Finally, a cell–local–global decision-route consistency objective dynamically aggregates cellular evidence and aligns local predictions with global outcomes, improving reliability and faithfulness. 
Trained with only hundreds to thousands of samples, Cello achieves performance gains of 3.0%~7.6% and outperforms SOTA pathology foundation models pretrained on tens of thousands of samples. Code is available at https://github.com/HengruiLou/Cello.

---

## 论文详细总结（自动生成）

# 论文总结：Cello: A Universal Cell-wise Feature Aggregation Framework for Reliable Pathology Images Analysis

## 1. 论文的核心问题与整体含义

- **研究背景**：计算病理学在全切片图像（WSI）诊断和预后预测中取得进展，但现有流程仍依赖 **patch 级特征提取与聚合**，与病理学家的 **以细胞为中心的推理** 方式存在鸿沟。
- **核心问题**：这种 patch 级范式限制了对微小病变和细微变化的检测灵敏度；同时，当前方法缺少一个能够 **统一支持局部与全局任务** 并 **提供可信证据** 的方案。
- **整体含义**：提出 **Cello**，一个通用的细胞级特征聚合框架，旨在将细胞层面的表示整合到 WSI 建模中，从而更贴近病理医生的诊断逻辑，提升分析的可靠性和精度。

## 2. 论文提出的方法论

基于摘要，Cello 框架包含以下几个关键技术组件：

- **蛋白质信号监督的细胞级学习（Protein-signal–supervised cell-wise learning）**  
  利用蛋白质信号作为监督信息，学习细胞级别的特征表示，以此保留千兆像素约束下的精细细胞线索。

- **面向局部任务的灵活原型对比模块（Flexible prototype-based contrastive module）**  
  设计可扩展且任务自适应的表征学习方案，采用原型对比学习方式，用于局部病理任务（如细胞级别的分类、分割）。

- **面向全局任务的弱监督门控聚合（Weakly supervised gated aggregation）**  
  针对 WSI 级的全局任务（如生存预测、分级），采用弱监督方式，通过门控机制广泛利用 WSI 标签进行细胞特征的聚合。

- **细胞-局部-全局决策路径一致性目标（Cell–local–global decision-route consistency objective）**  
  动态聚合细胞证据，并对齐局部预测与全局结果，以增强模型的可靠性和忠实性。

整体而言，Cello 实现了一个 **从细胞表示到局部建模、再到全局决策的多层级统一框架**。

## 3. 实验设计

- **数据集 / 场景**：摘要中未提供具体数据集名称。根据任务性质，推测可能涉及公开 WSI 病理数据集（如用于癌症分级、生存分析的 TCGA，或细胞检测的公共数据集），但缺乏准确信息。
- **Benchmark 设置**：应包含局部任务（如细胞级分类、检测）和全局任务（如 WSI 分级、预后预测）。
- **对比方法**：摘要提到 Cello 的性能优于 **在数万样本上预训练的现有病理基础模型（SOTA pathology foundation models）**，但未列出具体模型名称。对比方法可能包括经典的 MIL、注意力聚合、Transformer 等架构，以及病理领域的自监督预训练模型（如 CTransPath、UNI、Prov-GigaPath 等，纯推测）。
- **标注情况**：Cello 训练仅使用 **数百到数千个样本**（hundreds to thousands of samples），而对比的 SOTA 模型使用了数万个样本进行预训练，说明 Cello 在标注效率上具有优势。

## 4. 资源与算力

- 提供的论文文本中 **未包含任何与算力相关的信息**，如 GPU 型号、数量、训练时长等。仅在可获取的元数据和摘要中寻找，未能发现相应描述。需阅读全文才能确认。

## 5. 实验数量与充分性

- 摘要仅给出总体性能提升范围（3.0%~7.6%），没有列出具体实验组数或消融研究细节。
- 无法判断实验的充分性；是否覆盖多中心数据、不同病种、不同放大倍数等关键变量均不得而知。
- 但从投稿渠道（ICML-2026-Accepted，score 9.0）推断，实验部分接受了严格的同行评审，推测实验设计较为充足，且包含必要的消融实验、同类方法对比和统计分析。

## 6. 论文的主要结论与发现

- Cello 在仅使用数百至数千样本训练的条件下，实现了 **3.0%~7.6% 的性能提升**，且 **优于那些在数万样本上预训练的病理基础模型**。
- 验证了在 WSI 分析中显式引入细胞级表示能够 **弥补 patch 级流程与病理学家细胞中心推理之间的鸿沟**。
- 通过细胞-局部-全局的一致性约束，Cello 能够提供 **更可靠、更具可解释性** 的病理分析证据。

## 7. 优点

- **概念新颖**：将细胞级视角统一引入 WSI 建模，更符合病理学家的实践逻辑。
- **框架通用性强**：同时支持局部任务和全局任务，并提供可信的证据输出。
- **数据效率高**：不需要海量预训练样本即可超越大型预训练模型。
- **设计精巧**：蛋白质信号监督、原型对比、门控聚合与一致性目标组合成一个协调的多层次框架。
- **代码开源**，易于复现和推广。

## 8. 不足与局限

- **信息缺失严重**：当前仅依据摘要分析，缺乏详细方法论描述、实验设置和数据，无法深入评估。
- **数据集不明**：未公布是否在多样化、多中心的真实世界数据上验证，泛化能力存疑。
- **任务覆盖度未知**：局部任务和全局任务的具体类型、难度未说明；是否包含罕见病种、不同染色平台等也不清楚。
- **计算成本**：没有提供计算开销信息，细胞级特征提取是否在千兆像素 WSI 上足够高效缺乏证据。
- **对比方法的全面性**：摘要仅提“优于预训练基础模型”，未指明是否对比了最新的 patch 级 or MIL 方法，可能存在选择性报告的风险。
- **可解释性证明**：虽声称提供“可信证据”，但未展示具体的可视化、归因分析或病理专家评估，可信度有待原文证实。

（完）
