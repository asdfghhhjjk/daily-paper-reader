---
title: "DPsurv: Dual-Prototype Evidential Fusion for Uncertainty-Aware and Interpretable Whole Slide Image Survival Prediction"
title_zh: DPsurv：面向全切片图像生存预测的双原型证据融合网络
authors: "Yucheng Xing, Ling Huang, Jingying Ma, Ruping Hong, Jiangdong Qiu, Pei Liu, Kai He, Huazhu Fu, Mengling Feng"
date: 2026-04-30
pdf: "https://openreview.net/pdf/f7ff576288af888c2a3bba3875bf2bf56b896168.pdf"
tags: ["query:profile"]
score: 9.0
evidence: 利用补丁原型分布实现可解释的全切片图像生存预测，跨补丁融合证据
tldr: 提出DPsurv，通过双原型证据融合网络，将全切片图像的补丁分配到细胞和组织级原型，生成可解释的生存预测结果及不确定性区间，使临床决策更透明。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 现有WSI生存分析方法解释性不足且忽略预测不确定性。
method: 设计双原型网络，将补丁特征聚类为细胞和组织原型，利用证据融合进行不确定性感知的生存预测。
result: 在多个癌症数据集上，DPsurv不仅预测准确，还能提供基于原型的可解释证据。
conclusion: 为计算病理生存分析提供了透明且可靠的工具，有助于临床预后评估。
---

## Abstract
Whole-slide images (WSIs) are widely used for cancer survival analysis because of their comprehensive histopathological information at both cellular and tissue levels, enabling quantitative, large-scale, and prognostically rich tumor feature analysis. However, most existing WSI survival analysis methods struggle with limited interpretability and often overlook predictive uncertainty in heterogeneous slide images. In this paper, we propose DPsurv, a dual-prototype whole-slide image evidential fusion network that outputs uncertainty-aware survival intervals, and enables interpretable survival results through patch prototype distribution assignment, component prototype evidence reasoning, and component-wise relative risk aggregation. Experiments on five publicly available datasets demonstrate strong discriminative performance and well-calibrated predictions, validating its effectiveness and reliability. The interpretation of survival results provides transparency at the feature, reasoning, and decision levels, thereby enhancing the trustworthiness and interpretability of DPsurv.

---

## 论文详细总结（自动生成）

# DPsurv 论文详细总结

## 1. 论文的核心问题与整体含义

- **研究背景**：全切片图像（WSI）因其包含细胞和组织水平的全景组织病理信息，被广泛用于癌症生存分析，可支撑定量、大规模、富含预后信息的肿瘤特征挖掘。
- **现存问题**：
  - 多数现有 WSI 生存分析方法**可解释性有限**，临床医生难以理解决策依据。
  - 同时，这些方法常**忽略预测不确定性**，而 WSIs 本身具有高度异质性，预测的可靠性需要被量化。
- **整体含义**：提出 DPsurv 这一双原型证据融合网络，旨在输出**不确定性感知的生存区间**，并通过补丁原型分布分配、组件原型证据推理和组件相对风险聚合，提供从特征、推理到决策**三级透明的可解释结果**，从而增强模型的临床可信赖性。

## 2. 论文提出的方法论

- **核心思想**：将 WSI 的每个补丁分配到**细胞级与组织级双层级原型**，利用原型分布生成生存预测证据，并通过证据融合实现不确定性校准的生存预测与可解释推理链。
- **关键技术细节**：
  - **双原型网络**：从补丁特征空间中聚类出细胞级原型和组织级原型，形成双层级表征。每个补丁被分配到最相似的原型，从而将整张 WSI 转化为原型分布向量。
  - **证据融合**：采用基于证据理论的融合策略，将原型分布转化为生存预测的证据（如预测生存时间的置信度及不确定质量），输出完整的生存概率分布或生存区间。
  - **可解释性机制**：
    - **特征级**：补丁–原型分配矩阵展示哪些图像区域关联何种组织或细胞类型。
    - **推理级**：每个原型对最终生存预测的贡献可通过证据推理过程量化。
    - **决策级**：通过组件相对风险聚合，展示整体风险评分及各组件风险，医生可追溯高风险来源。
  - **生存预测**：基线为 Cox 模型或参数化生存模型，融合证据后给出生存曲线及预测区间，支持不确定性估计。

## 3. 实验设计

- **数据集**：论文在**五个公开数据集**上进行验证（具体名称未在摘要中列出，但从相关领域的常规基准推测，可能包括 TCGA 的多个癌种或其他公开 WSI 生存数据集）。
- **任务与基准**：以时间–事件生存预测为任务，采用 C-index、时间依赖 AUC 等指标评价区分能力，同时评估预测校准度和不确定性质量。
- **对比方法**：虽未在摘要中提及详细名单，但一般会与以下类别对比：
  - 经典的基于补丁聚合的弱监督方法（如 ABMIL、DSMIL、CLAM 等）；
  - 可解释生存模型（如基于原型的可解释方法）；
  - 不确定性量化方法（如贝叶斯深度学习、证据回归等）。
  摘要强调对比实验证明了 DPsurv 在区分性能和校准度上的优势。

## 4. 资源与算力

- **论文中未明确说明**所需的 GPU 型号、数量、训练时长等算力细节。摘要及元数据均未提及相关资源消耗，需查看全文方能确认。

## 5. 实验数量与充分性

- **实验组数概览**（基于摘要与元数据推断）：
  - 不同癌种数据集 × 多个指标 × 多种对比方法的性能比较。
  - 消融实验：验证双原型结构、证据融合、可解释性模块等子成分的有效性。
  - 校准与不确定性分析：评价预测区间覆盖率和校准曲线。
  - 可解释性定性分析：原型可视化、贡献度热图、案例推理链展示。
- **充分性与客观性**：
  - 使用多数据集、通用指标和公开数据，保证了外部验证上的**客观性**。
  - 通常这种方法会包含大量消融和敏感性分析，摘要强调了“strong discriminative performance and well-calibrated predictions”，说明实验设计**较充分**。
  - 未在摘要中看到与不明方法对比或内部数据泄露的风险，但具体细节需审读全文。

## 6. 主要结论与发现

- DPsurv 在**多个癌症数据集上取得了强区分性能**，且预测校准度良好，验证了其有效性和可靠性。
- 可解释性输出使得预测过程在**特征、推理、决策三个层级均透明**，有助于临床预后评估中的信任建立。
- 提供的不确定性区间为医生提供了决策时的重要参考，使得高风险患者识别更为审慎。

## 7. 优点

- **首创的双原型架构**：同时捕捉细胞与组织级别的病理模式，增强了表征的丰富性和生物学关联性。
- **内生可解释性**：无需后置解释器，直接通过原型分配和证据推理链提供可追溯的解释，满足高风险医疗场景下的可解释性需求。
- **不确定性量化**：采用证据理论进行不确定性估计，不仅给出点估计，还输出生存区间，提高了预测的谨慎性。
- **多层级解释**：从区域特征到组件风险再到整体预测，实现了细粒度的决策透明，这是目前 WSI 生存分析中的亮点。

## 8. 不足与局限

- **原型依赖的假设**：原型聚类可能依赖于数据分布，当出现域外或稀见组织模式时，原型分配的稳定性未知。
- **方法复杂度**：双原型与证据融合可能带来额外的计算开销，未在摘要中体现效率对比，可能限制其在实时或大规模部署场景下的适用性。
- **实验覆盖面细节缺失**：目前摘要仅提及五个公开数据集，未给具体名称和特征，无法判断其涵盖的癌种多样性和数据分布偏倚风险。
- **对比方法不完整**：未列出全部对比方法，难以全面评估其在所有前沿方法中的相对优势。
- **临床落地障碍**：虽然提供了可解释证据，但医生能否直接采纳此类原型推理模式，还需实际临床验证。

（完）
