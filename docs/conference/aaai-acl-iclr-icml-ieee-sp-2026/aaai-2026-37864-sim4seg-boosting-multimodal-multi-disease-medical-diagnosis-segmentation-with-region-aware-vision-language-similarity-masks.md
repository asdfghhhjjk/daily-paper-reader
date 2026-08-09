---
title: "Sim4Seg: Boosting Multimodal Multi-disease Medical Diagnosis Segmentation with Region-Aware Vision-Language Similarity Masks"
title_zh: "Sim4Seg: 利用区域感知视觉-语言相似性掩膜提升多模态多疾病医学诊断分割"
authors: "Lingran Song, Yucheng Zhou, Jianbing Shen"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/37864/41826"
tags: ["query:path-xai-sel"]
score: 4.0
evidence: 通过视觉-语言相似性实现可解释医学诊断分割
tldr: 现有医学分割模型很少同时提供诊断解释。Sim4Seg提出医学诊断分割任务，结合视觉-语言模型生成分割掩膜和诊断结果，通过区域感知相似性掩膜提升分割与可解释性，为多模态多疾病诊断提供新方案。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-37864/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 864, \"height\": 372, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-37864/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1782, \"height\": 757, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-37864/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1801, \"height\": 307, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-37864/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 848, \"height\": 842, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-37864/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 867, \"height\": 895, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-37864/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 873, \"height\": 350, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-37864/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 873, \"height\": 356, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-37864/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 871, \"height\": 560, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-37864/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 876, \"height\": 550, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-37864/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 803, \"height\": 182, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-37864/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1850, \"height\": 1068, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-37864/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 869, \"height\": 357, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-37864/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 850, \"height\": 356, \"label\": \"Table\"}]"
motivation: 医学分割模型缺乏可解释诊断输出，无法满足临床需求。
method: 提出MDS任务与Sim4Seg框架，利用区域感知相似性掩膜融合视觉与语言信息。
result: （摘要截断）预期实现性能提升。
conclusion: 该方法推动了可解释医学影像分析的发展。
---

## Abstract
Despite significant progress in pixel-level medical image analysis, existing medical image segmentation models rarely explore medical segmentation and diagnosis tasks jointly. However, it is crucial for patients that models can provide explainable diagnoses along with medical segmentation results. In this paper, we introduce a medical vision-language task named Medical Diagnosis Segmentation (MDS), which aims to understand clinical queries for medical images and generate the corresponding segmentation masks as well as diagnostic results. To facilitate this task, we first present the Multimodal Multi-disease Medical Diagnosis Segmentation (M3DS) dataset, containing diverse multimodal multi-disease medical images paired with their corresponding segmentation masks and diagnosis chain-of-thought, created via an automated diagnosis chain-of-thought generation pipeline. Moreover, we propose Sim4Seg, a novel framework that improves the performance of diagnosis segmentation by taking advantage of the Region-Aware Vision-Language Similarity to Mask (RVLS2M) module. To improve overall performance, we investigate a test-time scaling strategy for MDS tasks. Experimental results demonstrate that our method outperforms baselines in both segmentation and diagnosis.

---

## 论文详细总结（自动生成）

# Sim4Seg 论文深度分析与结构化总结

## 1. 论文的核心问题与整体含义

- **研究背景与动机**：
  - 现有医学图像分割模型（如 U-Net 系列、SAM 变体等）大多仅聚焦于像素级分割精度，缺乏直接输出诊断及解释的能力，难以满足实际临床流程对“可解释性诊断”的需求。
  - 医学大型视觉-语言模型（LVLMs）虽然具备一定的问答交互能力，但普遍不擅长生成精准的分割掩膜；而推理分割模型（如 LISA）虽能将文本推理与分割结合，但在医学领域尚未被充分探索。
  - 因此，论文提出一个全新的医学视觉-语言任务——**医学诊断分割（Medical Diagnosis Segmentation, MDS）**，其核心目标是：**输入医学影像与临床查询，模型需同时输出目标区域的分割掩膜及带有推理链的诊断结果**。

- **整体研究意义**：
  - 首次将“医学分割”与“可解释诊断推理”统一到一个端到端框架中。
  - 为医学多模态大模型提供像素级可解释性（分割）与文本级可解释性（诊断思维链）的双重输出范式。

## 2. 论文提出的方法论

### 2.1 总体框架 Sim4Seg

模型整体由 **LVLM（大型视觉-语言模型）** 与 **SAM（分割一切模型）** 级联构成：
- **LVLM 负责理解图像和文本查询**，生成含特殊 `[SEG]` 标记的文本响应（包含诊断结论或诊断思维链）。
- **SAM 负责根据 LVLM 提取的提示信息生成分割掩膜**。

### 2.2 核心创新模块：RVLS2M（区域感知视觉-语言相似性掩膜）

**目标**：从冻结的 LVLM 隐藏状态中自动构造区域级提示信息，替代 SAM 原本需要的交互式点/框/掩膜。

**关键技术流程**（对应于算法 1）：
1. **提取特殊标记嵌入**：在 LVLM 最后一层隐藏状态中，定位 `[SEG]` 标记的嵌入 `˜Eseg`，经 MLP 投影得到 `Eseg`。
2. **计算视觉-语言相似度**：取 LVLM 中所有图像 token 嵌入 `Eimg`，与 `Eseg` 计算点积相似度，得到一维相似度向量 `Sim`。
3. **归一化与重塑**：对 `Sim` 做 softmax 归一化，增强区域可分性；然后重塑为二维相似度图 `M`（尺寸 `h'×w'`）。
4. **区域池化与自适应阈值二值化**：
   - 将 `M` 划分为 `g×g` 个网格，在每个网格内做平均池化，得到区域相似度矩阵 `R`。
   - 通过自适应阈值将 `R` 二值化为粗粒度区域掩膜 `Mregion`（仅有 `g×g` 个单元）。
5. **多提示输入 SAM 解码器**：将 `Mregion` 与全局视觉特征 `F`、特殊标记提示 `Eseg` 共同输入 SAM 掩膜解码器，生成最终高精度掩膜。

**公式核心逻辑**：
- 相似度：`Sim = Eimg · (Eseg)^T`
- 归一化：`Sim_norm = softmax(Sim)`
- 区域矩阵：`R_{k,l} = mean(M[bk:b(k+1), bl:b(l+1)])`
- 二值掩膜：`Mregion = I(τ(R))`

### 2.3 训练目标

联合优化：

- 文本生成损失：`Ltxt`（交叉熵）
- 分割掩膜损失：`Lmask = λbce·Lbce + λdice·Ldice`
- 总损失：`L = λtxt·Ltxt + λmask·Lmask`

### 2.4 测试时扩展策略（Test-Time Scaling）

专为 MDS 任务设计，通过多路径推理与多样性掩膜生成提升最终精度：
1. LVLM 生成 `m` 条不同的诊断思维链 `{Oitxt}`。
2. 每条思维链通过 RVLS2M 产生区域掩膜 `M_region^i`。
3. 对 `M_region^i` 施加 `n` 种随机扰动（参数 θj），送入 SAM 生成 `m×n` 个候选掩膜。
4. 根据质量评价指标 `Q`（gIoU 和 cIoU 均值）自动选择最优掩膜作为最终输出。

## 3. 实验设计

### 3.1 核心训练/评估数据集：M3DS

- **构建方式**：整合 10 个公开多模态、多病种医学分割数据集（X射线、皮肤镜、内窥镜、超声、眼底照相等共计 5 种模态），并利用开源医学 LVLM **HuatuoGPT-Vision** 以“医学助手-审校助手-人工复核”的多角色流水线自动生成**诊断思维链（CoT）** 问答对。
- **数据集划分**：训练集 12,000 样本，验证集 2,284 样本，测试集 1,864 样本。
- **包含子集示例**：FracAtlas（骨裂）、ISIC/ISBI（皮肤病变）、Kvasir-SEG（息肉）、BUSI（乳腺超声）、TN3K（甲状腺结节）、ChestX-Det（胸部X光）、FIVES（眼底血管）。

### 3.2 评价指标

- **分割指标**：gIoU（广义交并比）、cIoU（中心距离交并比）。
- **诊断指标**：诊断结论准确率（Acc）。

### 3.3 对比基线方法

- LLaVA-Med（医疗 LVLM，仅能文本输出）
- SAM-Med2D（专门化分割模型，无诊断能力）
- READ（点提示的推理分割方法）
- LISA（通用推理分割基线）及其实验变体：原始零样本、仅微调无诊断文本、微调含诊断文本、微调含诊断思维链。

## 4. 资源与算力

- **训练 GPU**：所有实验均使用 **单个 NVIDIA H800 GPU** 完成。
- **训练配置**：训练 4 个 epoch，优化器 AdamW，学习率 `3×10^-4`，权重衰减 0.01，批大小 2，梯度累积步数 10。
- **训练时长**：文中未明确报告具体总训练时长（仅给出 epoch 数和硬件型号）。
- **测试时扩展**：在推理阶段生成多条思维链与掩膜，计算成本数倍于单次前向传播，但具体时间消耗未给出定量分析。

## 5. 实验数量与充分性

论文进行了较为系统且全面的实验验证：

- **主结果对比**：与 7 种不同配置的基线方法在 M3DS 测试集上比较。
- **消融实验**：
  - 有无 RVLS2M 模块的逐子数据集效果对比（零样本、微调无诊断、微调含诊断、微调含诊断 CoT 四种训练设置）。
  - 不同 τ 策略（网格数、区域选择数）对分割性能的影响曲线（图 6）。
  - 测试时扩展参数 m（CoT 路径数）与 n（掩膜扰动数）的影响分析（图 7）。
- **零样本泛化**：未训练状态下，将 RVLS2M 直接嵌入 LISA 带来的提升。
- **跨模态泛化**：逐次排除某模态全部数据进行训练，在该模态上测试（表 5）。
- **跨数据集泛化**：逐一排除某个子数据集，在未见过数据集上测试（表 6）。
- **定性案例**：对比 Sim4Seg 与 LISA 在诊断 CoT 和掩膜细节上的可视化效果。

> **充分性评价**：实验维度覆盖了**模块有效性、设计参数敏感性、训练范式影响、泛化能力（跨模态、跨数据集）、推理阶段策略**，对比基线涵盖通用分割、医学专用模型及强相关推理分割变体，设计客观、公平，能够有力支撑论文主要主张。

## 6. 主要结论与发现

1. **Sim4Seg 在 MDS 任务上全面超越基线**：在微调含诊断 CoT 设定下，分割指标（gIoU 51.86，cIoU 53.90）比 LISA 同设定高出约 6 个点；诊断准确率从 58.05% 提升至 69.04%，结合测试时扩展后可达 82.63%。
2. **RVLS2M 模块是即插即用的高效提示生成器**：即使在零样本下也能为 LISA 带来 11.6% 的分割性能提升。
3. **诊断 CoT 数据能显著提升诊断准确率**：从仅诊断文本的 53.27% 提升至含 CoT 的 58.05%，Sim4Seg 更是提升至 69.04%，验证了思维链对医学推理的有效性。
4. **区域相似度粒度的“倒 U 型”规律**：选择 top-36 网格且采用 16×16 网格分辨率时达到最优，过粗或过细都会导致性能下降。
5. **测试时扩展策略可跨任务协同增益**：增加思维链条数 `m` 主要提升诊断准确率，增加掩膜扰动数 `n` 主要提升分割精度。
6. **模型具备良好的跨模态与跨数据集泛化能力**，提高了现实临床部署的潜力和鲁棒性。

## 7. 优点

- **任务与数据集创新**：提出的 MDS 任务和 M3DS 数据集首次将多病种、多模态分割与可解释诊断 CoT 统一，为医学多模态研究提供了高价值基准。
- **方法论跳脱微调范式**：RVLS2M 模块巧妙利用冻结 LVLM 内部隐藏状态中的跨模态相似性，以轻量级、即插即用方式生成区域感知提示，避免额外训练复杂的掩膜提议网络。
- **可解释性增强**：模型同时输出诊断思维链和像素级分割，显著提升了模型决策的透明度和临床可信度。
- **推理阶段优化**：测试时扩展策略不改变模型权重，通过多路径“思考”和多掩膜“评价”提升性能，兼具实用性和低部署成本。
- **实验全面扎实**：从模块消融、参数敏感性、零样本、跨模态、跨数据集到推理策略，构建了多维度、链条完整的评估体系。

## 8. 不足与局限

- **数据集自动构建的噪声风险**：M3DS 的诊断 CoT 由 HuatuoGPT-Vision 自动生成，尽管经过人工抽检，但仍可能存在医学事实错误或模板化痕迹，影响模型的确定性诊断能力。
- **二值掩膜局限**：当前仅支持单一目标的二值分割，未涉及多目标实例分割或更细粒度分割场景。
- **区域掩膜分辨率粗**：RVLS2M 生成的提示掩膜为 `g×g` 低分辨率，虽然经过 SAM 上采样，但细节边缘可能受网格粗粒度限制。
- **推理计算开销分析不足**：测试时扩展生成 `m×n` 次前向传播会成倍增加推理延迟，文中未给出具体延迟时间对比，实际临床实时性存疑。
- **诊断评估指标单一**：诊断评价仅依赖准确率（Acc），缺乏更细腻的自然语言诊断评估指标（如 CHEXBERT、RadGraph F1 等）。
- **私有临床数据缺失**：所有验证均基于公开数据集，未在真实私有临床数据上进行外部验证，部署到不同设备或人群时可能出现分布偏移。

（完）
