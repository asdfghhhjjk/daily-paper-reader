---
title: "EFDTR: Learnable Elliptical Fourier Descriptor Transformer for Instance Segmentation"
title_zh: EFDTR：可学习的椭圆傅里叶描述子Transformer用于实例分割
authors: "Jiawei Cao, Chaochen Gu, Hao Cheng, Xiaofeng Zhang, Kaijie Wu, Changsheng Lu"
date: 2025-05-01
pdf: "https://openreview.net/pdf?id=nSldadGGY5"
tags: ["query:cellseg"]
score: 7.0
evidence: 基于傅里叶描述子的实例分割方法
tldr: 多边形表示能高效建模物体边界，但优化复杂度高。本文提出EFDTR，利用椭圆傅里叶描述子作为顶点回归损失，无需光栅化或启发式近似，在频域匹配解决边界点歧义。结合Transformer端到端学习，实现精确轮廓预测。该方法为实例分割提供了新范式，可迁移至细胞分割任务。
source: ICML-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-icml-2025-nsldadggy5/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 822, \"height\": 834, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-nsldadggy5/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 846, \"height\": 776, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-nsldadggy5/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 819, \"height\": 325, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-nsldadggy5/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1756, \"height\": 909, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-nsldadggy5/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1770, \"height\": 906, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-nsldadggy5/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 860, \"height\": 299, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-icml-2025-nsldadggy5/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1767, \"height\": 884, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-nsldadggy5/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 855, \"height\": 227, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-nsldadggy5/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 848, \"height\": 223, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-nsldadggy5/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 856, \"height\": 260, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-nsldadggy5/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 855, \"height\": 194, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-nsldadggy5/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 845, \"height\": 154, \"label\": \"Table\"}]"
motivation: 多边形实例分割受限于高优化复杂度，阻碍其实际应用。
method: 提出基于傅里叶椭圆描述子的顶点回归损失，并设计端到端Transformer框架。
result: 模型实现精确轮廓预测，无需光栅化。
conclusion: EFDTR为实例分割提供了高效的多边形表示学习方案。
---

## Abstract
Polygon-based object representations efficiently model object boundaries but are limited by high optimization complexity, which hinders their adoption compared to more flexible pixel-based methods. 
In this paper, we introduce a novel vertex regression loss grounded in Fourier elliptic descriptors, which removes the need for rasterization or heuristic approximations and resolves ambiguities in boundary point assignment through frequency-domain matching.
To advance polygon-based instance segmentation, we further propose EFDTR (\textbf{E}lliptical \textbf{F}ourier \textbf{D}escriptor \textbf{Tr}ansformer), an end-to-end learnable framework that leverages the expressiveness of Fourier-based representations. 
The model achieves precise contour predictions through a two-stage approach: the first stage predicts elliptical Fourier descriptors for global contour modeling, while the second stage refines contours for fine-grained accuracy. Experimental results on the COCO dataset show that EFDTR outperforms existing polygon-based methods, offering a promising alternative to pixel-based approaches. Code is available at \url{https://github.com/chrisclear3/EFDTR}.

---

## 论文详细总结（自动生成）

# EFDTR：可学习的椭圆傅里叶描述子Transformer用于实例分割——详细中文总结

## 1. 核心问题与整体含义（研究动机和背景）
- **问题**：实例分割是计算机视觉基本任务，传统方法依赖像素级掩码，而基于多边形（polygon）的表示方法能更紧凑地建模物体边界，但存在优化复杂度高、回归目标分配歧义等挑战，难以与灵活但计算成本高的像素方法竞争。
- **背景**：现有多边形方法（如PolarMask、DeepSnake、BoundaryFormer）采用极坐标或欧氏距离分配目标点，存在对非凸形状不适用、缺乏全局拓扑一致性、或需要启发式光栅化等局限。
- **动机**：引入椭圆傅里叶描述子（EFDs）作为紧凑、可靠的轮廓表示，利用频域相位信息建立轮廓点与相位间的双射，解决回归目标歧义，并设计端到端Transformer框架提升多边形预测质量。

## 2. 方法论：核心思想、关键技术细节
### 2.1 核心思想
- 将轮廓表示为椭圆傅里叶级数，通过预测傅里叶描述子（4n+1个参数）实现全局形状建模，再通过相位对齐的顶点回归损失进行精细轮廓细化。
- 两阶段解码：第一阶段预测EFD参数得到粗轮廓；第二阶段基于相位采样进行特征采样和变形注意力，得到精细多边形。

### 2.2 关键技术细节
- **多多边形连接**：针对实例包含多个分离轮廓（如孔洞），构建完全图并通过最小生成树（MST）合并为单一闭合轮廓，最小化连接边长度。
- **椭圆傅里叶描述子（EFDs）**：采用弧长参数化，计算傅里叶系数（An, Bn, Cn, Dn），并对一阶系数施加相位约束（A1>0, C1=0, D1>0），确保零相位与正x轴对齐。
- **相位分配**：通过相位θp = 2πt_p/T建立轮廓点与参数相位的双射，用于目标点匹配。采用“snapping”操作将均匀相位采样点映射到目标相位集合，解决欧氏距离的歧义。
- **模型结构**（EFDTR）：
  - 特征提取：基于RT-DETR的Hybrid Feature Fusion，输出多尺度特征P2~P5。
  - EFD解码器：对P3~P5特征，通过Score Encoder选择top-k特征，结合噪声目标输入，经自注意力和可变形注意力后，由Class Head和EFD Head预测分类和EFD参数。
  - 多边形解码器：利用网格采样对P2~P5多尺度特征按预测轮廓点采样，分组(g=4)减少计算量，自适应融合权重后送入变形注意力迭代细化，最终输出128个顶点。
- **损失函数**：分类使用Varifocal Loss（VFL）；EFD回归用L1 loss；多边形回归用相位对齐的Smooth-L1 loss（含L1和L2两项）；总损失L = L_cls + αL_efd + βL_polygon，α=6, β=10。

## 3. 实验设计
- **数据集**：MS COCO （val2017），使用多边形标注，预处理时统一方向为右手系。
- **Benchmark**：对比方法包括像素级方法（Mask R-CNN、Mask DINO、Mask2Former等）和多边形方法（DeepSnake、PolarMask、DANCE、SharpContour、BoundaryFormer等）。
- **主要对比**：
  - ResNet-50骨干：EFDTR达到AP 43.6，优于所有多边形方法（最高BoundaryFormer 36.1），接近Mask DINO（46.0）。
  - ResNet-101骨干：AP 45.1，超越Mask2Former（44.2）等。
- **消融实验**：在12个epoch下验证了：
  - 解码器层数（NE=6, NP=3最优）
  - EFD阶数（1阶最优，高阶引入噪声）
  - 顶点分组大小（4个最优平衡性能与计算）
  - 多尺度融合方法（加权融合优于平均和仅P2）
  - IoU类型（轴对齐IoU优于旋转IoU）
- **定性分析**：展示了精细边界分割（伞柄、自行车内部）和多个多边形实例的连接效果，同时指出辅助边界对齐仍有改进空间。

## 4. 资源与算力
- **文中说明**：使用AdamW优化器，多步学习率调度，EMA，数据增强（RandomFlip, RandomIoUCrop, 多尺度训练），推理时固定输入800×800。但**未明确提及GPU型号、数量、训练总时长**。实验基于COCO训练集训练36个epoch（消融为12 epoch）。

## 5. 实验数量与充分性
- **总体实验数量**：约10组对比实验（表1）+ 5组消融实验（表2~6）+ 定性可视化（图5、6）。
- **充分性**： 
  - 对比方法覆盖了主流多边形和像素方法，指标全面（AP、AP50、AP75、AP_S/M/L）。
  - 消融实验考察了解码器深度、EFD阶数、分组、融合方式、损失函数变体等关键设计，较为充分。
  - 但缺少在更小或特定领域数据集（如医学图像）上的验证，也未见运行效率（FPS）比较。
- **客观公平**：与多边形方法相比，EFDTR使用了更长的训练epoch（36 vs 12~160不等），且采用更现代的Transformer架构，对比不一定完全等架构公平，但结果仍具说服力。

## 6. 主要结论与发现
- 椭圆傅里叶描述子能够通过频域相位唯一映射轮廓点，有效解决回归目标歧义。
- 一阶EFD（仅椭圆形状）比高阶EFD更适合粗定位，高阶易引入噪声。
- 两阶段架构（全局EFD + 细粒度多边形卷积）显著优于单阶段多边形回归。
- EFDTR在COCO上大幅超越现有多边形方法（+7.5 AP vs BoundaryFormer），并接近顶尖像素方法，证明了多边形方法在性能上可以媲美像素方法。
- 多尺度加权融合和轴对齐IoU的Varifocal Loss有助于提升AP。

## 7. 优点
- **创新性**：首次将椭圆傅里叶描述子引入实例分割的顶点回归损失，利用相位实现全局一致的匹配，无需光栅化或启发式近似。
- **简洁性**：EFD参数数量少（4n+1），可端到端学习，且相位约束保证了特征规范性。
- **性能**：在COCO上达到多边形方法最优，且在中小物体和大物体上均有提升，证明泛化强。
- **结构设计**：两阶段解码、分组采样、可变形注意力等兼顾精度与效率；多轮廓合并策略（MST）实用。
- **代码开源**：促进可复现性。

## 8. 不足与局限
- **实验覆盖不足**：仅测试COCO一个数据集，缺乏在医学影像、遥感等领域的验证；未提供推理速度（FPS）和参数量对比（仅消融中提到参数量）。
- **多轮廓连接缺陷**：当实例包含多个分离区域时，辅助边界对齐仍不够紧密，可能引入额外IoU误差（图6已提及）。
- **计算资源不明确**：未提供GPU型号、数量、训练时长，难以评估可复现性。
- **EFD阶数选择**：仅测试了1、2、4阶，未探索最优阶数范围；且一阶EFD可能丢失某些非凸形状的细节，二阶高阶虽然噪声敏感但或许可以通过更好的正则化改善。
- **对比公平性**：与Mask DINO等大规模预训练方法相比，EFDTR未使用更强的骨干或更大batch，可能未能充分展现上限。

（完）
