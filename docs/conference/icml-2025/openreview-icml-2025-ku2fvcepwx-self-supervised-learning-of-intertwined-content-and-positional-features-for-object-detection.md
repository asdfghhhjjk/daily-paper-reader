---
title: Self-Supervised Learning of Intertwined Content and Positional Features for Object Detection
title_zh: 自监督学习交织的内容和位置特征用于目标检测
authors: "Kang-Jun Liu, Masanori Suganuma, Takayuki Okatani"
date: 2025-05-01
pdf: "https://openreview.net/pdf?id=Ku2fvCEpwx"
tags: ["query:cellseg"]
score: 8.0
evidence: 提出使用ViT的自监督方法用于目标检测和实例分割
tldr: 针对目标检测和实例分割任务，现有自监督方法未能有效同时捕获类别和位置信息。该论文提出一种基于Vision Transformer的自监督学习方法，通过将裁剪过程中的位置编码与掩码预测相结合，学习内容与位置交织的特征表示。实验表明该方法在多个检测和分割基准上取得优异性能，无需人工标注即可学习到具有区分性的特征，为实例分割的自监督预训练提供了新思路。
source: ICML-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-icml-2025-ku2fvcepwx/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1602, \"height\": 467, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-ku2fvcepwx/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1477, \"height\": 531, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-ku2fvcepwx/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 334, \"height\": 289, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-ku2fvcepwx/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 512, \"height\": 259, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-ku2fvcepwx/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1581, \"height\": 513, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-ku2fvcepwx/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1674, \"height\": 1409, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-ku2fvcepwx/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 849, \"height\": 1140, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-icml-2025-ku2fvcepwx/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 815, \"height\": 932, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-ku2fvcepwx/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 846, \"height\": 214, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-ku2fvcepwx/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 740, \"height\": 213, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-ku2fvcepwx/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 597, \"height\": 869, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-ku2fvcepwx/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 725, \"height\": 607, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-ku2fvcepwx/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 725, \"height\": 607, \"label\": \"Table\"}]"
motivation: 现有自监督特征学习方法难以同时提取目标检测和实例分割所需的类别与位置信息。
method: 提出两种关键组件：裁剪过程的位置编码（向量场表示）和内容与位置嵌入的并行掩码预测，使用ViT学习交织特征。
result: 在多个目标检测和实例分割数据集上，该方法超越了对比学习和掩码图像建模等基线方法。
conclusion: 该自监督范式能够有效学习实例级的内容和位置特征，为下游视觉任务提供强预训练表示。
---

## Abstract
We present a novel self-supervised feature learning method using Vision Transformers (ViT) as the backbone, specifically designed for object detection and instance segmentation. Our approach addresses the challenge of extracting features that capture both class and positional information, which are crucial for these tasks. The method introduces two key components: (1) a positional encoding tied to the cropping process in contrastive learning, which utilizes a novel vector field representation for positional embeddings; and (2) masking and prediction, similar to conventional Masked Image Modeling (MIM), applied in parallel to both content and positional embeddings of image patches. These components enable the effective learning of intertwined content and positional features. We evaluate our method against state-of-the-art approaches, pre-training on ImageNet-1K and fine-tuning on downstream tasks. Our method outperforms the state-of-the-art SSL methods on the COCO object detection benchmark, achieving significant improvements with fewer pre-training epochs. These results suggest that better integration of positional information into self-supervised learning can improve performance on the dense prediction tasks.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 核心问题与整体含义（研究动机和背景）

- **研究动机**：目标检测（Object Detection, OD）和实例分割（Instance Segmentation, IS）等密集预测任务需要同时捕获图像局部区域的 **内容信息**（如物体类别）和 **位置信息**（如物体在图像中的空间位置）。现有的自监督学习方法（如对比学习、掩码图像建模）要么侧重全局不变性（忽略位置细节），要么在位置建模上不够充分，导致预训练特征难以同时兼顾两类信息。
- **整体含义**：本文提出一种新颖的自监督学习方法，专门为 OD/IS 设计，通过在对比学习框架中引入**与裁剪对齐的位置编码**和**位置‑内容双掩码预测**，使 Vision Transformer（ViT）学习到“交织”（intertwined）的内容与位置特征，从而提升下游密集预测任务的性能。

## 2. 方法论：核心思想与关键技术细节

### 核心思想
基于 DINOv2 框架，增加两个关键组件：
1. **与图像裁剪对齐的位置编码** – 将位置编码视为一个与输入图像同分辨率的向量场，裁剪图像时同时裁剪该向量场，从而保留裁剪区域在原图中的绝对位置和尺度信息。
2. **位置嵌入与内容嵌入的并行掩码预测** – 对 ViT 的 patch 嵌入同时进行内容掩码和位置掩码，分别预测被掩码的部分，强制模型同时利用内容和位置线索。

### 关键技术细节
- **位置编码向量场**  
  定义一个大小为 \( w_p \times h_p \times d \) 的连续向量场 \( P \)，其中 \( w_p, h_p \) 为超参数（实验中默认 \(50 \times 50\)）。对于每个裁剪视图 \( u = t_u(x) \)，使用相同的变换 \( t_u \) 裁剪 \( P \) 得到 \( p_u = t_u(P) \)，然后在 patch 网格上插值采样得到每个 patch 的位置向量 \( p_{u,i} \)，与内容嵌入 \( u_i \) 相加后输入 ViT。

- **位置和尺度增强**  
  为了避免模型过度依赖绝对位置（ImageNet 物体通常居中且较大，而 COCO 物体尺度多样），对裁剪后的位置向量场施加随机缩放和平移变换。缩放因子 \( s \) 从 Beta(2,5) 分布中采样，平移均匀随机。

- **位置掩码与预测**  
  在全局裁剪中随机选择一定比例的 patch，将其位置嵌入替换为特殊标记 \( e_{\text{POSMASK}} \)，然后通过 ViT 的输出预测原始位置嵌入在特征空间中的分布（类似 MIM 的分类损失）。同时保留内容掩码预测（沿用 iBOT/DINOv2 的设置）。两种掩码互斥，每张图像随机只做一种（比例 50:50）。位置掩码采用“交叉形”采样策略（cross‑wise）而非传统的“框形”采样。

- **损失函数**  
  总损失为：
  \[
  \mathcal{L}_{\text{ours}} = \underbrace{\mathcal{L}_{\text{image}} + \mathcal{L}_{\text{content}}}_{\text{iBOT}} + \lambda_{\text{KoLeo}}\mathcal{L}_{\text{KoLeo}} + \mathcal{L}_{\text{pos}}
  \]
  其中 \(\mathcal{L}_{\text{pos}}\) 为位置预测损失，\(\mathcal{L}_{\text{KoLeo}}\) 用于增加特征多样性（权重设为 1）。训练时只将 \(\mathcal{L}_{\text{pos}}\) 应用于学生模型，教师模型通过指数移动平均更新。

## 3. 实验设计

### 数据集与基准
- **预训练**：ImageNet‑1K（100 个 epoch）。
- **下游微调**：
  - **COCO 目标检测 + 实例分割**（主要 benchmark）：使用 ViTDet 检测框架，微调 12 epoch（22,128 次迭代），batch size 64。
  - **ADE20K 语义分割**（次要 benchmark）：使用 Segmenter 线性解码器，微调 127 epoch（160k 迭代）。

### 对比方法
- 通用 SSL：DINO、MAE、iBOT、DINOv2（作者在 ImageNet‑1K 上复现的版本记为 DINOv2†）。
- 密集预测专用 SSL：Mugs、DropPos、CrIBo、SelfPatch、FLSL、CrOC、LOCA。
- 额外对比：官方 DINOv2 / DINOv2‑reg（预训练于 LVD‑142M 大数据集）。

### 骨干网络
- 主要结果采用 ViT‑B/16，消融实验采用 ViT‑S/16。

## 4. 资源与算力

论文明确说明：
- ViT‑S 使用 **4 块 A6000 GPU**（单节点）。
- ViT‑B 使用 **2 个节点，每个节点 4 块 A6000 GPU**（共 8 块）。
- 预训练 100 epoch，训练时间约为 DINOv2† 的 **1.3 倍**。
- 微调阶段使用了 checkpoint 和高效注意力内核（xformers）以节省 GPU 内存。

未说明总 GPU 小时数，但给出了硬件和训练相对时间。

## 5. 实验数量与充分性

### 实验数量
- **主要结果**：COCO（AP Box、AP Mask）和 ADE20K（mIoU），在 ViT‑S 和 ViT‑B 上各对比 10 种以上方法。
- **消融实验**：共 4 组，分别验证：
  1. 两个组件的单独效果。
  2. 缩放因子分布（Const、Uniform、Beta(2,5)）。
  3. 位置编码场分辨率（19×19 vs 50×50）。
  4. 位置掩码采样策略（box‑wise vs cross‑wise）以及内容/位置掩码比例（100:0、0:100、50:50）。
- **额外分析**：注意力图可视化（NMI、MAD 指标）和 patch attention 热图比较。

### 充分性与公平性
- 对比方法的权重均来自官方仓库（DINOv2 因原始模型在更大数据集上训练，作者自行在 ImageNet‑1K 上复现并记为 DINOv2†），保证了公平性。
- 对 FLSL 的结果指出了其官方代码存在 bug，已做备注。
- 消融实验覆盖了关键超参数，但未进行大规模网格搜索（仅选用了合理的默认值）。
- 语义分割（ADE20K）上方法未显著优于竞品，作者承认了这一点。

结论：实验较为充分，但主要优势体现在 COCO 检测/分割上，语义分割任务提升有限。

## 6. 主要结论与发现

1. **两个核心组件均有效**：位置编码对齐裁剪（+1.9 AP Box）和位置掩码预测（+2.4 AP Box）单独使用均有提升，联合使用进一步提升（+3.5 AP Box 相对于 DINOv2†）。
2. **比现有 SSL 方法更优**：在 COCO 上以更少的有效 epoch 超越所有对比方法（包括专为密集预测设计的 DropPos、LOCA 等）。
3. **注意力分析解释性能**：本文方法的注意力图能更清晰地分离前景物体实例和背景，适合 OD/IS 任务。
4. **DINOv2† 复现性能与 iBOT 相当**，表明 DINOv2 的改进（如 KoLeo 正则化）在 ImageNet‑1K 规模下已有效。
5. **语义分割上无明显优势**：说明位置线索对于像素级分类任务的重要性低于实例级区分任务。

## 7. 优点

- **创新性**：将位置编码与裁剪过程对齐（类似“局部坐标系”保留全局信息），以及对称地对位置和内容进行掩码预测，是两个新颖且有效的设计。
- **实用性强**：仅需在 DINOv2 代码上做少量扩展，可无缝嵌入现有数据增强流水线，且推理时用标准 ViT，无额外开销。
- **消融实验清晰**：每个组件和超参数的影响都进行了定量分析，便于理解和复现。
- **实验充分且公正**：对比了多个官方预训练权重，并复现了 DINOv2 在相同预训练条件（ImageNet‑1K）下的表现，控制了变量。
- **注意力可视化提供直觉解释**：通过 NMI、MAD 和注意力热图，定性展示了方法如何改善实例区分能力。

## 8. 不足与局限

- **实验覆盖的局限性**：
  - 仅在 ImageNet‑1K 上预训练，未在大规模数据集（如 LVD‑142M）上验证。官方 DINOv2 在 LVD‑142M 上训练后仍优于本文方法（表 6），说明方法优势可能随数据规模扩大而减弱。
  - 语义分割（ADE20K）上提升不显著，甚至落后于部分竞品，表明方法更适用于实例级任务而非像素级分类。
  - 仅测试了 ViT‑S 和 ViT‑B，未在更大骨干（如 ViT‑L、ViT‑g）或卷积网络（如 ResNet）上验证泛化性。
- **潜在偏差**：
  - 位置和尺度增强中 Beta(2,5) 分布的选择基于经验，未提供理论依据或跨数据集验证（例如 COCO 中物体尺度分布是否严格匹配）。
  - 位置掩码采用“交叉形”策略的实验仅比较了“框形”和“交叉形”，未探索其他更优模式。
- **应用限制**：
  - 方法依赖 ViT 架构和对比学习框架，对于传统 CNN 或不使用位置编码的模型可能不直接适用。
  - 训练时间相对 DINOv2† 增加 30%，虽然可接受但未深入讨论计算开销。
- **理论分析不足**：未从信息论或梯度传播角度解释为何“交织”特征更优，依赖于经验验证和可视化。

（完）
