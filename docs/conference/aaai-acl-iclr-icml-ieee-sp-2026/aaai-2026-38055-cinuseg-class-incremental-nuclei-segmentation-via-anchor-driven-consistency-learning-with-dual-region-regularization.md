---
title: "CiNuSeg: Class Incremental Nuclei Segmentation via Anchor-driven Consistency Learning with Dual Region Regularization"
title_zh: CiNuSeg：基于锚点驱动一致性学习与双区域正则化的类别增量细胞核分割
authors: "Xuexin Wu, Zhenhui Ding, Huisi Wu, Jing Qin"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/38055/42017"
tags: ["query:immuno-topo"]
score: 10.0
evidence: "从组织学图像进行细胞核分割，直接针对H&E切片细胞分割"
tldr: 针对组织学图像中增量类别细胞核分割的遗忘问题，提出CiNuSeg，通过锚点驱动一致性学习和双区域正则化，在保留旧类知识的同时准确分割新类别，显著提升增量学习下的分割性能。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38055/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 869, \"height\": 505, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38055/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1833, \"height\": 776, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38055/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 875, \"height\": 712, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38055/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1654, \"height\": 717, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38055/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 845, \"height\": 380, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38055/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 884, \"height\": 413, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38055/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 836, \"height\": 327, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38055/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 832, \"height\": 153, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38055/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1841, \"height\": 574, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38055/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1536, \"height\": 574, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38055/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 875, \"height\": 356, \"label\": \"Table\"}]"
motivation: 临床实际中需增量学习新类别，现有方法难以平衡新旧类别并捕捉细粒度细节。
method: 引入锚点驱动一致性学习与双区域正则化，增强旧类知识保持和区域细节分割。
result: 在多个组织学图像数据集上取得优于现有方法的增量分割性能。
conclusion: CiNuSeg为临床环境中不断新增类别的细胞核分割提供了有效解决方案。
---

## Abstract
Recent advances in deep learning have led to significant improvements in nuclei segmentation from histological images, particularly when labels of all classes are available simultaneously during training. However, in clinical practice, real-world scenarios require a model to perform well in an incremental learning setting, where we anticipate the model to achieve satisfactory performance on previously unseen data while effectively mitigating catastrophic forgetting of old classes. Most previous methods alleviate forgetting by distilling old class knowledge through prototypes; however, they fail to adequately capture fine-grained details to address the challenge of high class similarity, which is particularly severe in histological images. To overcome these limitations, we propose a novel incremental learning method for nuclei segmentation (we call it CiNuSeg), which is composed of two key innovative modules. First, we propose a new Anchor-driven Consistency Learning (ACL) module to construct multi-level class anchors within each sample to effectively capture fine structural and textural details of nuclei, thereby significantly mitigating forgetting. Second, we develop a Dual Region Regularization (DRR) module to suppress new class representations within old class regions while enhancing new class representations within new class regions, strengthening the model's ability to discriminate between different nuclei types and improving inter-class separability. We further introduce an Adaptive Temperature Tuning (ATT) strategy to dynamically balance model stability and plasticity. Extensive experiments conducted on benchmarking MoNuSAC and CoNSeP pathological datasets demonstrate the effectiveness of our method, consistently achieving better performance than SOTAs in different settings. Codes will be available upon publication.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义（研究动机和背景）
- **应用场景**：组织病理图像中多类细胞核的分割是癌症诊断等任务的基础。实际临床需要模型持续学习新类别，同时不忘已有类别。
- **核心挑战**：类别增量学习（CIL）中的灾难性遗忘问题。在组织学图像中，细胞核形态、颜色高度相似，新旧类之间极难区分，以往基于原型的知识蒸馏方法难以捕捉细粒度细节，导致遗忘严重。
- **研究目标**：提出一种无需存储旧数据的类别增量细胞核分割方法，在有效学习新类的同时最大程度保留旧类分割能力。

### 2. 论文提出的方法论
- **整体框架（CiNuSeg）**：包含三大模块：锚点驱动一致性学习（ACL）、双区域正则化（DRR）和自适应温度调节（ATT）。
- **ACL 模块**：
  - 利用冻结的旧模型生成伪标签，在编码器每一层（ \( l = 1,2,3,4 \) ）为每个旧类构建类锚点（class anchor），即该类所有像素特征的均值。
  - 通过余弦相似度约束新旧模型对应层锚点的一致性（Class Anchor Consolidation loss, \( \mathcal{L}_{\text{CAC}} \)），并结合输出层预测知识蒸馏（\( \mathcal{L}_{\text{PKD}} \)）组成 \( \mathcal{L}_{\text{ACL}} \)。这比仅用最终层原型更好地保留了多尺度结构细节。
- **DRR 模块**：
  - 前景引导损失（\( \mathcal{L}_{\text{FGL}} \)）：在真实新类区域用BCE强化新类学习。
  - 背景抑制损失（\( \mathcal{L}_{\text{BGL}} \)）：在新类区域内抑制旧类预测，降低混淆。
  - 加权BCE损失（\( \mathcal{L}_{\text{NS}} \)）：识别旧模型误将新类像素判为旧类的“困难负样本”，增大其权重，提升新类判别力。
  - 综合三部分形成 \( \mathcal{L}_{\text{DRR}} \)。
- **ATT 策略**：
  - 针对图像内新旧类像素严重不平衡问题，计算新类像素占比 \( r \)，当 \( r > \sigma \) 时，对新类学习损失降温（\( \alpha_n < 1 \)）、对旧类保持损失升温（\( \alpha_o > 1 \)），动态平衡稳定性与可塑性。
- **总损失**：\( \mathcal{L} = t_o \mathcal{L}_{\text{ACL}} + t_n \mathcal{L}_{\text{DRR}} \)。

### 3. 实验设计
- **数据集**：
  - MoNuSAC：多器官细胞核分割分类挑战赛数据集，4类（上皮、淋巴、巨噬、中性粒细胞）。
  - CoNSeP：41张H&E图像，原始7类重组为3类（上皮、梭形、其他）。
- **增量协议**：
  - 采用重叠（overlapped）配置，像素可能包含旧类、新类和未来类。
  - 在MoNuSAC上测试1-1（4步）、2-1（3步）、2-2（2步）、3-1（2步）四种设置；CoNSeP上测试1-1和2-1。
- **评价指标**：平均Dice系数（mDice），区分旧类、新类和总平均。
- **对比方法**：MiB、PLOP、CoNuSeg、EWF、IDEC、NeST、BARM、INS等SOTA类别增量分割方法，并提供离线全量训练作为上限。

### 4. 资源与算力
- 文中明确说明实验使用 **NVIDIA RTX 3090 GPU** 进行，未提及GPU数量或具体训练时长，但给出了超参数设置（如epoch=100，batch size=12），训练成本可控。

### 5. 实验数量与充分性
- **主要对比实验**：在2个数据集、共6种增量协议下与8种方法比较，提供平均Dice和分别新旧类性能，表格详尽。
- **消融实验**：在MoNuSAC 1-1设置下逐步加入ACL、DRR、ATT，分析各模块贡献，并展示相似度矩阵和注意力图演化。
- **定性分析**：展示分割结果对比、增量步骤性能变化曲线、失败案例。
- 实验覆盖面广，比较公平，消融充分，结论客观。

### 6. 论文的主要结论与发现
- CiNuSeg在MoNuSAC和CoNSeP所有增量协议上均优于现有SOTA方法，mDice提升幅度显著。
- ACL有效保留旧类细粒度特征，DRR显著增强新旧类分离度，ATT缓解类别不平衡带来的偏向。
- 定性结果表明分割更完整，遗忘更少。

### 7. 优点
- **方法创新**：首次将多尺度锚点一致性用于类别增量分割，结合区域正则化和自适应温度调节，针对细胞核高相似性痛点。
- **无需旧数据**：完全符合医疗数据隐私限制，具有实际部署价值。
- **模块化即插即用**：不依赖特定骨干网络，易于集成。
- **实验设计严谨**：多数据集、多协议、全面对比与消融，结果可靠。

### 8. 不足与局限
- **错误分类非核区域**：因过度关注细节，偶将背景误判为核，需后续改进。
- **超参数较多**：如 \( \tau, \omega, \sigma, \alpha_o, \alpha_n \) 等，实际应用中可能需要调参。
- **未探索任务序号影响**：仅测试类别增量，未讨论顺序变化对性能的敏感度。
- **受限于染色与器官类型**：仅评估H&E染色、特定器官，泛化到其他染色或器官仍有待验证。
- **计算开销**：构建锚点和伪标签需运行旧模型，推理时虽无额外开销，但训练时需前向旧模型，增量步数增多可能累积时间成本。

（完）
