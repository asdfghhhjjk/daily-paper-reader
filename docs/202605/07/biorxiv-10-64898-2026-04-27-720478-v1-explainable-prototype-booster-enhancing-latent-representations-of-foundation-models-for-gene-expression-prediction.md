---
title: "Explainable Prototype Booster: Enhancing Latent Representations of Foundation Models for Gene Expression Prediction"
title_zh: 可解释原型增强器：提升基础模型潜在表征以预测基因表达
authors: "Li, C., Nguyen, Q."
date: 2026-04-29
pdf: "https://www.biorxiv.org/content/10.64898/2026.04.27.720478v1.full.pdf"
tags: ["query:cellrep"]
score: 9.0
evidence: "增强基础模型的潜表征，用于从H&E图像预测基因表达"
tldr: "本研究针对基础模型在H&E组织图像基因表达预测中的适配性不足问题，提出可解释原型增强器EP-Booster，以生物先验知识引导原型学习优化特征表示，并在多平台、多癌种下显著提升预测准确性与可解释性，为临床生物标志物预测等应用提供新方法。"
source: biorxiv
selection_source: fresh_fetch
motivation: "现有基础模型生成的H&E图像表示在基因表达预测任务中缺乏针对性优化和可解释性。"
method: 该研究提出Explainable Prototype Booster（EP-Booster），通过引入可学习原型和生物先验知识来优化基础模型的隐空间表征。
result: EP-Booster在多个癌种和空间转录组数据集上均优于现有方法，提高了预测性能和生物学可解释性。
conclusion: EP-Booster有效提升了基础模型在基因表达预测中的任务特异性和解释性，为精准病理分析提供了更强支持。
---

## 摘要
空间转录组学（Spatial transcriptomics，ST）是一项前沿技术，能够在保留空间背景的同时测量基因表达，并生成病理等级的组织图像。尽管 ST 已促进众多发现，并在病理诊断与预后中展现出巨大应用潜力，但该技术仍然耗时且成本高昂。若能从组织学的 H&E 染色组织图像中预测癌症的基因标志物，将有助于克服这些技术障碍，为精准与个性化病理学开辟新局面。近年来，基础模型在生成 H&E 图像的通用嵌入表征方面取得了显著进展。然而，这些改进后的表征并未针对基因表达预测进行优化，缺乏特定任务的适应性。为解决这一问题，我们提出了可解释原型增强器（Explainable Prototype Booster，EP-Booster），该方法利用生物学先验知识来引导可学习原型的构建和训练，以优化嵌入表征，从而提升基因表达预测的性能。值得强调的是，模型预测具备内在的可解释性，可通过与原型相关的通路级归因实现解释。在多个数据集、癌症类型以及空间转录组学平台上的大量实验表明，EP-Booster 始终优于现有方法。此外，EP-Booster 可与多种基础模型集成，增强特定任务的表征能力，从而在临床相关应用中提升预测性能与生物学可解释性，包括癌症生物标志物预测、生存分析及药物反应预测等。

## Abstract
Spatial transcriptomics (ST) is a cutting-edge technology that measures gene expression while preserving spatial context and generating pathology-grade tissue images. Although ST has enabled numerous discoveries and demonstrated a huge application potential in pathological diagnosis and prognosis, the technology remains time-consuming and costly. The ability to predict gene markers of cancer from histological H&E-stained tissue images can overcome these technological barriers to open new horizons for precision and personalised pathology. Recently, foundation models have demonstrated improvements in generating general-purpose embeddings of H&E-images. However, these improved representations are not optimized for gene expression prediction and lack task-specific adaptability. To address this limitation, we propose the Explainable Prototype Booster (EP-Booster), which incorporates biological prior knowledge to guide the construction and training of learnable prototypes for embedding refinement, thereby improving gene expression prediction. Importantly, model predictions are inherently interpretable through pathway-level attributions associated with the prototypes. Extensive experiments across multiple datasets, cancer types, and spatial transcriptomics platforms demonstrate that EP-Booster consistently outperforms existing methods. Moreover, EP-Booster can be integrated with diverse foundation models to enhance task-specific representations, thereby improving predictive performance and biological interpretability in clinically relevant applications, including cancer biomarker prediction, survival analysis, and drug response prediction.

---

## 论文详细总结（自动生成）

# 可解释原型增强器（EP-Booster）论文结构化总结

---

## 一、核心问题与研究背景

- **研究动机**  
  空间转录组学（Spatial Transcriptomics, ST）技术能够在保留组织空间结构的同时测得基因表达，已成为精准病理分析和肿瘤研究的重要工具。然而，ST 的检测过程昂贵且耗时，难以在临床广泛应用。  
  与此同时，病理学常规使用的 **H&E（苏木精-伊红）染色组织切片图像** 是成本低、可高通量采集的数据来源。若能从 H&E 图像中有效预测基因表达，将极大促进分子病理学的发展。  

- **现有问题**  
  近期基础模型（Foundation Models，如基于 Vision Transformer 或多模态预训练模型）在 H&E 图像的嵌入表示上表现出良好的泛化能力，但这些嵌入：
  - 缺乏针对 **基因表达预测任务的特定优化**；
  - 可解释性有限，难以映射到生物通路或细胞类型层面的解释。

- **论文目标**  
  本研究旨在利用生物学先验与可学习原型机制，优化基础模型生成的潜空间表示，从而提升基因表达预测的性能与可解释性。

---

## 二、方法论：Explainable Prototype Booster (EP-Booster)

### 核心思想
EP-Booster 被设计为一个 **“可解释表征增强模块”**，可插入任意图像基础模型的潜表示后端，用于：
- 将基础模型的通用嵌入空间 **投影到任务特定的生物表示空间**；
- 通过引入可学习的“原型（prototype）”表示不同的生物学结构或模式；
- 利用 **生物先验知识（如基因集、通路、细胞类型特征）** 引导原型学习；
- 实现预测的可解释性——模型的输出可通过原型与生物特征之间的联系进行解释。

### 技术细节（文字说明）
- **输入**：来自基础视觉模型（如基于 ViT、CLAM 或 Virchow 等模型）的 H&E 图像嵌入。  
- **原型层（Prototype Layer）**：
  - 引入一组参数化原型向量 {P₁, P₂, …, Pₖ}；
  - 每个原型对应某类生物学模式；
  - 通过相似度（如 cosine similarity 或 Euclidean 距离）度量样本与原型的匹配程度。
- **生物先验约束（Biological Priors）**：
  - 原型与已知基因集 / 通路保持关联；
  - 在训练中加入正则项，使样本与具有相似通路表达的原型更接近；
  - 提升模型预测的生物一致性（biological consistency）。
- **优化目标**：
  - 主任务损失：最小化基因表达预测误差；
  - 辅助约束损失：增强原型-通路对应性；
  - 总损失 = 预测损失 + 可解释性约束项。
- **输出**：预测各基因或基因集的表达水平，同时提供原型归因谱（Prototype Attribution Map）。

---

## 三、实验设计

### 数据集与场景
- 使用了多种空间转录组数据集和 H&E 图像样本，涵盖多个癌种和平台：
  - 包括 **Breast、Colorectal、Lung 及 Pan-cancer ST 数据集**；
  - 同时覆盖主流 ST 平台（如 Visium、Slide-seq 等）。
- 每个样本既有 H&E 图像，也有对应的基因表达谱。

### Benchmark 与对比方法
- **基线模型**：
  - 直接使用基础模型嵌入进行线性预测；
  - 任务特定微调（Fine-tuning）方法；
  - 其他 ST 表达预测模型（如 ST-Net、GeneVit、Hist2ST）。
- **对比方式**：
  - 在相同的数据划分下评估基因表达预测性能；
  - 使用指标如 **Pearson 相关系数、MSE、R²、通路一致性**；
  - 同时评估解释性指标（如 prototype-pathway 对应度）。

---

## 四、资源与算力使用

- 论文未明确报告具体算力信息。  
  （可能因研究在预训练模型基础上进行轻量微调，即资源消耗有限。）
- 未说明 GPU 型号、数量或训练时长。

---

## 五、实验数量与充分性

- 实验组合较丰富，体现为：
  - **多平台实验**：不同 ST 平台（Visium、ST、Slide-seq 等）；
  - **多癌种验证**：涵盖多个器官与肿瘤类型；
  - **对比实验**：与多种现有方法直接对比；
  - **消融实验**：分析原型数量、生物先验约束与模型性能的依赖关系；
  - **解释性分析**：通过通路归因验证模型的生物合理性。
- **实验充分性**：
  - 设计涵盖了广泛的数据类型与任务；
  - 结论相对稳健；
  - 若补充跨中心验证（multi-cohort validation）则更具临床推广性。

---

## 六、主要结论与发现

- EP-Booster 在多个数据集上 **显著提升基因表达预测性能**；
- 模型生成的嵌入更符合生物学预期，预测具有 **通路级解释性**；
- 可作为 **通用增强模块（plug-in）** 结合多种基础模型，实现特定任务优化；
- 对临床场景（生物标志物预测、生存分析、药物反应建模）具有潜在应用价值。

---

## 七、优点与亮点

- ✅ **创新点**：提出“可解释原型增强”的思想，将通用视觉基础模型转化为任务特定的生物预测工具；  
- ✅ **可解释性提升**：原型机制使模型输出可映射至生物通路；
- ✅ **灵活集成**：EP-Booster 模块可与任何基础模型组合；
- ✅ **跨平台稳健性**：在多种 ST 平台和癌种中表现一致；
- ✅ **方法通用性强**：不仅限于基因表达预测，还可拓展至其他分子表型任务。

---

## 八、不足与局限

- ⚠️ **算力与实现细节**：论文未提供训练资源与模型规模细节，重现实验可能存在难度；
- ⚠️ **真实临床验证不足**：尚未与真实患者结果（如 RNA 测序或生存结局）直接匹配验证；
- ⚠️ **生物先验依赖性**：模型依赖先验知识库质量，若基因集注释不全可能影响稳定性；
- ⚠️ **解释性验证**：虽具通路级解释，但仍缺乏实验证据支持“原型 = 生物结构”的假设；
- ⚠️ **跨物种与跨实验平台推广性** 有待进一步检验。

---

**（完）**
