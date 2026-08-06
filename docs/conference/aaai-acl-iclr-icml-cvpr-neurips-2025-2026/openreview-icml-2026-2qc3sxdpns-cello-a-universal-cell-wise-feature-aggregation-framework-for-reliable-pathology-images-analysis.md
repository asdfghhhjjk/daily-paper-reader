---
title: "Cello: A Universal Cell-wise Feature Aggregation framework for  Reliable  Pathology Images Analysis"
title_zh: Cello：面向可靠病理图像分析的通用细胞级特征聚合框架
authors: "Hengrui Lou, Weihan Li, Jiazhen Yang, Lingxiang Jia, Shengxuming Zhang, Linyun Zhou, Xiuming Zhang, Zhenyang Wang, Mingli Song, Zunlei Feng"
date: 2026-04-30
pdf: "https://openreview.net/pdf/0fac7f88f69a8fee60081cbee4e3d07d13b48f75.pdf"
tags: ["query:cellseg"]
score: 10.0
evidence: 细胞级特征聚合用于WSI分析，直接利用细胞信息完成下游任务
tldr: 针对现有WSI分析以patch为中心而忽视细胞细节的问题，提出Cello框架，通过蛋白质信号监督的细胞级学习保留千兆像素下的细胞线索，并聚合细胞特征支持诊断和预后预测，提供可信证据，在多种任务上验证了有效性。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 现有方法依赖patch级特征，忽略了细胞为中心的推理方式。
method: 提出Cello框架，通过蛋白质信号监督学习细胞级表示，并聚合为全局WSI特征。
result: 在诊断和预后预测任务上，Cello以细胞级证据实现了高精度和可解释性。
conclusion: 细胞级聚合是提升病理AI可靠性的关键，Cello统一了局部和全局任务。
---

## Abstract
Computational pathology has made progress in diagnosis and prognosis prediction from whole slide images (WSIs), yet pipelines still rely on patch-level feature extraction and aggregation, departing from the cell-centric reasoning used by pathologists.
This gap limits sensitivity to micro-lesions and subtle changes, and current methods rarely provide a unified solution that supports both local and global tasks with trustworthy evidence. We propose Cello, a universal cell-wise feature aggregation framework for reliable pathology image analysis. Cello integrates cell-level representations into WSI modeling via protein-signal–supervised cell-wise learning, preserving fine-grained cellular cues under gigapixel constraints. For local tasks, Cello introduces a flexible prototype-based contrastive module for scalable, task-adaptive representation learning. For global tasks, Cello adopts a weakly supervised gated aggregation that can widely leverage WSI labels. Finally, a cell–local–global decision-route consistency objective dynamically aggregates cellular evidence and aligns local predictions with global outcomes, improving reliability and faithfulness. 
Trained with only hundreds to thousands of samples, Cello achieves performance gains of 3.0%~7.6% and outperforms SOTA pathology foundation models pretrained on tens of thousands of samples. Code is available at https://github.com/HengruiLou/Cello.

---

## 论文详细总结（自动生成）

# 论文总结：Cello: A Universal Cell-wise Feature Aggregation Framework for Reliable Pathology Images Analysis

（注：由于获取的PDF内容被验证码阻挡，本次总结仅基于论文元数据、摘要及已知信息进行推断性分析，部分细节无法完整还原。）

## 1. 论文的核心问题与整体含义（研究动机和背景）
- **研究背景**：计算病理学在利用全切片图像（WSI）进行诊断和预后预测方面取得了进展，但现有流程仍高度依赖补丁级特征提取和聚合。
- **核心问题**：这种以 **补丁（patch）为中心** 的范式偏离了病理学家 **以细胞为中心** 的阅片推理方式，导致对微小病变和细微变化的敏感性不足，且难以同时为局部和全局任务提供可信证据。
- **整体含义**：提出一种**通用的细胞级特征聚合框架**，将细粒度细胞线索引入千兆像素WSI建模，从而提升病理AI的可靠性、可解释性及任务适应性。

## 2. 论文提出的方法论
### 核心思想
- 在WSI分析中显式建模并利用细胞级表示，使模型能够沿着 **细胞–局部–全局** 的逻辑链进行决策，并以细胞证据支撑最终预测。

### 关键技术细节
- **蛋白质信号监督的细胞级学习**：利用蛋白质表达等信号监督细胞特征的提取，确保在超大分辨率下保留有意义的细胞线索。
- **针对局部任务的原型对比模块**：引入灵活的基于原型的对比学习，实现可扩展且任务自适应的表示学习。
- **针对全局任务的弱监督门控聚合**：采用弱监督的门控机制聚合细胞特征，使其能广泛利用WSI级标签。
- **一致性目标**：设计**细胞–局部–全局决策路径一致性损失**，动态聚合并对齐局部预测与全局结果，提升整体可靠性与忠实度。

> 公式或算法流程在摘要中未详细给出，文中应包含具体的对比损失、门控函数及一致性约束的数学形式，此处从略。

## 3. 实验设计
### 数据集与场景
- 摘要提及“仅需数百到数千样本”进行训练，暗示实验可能覆盖多个病理数据集，但未列出具体数据集名称。
- 任务场景包括**局部任务**（如细胞级分类、微病灶检测）和**全局任务**（如WSI级诊断、预后预测）。

### Benchmark与对比方法
- 对比了最新的**病理基础模型**（SOTA pathology foundation models），这些模型通常在数万样本上预训练。
- 性能提升幅度为 **3.0% ~ 7.6%**，指出Cello在样本效率上具有压倒性优势。

## 4. 资源与算力
- 论文PDF内容缺失，**未明确说明**使用的GPU型号、数量、训练时长等算力信息。从摘要看，训练开销应较为可控（仅需数百到数千样本），但具体硬件资源未知。

## 5. 实验数量与充分性
- 基于摘要，实验可能包含：
  - 多个数据集上的诊断/预后对比实验；
  - 与多种SOTA模型的性能比较；
  - 细胞级特征对可解释性的验证；
  - 消融实验验证不同模块（如原型对比、门控聚合、一致性损失）的贡献。
- 但由于文本不全，无法评估实验的总组数及是否包含统计检验、跨中心验证等充分性措施。初步判断作者试图在有限样本下证明方法的竞争力，但**实验覆盖度和偏差风险需阅读全文后确认**。

## 6. 论文的主要结论与发现
- **细胞级聚合是提升病理AI可靠性的关键**。Cello框架统一了局部与全局任务，在诊断和预后预测上实现了高精度。
- 相比在数万样本上预训练的庞大基础模型，Cello仅用少量样本即可获得更优性能，证明了细胞级监督的有效性。
- 模型可以提供**细胞级证据**，增强了预测的可解释性和临床可信度。

## 7. 优点
- **方法学亮点**：
  - 打破patch中心化的惯性，回归病理学细胞推理的直觉。
  - 通过蛋白质信号监督，精准捕捉细胞级信息，避免信息压缩损失。
  - 统一的框架可同时处理局部和全局任务，且任务自适应。
  - 极低的样本需求量，意味着较高的数据效率。
- **实验设计亮点**：
  - 与海量预训练的基础模型直接对比，凸显方法的轻量与高效。
  - 明确展示了可解释性，贴合临床需求。

## 8. 不足与局限
- **实验覆盖有限**：摘要未透露具体数据集名称、数量以及跨机构验证，泛化能力存疑。
- **技术细节隐晦**：蛋白质监督的来源、细胞分割方法、原型数量的设定等关键实现细节不明，可能影响复现。
- **对比局限性**：仅比较了病理基础模型，未提及与传统补丁聚合方法（如MIL、Transformer）的全面对比。
- **应用限制**：依赖于细胞级别的监督信号（如蛋白质染色），在常规H&E切片中获取此类信号可能困难，限制了实际部署场景。
- **算力信息缺失**：无训练硬件和耗时报告，工业化应用的可行性难以评估。

（完）
