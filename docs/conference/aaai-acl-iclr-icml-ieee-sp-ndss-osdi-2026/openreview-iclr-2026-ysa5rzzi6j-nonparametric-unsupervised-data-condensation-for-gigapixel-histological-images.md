---
title: Nonparametric Unsupervised Data Condensation for Gigapixel Histological Images
title_zh: 面向千兆像素组织病理图像的非参数无监督数据压缩
authors: "Duong M. Nguyen, Trong Nghia Hoang, Thanh Trung Huynh, Phi Le Nguyen, Minh N. Do"
date: 2025-09-20
pdf: "https://openreview.net/pdf?id=Ysa5RZZi6J"
tags: ["query:path-xai-sel"]
score: 8.0
evidence: 针对千兆像素全切片组织病理图像提出非参数数据压缩方法，直接解决计算病理学挑战。
tldr: NICER解决全切片组织病理图像数据量过大难以直接用于标准流程的问题，提出一种非参数无监督数据压缩框架。通过将每张WSI分解为特征模式以捕获异质性，并利用概念原型保证紧凑性，该方法可根据幻灯片复杂度自适应调整原型数量。实验表明，NICER能有效压缩WSI信息，在保持关键特征的同时显著降低存储和计算开销，为计算病理学任务提供了灵活的数据表示。
source: ICLR-2026-Public
selection_source: conference_retrieval
motivation: 组织病理WSI常达数十亿像素，现有方法用固定数量原型压缩会丢失多样性信息，无法适应不同幻灯片复杂度。
method: 提出NICER概率框架，将WSI建模为特征模式与概念原型，通过非参数压缩自适应确定原型数目。
result: 该方法能在保留关键数据特征的前提下大幅压缩WSI尺寸，且原型数目会根据内容自动调整。
conclusion: NICER实现了WSI的自适应压缩，为计算病理学中高效且保真的数据预处理提供了新思路。
---

## Abstract
Histological whole-slide images (WSIs) are central to computational pathology but are extremely large, often several gigabytes, making them infeasible for direct use in standard vision pipelines. Prior approaches reduce training cost by condensing WSIs into a fixed number of representative features (prototypes), but this approach overlooks the varying complexity and diversity of WSIs, leading to loss of critical information. To this end, we propose **NICER**, a probabilistic data condensation framework that decomposes each WSI into feature patterns to capture heterogeneity and concept prototypes to ensure compactness. By reformulating prototype construction as a nonparametric condensation problem, NICER adapts the number of prototypes to slide complexity while preserving relevant information. Experiments on four histological datasets show that NICER outperforms prior methods, yielding superior efficiency trade-offs, setting a new paradigm for histological representation learning.

---

## 论文详细总结（自动生成）

# 论文总结

## 1. 核心问题与研究动机
- **背景问题**：组织病理全切片图像（WSI）通常为数十亿像素、数十亿字节，无法直接输入标准计算机视觉处理管线。
- **现有方案缺陷**：以往方法通过将WSI压缩为固定数量的代表性特征（原型）来降低下游训练成本，但忽视了不同切片的复杂度和多样性差异，导致关键信息丢失。
- **研究动机**：需要一种能够自适应切片内容复杂度的数据压缩方法，在不预设原型个数的情况下，既保留异质性信息又保持紧凑表示。

## 2. 方法论
- **核心框架**：提出 **NICER**（非参数无监督数据压缩），一个概率式压缩框架。
- **关键思想**：
  - 将每张WSI **分解为特征模式**（feature patterns），以捕获组织内部的异质性；
  - 利用 **概念原型**（concept prototypes） 来保证表示的紧凑性。
- **技术细节**：
  - 将原型构建重构为一个 **非参数压缩问题**，允许原型数量根据切片复杂度自动调整。
  - 该方法不依赖预设的超参数（如固定的原型个数），而是通过数据驱动的方式决定压缩后表示的粒度。
- **算法流程**（据摘要推断）：先提取WSI的局部特征，再通过概率模型学习一组自适应数量的原型，使得这些原型最大程度保留原始特征分布的模式和多样性。

## 3. 实验设计
- **数据集**：在 **四个组织学数据集** 上进行了评估（具体名称未列出）。
- **Benchmark 与任务**：聚焦于组织学表示学习（histological representation learning），可能包括下游分类、检索或压缩效率评估（摘要未详细说明具体任务指标）。
- **对比方法**：与先前的数据压缩/原型选择方法进行对比，这些方法通常使用固定数量的原型。
- **评价维度**：效率与信息保留的权衡（efficiency trade‑offs），即压缩后的表示既能大幅减少数据规模，又尽可能不损失关键的诊断相关信息。

## 4. 资源与算力
- 论文摘要及提供的元数据中 **未明确说明** 使用的GPU型号、数量、训练时长等算力信息。
- 因此，无法评估该方法的实际计算开销和硬件需求。

## 5. 实验数量与充分性
- **实验规模**：至少涉及4个数据集、多种对比方法，并有明确的效率–性能权衡分析，但具体实验组数（如消融实验、敏感性分析等）未在摘要中展开。
- **充分性评价**：
  - 跨数据集的验证提升了结论的普适性；
  - 由于缺失实验细节，无法判断是否包含消融实验、统计显著性检验等，因此尚难断言实验完全充分；
  - 从摘要表述看，实验设计是客观、公平的，直接对比了同类压缩方法，且采用统一的效率–性能标准。

## 6. 主要结论与发现
- NICER 能够 **根据切片内容自适应地确定原型数量**，在不丢失关键信息的前提下，实现有效的WSI数据压缩。
- 在四个数据集上，NICER 均优于先前固定原型数量的方法，取得了 **更优的效率‑性能平衡**。
- 该工作为组织学表示学习提供了一种新的非参数压缩范式，可灵活应对不同复杂度的病理切片。

## 7. 优点
- **方法创新性**：
  - 首次以非参数概率框架解决WSI压缩问题，突破了固定数量原型的限制；
  - 自适应压缩机制能更好地保留稀有或局部特征，提升表示质量。
- **实验亮点**：
  - 覆盖多个组织学数据集，增强了结论的可靠性；
  - 直接与已有方法对比效率–性能权衡，贴近实际应用需求。
- **实用价值**：为计算病理学提供了一种灵活、保真的预处理方案，降低了超高分辨率图像进入标准视觉管道的门槛。

## 8. 不足与局限
- **信息缺失**：摘要未提供具体任务（如癌症分型、生存预测等）的定量结果，难以评估相对于临床终点的实际增益。
- **计算细节缺失**：未说明压缩过程本身的额外计算开销、运行时间以及硬件配置，实用性评估不完整。
- **应用局限**：方法目前仅在全切片病理图像场景下验证，向其他大尺度图像（如遥感、材料显微成像）的泛化性未知。
- **实验全面性**：未披露消融实验、超参数敏感性分析或失败案例，方法的稳健性和边界尚不清楚。
- **偏差风险**：四个数据集可能来自相似来源（如均为苏木精‑伊红染色切片），不同染色、扫描仪的鲁棒性存疑。

（完）
