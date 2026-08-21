---
title: "CiNuSeg: Class Incremental Nuclei Segmentation via Anchor-driven Consistency Learning with Dual Region Regularization"
title_zh: CiNuSeg：通过锚驱动一致性学习与双区域正则化的类增量细胞核分割
authors: "Xuexin Wu, Zhenhui Ding, Huisi Wu, Jing Qin"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/38055/42017"
tags: ["query:cell-path"]
score: 8.0
evidence: "组织病理图像类增量细胞核分割，支撑H&E全切片细胞核分割"
tldr: "CiNuSeg针对组织病理图像中类增量式细胞核分割的灾难性遗忘问题，提出锚驱动一致性学习和双区域正则化方法。该方法通过锚定旧类知识并约束区域一致性，在保持旧类性能的同时学习新类细胞核。实验表明其优于现有增量学习方法。该工作为H&E全切片图像中细胞核分割的持续更新提供了有力工具，支持后续细胞级分析。"
source: AAAI-2026-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38055/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 869, \"height\": 505}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38055/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1833, \"height\": 776}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38055/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 875, \"height\": 712}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38055/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1654, \"height\": 717}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38055/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 845, \"height\": 380}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38055/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 884, \"height\": 413}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38055/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 836, \"height\": 327}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38055/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 832, \"height\": 153}]"
tables_json: "[{\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38055/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1841, \"height\": 574}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38055/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1536, \"height\": 574}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38055/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 875, \"height\": 356}]"
motivation: 现有增量学习方法无法充分处理高类间相似性，导致细胞核分割遗忘严重。
method: 采用锚驱动一致性学习和双区域正则化，约束旧类知识并强化细节。
result: 在类增量基准上取得更高性能，有效缓解遗忘并精确分割新核。
conclusion: 为组织病理细胞核分割提供新的增量学习方案，促进下游细胞分析。
---

## Abstract
Recent advances in deep learning have led to significant improvements in nuclei segmentation from histological images, particularly when labels of all classes are available simultaneously during training. However, in clinical practice, real-world scenarios require a model to perform well in an incremental learning setting, where we anticipate the model to achieve satisfactory performance on previously unseen data while effectively mitigating catastrophic forgetting of old classes. Most previous methods alleviate forgetting by distilling old class knowledge through prototypes; however, they fail to adequately capture fine-grained details to address the challenge of high class similarity, which is particularly severe in histological images. To overcome these limitations, we propose a novel incremental learning method for nuclei segmentation (we call it CiNuSeg), which is composed of two key innovative modules. First, we propose a new Anchor-driven Consistency Learning (ACL) module to construct multi-level class anchors within each sample to effectively capture fine structural and textural details of nuclei, thereby significantly mitigating forgetting. Second, we develop a Dual Region Regularization (DRR) module to suppress new class representations within old class regions while enhancing new class representations within new class regions, strengthening the model's ability to discriminate between different nuclei types and improving inter-class separability. We further introduce an Adaptive Temperature Tuning (ATT) strategy to dynamically balance model stability and plasticity. Extensive experiments conducted on benchmarking MoNuSAC and CoNSeP pathological datasets demonstrate the effectiveness of our method, consistently achieving better performance than SOTAs in different settings. Codes will be available upon publication.

---

## 论文详细总结（自动生成）

# CiNuSeg 论文总结

## 1. 论文的核心问题与整体含义

- **研究背景**：细胞核分割是组织病理图像分析的基础任务，准确分割细胞核有助于细胞类型识别和疾病诊断，尤其是癌症诊断。
- **核心问题**：在临床实际中，模型需要以类增量方式持续学习新细胞类型。传统深度学习模型在增量学习新类时，会因参数向新数据偏移而严重遗忘旧类，即“灾难性遗忘”。
- **关键挑战**：组织病理图像中细胞核高度密集，不同细胞核在颜色、形态上高度相似，例如中性粒细胞、淋巴细胞和上皮细胞经常共存且形态相近；这种高类间相似性进一步加剧了遗忘风险。
- **现有方法局限**：许多方法通过原型蒸馏旧类知识，但通常只使用最后一层特征构建原型，难以保留早期层中的细粒度结构、纹理信息；同时全局类原型会掩盖同一类内部样本间的细微差异，不利于检测表征漂移。
- **整体含义**：论文提出一种无需保存旧数据、可插拔的类增量细胞核分割框架 CiNuSeg，旨在在保护隐私、不存储旧患者数据的前提下，更有效地平衡旧类记忆与新类学习，提升组织病理图像中细粒度、高相似性细胞核的持续分割能力。

---

## 2. 论文提出的方法论

CiNuSeg 主要由三个模块构成：Anchor-driven Consistency Learning（ACL）、Dual Region Regularization（DRR）和 Adaptive Temperature Tuning（ATT）。

### 2.1 Anchor-driven Consistency Learning（ACL）

- **目标**：通过对齐旧模型和新模型在多个特征层上的类别锚点，防止旧类表征发生漂移，从而缓解灾难性遗忘。
- **核心思想**：不只在最后一层构建原型，而是在编码器每一层（共 4 层）为每个旧类构建类锚点，以保留细粒度结构和纹理信息。
- **具体流程**：
  1. 使用冻结的旧模型对当前图像生成伪标签。对于当前真实标签属于新类的像素，如果旧模型对某个旧类的预测分数超过阈值 τ，则将伪标签设为该旧类；否则标记为背景。
  2. 在每个编码器层 l，使用伪标签作为掩码，对中间特征 f^l 做掩码平均，得到该层、该类的锚点 A_l^c。
  3. 将当前模型生成的锚点与旧模型生成的锚点进行余弦相似度对齐，构建 Class Anchor Consolidation（CAC）损失。
  4. 同时保留输出层预测知识蒸馏（PKD）损失，对旧类预测和背景合并项进行约束。
- **最终 ACL 损失**：CAC 损失与 PKD 损失之和。

### 2.2 Dual Region Regularization（DRR）

- **目标**：在旧类区域中抑制新类表示，在新类区域中增强新类表示，从而增强新旧类之间的判别性。
- **包含三个损失**：
  1. **Foreground Guidance Loss（FGL）**：对当前新类真实标签区域，使用二值交叉熵直接强化新类预测。
  2. **Background Suppression Loss（BGL）**：在新类区域中，对旧类预测得分施加 L2 范数惩罚，显式抑制旧类响应对新类区域的干扰。
  3. **Weighted BCE Loss with Negative Sample Focus（NS）**：识别旧模型容易把真实新类像素误判为旧类的“困难负样本”区域；对这些区域增加权重，使模型更关注被旧模型误分类的像素，从而提升新类学习效果。
- **最终 DRR 损失**：FGL + BGL + NS。

### 2.3 Adaptive Temperature Tuning（ATT）

- **目标**：缓解增量学习中的类内图像不平衡问题，动态平衡模型稳定性（记忆旧类）与可塑性（学习新类）。
- **核心思想**：当当前图像中新类像素占绝对主导时，增强旧类保留损失，减弱新类学习损失；当新旧类分布较均衡时，保持默认权重。
- **具体方式**：
  - 计算新类像素占所有前景旧/新类像素的比例 r。
  - 若 r 超过阈值 σ（论文设定 0.7），则旧类保留损失温度系数 α_o 增大（论文设定 10），新类学习损失温度系数 α_n 减小（论文设定 0.5）；否则两者均为 1。
- **最终损失**：L = to * L_ACL + tn * L_DRR。

---

## 3. 实验设计

- **数据集**：
  - **MoNuSAC**：来自 2020 年多器官细胞核分割与分类挑战，包含 4 类细胞核：上皮细胞、淋巴细胞、巨噬细胞、中性粒细胞。
  - **CoNSeP**：来自 Hover-Net，原始 7 类被重新归并为 3 类：上皮（健康/增生/恶性）、梭形（成纤维/肌肉/内皮）、其他。
- **任务设置**：采用 overlapped 配置，即图像中可能同时包含旧类、当前新类和未来类像素；这比 disjoint 设置更接近真实临床场景。
- **增量协议**：
  - MoNuSAC：1-1（4 个任务）、2-1（3 个任务）、2-2（2 个任务）、3-1（2 个任务）。
  - CoNSeP：1-1（3 个任务）、2-1（2 个任务）。
- **评价指标**：由于细胞核在医学图像中较小，使用平均 Dice 相似系数（mDice）作为主要指标，分别报告旧类、新类和平均 mDice。
- **Baseline 对比方法**：MiB、PLOP、CoNuSeg、EWF、IDEC、NeST、BARM、INS，以及 Offline 上界。
- **实现细节**：
  - Backbone：ImageNet 预训练 ResNet-101。
  - 初始任务学习率 0.01，增量任务学习率 0.001；训练 100 个 epoch；batch size 12。
  - 优化器：SGD，动量 0.9，权重衰减 0.01。
  - 超参数：α_o=10，α_n=0.5，τ=0.7，ω=0.1，σ=0.7。

---

## 4. 资源与算力

- 论文明确提到实验在 **NVIDIA RTX 3090 GPU** 上完成，但使用了单数/复数不明确，未给出具体 GPU 数量。
- 没有报告单次训练的总耗时、不同增量任务的计算开销，也未说明是否进行多卡并行训练。
- 训练设置为 100 个 epoch、batch size 12，且使用 ResNet-101，大致可推断计算成本中等；但缺乏可精确复现算力成本的细节。
- 因此，**算力资源描述不充分**，难以准确评估训练耗时和计算开销。

---

## 5. 实验数量与充分性

- **主要实验**：在 2 个病理数据集上，共开展 6 种增量协议实验（MoNuSAC 4 种、CoNSeP 2 种），并与 8 个近年 SOTA 方法及 Offline 上界对比，覆盖面较好。
- **消融实验**：在 MoNuSAC 1-1 协议下，对 ACL、DRR、ATT 三个模块逐一消融，分别展示旧类、新类、平均 mDice 变化。
- **进一步分析**：
  - 可视化 DRR 对类别原型相似度矩阵的影响；
  - 可视化加入不同模块后的注意力区域变化；
  - 提供失败案例图；
  - 与 INS 的可视化分割结果对比；
  - 展示增量步骤中 mDice 变化曲线。
- **充分性评价**：整体实验较丰富，涵盖多数据集、多协议、多对比方法、消融和定性分析，能较有力地支撑主要结论。
- **局限性**：
  - 未见多次随机种子重复实验和方差/标准差，缺乏统计显著性检验；
  - 数据集仅两个，且类别数量较少（4 类和 3 类），普适性仍需更多场景验证；
  - 没有报告超参数敏感性分析，例如 τ、σ、α_o、α_n 等对性能的影响；
  - 没有明确所有对比方法是否在同一代码框架和相同调参条件下复现，公平性仍有潜在风险。

---

## 6. 论文的主要结论与发现

- CiNuSeg 在 MoNuSAC 和 CoNSeP 两个病理数据集上，在多种增量协议下均取得优于现有 SOTA 方法的 mDice 分数。
- 具体在 MoNuSAC 上，相比 INS，在 1-1、2-1、2-2、3-1 协议下平均 mDice 分别提升 1.68、0.65、1.74、1.02 个百分点。
- ACL 模块能显著提升旧类 mDice，说明其有效保留旧类知识、缓解遗忘。
- DRR 模块能提升新类 mDice，并降低类别原型之间的相似度，表明其增强了类间可分性。
- ATT 模块在 ACL+DRR 基础上进一步提升新旧类性能，证明动态平衡稳定性和可塑性是有效的。
- 定性结果表明，CiNuSeg 的注意力区域更聚焦、分割结果更完整，且对新旧类都具有更好的判别能力。
- 失败案例显示，模型有时会过度关注细胞核细节，从而误分割非细胞核区域，这被认为是方法的一个局限。

---

## 7. 优点

- **细粒度知识保留**：ACL 模块在多个编码器层构建样本级类锚点，相比传统全局、末层原型，能够保留更丰富的结构纹理信息，适合高相似性细胞核。
- **显式区域级类间分离**：DRR 从新旧区域出发进行差异化正则化，不像普通 BCE 那样独立预测各类，能直接提升新旧类区分度。
- **无需存旧数据**：方法属于 exemplar-free，不依赖旧类样本回放，符合医学图像隐私保护需求，具备实际落地潜力。
- **自适应当前图像类分布**：ATT 根据每张图像中新旧类比例动态调整损失温度，更贴合增量学习中图像级不平衡的现实。
- **实验对比全面**：与多个近年 SOTA 方法比较，并有消融、相似度矩阵、注意力图和失败案例等多角度分析。
- **代码开源**：论文提供代码链接，有助于复现和后续研究。

---

## 8. 不足与局限

- **数据集覆盖有限**：仅在 MoNuSAC 和 CoNSeP 上验证，类别数少，未见更大规模、更多器官或更多类别数据集的实验，泛化性证据不足。
- **缺乏统计稳健性**：没有报告多次实验的均值和方差，无法判断性能提升是否显著。
- **超参数依赖未分析**：τ、σ、α_o、α_n、ω 等关键超参数缺乏敏感性实验，实际使用时调参难度和鲁棒性未知。
- **算力描述不完整**：只提到 RTX 3090，未说明数量、训练时长、单次实验成本，影响可复现性和资源评估。
- **失败模式**：作者自述模型因过度聚焦细节而可能误分割非细胞核区域，说明该方法在复杂组织背景下的鲁棒性仍需改进。
- **对比公平性潜在风险**：未说明所有对比方法是否在相同实现框架、相同训练 epoch 和调参预算下公平比较。
- **伪标签依赖**：ACL 使用旧模型生成伪标签，旧模型自身误差可能被传播并放大

，尤其是在类别高度相似且细胞核密集的场景中，错误伪标签会进入多层锚点对齐与预测蒸馏损失，可能使旧类表征被持续带偏，降低锚点的可靠性。  
- **类别顺序敏感性未分析**：不同类增量顺序可能显著影响遗忘程度，但论文未系统报告不同顺序下的性能波动，难以判断方法对任务顺序是否鲁棒。  
- **主干网络适用范围有限**：实验仅采用 ResNet-101，未验证该方法在更轻量 CNN 或 Transformer 分割主干上的可插拔性和收益，实际部署时的灵活性仍待证明。  
- **推理与存储开销未讨论**：ACL 在训练时需要保留旧模型用于伪标签和锚点生成，虽然不存旧数据，但继续训练或部署时仍需额外维护旧模型参数，相关显存和计算成本未评估。  
- **跨域/多中心鲁棒性不足**：仅在两个特定数据集上验证，未考察不同染色协议、扫描仪或医疗机构来源的数据分布变化对持续分割性能的影响。  

（完）
