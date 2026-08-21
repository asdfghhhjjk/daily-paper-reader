---
title: Unsupervised Foundation Model-Agnostic Slide-Level Representation Learning
title_zh: 无监督的与基础模型无关的切片级表示学习
authors: "Lenz, Tim, Neidlinger, Peter, Ligero, Marta, Wölflein, Georg, van Treeck, Marko, Kather, Jakob N."
date: 2025-06-01
pdf: "https://openaccess.thecvf.com/content/CVPR2025/papers/Lenz_Unsupervised_Foundation_Model-Agnostic_Slide-Level_Representation_Learning_CVPR_2025_paper.pdf"
tags: ["query:cell-graph"]
score: 4.0
evidence: WSI切片级表示学习，非细胞级特征
tldr: 本文针对WSI患者级嵌入难以生成的问题，提出一种无监督且与基础模型无关的切片级表示学习方法。该方法通过在特征空间中对齐多个基础模型的瓦片嵌入，并在切片水平进行自监督学习，从而获得任务无关的表示。预期能提升下游任务的性能，但其关注点在切片级而非细胞级特征。
source: CVPR-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-lenz-unsupervised-foundation-model-agnostic-slide-level-representation-learning-cvpr-2025-paper/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1548, \"height\": 1142}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-lenz-unsupervised-foundation-model-agnostic-slide-level-representation-learning-cvpr-2025-paper/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 760, \"height\": 641}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-lenz-unsupervised-foundation-model-agnostic-slide-level-representation-learning-cvpr-2025-paper/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1141, \"height\": 568}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-lenz-unsupervised-foundation-model-agnostic-slide-level-representation-learning-cvpr-2025-paper/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 724, \"height\": 526}]"
tables_json: "[{\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-lenz-unsupervised-foundation-model-agnostic-slide-level-representation-learning-cvpr-2025-paper/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 858, \"height\": 392}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-lenz-unsupervised-foundation-model-agnostic-slide-level-representation-learning-cvpr-2025-paper/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1809, \"height\": 515}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-lenz-unsupervised-foundation-model-agnostic-slide-level-representation-learning-cvpr-2025-paper/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1809, \"height\": 542}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-lenz-unsupervised-foundation-model-agnostic-slide-level-representation-learning-cvpr-2025-paper/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1807, \"height\": 741}]"
motivation: 现有WSI表示学习依赖弱监督MIL或需要多模态数据，生成患者/切片级嵌入困难。
method: 提出单一模态自监督方法，在特征空间整合多个基础模型的切片嵌入，通过对齐不同增强视图学习切片级表示。
result: 摘要未完整，预期生成任务无关且性能更好的切片表示。
conclusion: 该方法改进WSI表示学习，但不涉及细胞级特征提取。
---

## Abstract
Representation learning of pathology whole-slide images (WSIs) has primarily relied on weak supervision with Multiple Instance Learning (MIL). This approach leads to slide representations highly tailored to a specific clinical task. Self-supervised learning (SSL) has been successfully applied to train histopathology foundation models (FMs) for patch embedding generation. However, generating patient or slide level embeddings remains challenging. Existing approaches for slide representation learning extend the principles of SSL from patch level learning to entire slides by aligning different augmentations of the slide or by utilizing multimodal data. By integrating tile embeddings from multiple FMs, we propose a new single modality SSL method in feature space that generates useful slide representations. Our contrastive pretraining strategy, called COBRA, employs multiple FMs and an architecture based on Mamba-2. COBRA exceeds performance of state-of-the-art slide encoders on four different public Clinical Protemic Tumor Analysis Consortium (CPTAC) cohorts on average by at least +4.4% AUC, despite only being pretrained on 3048 WSIs from The Cancer Genome Atlas (TCGA). Additionally, COBRA is readily compatible at inference time with previously unseen feature extractors. Code available at https://github.com/KatherLab/COBRA

---

## 论文详细总结（自动生成）

## 1. 论文的核心问题与整体含义（研究动机与背景）

- **核心问题**：病理全切片图像（WSI）的表示学习主要依赖弱监督多实例学习（MIL），导致生成的切片表示高度针对特定临床任务，缺乏任务无关性。自监督学习（SSL）已在病理基础模型（FMs）的 patch 级嵌入生成中取得成功，但**患者级 / 切片级嵌入的生成仍具挑战性**。
- **现有局限**：
  - 图像级增强可能失效，因为现代 FMs 对许多变换具有不变性；
  - 多染色（如 H&E 与 IHC）或多模态（文本、基因表达）对齐受数据可用性和计算开销限制；
  - 已有 slide 级编码器（如 GigaPath、PRISM、CHIEF、MADELEINE）通常需要大量预训练数据（>10K，甚至 >100K WSIs）。
- **整体含义**：本文提出一种**单模态、特征空间内的对比学习**方法，整合多个基础模型的 tile 嵌入，以极低数据量（仅 3048 张 WSI）实现高性能、任务无关的切片级表示，同时与未见过的特征提取器兼容。

## 2. 论文提出的方法论：核心思想、关键技术细节

- **核心思想**：**COBRA**（COntrastive Biomarker Representation Alignment）不依赖图像级随机增强，而是在**冻结的 patch 嵌入空间**中，利用不同基础模型（FMs）和不同放大倍数作为“特征空间增强”，通过对比学习训练一个 slide 编码器，使同一患者的不同增强视图在嵌入空间中靠近。
- **预处理**：
  - WSI 切割为 224×224 px 的 patch，用 Canny 背景检测去除背景；
  - 用多个 FMs（CTransPath、UNI、Virchow2、H-Optimus-0）提取 patch 嵌入；
  - 在三种放大倍数（0.5、1.14、2 微米/像素，MPP，对应约 20×、9×、5×）下分别提取特征。
- **架构**（如图 1 所示）：
  - **嵌入模块** $f_E$：对每个 FM 的 patch 嵌入应用 LayerNorm + 线性层 + SiLU 激活，将不同维度（768/1024/1280/1536）映射到共享空间；
  - **状态空间模块** $f_S$：两个 Mamba-2（SSD）层，采用残差连接，高效编码长序列的 tile 特征；
  - **聚合模块** $f_A$：多头门控注意力（multi-head gated attention），为每个 tile 计算注意力权重并加权平均，得到 slide 级向量 $z$。
- **对比学习目标**：
  - 使用 InfoNCE 损失：$L_q = -\log \frac{\psi(q, k^+)}{\sum_{i=1}^{N} \psi(q, k_i)}$，其中 $\psi(x_1, x_2) = \exp(\text{sim}(x_1, x_2)/\tau)$；
  - 采用 MoCo-v3 风格的动量编码器，query encoder 参数 $\theta_q$ 通过反向传播更新，key encoder 参数 $\theta_k$ 按 $\theta_k \leftarrow m\theta_k + (1-m)\theta_q$ 动量更新。
- **推理模式**：
  - **单 FM 模式**：使用编码后的嵌入计算注意力权重 $a_k(H_{S,k})$，但聚合原始 patch 嵌入 $H^{fe_n}$，即 $z = f_A^{inf}(H_S, H^{fe_n}) = \sum_k a_k(H_{S,k}) \cdot H^{fe_n}_k$；
  - **多 FM 模式**：将多个 FM 的嵌入经嵌入模块后平均，再经状态空间模块得到注意力权重，最后聚合某个指定 FM 的原始嵌入（公式 (8)）。
- **可解释性**：注意力权重可直接生成 tile 级热图，无需 GradCAM，能突出肿瘤区域。

## 3. 实验设计：数据集、benchmark、对比方法

- **预训练数据**：TCGA 中的 3048 张 WSI，来自 2848 名患者，涵盖 BRCA（1112）、CRC（566）、LUAD（524）、LUSC（496）、STAD（350）。
- **外部验证数据**：CPTAC 的 1604 张 WSI，来自 444 名患者，涵盖 BRCA（395）、COAD（233）、LUAD（498）、LUSC（478）。
- **下游任务（共 15 个）**：
  - **LUAD**：STK11、EGFR、TP53、KRAS 突变预测；
  - **BRCA**：ESR1、PGR、ERBB2 表达，PIK3CA 突变；
  - **COAD**：MSI 状态、BRAF、KRAS、PIK3CA 突变；
  - **表型/其他**：NSCLC 亚型分类、COAD 侧别（sidedness）、淋巴结状态（N-Status）。
- **评估协议**：
  - 在 TCGA 上做 5 折交叉验证训练 MLP 分类器，然后在 CPTAC 完整外部验证集上测试；
  - 主要指标为 AUC（主文），附录包含 F1、AUPRC、balanced accuracy；
  - 默认使用 0.5 MPP（20×）嵌入。
- **对比方法**：
  - **Mean patch embeddings**：CTransPath、Virchow、CONCH、UNI、H-Optimus、GigaPath、Virchow2；
  - **Slide encoders**：GigaPath-SE、MADELEINE、CHIEF、PRISM；
  - **集成策略**：Ensemble Prediction（各 FM 平均预测）、Concatenated（拼接所有 FM 的 mean embeddings）。
- **其他实验**：
  - Few-shot 线性探测（k=5、10、25 样本/类）；
  - 不同放大倍数下的推理性能；
  - 未见过的 FM（GigaPath）适应性；
  - 单放大倍数 vs 多放大倍数预训练消融。

## 4. 资源与算力

- **GPU**：4 块 NVIDIA A100；
- **Batch size**：1024；
- **训练轮数**：2000 epochs；
- **训练时间**：约 40 小时；
- **特征数据规模**：共 36576 个特征嵌入（3048 WSIs × 4 FMs × 3 放大倍数）；
- **说明**：论文明确给出了上述算力信息，但未提及 CPU、内存或推理阶段的算力消耗。

## 5. 实验数量与充分性

- **实验数量较多**，包括：
  - 15 个下游任务 × 多组对比方法（约 10+ 个 baseline）；
  - 消融实验：不同推理模式、不同 FM、不同放大倍数（5×/9×/20×）、单 vs 多放大倍数预训练；
  - Few-shot 实验（3 种 k 值）；
  - 可解释性分析（热图、UMAP 可视化）。
- **充分性**：整体实验设计较为全面，覆盖多癌种、多任务、多对比方法，并进行了外部验证。
- **客观性与公平性**：
  - **优势**：COBRA 仅用 3048 张 WSI 预训练，而 PRISM 使用 587K、GigaPath 使用 171K，但 COBRA 仍取得最优平均 AUC，体现了方法的高数据效率；
  - **潜在偏差**：
    - 外部验证仅使用 CPTAC 一个队列，缺乏更多独立中心的数据，泛化性证据有限；
    - 对比的 slide encoders（如 MADELEINE 只在 BRCA 上训练）在任务覆盖上不完全匹配；
    - 下游评估统一使用 MLP 和 5 折 CV，但未明确说明是否对所有 baseline 采用完全相同的超参数搜索空间；
    - 部分任务（如 KRAS）的 AUC 提升不明显，甚至低于某些 mean baseline。

## 6. 论文的主要结论与发现

- **性能优越**：在 15 个下游任务上，COBRA 的平均 AUC 比 SOTA slide encoder PRISM 高出 **+4.4%**，比 Virchow2 mean patch embeddings 高出 **+1.5%**。
- **数据效率极高**：仅使用 3048 张 TCGA WSI 预训练，即超越使用数十万张 WSI 的多模态 slide encoders。
- **FM 无关性**：COBRA 可以提升未见过的 FM（如 GigaPath）的 slide 级表示，比其 mean baseline 平均 AUC 提高 **+2.5%**，且比 PRISM 高 **+3.1%**。
- **多尺度预训练有效**：使用 0.5/1.14/2 MPP 三种放大倍数的特征进行对齐，比单一 0.5 MPP 预训练平均 AUC 提高 **+1.73%**，且在低倍（5×）下 NSCLC 亚型分类提升显著。
- **低倍放大下仍具竞争力**：COBRA 使用 5× 或 9× 嵌入时，平均 AUC 仍超过 PRISM 在 20× 下的表现，可大幅降低计算成本。
- **可解释性强**：无需监督即可生成肿瘤区域热图；UMAP 显示不同组织类型在嵌入空间中自然分离。

## 7. 优点

- **方法创新**：首次在特征空间内利用多 FM + 多放大倍数作为增强，避免图像级增强失效问题。
- **数据效率**：仅 3K WSI 预训练即达到 SOTA，对医疗数据稀缺场景极具价值。
- **模型无关性**：与多种 patch 级 FMs 兼容，且可泛化到未来新 FM，适应性强。
- **计算友好**：低倍放大下仍保持高性能，推理时可大幅减少 patch 提取和嵌入计算量。
- **可解释性**：注意力权重直接提供 tile 级热图，无需额外梯度计算。
- **架构选择合理**：Mamba-2 适合长序列建模，多头门控注意力聚合有效。

## 8. 不足与局限

- **预训练数据规模和多样性有限**：仅 TCGA 四种癌型（BRCA/CRC/LUAD/LUSC/STAD），可能限制在罕见癌或非肿瘤病理上的泛化。
- **外部验证队列单一**：仅在 CPTAC 上验证，缺乏多中心、不同扫描仪/染色条件的独立队列。
- **对比公平性存疑**：部分对比 slide encoders 的预训练数据量远大于 COBRA，虽然 COBRA 胜出，但可能因为 baseline 未在相同下游协议下充分调优。
- **任务覆盖不完全**：15 个任务集中在突变/表达/亚型，未涉及生存预测、治疗反应等预后任务。
- **仅用对比学习目标**：未探索其他 SSL 目标（如 masked modeling、蒸馏等），可能限制表示质量。
- **推理模式复杂度**：多 FM 模式需要存储和计算多个 FM 的嵌入，增加部署复杂度。
- **热图分辨率为 tile 级**：非像素级解释，可能丢失细微形态信息。
- **部分任务提升有限**：如 KRAS 突变、PIK3CA 突变等，COBRA 性能与 baseline 接近或略低，说明并非所有任务都受益。

（完）
