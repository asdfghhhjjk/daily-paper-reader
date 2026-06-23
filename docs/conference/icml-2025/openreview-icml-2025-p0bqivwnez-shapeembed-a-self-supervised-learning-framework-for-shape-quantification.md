---
title: "ShapeEmbed: a self-supervised learning framework for shape quantification"
title_zh: "ShapeEmbed: 一种用于形状量化的自监督学习框架"
authors: "Anna Foix Romero, Craig Russell, Alexander Krull, Virginie Uhlmann"
date: 2025-01-21
pdf: "https://openreview.net/pdf?id=P0bQIvwnEZ"
tags: ["query:pathology-ai"]
score: 6.0
evidence: 适用于细胞形态分析的自监督形状量化框架
tldr: ShapeEmbed是一个自监督框架，通过学习物体轮廓的不变形状描述符，实现了鲁棒的形状量化，可应用于细胞形态分析。该方法解决了形状测量对几何变换的敏感性问题，为细胞形态学特征提取提供了可转移的工具。
source: ICML-2025-Rejected-Public
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-icml-2025-p0bqivwnez/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1705, \"height\": 513, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-p0bqivwnez/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 868, \"height\": 543, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-p0bqivwnez/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 857, \"height\": 401, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-p0bqivwnez/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 696, \"height\": 372, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-icml-2025-p0bqivwnez/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 865, \"height\": 243, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-p0bqivwnez/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 834, \"height\": 223, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-p0bqivwnez/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 786, \"height\": 209, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-p0bqivwnez/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 871, \"height\": 280, \"label\": \"Table\"}]"
motivation: 形状量化在多个领域至关重要，但现有方法难以保证对几何变换的不变性。
method: 提出自监督框架ShapeEmbed，利用欧氏距离矩阵表征物体轮廓，学习平移、缩放、旋转等不变形状描述符。
result: 在形状量化任务上验证了方法的不变性和有效性。
conclusion: ShapeEmbed为形状分析提供了通用的自监督工具，可迁移至细胞形态学等应用。
---

## Abstract
The shape of objects is an important source of visual information in a wide range of applications. One of the core challenges of shape quantification is to ensure that the extracted measurements remain invariant to transformations that preserve an object’s intrinsic geometry, such as changing its size, orientation, and position in the image. In this work, we introduce ShapeEmbed, a self-supervised representation learning framework designed to encode the outline of objects in 2D images into a shape descriptor that is invariant to translation, scaling, rotation, reflection, and outline point indexing. ShapeEmbed relies on a Euclidean distance matrix representation of the outline of input objects. Our approach overcomes the limitations of traditional shape descriptors while improving upon existing state-of-the-art autoencoder-based approaches. We demonstrate that the descriptors learned by our framework outperform their competitors in shape classification tasks on natural and microscopy images. Our framework is also generative, thus allowing for sampling and full reconstruction of 2D outlines from their latent feature vectors.

---

## 论文详细总结（自动生成）

# 论文总结：ShapeEmbed: 一种用于形状量化的自监督学习框架

## 1. 核心问题与整体含义（研究动机和背景）

形状是图像中物体视觉信息的重要来源，在许多应用中至关重要。形状量化的核心挑战是确保提取的测量指标对保持物体内在几何结构的变换（如大小、朝向、位置变化）保持不变。传统的形状描述方法（如区域属性、傅里叶描述符）虽然部分具有不变性，但通常通过平均或压缩信息来获得，无法完整恢复原始轮廓细节。基于自动编码器的表示学习方法开始被使用，但现有方法往往依赖复杂的训练策略来保证几何不变性。本文提出ShapeEmbed，一种自监督表示学习框架，通过直接对物体轮廓的欧氏距离矩阵进行编码，学习一个对平移、缩放、旋转、反射和轮廓点索引均不变形的形状描述符，并具有良好的生成能力。

## 2. 方法论

### 核心思想
- 将物体轮廓采样为固定数量的点（N=64），构建N×N的欧氏距离矩阵（EDM），该矩阵天然具有对平移和旋转的不变性。
- 通过除以矩阵范数实现缩放不变性。
- 对距离矩阵进行归一化后，输入到变分自编码器（VAE）中，通过修改编码器架构和损失函数，实现对抗轮廓点索引（起始点和方向）的不变性，从而也获得反射不变性。

### 关键技术细节
1. **从分割掩膜到距离矩阵**：对二值分割掩膜提取轮廓，用样条插值并均匀采样N个点，计算所有点对之间的欧氏距离得到距离矩阵。缩放不变性通过除以矩阵范数实现。
2. **索引不变编码器**：
   - 使用修改的ResNet-18作为编码器骨干，将标准卷积和池化操作中的填充替换为**循环填充（circular padding）**，使得卷积层对输入的循环移位保持等变性。
   - 对于方向不变性（反射），将每个输入矩阵同时处理其原始版本和水平垂直镜像版本，并将两个输出向量相加，使网络无法区分矩阵与其镜像。
3. **损失函数**：
   - **重建损失**：定义`L_rec`为在所有可能的2N种索引版本（起始点k和方向o）中，取解码输出与输入的最小MSE。这样解码器学习重构一个与输入等价的距离矩阵，而不强制匹配特定索引。
   - **距离矩阵正则化损失**：包括对角线为零损失（`L_diag`）、非负损失（`L_non-neg`）、对称损失（`L_sym`），以确保解码器输出符合距离矩阵的数学性质。
   - **总损失**：`L_VAE = L_rec + β L_KL + γ L_diag + δ L_non-neg + ε L_sym`。默认β=1e-10，γ=δ=ε=1e-5。
4. **轮廓重建**：从潜变量解码得到的距离矩阵经后处理（强制对称、对角线置零），使用多维尺度变换（MDS）恢复二维轮廓点。重建的轮廓具有任意旋转、平移和反射。

## 3. 实验设计

### 数据集
- **MNIST**：手写数字（0-9），约70,000张图像。
- **MPEG-7 CE-Shape-1 Part B**：物体形状基准，1,400个二值掩膜，70类，每类20张。
- **MEF（Mouse Embryonic Fibroblast）**：生物成像数据集，300个图像包含三类细胞（圆形图案、三角形图案、对照），经分割得到26,198个细胞掩膜。
- **BBBC010**：线虫（C. elegans）图像，1,407个二值掩膜，分为活和死两类。

### 基准与对比方法
- **区域属性（Region Properties）**：19个形状相关的统计特征（如面积、周长、曲率等）。
- **椭圆傅里叶描述符（EFD）**：30阶系数，共120个特征。
- **O2VAE**：面向旋转不变性的自编码器方法，使用旋转等变卷积和池化。
- 所有方法均使用逻辑回归分类器（5折交叉验证）在潜变量或特征上评估，以F1分数作为主要指标。

### 消融实验
- 缩放和索引不变性：在随机缩放版的MNIST和MPEG-7上，分别去除归一化、去除索引不变性。
- 旋转和平移不变性：在随机旋转平移版的数据集上，对比原始VAE（直接编码掩膜）、O2VAE和ShapeEmbed。
- 进一步消融：附录中比较潜变量与直接使用距离矩阵作为描述符、正则化项的影响。

## 4. 资源与算力

论文中**未明确说明**使用的GPU型号、数量以及训练时长。仅在附录A.2的Implementation Details中提及了优化器使用Adam、学习率等，但未提及算力资源。因此无法评估训练成本。

## 5. 实验数量与充分性

- **基准实验**：在MNIST和MPEG-7上进行了完整的分类性能对比（包括区域属性、EFD、O2VAE）。
- **消融实验**：两个主要的消融系列（缩放与索引、旋转与平移各两组），每个都在两个数据集上进行，报告均值±标准差。
- **生物成像应用**：在MEF和BBBC010上进行了对比，并增加了加上尺寸信息的变体。
- **附加验证**：附录中还提供了潜变量与距离矩阵直接对比、正则化项的效果、t-SNE可视化、以及使用不同指标（如准确率）的结果。

总体实验设计较为充分：涵盖了标准基准和真实生物数据，消融实验的设计能有效验证各不变性组件的贡献。对比方法包括经典和学习型基线，且均使用了统一的下游分类器，保证了公平性。不足在于缺少与最新生成式或解耦方法（如Vadgama等人的工作）的直接比较（原文解释因代码不可用无法对比），但文中已说明原因。

## 6. 主要结论与发现

1. ShapeEmbed在MNIST（0.963 F1）和MPEG-7（0.751 F1）上显著优于区域属性、EFD和O2VAE。
2. 缩放和索引不变性的消融实验表明，去除索引不变性会导致MNIST性能下降7.24%，去除归一化下降4.18%；在MPEG-7上差距更大，验证了这两个组件的重要性。
3. 在随机旋转平移数据集上，ShapeEmbed（0.846/0.656）大幅领先O2VAE（0.658/0.102）和原始VAE（0.382/0.042），证明了距离矩阵表示带来的强不变性。
4. 在生物成像数据集上，加入尺寸信息后ShapeEmbed在MEF（0.745）和BBBC010（0.859）上均超过所有对比方法。
5. t-SNE可视化显示，ShapeEmbed的潜空间能根据真实形状形成清晰的分类簇，且能发现标签错误的数据点，展示了其在无监督探索中的价值。

## 7. 优点

- **设计简洁有效**：利用距离矩阵天然的不变性质，仅需对编码器进行简单的修改（循环填充、镜像相加）和自定义损失，而非依赖复杂的网络结构。
- **全面的不变性**：同时实现了平移、旋转、缩放、反射和索引不变性，这在实际图像（尤其是生物成像）中非常实用。
- **生成能力**：VAE架构允许从潜空间采样并完整重建轮廓，便于可视化与质量控制。
- **灵活性**：可分离出尺寸信息作为额外特征，以适应不同生物学问题（需要或不需要尺寸不变性）。
- **开源代码**：提供Python实现，便于复现和应用。

## 8. 不足与局限

- **仅限2D**：当前框架只适用于2D图像轮廓，扩展到3D需要额外工作。
- **MDS重建不唯一**：从距离矩阵恢复轮廓时依赖MDS，其解不唯一（仅等价于旋转、平移、反射），且不能保证全局最优。
- **索引不变性缺乏严格理论保证**：作者指出因ResNet中存在步长和池化，严格来说不再保持完全的移位等变性，但实践效果足够。理论上可能存在边界情况。
- **尺寸信息处理**：在需要尺寸信息的场景下，需要手动保存并添加回特征，增加了使用复杂度。
- **实验范围有限**：在生物成像方面仅测试了两个数据集（MEF、BBBC010），且类别较少。更多真实医学或生物学场景下的验证有待进行。
- **缺少与部分最新工作对比**：如Vadgama等人的方法因代码未公开而无法比较，削弱了最先进性的证明力度。
- **计算资源未公开**：未说明训练模型所需的硬件配置和时间，不便于评估可复现性。

（完）
