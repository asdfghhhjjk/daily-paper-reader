---
title: Spatially Informed Autoencoders for Interpretable Visual Representation Learning
title_zh: 面向可解释视觉表示学习的空间信息自编码器
authors: "Dominik Sturm, Hiba Bensalem, Ivo F. Sbalzarini"
date: 2026-01-26
pdf: "https://openreview.net/pdf?id=09YSBymX6O"
tags: ["query:path-xai-sel"]
score: 6.0
evidence: 通过点过程学习可解释的空间组织模式，适用于基于空间纹理的感兴趣区域检测
tldr: 提出空间信息变分自编码器，结合点过程似然学习图像中空间组织模式的可解释表示，能进行零样本条件模拟和空间定位分析。
source: ICLR-2026-Accepted
selection_source: conference_retrieval
motivation: 现有VAE难以捕捉对象间的空间相关性，关注像素强度。
method: 引入Papangelou条件强度点过程作为自监督目标，学习空间定位模式。
result: 学习统计可解释的空间定位表示，支持零样本条件模拟。
conclusion: 为图像空间模式的可解释学习提供了新框架。
---

## Abstract
We introduce spatially informed variational autoencoders (SI-VAE) as self-supervised deep-learning models that use stochastic point processes to predict spatial organization patterns from images.  Existing approaches to learning visual representations based on variational autoencoders (VAE) struggle to capture spatial correlations between objects or events, focusing instead on pixel intensities. We address this limitation by incorporating a point-process likelihood, derived from the Papangelou conditional intensity, as a self-supervision target. This results in a hybrid model that learns statistically interpretable representations of spatial localization patterns and enables zero-shot conditional simulation directly from images. Experiments with synthetic images show that SI-VAE improve the classification accuracy of attractive, repulsive, and uncorrelated point patterns from 48% (VAE) to over 80% in the worst case and 90% in the best case, while generalizing to unseen data. We apply SI-VAE to a real-world microscopy data set, demonstrating its use for studying the spatial organization of proteins in human cells and for using the representations in downstream statistical analysis.

---

## 论文详细总结（自动生成）

# 面向可解释视觉表示学习的空间信息自编码器（SI-VAE）论文总结

## 1. 论文的核心问题与整体含义

- **研究动机**  
  传统变分自编码器（VAE）在视觉表示学习中主要关注像素强度，难以捕捉图像中物体或事件之间的**空间相关性**（如吸引、排斥或随机分布模式）。这类空间组织模式在生物图像、遥感、人群分析等领域至关重要，但现有自监督方法缺乏对空间定位关系的显式建模与统计可解释性。

- **整体含义**  
  本文提出将**随机点过程**融入VAE，从图像中自监督地学习空间定位模式的**可解释统计表示**。该模型不仅能提升空间模式分类精度，还具备**零样本条件模拟**能力——即仅凭输入图像就能生成符合观测部分点的完整空间配置，为下游统计分析和空间推理提供了新范式。

## 2. 论文提出的方法论

- **核心思想**  
  将点过程的**Papangelou条件强度函数**作为自监督目标，与VAE的变分推理框架相结合，构建一个**混合生成模型**。编码器从图像提取空间结构的潜在变量，解码器输出点过程的强度函数，训练时最大化观测点配置的对数似然，从而使潜在表示天然携带空间互作信息。

- **关键技术细节**  
  - **模型结构**：编码器（如CNN）输入图像，输出潜在变量 $z$ 的分布参数；解码器则根据 $z$ 生成空间连续或离散的强度场 $\lambda(x;z)$，该强度场定义了点过程的条件强度。  
  - **损失函数**：在标准VAE的证据下界（ELBO）中，将重建损失替换为**点过程对数似然**项 $\sum_i \log \lambda(x_i;z) - \int \lambda(x;z)dx$，同时保留KL散度正则项。  
  - **可解释性**：通过学习，潜在变量 $z$ 可编码“吸引”、“排斥”或“随机”等空间模式，且这些模式具备统计上的可区分性。  
  - **零样本模拟**：给定部分观测点位置，可通过固定编码器输出并结合过程采样，生成符合全局空间结构的新点集，实现条件模拟。

- **算法流程（文字描述）**  
  1. 将输入图像送入编码器，得到近似后验 $q(z|x)$。  
  2. 从 $q(z|x)$ 中采样 $z$，解码器输出强度函数 $\lambda(\cdot;z)$。  
  3. 计算当前图像中所有点（可通过关键点检测或标注获得）在此强度场下的对数似然。  
  4. 联合ELBO优化编码器和解码器参数。  
  5. 推理时，既可对潜在空间进行分类或回归，也可通过修改部分点并重采样实现条件生成。

## 3. 实验设计

- **数据集与场景**  
  - **合成图像**：生成包含**吸引型、排斥型、无相关型**点模式的图像，用于分类任务与控制实验。  
  - **真实显微镜图像**：人类细胞中蛋白质空间组织数据，用于验证方法的实用性和下游统计分析能力。

- **评估指标与benchmark**  
  以点模式**三分类准确率**作为核心指标。基准线为标准VAE（仅重建像素强度），其分类准确率为48%；SI-VAE将其提升至**最差80%、最好90%以上**。

- **对比方法**  
  摘要仅明确提及与**标准VAE**对比，未提及其他基于空间建模的自编码器、图神经网络或显式空间点过程模型。

- **下潜任务**  
  除分类外，还展示了**零样本条件模拟**（根据部分观测点采样完整空间分布）及真实数据中的**空间组织统计分析**。

## 4. 资源与算力

- 提供的摘要和元数据中**未明确说明**所使用的GPU型号、数量、训练时长或总计算开销。无法对此进行评估。

## 5. 实验数量与充分性

- **实验组数推断**  
  至少包含：  
  - 合成数据上的多类点模式分类实验（可能包含不同参数下的吸引/排斥强度）；  
  - 真实显微镜数据的定性/定量分析；  
  - 零样本条件模拟的可视化验证。  
  但摘要未提及消融实验（如移除点过程似然仅保留VAE结构、不同强度函数形式的影响等），也未说明是否进行了统计显著性检验。

- **充分性与公平性评价**  
  - **优点**：合成数据设计能直观反映方法对空间模式的捕获能力，分类准确率提升显著。  
  - **不足**：对比方法**仅限标准VAE**，缺乏与现有空间感知模型（如空间点过程自编码器、Deep Point Process、空间Transformer等）的比较，难以全面体现优势。实验规模和多样性可能有限，从现有信息看，难以断定实验是否足够客观、公平。

## 6. 论文的主要结论与发现

- SI-VAE成功将点过程建模与VAE融合，能够从图像中以**自监督方式**提取空间定位的统计可解释表示。  
- 该表示能清晰区分吸引、排斥、随机模式，分类性能远超普通VAE。  
- 模型具备**零样本条件模拟**能力，可直接根据图像生成符合空间结构的点配置。  
- 在真实细胞图像上，方法可用于研究蛋白质空间组织，表明其具有实际生物应用价值，并为图像空间模式分析提供了新框架。

## 7. 优点

- **创新性强**：首次将Papangelou条件强度点过程用作VAE的自监督目标，桥接了点过程统计与深度表示学习。  
- **可解释性**：潜在空间直接对应统计可解释的空间互作类型（吸引/排斥），便于后续分析。  
- **多功能性**：兼具表示学习、空间分类与条件生成，应用潜力广泛。  
- **合成与真实验证**：既有受控合成实验证明概念，也有真实数据展示实用性。

## 8. 不足与局限

- **对比基线单一**：仅与标准VAE比较，缺乏与当前先进空间表示模型或点过程模型的横向对比。  
- **点提取依赖性**：需要从图像中预先提取或检测关键点位置，这可能引入前端误差，且不适用于无明确“点”定义的任务。  
- **点过程假设局限**：Papangelou条件强度假设可能对复杂、多尺度空间交互不够鲁棒，真实场景下模型表现未深入分析。  
- **计算开销未明**：点过程似然中的积分项可能需蒙特卡洛近似，训练代价可能较高，但论文未提供资源报告。  
- **实验充分性存疑**：未见消融研究、参数敏感性分析或多数据集迁移验证，结论的泛化性尚需更多证据支持。

（完）
