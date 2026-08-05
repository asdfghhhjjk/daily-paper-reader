---
title: Nonparametric Unsupervised Data Condensation for Gigapixel Histological Images
title_zh: 吉像素组织学图像的非参数无监督数据浓缩
authors: "Duong M. Nguyen, Trong Nghia Hoang, Thanh Trung Huynh, Phi Le Nguyen, Minh N. Do"
date: 2025-09-20
pdf: "https://openreview.net/pdf?id=Ysa5RZZi6J"
tags: ["query:profile"]
score: 7.0
evidence: 非参数WSI浓缩为原型保留异质性
tldr: 针对现有WSI浓缩固定原型数忽略复杂性的问题，提出非参数概率框架NICER，将每个WSI分解为特征模式并自适应提取原型，保留异质性，降低下游任务训练开销。
source: ICLR-2026-Public
selection_source: conference_retrieval
motivation: 现有浓缩方法固定原型数，丢失WSI多样性信息。
method: 将WSI浓缩为非参数问题，分解特征模式捕获异质性，自适应确定原型数量。
result: 相比固定原型方法，在下游分类任务上性能更优且计算高效。
conclusion: 提供了一种灵活高效的WSI表示方法，支持大规模病理图像分析。
---

## Abstract
Histological whole-slide images (WSIs) are central to computational pathology but are extremely large, often several gigabytes, making them infeasible for direct use in standard vision pipelines. Prior approaches reduce training cost by condensing WSIs into a fixed number of representative features (prototypes), but this approach overlooks the varying complexity and diversity of WSIs, leading to loss of critical information. To this end, we propose **NICER**, a probabilistic data condensation framework that decomposes each WSI into feature patterns to capture heterogeneity and concept prototypes to ensure compactness. By reformulating prototype construction as a nonparametric condensation problem, NICER adapts the number of prototypes to slide complexity while preserving relevant information. Experiments on four histological datasets show that NICER outperforms prior methods, yielding superior efficiency trade-offs, setting a new paradigm for histological representation learning.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义

- **研究背景**：计算病理学高度依赖全切片组织学图像（WSI），但WSI尺寸极大（常达数GB），无法直接输入标准视觉模型，必须进行浓缩或降采样。
- **现有方法局限**：已有的WSI浓缩方法通常将每张切片压缩为固定数量的代表性特征（原型），忽略了不同切片的复杂度和异质性差异，容易丢失关键信息。
- **研究动机**：需要一种能自适应决定原型数量的非参数浓缩方法，既能保留切片内的多样性信息，又能实现高效紧凑的表示。
- **整体含义**：提出将WSI浓缩转化为非参数问题，使下游任务在显著降低计算开销的同时，不牺牲甚至提升性能，为大规模组织学表示学习建立新范式。

### 2. 论文提出的方法论

- **核心思想**：将每张WSI分解为若干特征模式（feature patterns），以捕获其内部的异质性；同时提取概念原型（concept prototypes）来保证表示的紧凑性。原型数量根据切片复杂度自适应确定，而非预设的固定值。
- **框架名称**：NICER（NonparametrIC data condEnsation for histological images）。
- **关键技术细节**（基于摘要推断）：
  - 使用概率数据浓缩框架，将WSI浓缩建模为非参数问题。
  - 特征模式捕捉组织形态、细胞分布等局部异质性。
  - 原型构造通过非参数过程完成，自动推断最优原型数量，避免过少丢失信息或过多冗余。
  - 整体流程可能涉及：特征提取 → 模式分解 → 非参数原型选择 → 下游任务适配。
- **公式或算法**：摘要未给出具体公式，但提及“reformulating prototype construction as a nonparametric condensation problem”。

### 3. 实验设计

- **数据集**：在四个组织学数据集上进行实验（具体名称未在提供文本中列出）。
- **Benchmark与对比方法**：与先前固定原型数量的浓缩方法比较，可能是多种经典的WSI压缩或表示学习方法（未列明）。
- **评估指标**：主要依据下游分类任务的性能与效率权衡（trade-offs）。

### 4. 资源与算力

- 提供的论文文本中**未明确说明**GPU型号、数量或训练时长，仅提到“计算高效”。因此无法给出具体算力配置。

### 5. 实验数量与充分性

- 明确提及使用了四个组织学数据集进行实验。
- 推断至少包含：与多种先前方法的对比实验、反映效率与性能权衡的曲线或表格。
- 若无其他信息，无法判断消融实验的数量，但从研究目标看应具有特征模式分解、非参数原型选择等模块的消融验证。
- 实验设计在摘要中表现为客观、公平（与先前方法比较、多数据集验证），但缺少具体数字支撑。

### 6. 论文的主要结论与发现

- NICER在四个组织学数据集上均优于先前固定原型方法。
- 能提供更优的效率-性能权衡，即用更少的计算资源获得更好的下游分类性能。
- 自适应原型数量有效保留了切片中的异质性信息，克服了固定原型数的信息损失。
- 为大规模病理图像分析提供了一种灵活且高效的WSI表示新范式。

### 7. 优点

- **自适应原型数设计**：突破固定原型数限制，能根据切片复杂度弹性调整，更具普适性。
- **异质性保留**：通过特征模式分解显式建模WSI内多样性，避免关键诊断信息丢失。
- **非参数框架**：无需手动设定原型数量，减少人工调参负担，模型更具灵活性。
- **性能与效率并重**：实验证明在下游任务中同时提升了准确率和计算效率。

### 8. 不足与局限

- **技术细节缺失**：从现有摘要无法了解概率模型的实现方式、非参数过程的具体算法，可复现性存疑。
- **数据集不详**：未公布四个组织学数据集的具体名称和规模，难以评估泛化能力是否受数据集偏差影响。
- **实验对比有限**：只提及与“prior methods”对比，未说明是否包含最新的图神经网络、多实例学习等方法。
- **算力报告缺失**：无任何硬件资源或时间开销报告，难以定量评估“高效”的具体程度。
- **应用限制**：方法的有效性可能受限于切片染色、扫描仪差异等实际协变量漂移，摘要未讨论此类鲁棒性。

（完）
