---
title: "Cello: A Universal Cell-wise Feature Aggregation framework for  Reliable  Pathology Images Analysis"
title_zh: Cello：一种用于可靠病理图像分析的通用细胞级特征聚合框架
authors: "Hengrui Lou, Weihan Li, Jiazhen Yang, Lingxiang Jia, Shengxuming Zhang, Linyun Zhou, Xiuming Zhang, Zhenyang Wang, Mingli Song, Zunlei Feng"
date: 2026-04-30
pdf: "https://openreview.net/pdf/0fac7f88f69a8fee60081cbee4e3d07d13b48f75.pdf"
tags: ["query:cellseg"]
score: 9.0
evidence: 细胞级特征聚合，将细胞级表示融入WSI建模，直接利用细胞分割/分类结果完成下游任务。
tldr: 现有计算病理流程依赖图块级特征提取，缺少病理医生使用的细胞级推理。本文提出Cello框架，通过蛋白质信号监督的细胞级学习，将细胞表示融入全切片建模，在千兆像素约束下保留细微细胞线索。实验表明，Cello在诊断和预后预测上优于传统方法，且能够提供可信的证据支持，实现了从细胞到切片的统一可靠分析。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 当前WSI分析依赖图块级特征，忽视细胞级精细线索，限制对微小病灶的灵敏度。
method: 提出Cello，通过蛋白质信号监督的细胞级学习，将细胞表示聚合到WSI模型中。
result: 在局部与全局任务上表现优于传统方法，并提供可信证据。
conclusion: Cello实现了细胞级到WSI级的统一可靠建模，提升病理图像分析精度。
---

## Abstract
Computational pathology has made progress in diagnosis and prognosis prediction from whole slide images (WSIs), yet pipelines still rely on patch-level feature extraction and aggregation, departing from the cell-centric reasoning used by pathologists.
This gap limits sensitivity to micro-lesions and subtle changes, and current methods rarely provide a unified solution that supports both local and global tasks with trustworthy evidence. We propose Cello, a universal cell-wise feature aggregation framework for reliable pathology image analysis. Cello integrates cell-level representations into WSI modeling via protein-signal–supervised cell-wise learning, preserving fine-grained cellular cues under gigapixel constraints. For local tasks, Cello introduces a flexible prototype-based contrastive module for scalable, task-adaptive representation learning. For global tasks, Cello adopts a weakly supervised gated aggregation that can widely leverage WSI labels. Finally, a cell–local–global decision-route consistency objective dynamically aggregates cellular evidence and aligns local predictions with global outcomes, improving reliability and faithfulness. 
Trained with only hundreds to thousands of samples, Cello achieves performance gains of 3.0%~7.6% and outperforms SOTA pathology foundation models pretrained on tens of thousands of samples. Code is available at https://github.com/HengruiLou/Cello.

---

## 论文详细总结（自动生成）

## 1. 论文的核心问题与整体含义

- **研究背景**：计算病理学在利用全切片图像（WSIs）进行诊断和预后预测方面已取得进展，但主流流程仍依赖图块（patch）级特征的提取与聚合，这偏离了病理医生以细胞为中心进行推理的实践。
- **核心问题**：图块级方法难以捕捉微病灶和细微的细胞形态变化，且现有方案很少能同时支持局部和全局任务，并提供具有可信证据的统一分析框架。
- **本文意图**：提出 Cello，一个通用的细胞级特征聚合框架，旨在将病理医生的细胞中心推理方式引入 WSI 建模，在千兆像素尺度下保留精细的细胞线索，实现从细胞到切片级别的统一可靠分析。

## 2. 论文提出的方法论

Cello 的方法围绕细胞级表示的学习、聚合与对齐展开，核心思想及关键技术细节如下：

- **蛋白质信号监督的细胞级学习**
  - 利用与蛋白质表达相关的信号作为监督，训练模型捕获具有病理意义的细胞表示。这一步保留了千兆像素图像中不易被图块特征捕捉的细微细胞特征。
- **面向局部任务的原型对比模块**
  - 针对分类、检测等局部任务，设计了一种基于原型的柔性对比学习策略，使得特征表示可以按任务自适应调整，同时保持较好的可扩展性。
- **面向全局任务的弱监督门控聚合**
  - 对于切片级的全局预测（如患者预后），采用弱监督方式，通过门控机制动态聚合来自各细胞的证据，充分利用切片级别的标签信息。
- **细胞–局部–全局决策路径一致性目标**
  - 提出一个新的约束目标，动态整合细胞级证据，并强制局部预测与全局预测在决策逻辑上保持一致。这一机制既提升了模型的可信度，也提高了对真实病理关联的忠实程度。

（无具体公式，原文中可能包含数学表达，但当前提供的内容未涉及。）

## 3. 实验设计

由于提供的 PDF 提取失败，仅能从摘要和元数据获得有限的实验信息：

- **数据集与场景**：文中未明确列出具体数据集。根据“局部与全局任务”“诊断和预后预测”等描述，推测覆盖了如癌症分型、微病灶检测、生存预测等多种病理分析场景。
- **基准（Benchmark）**：声称与当前最优（SOTA）的病理基础模型比较，这些模型曾在数万样本上预训练。
- **对比方法**：未给出具体名称，但提到了“SOTA pathology foundation models”。
- **训练规模**：Cello 仅使用数百至数千个样本进行训练，即在小样本条件下达到了优于大规模预训练模型的性能。
- **性能提升**：主要结果提升了 3.0% 至 7.6% 的相对性能。

> 因为文本提取受限，关于数据集名称、评价指标、具体百分比的对应任务等细节无法补全，只能依据以上摘要内容推测。

## 4. 资源与算力

- 文中完全没有提及所使用的 GPU 型号、数量、训练时长或任何计算资源细节。这一点在提供的信息中是缺失的。

## 5. 实验数量与充分性

- **实验数量**：无法得知确切组数。摘要暗示了在多个任务（局部、全局）、多组对比（与预训练模型等）上进行了评估，并且很可能包含消融实验（因提出了多个模块），但均未给出定量描述。
- **充分性评估**：
  - 从宣称的效果来看，实验至少覆盖了诊断与预后两类任务，且在小样本条件下与大规模预训练模型对标，具有一定说服力。
  - 客观性与公平性方面，因缺乏对数据集、训练细节和对比方法的具体说明，难以准确判断。仅凭摘要无法认定实验是否完全公平（例如是否使用相同的训练配置，预训练模型微调方式等）。
  - 缺失的实验细节（如指标、误差棒、消融研究的具体结果）使得目前的总结无法对实验的充分性做出确凿评价。

## 6. 论文的主要结论与发现

- Cello 成功将细胞级特征融入 WSI 建模，实现了从细胞到切片的统一框架。
- 该框架在基于数百至数千样本的训练下，性能显著优于在数万样本上预训练的病理基础模型，提升幅度达 3.0%~7.6%。
- 细胞–局部–全局决策路径一致性机制可以增强模型的可信度和预测的忠实性，为病理分析提供可解释的证据支持。

## 7. 优点

- **病理驱动的设计理念**：回归细胞中心的推理方式，更贴近病理医生的真实诊断流程。
- **统一且灵活**：支持局部与全局任务，使用原型对比和门控聚合分别适应不同需求，无需为不同任务切换底层架构。
- **小样本高效性**：仅需数百至数千级样本即可超越需要海量预训练数据的 SOTA 模型，数据利用效率高。
- **可信证据机制**：通过决策路径一致性，让模型预测能够回溯到细胞级线索，提升在临床应用中的可靠性。

## 8. 不足与局限

- **实验细节严重缺失**：由于文本提取失败，本总结完全依赖摘要和元数据。无法获知具体使用的数据集、对比方法、评价指标、消融研究成果等，导致对方法全面性和稳健性的评估极为受限。
- **可复现性与偏差风险**：未提供算力、超参数、训练耗时等信息，复现可能存疑。同时，在小样本下超越大规模预训练模型的结论，其泛化性是否受数据集选择偏差影响，无法判断。
- **应用限制**：方法立足于细胞分割/分类结果的可用性，对前端细胞检测模型的精度存在依赖；文中未讨论当细胞分割不完美时框架的鲁棒性。

（完）
