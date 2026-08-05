---
title: "MoLF: Mixture-of-Latent-Flow for Pan-Cancer Spatial Gene Expression Prediction from Histology"
title_zh: "MoLF: 用于泛癌组织学空间基因表达预测的混合潜流模型"
authors: "Susu Hu, Stefanie Speidel"
date: 2026-04-30
pdf: "https://openreview.net/pdf/b32ff4edadd3fd921f2890cf1c725acd27272ea2.pdf"
tags: ["query:cellseg"]
score: 8.0
evidence: 从组织学图像预测空间基因表达，用于泛癌数字病理图像分析。
tldr: 当前从组织学图像推断空间基因表达的方法多限于单一组织，泛癌训练受到异质性挑战。该论文提出MoLF（混合潜流模型），利用条件流匹配和专家混合速度场，动态路由输入，从组织学图像预测基因表达。在多个癌症类型上实现了可扩展的组织基因组学分析，展现了数字病理图像在分子特征推断中的价值。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 单组织建模无法利用跨癌症的共同生物学原理，限制了泛化能力。
method: 提出MoLF模型，通过条件流匹配和专家混合速度场实现泛癌组织基因表达预测。
result: 在多癌症数据上有效预测空间基因表达，性能优于单组织模型。
conclusion: MoLF为数字病理图像提供了一种可扩展的分子推断工具，增强了组织学分析的生物学解释力。
---

## Abstract
Inferring spatial transcriptomics (ST) from histology enables scalable histogenomic profiling, yet current methods are largely restricted to single-tissue models. This fragmentation fails to leverage biological principles shared across cancer types and hinders application to data-scarce scenarios. While pan-cancer training offers a solution, the resulting heterogeneity challenges monolithic architectures. To bridge this gap, we introduce **MoLF** (*Mixture-of-Latent-Flow*), a generative model for pan-cancer histogenomic prediction. MoLF leverages a conditional Flow Matching objective to map noise to the gene latent manifold, parameterized by a Mixture-of-Experts (MoE) velocity field. By dynamically routing inputs to specialized sub-networks, this architecture effectively decouples the optimization of diverse tissue patterns. Our experiments demonstrate that MoLF establishes a new state-of-the-art, consistently outperforming both specialized and foundation model baselines on pan-cancer benchmarks. Furthermore, MoLF exhibits zero-shot generalization to cross-species data, suggesting it captures fundamental, conserved histo-molecular mechanisms.

---

## 论文详细总结（自动生成）

## 1. 论文的核心问题与整体含义

- **研究动机**：目前从组织学图像推断空间转录组（ST）的方法大多只能针对单一组织建模，割裂了不同癌症类型间共享的生物学规律，也难以适应数据稀缺的场景。
- **核心问题**：如何在泛癌（pan‑cancer）层面上，从组织学图像中准确预测空间基因表达，同时克服多组织、多癌症带来的高度异质性挑战。
- **整体含义**：该工作试图用统一的生成式模型桥接组织形态与分子特征，为数字病理图像提供可扩展、可迁移的分子推断工具。

## 2. 论文提出的方法论

- **模型名称**：MoLF（Mixture‑of‑Latent‑Flow）。
- **核心思想**：将条件流匹配（Conditional Flow Matching）用于从噪声到基因潜在流形的映射，并通过专家混合（Mixture‑of‑Experts, MoE）参数化速度场（velocity field），根据不同输入动态路由到专门的子网络，解耦各异质组织模式的优化。
- **关键技术细节**（基于摘要与元数据文字说明）：
  - 模型的生成目标是：给定组织学图像，输出对应空间点的基因表达估计。
  - 训练过程采用流匹配目标，学习一个从随机噪声到基因表达潜空间的连续变换。
  - 把映射动力学中的速度场设计为 MoE 结构，由多个“专家”子网络组成，并利用门控机制为每个输入样本/区域激活最相关的专家，以适应不同癌症类型的组织学–分子关联模式。
- 未给出完整公式，但流程可概括为：噪声 → 由条件（组织学特征）驱动的流匹配过程 → 专家混合速度场动态选择路径 → 生成基因表达。

## 3. 实验设计

- **数据集/场景**：多癌症组织微阵列或全切片组织学图像及其配准的空间转录组数据（具体数据集名称未给出，论文标记为泛癌 benchmark）。
- **基准比较方法**：包括单一组织专用模型和当前的基础模型（foundation model baselines）基线。
- **对比维度**：泛癌预测性能，可能还包括对未见过物种的零样本泛化能力（cross‑species zero‑shot）。
- **实验结果**：MoLF 在泛癌 benchmark 上达到新的最优性能，一致优于专用模型和基础模型基线。

## 4. 资源与算力

- 文中未提供任何 GPU 型号、数量、训练时长、显存消耗等与算力相关的具体信息。无法给出总结。

## 5. 实验数量与充分性

- **组数**：根据现有文字，能确认至少包含泛癌多数据集对比实验、与单组织模型和 foundation 模型的比较，以及跨物种零样本迁移实验。未提及消融实验的具体数目。  
- **充分性与公平性**：从声称的新 SOTA 和零样本泛化来看，实验覆盖了跨组织、跨物种场景，对比了代表性基线，具有一定的客观性和公平性。但受限于摘要信息，无法评估实验样本量、统计显著性、交叉验证等更细致的充分性指标。

## 6. 论文的主要结论与发现

- MoLF 能够有效解决泛癌组织学预测空间基因表达中的异质性问题，性能显著优于现有方法。
- 通过 MoE 速度场和流匹配，模型可解耦不同组织模式的学习，实现了跨癌种的可扩展组织基因组学推断。
- 模型展现了跨物种零样本泛化能力，暗示它可能捕捉到保守的组织–分子关联机制。

## 7. 优点

- **方法创新**：首次将条件流匹配与专家混合结合，用于泛癌病理图像到基因表达的跨模态生成任务，结构上自然解耦异质性。
- **性能优势**：在泛癌设定下取得最佳结果，并具备跨物种泛化能力，显示出较强的生物普适性。
- **应用潜力**：为数据稀缺场景（如罕见癌种、动物模型）提供了无需重新训练即可推断分子特征的工具。

## 8. 不足与局限

- **信息不完整**：由于仅能参考摘要和元数据，难以评估具体的实验规模、统计可靠性和消融验证深度。
- **可能的实验覆盖缺失**：未提及对空间分辨率、批次效应、染色差异等实际病理场景的鲁棒性测试。
- **应用限制**：泛癌训练依赖大规模、配准良好的组织学‑转录组配对数据，现实中此类数据的获取和标准化仍面临困难；跨物种零样本泛化虽被提及，但具体物种和任务范围未知。
- **偏差风险**：若训练数据中某些癌症类型比例失衡，MoE 的门控机制可能倾向于主要癌种，影响小样本癌种的预测公平性。

（完）
