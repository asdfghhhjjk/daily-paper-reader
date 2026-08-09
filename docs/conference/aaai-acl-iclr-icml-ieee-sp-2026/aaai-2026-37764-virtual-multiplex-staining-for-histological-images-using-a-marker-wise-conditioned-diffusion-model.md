---
title: Virtual Multiplex Staining for Histological Images Using a Marker-Wise Conditioned Diffusion Model
title_zh: 基于标记条件扩散模型的虚拟多标染色用于组织学图像
authors: "Hyun-Jic Oh, Junsik Kim, Zhiyi Shi, Yichen Wu, Yu-An Chen, Peter K Sorger, Hanspeter Pfister, Won-Ki Jeong"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/37764/41726"
tags: ["query:path-xai-sel"]
score: 7.0
evidence: "从H&E切片生成虚拟多标染色，增强病理分析的分子洞察。"
tldr: "针对多标成像成本高且现有H&E图像缺乏多模态分析能力的问题，本文提出一种基于标记条件扩散模型的虚拟多标染色方法。该模型利用H&E图像作为输入，生成对应的多标免疫组化图像，从而提供分子水平的额外信息。实验表明生成的虚拟染色图像具有高质量，可辅助病理诊断，降低了对真实多标数据的依赖。"
source: AAAI-2026-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-37764/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 822, \"height\": 414, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-37764/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1627, \"height\": 475, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-37764/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1561, \"height\": 617, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-37764/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1684, \"height\": 1011, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-37764/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 710, \"height\": 400, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-37764/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1728, \"height\": 338, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-37764/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1840, \"height\": 519, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-37764/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 853, \"height\": 230, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-37764/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 807, \"height\": 341, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-37764/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 788, \"height\": 273, \"label\": \"Table\"}]"
motivation: "多标成像成本高、普及难，大量H&E图像无法进行多模态分析。"
method: "利用标记条件潜在扩散模型，从H&E图像虚拟生成多标染色图像。"
result: 生成的虚拟多标图像质量高，可提供分子级信息。
conclusion: 虚拟多标染色为计算病理学提供了低成本的多模态分析途径。
---

## Abstract
Multiplex imaging is revolutionizing pathology by enabling the simultaneous visualization of multiple biomarkers within tissue samples, providing molecular-level insights that traditional hematoxylin and eosin (H&E) staining cannot provide. However, the complexity and cost of multiplex data acquisition have hindered its widespread adoption. Additionally, most existing large repositories of H&E images lack corresponding multiplex images, limiting opportunities for multi-modal analysis. To address these challenges, we leverage recent advances in latent diffusion models (LDMs), which excel at modeling complex data distributions by utilizing their powerful priors for fine-tuning to a target domain. In this paper, we introduce a novel framework for virtual multiplex staining that utilizes pretrained LDM parameters to generate multiplex images from H&E images using a conditional diffusion model. Our approach enables marker-by-marker generation by conditioning the diffusion model on each marker, while sharing the same architecture across all markers. To tackle the challenge of varying pixel value distributions across different marker stains and to improve inference speed, we fine-tune the model for single-step sampling, enhancing both color contrast fidelity and inference efficiency through pixel-level loss functions. We validate our framework on two publicly available datasets, notably demonstrating its effectiveness in generating up to 18 different marker types with improved accuracy, a substantial increase over the 2-3 marker types achieved in previous approaches. This validation highlights
the potential of our framework, pioneering virtual multiplex staining. Finally, this paper bridges the gap between H&E and multiplex imaging, potentially enabling retrospective studies and large-scale analyses of existing H&E image repositories.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义（研究动机和背景）
- **核心问题**：传统 H&E 染色虽然广泛使用，但无法提供分子级别的组织微环境信息。多重免疫荧光/免疫组化（mIF/mIHC）虽能弥补这一不足，但其流程复杂、成本高昂，且现有海量的 H&E 图像存储库缺乏对应的多标图像，限制了大规模、多模态的回顾性研究。
- **研究动机**：开发一种计算虚拟染色方法，能高效、准确地从单张 H&E 图像生成最多 18 种不同生物标记物（Marker）的多标图像，以低成本方式为 H&E 图像赋予分子层面的洞察力。
- **整体含义**：通过缩小 H&E 与多标成像之间的鸿沟，该框架有望革新数字病理学，推动大规模、多模态分析成为可能。

### 2. 论文提出的方法论
论文提出一个**基于标记条件扩散模型的两阶段训练框架**，核心思想与技术细节如下：
- **核心思想**：利用预训练的潜在扩散模型作为强大先验，并通过**标记类型的独热编码（one-hot embedding）** 作为条件信号，使一个共享架构的扩散 U-Net 能同时学习生成多种标记物的图像。
- **关键技术细节与流程**：
    - **模型基础**：以 Stable Diffusion 2 的潜在扩散模型架构为骨干，冻结其 VAE 编码器 `E` 和解码器 `D`，仅训练去噪 U-Net。
    - **第一阶段：多目标生成**
        - **输入处理**：将 H&E 图像编码为潜在 `x`，并与加噪后的目标标记物潜在 `z_{m,t}` 进行通道拼接，作为 U-Net 输入。
        - **标记条件机制**：为每种标记物 `m` 分配一个独热向量 `c_m`，经过位置编码后以元素加和的方式注入到时间步嵌入中，以此控制生成目标。
        - **训练损失**：使用平均噪声预测损失 `L_M = (1/M) * Σ || v*_{m，t} - \hat{v}_θ([x， z_{m，t}]， t， c_m) ||^2` 进行训练。
    - **第二阶段：色彩对比度保真度微调**
        - **目的**：解决因数据集背景暗区偏置造成的颜色失真问题，并提升推理速度。
        - **策略**：固定时间步 `t = T` 并将噪声 `ϵ` 置零，实现确定性**单步采样（single-step inference）**。
        - **损失函数**：直接在像素空间应用联合 `L1` 和 `L2` 像素级损失 `L_{FT}`，公式为 `(1/M) * Σ [(1-λ)||I*_m - \hat{I}_m||_1 + λ||I*_m - \hat{I}_m||^2]`。

### 3. 实验设计
- **数据集**：
    - **HEMIT**：包含 3 种 mIHC 标记物（DAPI, CD3, panCK），来自 5292 对 1024x1024 像素的配对图像。
    - **Orion-CRC**：包含 18 种 mIF 标记物（如 Hoechst, CD3e, panCK 等），来自 41 张结肠癌全切片图像（WSI），裁剪为 512x512 的图块，训练集约 13.3 万对。
- **基准对比方法**：pix2pix、pix2pixHD、HEMIT（专为 3 标记设计）、Parmar et al. 的方法、Marigold。
- **评估指标**：结构相似性指数（SSIM）、皮尔逊相关系数（R）、峰值信噪比（PSNR）。
    - *注：pix2pixHD 和 Marigold 因其架构限制，未参与 Orion-CRC 的 18 标记生成任务对比；Parmar et al. 因模式崩溃问题也无法在该数据集上评估。*

### 4. 资源与算力
- **硬件配置**：模型训练和微调均在**四块 NVIDIA H100 GPU** 上进行。
- **其他详情**：论文及补充材料未明确提及具体的总训练时长或 batch size 等细节。

### 5. 实验数量与充分性
实验设计较为充分和系统，主要包含：
- **主要结果实验**：在两个数据集上与多个现有方法进行了详尽的**定量**（两张主结果表格）和**定性**（多张可视化对比图）比较。
- **消融实验**（共三项）：
    - **条件策略消融**（表 3）：比较了“文本条件”与“独热编码条件”在可扩展性上的差异，特别是澄清了文本条件在标记数量增多时的失效问题。
    - **微调阶段与推理效率消融**（表 4）：对比了单模型、多模型、多步/单步采样，以及有无微调对性能、推理时间和内存占用的影响。
    - **损失函数权重消融**（表 5）：探讨了混合损失中超参数 `λ` 的调节作用，表明了数据集自适应的必要性。
- **公平性评价**：实验考虑到了不同方法的架构限制，选择了合理可对比的基准。对所有未微调的消融实验（表 3、4）提供了性能数据，确保了阶段间比较的公平性。

### 6. 论文的主要结论与发现
- 提出的框架在两个数据集上均取得了**最优（SOTA）** 性能，尤其在新颖的 18 标记生成任务（Orion-CRC）上，SSIM、R 和 PSNR 指标均大幅领先现有方法。
- 标记类型的独热编码是一种**鲁棒且可扩展**的条件策略，在标记种类扩增至 18 种时，性能远超基于文本的模糊条件。
- 两阶段训练，特别是像素级的色彩保真度微调阶段，对于纠正色彩失真和提高图像质量**至关重要**，同时实现了极速的**单步确定性推理**，大幅提升了计算效率。

### 7. 优点（方法或实验设计上的亮点）
- **高可扩展性**：单一模型统一生成多达 18 种标记图像，突破了以往方法需为每个标记训练单独模型或仅能处理 2-3 种标记的限制。
- **精巧的两阶段设计**：第一阶段利用扩散模型学习组织形态到多标信号的映射，第二阶段通过像素级监督精修色彩和细节，兼顾了生成多样性和准确性。
- **显著的效率提升**：单步推理机制极大地降低了推理时间和显存消耗，使该方法更贴近临床和大规模研究的实际部署需求。
- **严谨的消融分析**：通过清晰的消融实验，分别验证了独热条件、微调阶段、损失函数权重等各模块的有效性和影响。

### 8. 不足与局限
- **计算开销与标记数相关**：虽然单步推理很快，但总的计算成本仍然随着需要生成的标记物数量增加而线性增长。
- **缺乏标记间关系建模**：模型对每个标记进行条件生成，但并未显式地建模不同标记物之间的共定位或互斥等空间关系，可能限制图像的真实性。
- **数据集的局限性**：论文在生物标志物分布不均的数据集上和样本量极少的特定标记上（如 FOXP3）表现不佳，且模型对色彩的处理存在轻微的模糊和“过预测”倾向（即将信号预测在更广的范围）。
- **泛化能力未知**：实验仅在两个数据集上进行，模型在不同组织类型、染色协议或扫描仪下的泛化性能有待考证。

（完）
