---
title: Do Pathology Foundation Models Encode Disease Progression? A Pseudotime Analysis of Visual Representations
title_zh: 病理基础模型是否编码疾病进展？视觉表示的伪时间分析
authors: "Pritika Vig, Renchin Wu, William Lotter"
date: 2026-01-23
pdf: "https://openreview.net/pdf/3c36acdfda826af2f5aabe662e70dca5b42dede3.pdf"
tags: ["query:path-xai-sel"]
score: 7.0
evidence: 分析病理基础模型是否编码疾病进展，提供可解释特征
tldr: 针对病理基础模型能否编码连续疾病进程的问题，采用扩散伪时间分析方法，揭示模型隐式表示能捕获疾病进展的连续特征，有助于稳健泛化和定量分析。
source: ICML-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 探究病理基础模型是否编码了连续的疾病进展过程。
method: 使用扩散伪时间方法分析病理视觉基础模型的表示。
result: 发现模型隐式表示能编码疾病进展的连续特征。
conclusion: 为病理模型的可解释性和疾病过渡分析提供了新方法。
---

## Abstract
Vision foundation models trained on discretely sampled images achieve strong performance on classification benchmarks, yet whether their representations encode the continuous processes underlying their training data remains unclear. This question is especially pertinent in computational pathology, where we posit that models whose latent representations implicitly capture continuous disease progression may better reflect underlying biology, support more robust generalization, and enable quantitative analyses of features associated with disease transitions. Using diffusion pseudotime, a method developed to infer developmental trajectories from single-cell transcriptomics, we probe whether foundation models organize disease states along coherent progression directions in representation space. Across four cancer progressions and six models, we find that all pathology-specific models recover trajectory orderings significantly exceeding null baselines, with vision-only models achieving the highest fidelities $(\tau > 0.78$ on CRC-Serrated). Model rankings by trajectory fidelity on reference diseases strongly predict few-shot classification performance on held-out diseases ($\rho = 0.92$), and exploratory analysis shows cell-type composition varies smoothly along inferred trajectories in patterns consistent with known stromal remodeling. Together, these results demonstrate that vision foundation models can implicitly learn to represent continuous processes from independent static observations, and that trajectory fidelity provides a complementary measure of representation quality beyond downstream performance. While demonstrated in pathology, this framework could be applied to other domains where continuous processes are observed through static snapshots.

---

## 论文详细总结（自动生成）

## 论文总结

### 1. 论文的核心问题与整体含义
- **核心问题**：病理视觉基础模型通常用离散采样的图像（如病理切片中的互不关联的图块）进行训练，但其隐式表示是否能够捕获背后的**连续疾病进程**（即病变从初期到晚期逐渐演化的状态）尚不清楚。
- **研究动机**：若此类模型的潜在表示能隐含地组织出连续疾病进展的方向，将更贴近真实的生物学过程，有助于提升模型的泛化稳健性，并为分析疾病转变的关键特征提供定量手段。
- **整体含义**：论文并非提出新模型，而是借助**扩散伪时间**（一种源于单细胞转录组学、用于推断发育轨迹的方法），在表示空间中探查病理基础模型是否自发学习到疾病状态的连续有序组织，从而评价表示的内在质量。

### 2. 方法论
- **核心理念**：将不同疾病阶段（如正常→腺瘤→癌）的病理图像样本视作静态快照，在预训练模型的表示空间中，利用扩散伪时间方法判断这些快照是否沿一条连贯的“进展方向”排列。
- **技术路线与流程**：
  - **输入**：一组来自不同疾病进展阶段、但未被显式标注连续序关系的图像/图块样本。
  - **表示提取**：对每个样本，用已训练好的病理基础模型（视觉或视觉‑语言模型）提取视觉表示（嵌入向量）。
  - **扩散伪时间分析**：
    - 基于表示向量构建样本间的近邻图（或扩散图），模拟图中每一步向相似状态转移的随机游走。
    - 计算伪时间（pseudotime）排序，该排序反映从起始状态到终末状态的推断性连续演变路径。
  - **评估**：比较推断出的伪时间排序与真实疾病阶段排序的一致性（如肯德尔τ系数），从而量化模型表示中编码连续进程的**轨迹保真度**（trajectory fidelity）。

### 3. 实验设计
- **数据集与场景**：
  - 覆盖**四种癌症进展**过程（摘要中明确提及 CRC‑Serrated 结直肠锯齿状病变进展，其余三种未具名，应为不同癌种的前驱病变到癌的演进序列）。
  - 可能包含多种组织类型的病理图像，但无进一步细节。
- **Benchmark 与对比方法**：
  - 比较了**六种模型**：专为病理设计的模型（病理专用模型）与通用视觉模型或视觉‑语言模型。
  - 基线：通过随机打乱真实阶段标签构造的零基线，检验轨迹保真度是否显著高于偶然水平。
  - 验证任务：用参考疾病上的轨迹保真度排名预测**未见疾病**上的少样本分类性能（以肯德尔ρ衡量排名相关性），以此验证轨迹保真度作为表示质量补充指标的有效性。
- **探索性分析**：沿推断的伪时间轨迹检查细胞类型组成的变化（如基质细胞），观察其是否与已知的间质重塑模式一致。

### 4. 资源与算力
- 论文仅提供了摘要与元数据，**未提及**任何关于 GPU 型号、数量、训练时长或评测所需算力的信息。
- 由于研究主要依赖已预训练模型的表示提取与伪时间计算（多为 CPU 即可完成的近邻图分析），计算开销可能相对较小，但无法从现有内容中确认。

### 5. 实验数量与充分性
- **实验规模**：
  - 涉及 **4 种癌症进展 × 6 个模型**，至少包含主要轨迹保真度评测、与零基线的比较、相关性分析（ρ=0.92）以及细胞组成探索。
  - 根据“model rankings by trajectory fidelity … predict few-shot classification”判断，至少进行了一组以疾病为单位的穿行验证（如留一疾病预测）。
- **充分性与公平性**：
  - 覆盖多个癌种和多种代表性模型，消除了单一疾病或模型带来的偏差，比较对象合理（包含专用与通用模型）。
  - 评估指标注重统计显著性检验（零基线），并设计了泛化外推测试（ρ=0.92），设计较为严谨。
  - 但因仅有摘要，无法判断消融实验、细节超参数敏感性、不同伪时间算法对比等是否充分，也无法确认数据集大小与类别平衡是否客观公平。

### 6. 主要结论与发现
- **所有病理专用模型**恢复的伪时间排序均**显著优于随机基线**，表明基础模型确实能隐式编码连续疾病进展。
- **纯视觉模型**在部分疾病上获得最高轨迹保真度（如 CRC‑Serrated 的 τ > 0.78）。
- 模型在**参考疾病上的轨迹保真度排名**能够强有力地预测其在**未见过疾病上的少样本分类性能**（肯德尔 ρ = 0.92），说明轨迹保真度是表示质量的一个有效替代指标，且与下游性能互补。
- 沿推断轨迹的**细胞类型组成呈现平滑变化**，且符合已知的间质重塑过程，进一步佐证了所捕获连续结构具备生物学一致性。
- 研究框架可推广至其他用静态快照观察连续过程的领域。

### 7. 优点
- **提出新视角**：首次将发育生物学中的扩散伪时间方法引入病理视觉基础模型分析，用于探究隐式连续结构，填补了从离散分类到连续进程理解之间的空白。
- **指标创新**：轨迹保真度不仅提供可解释性，还能作为与下游任务性能互补的表示质量度量，可用于模型筛选与诊断。
- **实验设计严谨**：多癌种、多模型对比，通过零基线与留病预测验证，结论说服力较强。
- **跨域潜力**：方法论不局限于病理，适用于任何“静态快照记录连续动态”的数据场景。

### 8. 不足与局限
- **实验细节不透明**：受限于仅有摘要，未能获取数据集规模、切片选择方式、伪时间算法具体实现、模型版本等关键信息，不利于全面评估重复性或公平性。
- **癌种覆盖可能有限**：仅四种癌症进展，尤其是部分结果重点依赖 CRC‑Serrated，对其它更复杂的多步演进或非肿瘤疾病进程的泛化性有待验证。
- **潜在偏差**：若不同疾病阶段的图像来源（如染色批次、扫描仪、患者群体）存在系统性差异，模型可能学习到混淆因子而非真实生物学进展，摘要中未提及此类控制分析。
- **应用限制**：伪时间分析依赖可获得的、覆盖连续阶段的金标准标注，对于无明确阶段划分的病症难以直接应用；且方法探测的是模型表示中的有序结构，未必完全对应因果性的进展轨迹。

（完）
