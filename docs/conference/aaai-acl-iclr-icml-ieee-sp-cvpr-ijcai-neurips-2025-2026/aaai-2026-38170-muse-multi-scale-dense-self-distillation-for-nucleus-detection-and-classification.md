---
title: "MUSE: Multi-Scale Dense Self-Distillation for Nucleus Detection and Classification"
title_zh: "MUSE: 面向细胞核检测与分类的多尺度密集自蒸馏"
authors: "Zijiang Yang, Hanqing Chao, Bokai Zhao, Yelin Yang, Yunshuo Zhang, Dongmei Fu, Junping Zhang, Le Lu, Ke Yan, Dakai Jin, Minfeng Xu, Yun Bian, Hui Jiang"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/38170/42132"
tags: ["query:cellseg"]
score: 10.0
evidence: 组织病理学中细胞核检测与分类的自监督学习，利用无标签数据学习判别性细胞核表示
tldr: 细胞核检测与分类高度依赖人工标注，难以利用大规模无标签数据。MUSE提出多尺度密集自蒸馏方法，特别设计了基于坐标引导的局部自蒸馏模块NuLo，允许在增广视图间进行灵活的自蒸馏预训练，有效利用了无标签WSI。实验证明该方法在减少标注需求的同时，显著提升了检测与分类精度，在多个基准上达到最优。为数字病理细胞级分析提供了高效自监督学习范式，有望降低临床部署成本。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38170/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 877, \"height\": 518}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38170/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 863, \"height\": 666}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38170/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 873, \"height\": 579}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38170/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1780, \"height\": 519}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38170/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 869, \"height\": 341}]"
tables_json: "[{\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38170/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1846, \"height\": 1133}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38170/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1846, \"height\": 1135}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38170/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 801, \"height\": 212}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38170/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 887, \"height\": 252}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38170/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1820, \"height\": 459}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38170/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 625, \"height\": 212}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38170/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 626, \"height\": 219}]"
motivation: 现有核检测分类依赖昂贵标注，未能有效利用海量无标签数据。
method: 提出多尺度密集自蒸馏和坐标引导局部自蒸馏进行预训练。
result: 在减少标注需求的同时，显著提升检测与分类精度，达到最优性能。
conclusion: 为细胞核检测分类提供了减少标注依赖的高效自监督框架。
---

## Abstract
Nucleus detection and classification (NDC) in histopathology analysis is a fundamental task that underpins a wide range of high-level pathology applications. However, existing methods heavily rely on labor-intensive nucleus-level annotations and struggle to fully exploit large-scale unlabeled data for learning discriminative nucleus representations. In this work, we propose MUSE (MUlti-scale denSE self-distillation), a novel self-supervised learning method tailored for NDC. At its core is NuLo (Nucleus-based Local self-distillation), a coordinate-guided mechanism that enables flexible local self-distillation based on predicted nucleus positions. By removing the need for strict spatial alignment between augmented views, NuLo allows critical cross-scale alignment, thus unlocking the capacity of models for fine-grained nucleus-level representation. To support MUSE, we design a simple yet effective encoder-decoder architecture and a large field-of-view semi-supervised fine-tuning strategy that together maximize the value of unlabeled pathology images. Extensive experiments on three widely used benchmarks demonstrate that MUSE effectively addresses the core challenges of histopathological NDC. The resulting models not only surpass state-of-the-art supervised baselines but also outperform generic pathology foundation models.

---

## 论文详细总结（自动生成）

## 1. 论文的核心问题与整体含义

*   **研究动机与背景**
    *   细胞核检测与分类（NDC）是组织病理分析的基础任务，广泛应用于疾病诊断、生物标志物评估和预后预测。
    *   现有方法高度依赖像素级或点级的人工标注，成本极高且耗时，且仅在小视场（FoV）高倍率图像块上进行标注，无法充分捕捉组织架构和染色差异的全貌。
    *   近期自监督学习（SSL）已被用于从海量无标签数据中学习可泛化视觉表征，其预训练的基础模型在 WSI 级任务上表现良好，但在细胞核级密集预测任务上的表现仍受限。
    *   根本原因有三点：① 主流 SSL 方法要求不同增强视图间严格的空间对齐，难以引入尺度抖动等关键空间增强；② 缺少跨层级特征监督，无法有效融合多级特征；③ 模型通常在极小 FoV 的补丁上训练，无法捕获更广泛的组织上下文信息。
*   **整体含义**
    *   本文提出 **MUSE**（多尺度密集自蒸馏），一种专为 NDC 设计的新型自监督学习方法，通过灵活的跨尺度核级自蒸馏，让模型在不依赖严格空间对齐的情况下学习可区分的细胞核表征。
    *   配合编码器-解码器架构、大视场预训练和半监督微调策略，MUSE 能够高效利用大规模无标签病理图像，在仅使用较小模型和少量数据的情况下超越通用病理基础模型，并显著优于现有的全监督 NDC 方法。

## 2. 论文提出的方法论

### 2.1 整体框架
*   **编码器-解码器架构**
    *   基于 Vision Transformer (ViT) 构建，编码器提取多级特征，经重装配层（Reassembly Layer）转化为 2D 特征图，传递给基于残差块的解码器，逐步融合多级特征。
    *   最终输出一个统一的密集特征图 \(f_{\text{map}}\)（用于核级蒸馏）和一个 CLS token \(f_{\text{cls}}\)（用于图像级蒸馏）。
*   **自蒸馏预训练策略**
    *   以 DINO 的教师-学生自蒸馏框架为基础，学生网络使用梯度更新，教师网络通过指数移动平均（EMA）更新。
    *   损失函数包含两部分：
        *   图像级自蒸馏损失 \(L_{\text{image}}\)：作用于教师/学生网络的 CLS token 输出，保持全局表示能力。
        *   核级局部自蒸馏损失 \(L_{\text{nu}}\)：作用于教师/学生网络的密集特征图输出，围绕检测到的细胞核坐标进行特征插值和对比学习。整体损失 \(L_{\text{MUSE}} = \lambda_{\text{image}} L_{\text{image}} + \lambda_{\text{nu}} L_{\text{nu}}\)。

### 2.2 核心技术细节
*   **NuLo：Nucleus-based Local Self-distillation**
    *   核心思想：利用轻量细胞核检测器在无标签数据上自动估计核坐标，然后基于这些坐标从特征图插值出每个核的特征，允许在不同视图之间对同一个细胞核的特征进行对比学习。
    *   通过坐标索引机制实现跨视图的核匹配，完全解除对空间对齐的依赖，使得模型能够同时进行尺度变换、翻转等增强，并能学习同一细胞核在组织上下文中的不同视图（如大尺度组织上下文与小尺度细胞细节）之间的跨尺度对齐，类似于病理学家的诊断过程。
*   **MPP-Based Cropping (基于微米/像素的裁剪)**
    *   针对病理图像物理分辨率至关重要的特点，提出按物理尺度（MPP）随机采样生成成对视图，确保预训练视图分辨率具有明确的物理意义，从而支持有效的跨尺度对比学习。
*   **大视场 (Large FoV) 预训练与微调**
    *   预训练阶段：将全局视图和局部视图的分辨率从 \(224\times224\) / \(96\times96\) 扩展到 \(512\times512\) / \(208\times208\)，以融合更丰富的组织上下文。
    *   下游微调阶段：将标注区域自然地“扩展”成大视场样本，其中包含周围未标注的组织区域。在标注区域使用标准的检测/分类损失，在未标注区域使用基于伪标签的一致性正则化损失，实现半监督微调。

### 2.3 关键公式说明
*   图像级自蒸馏损失： \(L_{\text{image}} = -P_t^{(\text{cls})}(M_t(I^{(1)})) \log P_s^{(\text{cls})}(M_s(I^{(2)}))\)，遵循 DINO。
*   核级局部自蒸馏损失：
    \[
    L_{\text{nu}} = \sum_{K_{\text{cap}}} -P_t^{(\text{nu})}(F_c^{(1)}[K_{\text{cap}}]) \log P_s^{(\text{nu})}(F_c^{(2)}[K_{\text{cap}}]), \quad K_{\text{cap}} = K_o^{(1)} \cap K_o^{(2)}
    \]
    其中 \(K\) 是细胞核的全局唯一索引，实现了跨视图的核匹配。

## 3. 实验设计
*   **数据集与场景**
    *   预训练：基于 TCGA 构建了包含 483,627 个 ROI 补丁的数据集 **TCGA\(_{\text{nu}}\)**，核坐标通过自动检测获得。
    *   下游评测：使用三个广泛使用的多组织、多倍率 NDC 基准数据集——**BRCAM2C**（乳腺）、**OCELOT**（多器官组织重叠细胞）、**PUMA**（黑色素瘤）。
*   **评估协议与指标**
    *   核分类任务：使用 k-近邻 (KNN)、线性探测 (LIN) 和端到端微调 (FT) 三种模式，报告准确率 (ACC%)。
    *   核检测与分类任务：报告不同细胞类型（淋巴细胞、肿瘤细胞、其他细胞）及平均 F1 分数。
*   **对比方法**
    *   **通用预训练方法**：在 ImageNet-1k/22k 上预训练的 DINO、MAE、iBOT，以及在大规模数据 LVD-142M 上预训练的 DINOv2。
    *   **病理预训练基础模型**：MoCoV2、CTransPath、CHIEF、CONCH、UNI、Prov-GigaPath。
    *   **最先进的有监督 NDC 方法**：MCSpatNet、PointNu-Net、SMILE、SENC、CGT、CellViT、DPA-P2PNet。

## 4. 资源与算力
*   论文中未明确提及实验所使用 GPU 的型号、数量及训练总时长。仅说明了预训练数据集 TCGA\(_{\text{nu}}\) 包含约 48 万张 ROI 补丁，模型参数规模从 31M 到 123M 不等。这是实验复现时的一个关键信息缺失。

## 5. 实验数量与充分性
*   **实验数量**：实验设计非常详尽，总共约 6 组主要实验：
    1.  与通用预训练和病理预训练模型在核分类任务上的全面对比（表1、表2），覆盖 6 个 bench（3 数据集 × 2 倍率），3 种架构，3 种评测模式。
    2.  与大视场预训练版本（LFoV-MUSE）的对比（表1、表2）。
    3.  与有监督 NDC 方法在检测和分类任务上的对比（表3）。
    4.  详细的消融实验（表4-表7），包括解码器、多尺度打补丁、自蒸馏损失、大视场微调等核心组件的验证。
*   **充分性与公平性**
    *   实验非常充分，覆盖了从表征学习到下游任务转移的全流程，且与最先进方法进行了公平对比（选用相同或相近的骨干网络和预训练数据规模）。
    *   为了公平比较，还专门使用 DINOv2 在相同的 TCGA\(_{\text{nu}}\) 数据集上进行了预训练作为对照，证明性能增益来源于方法设计而非单纯的数据差异。

## 6. 论文的主要结论与发现
*   MUSE 能极大提升病理图像中细胞核级特征的表示能力。在核分类 KNN、线性探测和微调评估下，其表现显著优于同样在通用或病理数据上预训练的 DINOv2、CONCH、UNI 等强基线模型。
*   配合 LFoV 预训练和半监督微调，MUSE 在 BRCAM2C、OCELOT 和 PUMA 上的 NDC 性能全面大幅超越现有最先进的全监督方法（如 CellViT、DPA-P2PNet），平均 F1 分数提升高达 7.24 个百分点。
*   即便模型参数量（ViT-B, 86M）和预训练数据量（~0.5M 补丁）远小于 UNI（ViT-L, 300M）和 Prov-GigaPath（ViT-G, 1.1B），MUSE 仍然可以取得更优的性能，展现出极强的数据效率和任务针对性。

## 7. 优点
*   **创新性强**：提出的 NuLo 模块创造性地将坐标引导机制引入自蒸馏，解决了SSL在密集预测任务中难以应用强空间增强的根本矛盾，并实现跨尺度细胞上下文学习。
*   **框架完整且高效**：提供了一个从模型架构、预训练到下游微调的完整解决方案，高效利用无标签数据，且能灵活适配不同编码器（ViT、ResNet）。
*   **性能提升显著**：在核心的 NDC 任务上大幅领先，包括击败了参数量和数据量是其数倍的通用基础模型，证明了任务专用预训练在细胞级分析中的巨大价值。
*   **实验设计扎实**：包含广泛的基线模型、多组数据集和全面的消融实验，论证严谨，可比性强。

## 8. 不足与局限
*   **预训练成本不透明**：未公开关键的算力开销（GPU 类型/数量/训练时间），一定程度上限制了复现和实际部署的成本评估。
*   **预训练依赖伪标签**：NuLo 需要依赖自动检测的细胞核坐标，这些伪标签的质量直接决定了预训练效果，在图像质量差或组织结构复杂的场景下可能存在鲁棒性风险。
*   **微调策略限制**：提出的 LFoV 半监督微调要求输入是包含标注区域和周围未标注区域的扩展样本，这种采样策略有效，但前提是已知标注区域的有规则形状（如正方形），对于不规则的标注区域支持有限。
*   **泛化边界未探索**：虽然在三个组织学数据集上验证有效，但其在如细胞学涂片、免疫组化染色等其他病理图像模态上的泛化能力未进行系统验证。

（完）
