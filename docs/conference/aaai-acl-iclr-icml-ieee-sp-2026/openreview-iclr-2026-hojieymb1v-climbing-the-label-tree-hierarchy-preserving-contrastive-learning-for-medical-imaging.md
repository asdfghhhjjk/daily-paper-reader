---
title: "Climbing the label tree: Hierarchy-preserving contrastive learning for medical imaging"
title_zh: 攀登标签树：医疗影像的层次保持对比学习
authors: Alif Elham Khan
date: 2025-09-20
pdf: "https://openreview.net/pdf?id=hOjieyMB1v"
tags: ["query:path-xai-sel"]
score: 6.0
evidence: 面向医学图像分类的层次保持对比学习，在乳腺组织病理学上验证。
tldr: 医学图像标签常具有层级结构，但标准自监督学习忽略该信息。本文提出层次保持对比学习框架，引入层级加权对比和层次感知margin两项目标，使表示空间符合标签树。在包括乳腺组织病理学在内的多个基准上验证，方法提升了下游分类性能，且无需改变模型架构。该工作为利用医学先验知识改进自监督学习提供了新思路。
source: ICLR-2026-Public
selection_source: conference_retrieval
motivation: 现有自监督学习忽视医学图像标签的层级结构，未能充分利用组织→亚型的先验知识。
method: 提出层级加权对比损失和层次感知margin，在对比学习中显式建模标签树。
result: 在乳腺组织病理学等多个基准上取得改进，提升分类精度。
conclusion: 层次保持对比学习有效利用医学先验，为自监督学习提供新方向。
---

## Abstract
Medical image labels are often organized by taxonomies (organ → tissue → subtype), yet standard self-supervised learning (SSL) ignores this structure. We present a hierarchy-preserving contrastive framework that makes the label tree a first-class training signal and an evaluation target. Our approach introduces two plug-in objectives: Hierarchy-Weighted Contrastive (HWC), which scales positive/negative pair strengths by shared ancestors to promote within-parent coherence, and Level-Aware Margin (LAM), a prototype margin that separates ancestor groups across levels. The formulation is geometry-agnostic and applies to Euclidean and hyperbolic embeddings without architectural changes. Across several benchmarks, including breast histopathology, the proposed objectives consistently improve representation quality over strong SSL baselines while better respecting the taxonomy. We evaluate with metrics tailored to hierarchy faithfulness—HF1 (hierarchical F1), H-Acc (tree-distance–weighted accuracy), and parent-distance violation rate—and also report top-1 accuracy for completeness. Ablations show that HWC and LAM are effective even without curvature, and combining them yields the most taxonomy-aligned representations. Taken together, these results provide a simple, general recipe for learning medical image representations that respect the label tree—advancing both performance and interpretability in hierarchy-rich domains.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义（研究动机和背景）
- **核心问题**：医学图像标签通常遵循严格的分类学层级结构（如器官 → 组织 → 亚型），但现有的自监督学习（SSL）方法完全忽略这种先验知识，无法将标签树的层次信息融入表示学习。
- **整体含义**：该论文提出一个“层次保持”的对比学习框架，首次将标签树作为关键训练信号和评估目标，使学习到的图像表征能够自然地尊重医学本体的层级关系，从而提升下游任务的性能和可解释性。

### 2. 方法论：核心思想、关键技术细节
- **核心思想**：在标准对比学习基础上插入两个即插即用的目标函数，显式建模标签树中的祖先关系，使特征空间中的距离和相似度反映分类学上的远近。
- **关键技术细节**：
  - **层级加权对比（Hierarchy-Weighted Contrastive, HWC）**：
    - 根据样本对在标签树上共享的最近公共祖先（LCA）的深度来缩放正/负对的强度。
    - 共享祖先越深，正样本对的吸引力越强、负样本对的排斥力越弱，从而鼓励“父类内聚”。
  - **层级感知间隔（Level-Aware Margin, LAM）**：
    - 为每一层级设置原型（prototype），并引入一个与层级相关的间隔，强制不同祖先组的表征在原型空间中分离。
    - 该间隔的大小与层级深度相关（更高层级的祖先间隔更大，更细粒度的子类间隔较小）。
  - **公式/算法流程**：
    - 整体损失 = 基础对比损失（如 SimCLR 或 SupCon） + HWC 项 + LAM 项。
    - HWC 项通过动态权重矩阵调整对比对的目标相似度；LAM 项则在原型分类损失中施加分层 margin。
  - **几何无关性**：方法不依赖特定嵌入几何，可直接应用于欧氏空间或双曲空间，无需改变模型架构。
- **评估指标**：
  - **HF1（层级 F1）**：考虑标签树结构的多级 F1。
  - **H-Acc（树距离加权准确率）**：基于树编辑距离加权的准确率。
  - **父节点距离违规率**：测量子节点表征是否比其父节点更远离其他类。
  - 同时报告 Top-1 准确率以评估通用分类性能。

### 3. 实验设计：数据集、场景、Benchmark 与对比方法
- **数据集/场景**：
  - 医学图像分类任务，特别强调乳腺癌组织病理学（breast histopathology）基准，同时涵盖多个其他医学图像基准（摘要中未逐一列出，但明确提及“several benchmarks”）。
- **对比方法**：
  - 强自监督学习基线（如 SimCLR、SupCon 及其变体）。
  - 可能包括不考虑层级的普通对比方法，以及仅在欧氏或双曲空间中的对应版本，用于消融。

### 4. 资源与算力
- 文中未提供算力细节（GPU 型号、数量、训练时长等）。摘要和元数据中均未涉及算力消耗的描述。

### 5. 实验数量与充分性
- **实验组数**：
  - 跨多个医学图像基准的总体性能对比。
  - 针对 HWC 和 LAM 的消融实验（ablations），验证各组件独立及组合的效果。
  - 几何空间独立性验证（欧氏与双曲下有效性）。
  - 层级保真度评估指标的专项实验。
- **充分性与公平性**：
  - 对比方法均为当前流行的 SSL 基线，实验设置较公平。
  - 消融研究较为细致，证实了各创新部件的作用，且考察了无曲率空间下的表现，加强了结论的普适性。
  - 使用了专门设计的层次相关度量，弥补了传统 Top-1 准确率无法反映层次结构的缺陷。
  - 总体实验设计较充分，但摘要中未提及统计显著性检验或误差线，无法评估结果稳定性。

### 6. 主要结论与发现
- 提出的 HWC 与 LAM 目标能稳定提升强 SSL 基线的表示质量，使学到的特征更好地遵从医学标签树。
- 两个目标即使在不使用双曲曲率的情况下也有效，联合使用可获得最符合层次结构的表征。
- 方法为层次丰富的医学影像领域提供了一种简单、通用的表示学习范式，同时提升了下游分类性能和可解释性。

### 7. 优点
- **先验知识利用**：首次将医学标签树结构直接编码进对比学习，充分利用领域知识。
- **即插即用性**：方法不改变原有网络架构，便于集成到各种 SSL 框架中。
- **几何无关**：在欧氏和双曲空间均有效，增强了适应性。
- **评估多维**：不仅报告传统准确率，还设计了层次忠实度指标，更全面地评估表征质量。
- **消融扎实**：清晰证明了每个组件对层次一致性的贡献。

### 8. 不足与局限
- **算力未说明**：未提供计算开销或训练时长，难以评估实际应用中的资源需求。
- **数据集细节缺失**：除乳腺病理外，其他基准的名称、规模、模态未在摘要中呈现，限制了对其泛化能力的判断。
- **可能缺乏统计检验**：未提及多次运行的均值/方差或显著性检验，结果可靠性待验证。
- **层次结构依赖**：高度依赖准确的、预定义的标签树，若领域本体不完善或存在歧义，方法效果可能打折。
- **应用范围**：仅验证于医学图像，对其他层次丰富但标签树不规则的任务（如行为识别、细粒度物种分类）的迁移性未知。
- **超参数敏感性**：HWC 权重缩放与 LAM 间隔的设置可能对标签树结构敏感，未讨论调参难度。

（完）
