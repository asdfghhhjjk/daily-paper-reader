---
title: "OT-StainNet: Optimal Transport Driven Semantic Matching for Weakly Paired H&E-to-IHC Stain Transfer"
title_zh: "OT-StainNet：最优传输驱动的弱配对H&E到IHC染色转换语义匹配"
authors: "Xianchao Guan, Yifeng Wang, Ye Zhang, Zheng Zhang, Yongbing Zhang"
date: 2025-04-11
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/32329/34484"
tags: ["query:cellseg"]
score: 4.0
evidence: "虚拟染色方法将H&E图像转换为IHC，辅助下游分析"
tldr: "OT-StainNet采用预训练扩散模型和最优传输实现H&E到IHC的虚拟染色，通过弱配对图像间的语义匹配解决配准难题。该方法为数字病理学中依赖免疫组化标记的下游分析任务提供了便捷的转换工具。"
source: AAAI-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/aaai-2025-accepted/aaai-2025-32329/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 863, \"height\": 267, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2025-accepted/aaai-2025-32329/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1835, \"height\": 827, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2025-accepted/aaai-2025-32329/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1835, \"height\": 765, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2025-accepted/aaai-2025-32329/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 883, \"height\": 502, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2025-accepted/aaai-2025-32329/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 875, \"height\": 605, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2025-accepted/aaai-2025-32329/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 796, \"height\": 596, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/aaai-2025-accepted/aaai-2025-32329/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1837, \"height\": 843, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2025-accepted/aaai-2025-32329/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1808, \"height\": 330, \"label\": \"Table\"}]"
motivation: "IHC染色复杂昂贵，限制临床推广，亟需从H&E生成IHC的虚拟染色方法。"
method: "基于扩散模型和最优传输的弱配对H&E到IHC染色转换框架。"
result: "OT-StainNet能有效将H&E图像转换为IHC图像。"
conclusion: 该方法为数字病理图像分析提供了新的预处理工具。
---

## Abstract
Immunohistochemistry (IHC) examination is essential for characterizing tumor subtypes, providing prognostic information, and developing personalized treatment plans. However, IHC staining preparation is more complex and expensive compared to Hematoxylin and Eosin (H&E) staining, limiting its widespread clinical application. Transforming H&E images into IHC images presents a promising solution. In this paper, we propose OT-StainNet, a novel virtual IHC staining method. OT-StainNet employs a pre-trained diffusion model with richer prior knowledge as the generator and fine-tunes it with LoRA adapters through adversarial training. Given that adjacent images of the same tissue stained with H&E and IHC are not precisely aligned at the pixel level, existing methods struggle to fully utilize the supervisory information from weakly paired IHC images. To address this issue, we propose an optimal transport-driven semantic matching (OTSM) mechanism, establishing accurate semantic correspondences between H&E-IHC image pairs. By leveraging the real IHC features obtained through the OTSM mechanism, we design a semantic consistency constraint (SCC) to ensure that the correlations among virtual IHC features remain consistent with those among real IHC features, thereby preserving valuable correlation information during stain transfer. We validate OT-StainNet using four types of IHC staining across two datasets. Extensive experiments demonstrate the effectiveness of our method compared to state-of-the-art approaches.

---

## 论文详细总结（自动生成）

### 1. 研究背景与核心问题
- **核心问题**：免疫组化（IHC）染色对肿瘤亚型分类、预后及个性化治疗至关重要，但其制备复杂且昂贵，限制了临床应用。而苏木精-伊红（H&E）染色成本低、应用广，但缺少特定蛋白表达的对比度。因此，**从H&E图像虚拟生成IHC图像成为一种有前景的替代方案**。
- **主要挑战**：
  - 连续切片得到的H&E和IHC图像在像素级并不精确对齐（弱配对），传统方法依赖像素级损失难以充分利用监督信息，甚至引入错误病理特征。
  - 现有基于GAN的方法常需从头训练，对数据量要求高，且生成准确性有限。

### 2. 方法核心：OT‑StainNet
- **整体框架**：采用预训练扩散模型SD‑Turbo作为生成器，通过对抗训练和LoRA适配器微调，同时将VAE编码器、解码器和U‑Net集成为端到端网络，保留预训练知识。
- **最优传输驱动语义匹配（OTSM）**：
  - 计算H&E特征 \(F^H\) 和IHC特征 \(F^I\) 间的最优传输计划 \(P\)，最小化总成本。
  - 利用传输计划将IHC特征对齐到H&E空间：\(\hat{F}^I = P^\top F^I\)，从而建立准确的语义对应，回避像素级对齐问题。
- **语义一致性约束（SCC）**：
  - 计算对齐后的真实IHC特征两两之间的余弦相似度，形成相关矩阵 \(\hat{M}^I\)；同样计算虚拟IHC特征的相关矩阵 \(\tilde{M}^I\)。
  - 设计语义一致性损失 \(L_{sc} = \frac{1}{n^2}\sum_{i,j}|\hat{M}^I_{ij} - \tilde{M}^I_{ij}|\)，强制虚拟IHC特征之间的相关关系与真实IHC一致，从而保留病理相关的组级语义结构。
- **损失函数**：总损失 \(L_{total} = \lambda_{adv} L_{adv} + \lambda_{cycle} L_{cycle} + \lambda_{id} L_{id} + \lambda_{sc} L_{sc}\)。
- **训练过程**：固定VAE和U‑Net原始权重，仅训练LoRA适配器；采用分批更新判别器与生成器的策略。

### 3. 实验设计
- **数据集**：
  - **MIST**（约4000训练/1000测试片，各IHC类型）
  - **IHC4BC**（约20,000训练/1000测试片，各IHC类型）
  - 涵盖四种IHC染色：Ki67、ER、PR、HER2。
  - 图像均调整为256×256像素。
- **对比方法**：
  - 扩散类：Pix2Pix‑Turbo、CycleGAN‑Turbo
  - GAN类：CUT、PyramidP2P、PRGAN、ASP、U‑Frame
- **评价指标**：SSIM、PSNR、FID；还通过Pearson相关系数评估阳性区域大小的一致性（病理一致性）。

### 4. 资源与算力
- **硬件**：使用4块NVIDIA RTX 3090 GPU。
- **训练时长**：总共训练30,000次迭代。
- **优化器与学习率**：Adam优化器，学习率 \(1\times10^{-5}\)。
- **其他超参**：\(\lambda_{adv}=0.5, \lambda_{cycle}=10, \lambda_{id}=1, \lambda_{sc}=1000\)。
- （文中未提及单次训练的具体时间。）

### 5. 实验数量与充分性
- **定量实验**：在两个数据集上对四种IHC染色类型进行8种方法对比（7种基线+本方法），共 \(2\times4\times(7+1)=64\) 组结果，覆盖SSIM、PSNR、FID。
- **消融实验**：通过移除OTSM、移除SCC（同时移除两者为CycleGAN‑Turbo）在MIST数据集上评估，共3种消融配置×4种染色=12组结果。
- **定性分析**：展示不同方法的虚拟染色结果图，以及与真实IHC的视觉比较。
- **病理一致性评估**：计算虚拟IHC与真实IHC阳性区域大小的Pearson相关系数，并在消融实验中进一步验证。
- **总体评价**：实验设计较为全面，对比方法覆盖主流方案，评价指标多样，消融实验清晰证明了OTSM和SCC的贡献，具备较好的客观性与公平性。

### 6. 主要结论与发现
- OT‑StainNet在SSIM、PSNR和FID指标上全面超越现有SOTA方法。
- 定性上，生成的虚拟IHC图像在染色强度、病理特征与组织结构上最接近真实相邻层IHC图像。
- 通过OTSM与SCC的结合，模型能够更准确地捕捉阳性区域，并在病理一致性（Pearson相关系数）上表现最优。
- 方法不限于特定组织类型，理论上可扩展到多种特殊染色或荧光染色。

### 7. 优点与亮点
- **解决弱配对问题**：利用最优传输建立语义级匹配，避免了强制像素对齐带来的病理错误。
- **语义级监督**：SCC从特征相关性层面约束生成，比普通L1损失保留了更多组病理语义。
- **高效利用预训练知识**：基于扩散模型，仅LoRA适配器调参，减少训练数据需求且提升泛化性。
- **端到端设计**：统一VAE‑U‑Net框架，简化训练与推理。
- **实验扎实**：多数据集、多IHC类型、多维评价，且包含病理一致性评估。

### 8. 不足与局限
- **数据集依赖性**：方法性能与训练图像质量相关，若图像存在污染或细胞结构不清，效果可能下降。
- **未讨论跨组织泛化**：文中仅在乳腺组织切片上验证，未在其他组织类型上测试，泛化性有待进一步确认。
- **计算复杂度**：最优传输在特征维度较高时计算量较大，文中未量化该环节的时间开销。
- **未与更先进的扩散模型比较**：仅使用SD‑Turbo，未探索最新扩散变体（如ControlNet）是否更有优势。
- **临床落地限制**：缺乏病理专家参与的盲评或诊断准确性研究，无法评估对实际诊断流程的影响。

（完）
