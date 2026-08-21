---
title: "Cello: A Universal Cell-wise Feature Aggregation framework for  Reliable  Pathology Images Analysis"
title_zh: Cello：用于可靠病理图像分析的通用细胞级特征聚合框架
authors: "Hengrui Lou, Weihan Li, Jiazhen Yang, Lingxiang Jia, Shengxuming Zhang, Linyun Zhou, Xiuming Zhang, Zhenyang Wang, Mingli Song, Zunlei Feng"
date: 2026-04-30
pdf: "https://openreview.net/pdf/0fac7f88f69a8fee60081cbee4e3d07d13b48f75.pdf"
tags: ["query:cell-path"]
score: 10.0
evidence: 将细胞级表示整合到全切片图像建模中，用于可靠的病理分析
tldr: Cello针对计算病理中全切片图像分析依赖补丁级特征、缺乏细胞中心推理的问题，提出通用细胞级特征聚合框架，通过蛋白信号监督的细胞级学习，在吉像素限制下保留细微细胞线索，支持局部和全局任务并提供可信证据。该框架为病理图像分析提供了统一解决方案，增强了诊断和预后的敏感性。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 现有WSI分析依赖补丁级特征，偏离病理学家的细胞中心推理，限制了对微病灶和细微变化的敏感性。
method: 提出Cello框架，通过蛋白信号监督的细胞级学习，将细胞级表示整合到WSI建模中，保留细微细胞线索。
result: 在吉像素约束下支持局部和全局任务，提供可信证据。
conclusion: 为病理图像分析提供了统一的细胞级解决方案，提升了可靠性和敏感性。
---

## Abstract
Computational pathology has made progress in diagnosis and prognosis prediction from whole slide images (WSIs), yet pipelines still rely on patch-level feature extraction and aggregation, departing from the cell-centric reasoning used by pathologists.
This gap limits sensitivity to micro-lesions and subtle changes, and current methods rarely provide a unified solution that supports both local and global tasks with trustworthy evidence. We propose Cello, a universal cell-wise feature aggregation framework for reliable pathology image analysis. Cello integrates cell-level representations into WSI modeling via protein-signal–supervised cell-wise learning, preserving fine-grained cellular cues under gigapixel constraints. For local tasks, Cello introduces a flexible prototype-based contrastive module for scalable, task-adaptive representation learning. For global tasks, Cello adopts a weakly supervised gated aggregation that can widely leverage WSI labels. Finally, a cell–local–global decision-route consistency objective dynamically aggregates cellular evidence and aligns local predictions with global outcomes, improving reliability and faithfulness. 
Trained with only hundreds to thousands of samples, Cello achieves performance gains of 3.0%~7.6% and outperforms SOTA pathology foundation models pretrained on tens of thousands of samples. Code is available at https://github.com/HengruiLou/Cello.

---

## 论文详细总结（自动生成）

# Cello 论文总结

> 说明：提供的提取文本仅包含论文元数据与摘要，未包含全文细节；以下总结基于现有摘要、标题、作者声明等信息，部分条目（如具体数据集、算力）因原文缺失而无法展开，已明确标注。

## 1. 论文的核心问题与整体含义

- **研究背景**：计算病理学在利用全切片图像（WSI）进行诊断和预后预测方面已取得进展，但现有流程仍主要依赖“补丁级（patch-level）特征提取与聚合”。
- **核心问题**：
  - 这种补丁级建模方式偏离了病理学家“以细胞为中心”的推理逻辑。
  - 导致对微病灶和细微病理变化的敏感性不足。
  - 当前方法很少能提供统一框架，同时支持局部任务和全局任务，并给出可信的证据。
- **整体含义**：Cello 旨在提出一个通用的细胞级特征聚合框架，将细胞级表示整合到 WSI 建模中，从而在吉像素（gigapixel）尺度约束下保留细微的细胞线索，提升病理图像分析的可靠性和敏感性。

## 2. 论文提出的方法论

- **核心思想**：通过“蛋白信号监督的细胞级学习”（protein-signal–supervised cell-wise learning），将细胞级表示融入 WSI 建模，弥补补丁级特征丢失的细粒度信息。
- **关键技术模块**：
  - **局部任务模块**：引入一种灵活的“基于原型的对比学习模块”（prototype-based contrastive module），用于可扩展、任务自适应的表示学习。
  - **全局任务模块**：采用“弱监督门控聚合”（weakly supervised gated aggregation），能够广泛利用 WSI 级标签进行全局建模。
  - **决策一致性模块**：提出“细胞–局部–全局决策路由一致性目标”（cell–local–global decision-route consistency objective），动态聚合细胞证据，并对齐局部预测与全局结果，以提高模型的可靠性和忠实性。
- **算法流程（文字描述）**：
  1. 在蛋白信号监督下学习细胞级表示。
  2. 对局部任务使用原型对比模块，对全局任务使用弱监督门控聚合。
  3. 通过决策路由一致性约束，将细胞级、局部级、全局级预测进行对齐和融合。
- **训练数据规模**：摘要明确指出，Cello 仅使用“数百到数千个样本”进行训练。

## 3. 实验设计

- **任务类型**：涵盖局部任务和全局任务，体现框架的统一性。
- **对比对象**：与 SOTA 病理基础模型（pathology foundation models）对比；这些基线模型通常在数万样本上预训练。
- **性能表现**：Cello 在仅使用数百到数千样本训练的情况下，取得 3.0%~7.6% 的性能提升，并超越上述大规模预训练的 SOTA 模型。
- **局限说明**：提供的文本未列出具体数据集名称、具体 benchmark、具体对比方法列表或评估指标，因此无法展开说明实验场景的细节。

## 4. 资源与算力

- 提供的摘要和元数据中**未明确提及** GPU 型号、GPU 数量、训练时长、显存消耗等算力信息。
- 因此无法从当前文本中总结具体算力资源使用情况，该信息可能在论文正文中但未被提取。

## 5. 实验数量与充分性

- **可推断的实验范围**：
  - 至少包含局部任务和全局任务两类评估。
  - 与 SOTA 病理基础模型进行了对比。
  - 报告了性能提升区间（3.0%~7.6%），说明可能涉及多个数据集或任务。
- **充分性与公平性评估**：
  - 优点：摘要强调 Cello 使用少量样本即超越大规模预训练模型，说明实验设计具有一定公平性（训练数据规模差异明显）。
  - 不足：由于缺少具体实验组数、消融实验、统计显著性检验、跨中心验证等细节，无法对实验充分性和客观性做出准确判断。
  - 可能存在偏差风险：摘要未说明数据集来源、类别分布、外部验证或泛化性测试，需阅读全文验证。

## 6. 论文的主要结论与发现

- Cello 作为一个通用的细胞级特征聚合框架，能够在仅使用数百到数千样本的情况下，实现 3.0%~7.6% 的性能提升。
- 其性能优于在数万样本上预训练的 SOTA 病理基础模型，表明细胞级建模具有更高的数据效率和任务适应性。
- 该框架能够同时支持局部和全局任务，并通过决策路由一致性机制提供可信的细胞证据，从而增强病理诊断和预后预测的可靠性与敏感性。
- 代码已在 GitHub 公开：https://github.com/HengruiLou/Cello

## 7. 优点

- **方法层面**：
  - 回归细胞中心建模，更贴合病理学家的实际推理方式。
  - 统一局部与全局任务，避免为不同任务设计独立流程。
  - 蛋白信号监督的细胞级学习有助于保留补丁级特征中丢失的细微线索。
  - 决策路由一致性目标增强了模型的可解释性和证据可信度。
  - 数据效率高，仅需数百到数千样本即可达到或超越大规模预训练模型。
- **实验层面**：
  - 与大规模预训练 SOTA 模型对比，展示了少样本条件下的优势。
  - 同时覆盖局部和全局任务，验证了框架的通用性。

## 8. 不足与局限

- **信息缺失导致的评估局限**：
  - 提供文本未包含具体数据集、任务定义、评价指标、统计检验和消融实验细节，无法全面评估方法有效性。
  - 未说明算力消耗，无法判断实际部署成本和可复现性。
- **潜在方法局限**：
  - 蛋白信号监督可能需要额外的蛋白表达数据或标注，增加数据获取难度。
  - 细胞级建模在吉像素 WSI 上的计算和存储开销可能较高，文中未提供效率分析。
  - 仅报告了相对提升和超越 SOTA，未给出绝对性能或临床可接受性指标。
- **实验覆盖风险**：
  - 未说明是否涵盖多种癌症类型、不同染色平台、多中心数据或外部验证集。
  - 缺乏与最新补丁级方法的详细公平对比（如相同数据量下的对比）。
  - 摘要层面的积极结论可能存在选择性报告风险，需结合全文和代码验证。

（完）
