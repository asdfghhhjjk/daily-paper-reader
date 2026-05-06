---
title: "Semi supervised GAN for smart microscopy, fast and data efficient cell cycle classification"
title_zh: 用于智能显微镜的半监督 GAN：快速且数据高效的细胞周期分类
authors: "Manick, R., El Habouz, Y., Guillout, M., Martin, C., Bonnet, J., Ruel, L., Pastezeur, S., Chanteux, O., Bouchareb, O., Tramier, M., Pecreaux, J."
date: 2026-05-04
pdf: "https://www.biorxiv.org/content/10.64898/2026.04.23.720294v2.full.pdf"
tags: ["query:cellrep"]
score: 8.5
evidence: 用于细胞周期阶段分类的半监督生成对抗网络
tldr: 本文针对显微图像中细胞周期自动分类标注数据稀缺的问题，提出一种结合未标注数据和合成样本的半监督生成对抗网络方法，在少量标注样本情况下仍取得高精度表现，并可通过迁移学习适配不同细胞类型与显微镜模式，为智能显微系统的快速高效分析提供新方案。
source: biorxiv
selection_source: fresh_fetch
motivation: 为解决显微图像分析中标注样本不足及自动化系统智能性不高的问题。
method: 研究提出一种结合未标注显微图像与合成样本的半监督生成对抗网络框架。
result: "在Mitocheck五分类数据上仅用少量标注样本即可达93±2%的精度，表现稳定。"
conclusion: 该研究表明，半监督GAN框架能有效用于低标注样本条件下的细胞周期分类，并具备良好泛化与可扩展性。
---

## 摘要
现代光学显微镜已实现全电动化；然而，要将其真正转变为智能系统，还需要能够根据检测到的目标和动态生物事件实时调整采集参数。其核心在于分类算法，这类算法通常依赖定制化软件，并被设计用于定义范围狭窄的生物学应用。此外，它们通常需要大量带注释的数据集以实现有效训练。我们提出了一种半监督生成对抗网络（SGAN），用于在资源受限条件下实现鲁棒的细胞周期阶段分类，并可适应多种细胞结构。该框架通过结合无标注显微图像与合成生成样本来缓解标注不足的问题，同时在无标注样本类别不平衡的情况下仍保持稳定的性能。在包含五个有丝分裂类别的 Mitocheck 数据集上测试时，该模型在每类仅使用 80 张带标注图像和 600 张无标注图像的条件下达到了 93 ± 2% 的准确率。所提出的算法具有通用性，可通过迁移学习轻松适配新的标注方案、分类目标、细胞系或显微镜成像模式。SGAN 非常适合集成到自动化显微镜中，从而在多样化的生物学和显微成像应用中实现高效且可适应的图像分析。

## Abstract
Modern optical microscopes are fully motorised; however, transforming them into truly smart systems requires real-time adjustment of acquisition settings in response to detected objects and dynamic biological events. At the core are classification algorithms that commonly depend on customised softwares and are generally designed for narrowly-defined biological applications. In addition, they often require substantial annotated datasets for effective training. We introduce a semi-supervised generative adversarial network (SGAN) for robust cell-cycle stage classification under low-resource conditions, adaptable to diverse cellular structures. The framework combines unlabelled microscopy images with synthetically generated samples to mitigate limited annotation, while preserving stable performance even when the unlabelled subset is class-imbalanced. Tested on the Mitocheck dataset, which features five mitosis classes, the model achieved 93{+/-}2 % accuracy using only 80 labelled per class and 600 unlabelled images. The proposed algorithm is generic and can be readily adapted to new labelling schemes, classification targets, cell lines, or microscopy modalities through transfer learning. SGAN is well suited for integration into automated microscopes, enabling efficient and adaptable image analysis across diverse biological and microscopy applications.

---

## 论文详细总结（自动生成）

# 用于智能显微镜的半监督 GAN：快速且数据高效的细胞周期分类 — 深度总结

## 一、核心问题与研究背景
- **研究动机**：  
  智能显微镜需要能够自动识别并实时响应细胞状态变化（如细胞周期阶段），以实现“事件驱动”的自动成像。然而，传统的深度学习分类器往往：
  - 依赖大量手工标注数据；
  - 针对特定实验定制化，通用性差；
  - 在数据稀缺和类别不平衡条件下易退化。
- **研究目标**：  
  作者希望开发一种**在标注数据稀缺条件下仍能保持高精度的细胞周期图像分类模型**，并且可灵活适应不同显微镜平台与生物样本，为“智能显微系统”提供可泛化的分类核心。

---

## 二、提出的方法论

### 1. 核心思想
- 引入**半监督生成对抗网络 (Semi-Supervised GAN，SGAN)**，结合：
  - 少量标注样本（supervised learning）
  - 大量未标注显微图像（unsupervised learning）
  - 生成器合成的样本（synthetic data）
- 通过对抗训练，使判别器同时进行：
  - **有监督分类**（预测细胞周期阶段）
  - **无监督判别**（分辨真实与生成图像）

### 2. 网络结构
- **生成器 (G)**：  
  - 输入随机噪声向量 *z*（维度=500）；
  - 经过密集层 + 4 层转置卷积层；
  - 输出为 64×64 单通道图像，使用 *tanh* 函数约束范围 [-1,1]。
- **判别器/分类器 (D)**：  
  - 共享卷积特征提取主干（4层卷积）；
  - 输出包括两部分：
    - 有监督头：Softmax 分类 5 个细胞周期阶段；
    - 无监督头：使用自定义激活函数 \( D_{unsup}(x) = Z_x / (Z_x+1) \) 预测真假。
- **联合目标函数**：
  \[
  \nabla_{\theta_d} L_{total} = \nabla L_{sup} + \nabla L_{d,real} + \nabla L_{d,fake}
  \]
  三个损失（监督分类、无监督真样本与假样本判别）同时更新共享权重，实现多任务特征学习。

### 3. 训练机制
- 批大小：\( N_B = \min(100, \lfloor N_L / 2 \rfloor ) \)；
- 优化器：Adam（学习率 6×10⁻⁴, β=0.5）；
- 每轮迭代中依次输入（1）标注样本、（2）未标注样本、（3）生成样本；
- 加入旋转、平移、亮度缩放等实时数据增强；
- 训练时长 800–1500 epoch，带 early stopping；低样本条件下训练轮数更长。

---

## 三、实验设计

### 1. 数据集与任务
- **主数据集 – Mitocheck**  
  - 人 HeLa 细胞，绿色荧光染色（GFP），5 类：间期、前中期、中期、后期、凋亡；
  - 不同标注规模：每类 20、40、60、80 张；
  - 无标注图像：600 张（不平衡分布；进行聚类分析验证其多样性）。
- **迁移学习测试集**  
  包括 6 个不同来源、不同成像方式的数据集：
  - **CellCognition (8 类)**：HeLa 细胞，染色蛋白 H2B，α-tubulin；
  - **Homemade (7 类)**：自建数据，Hoechst 染色；
  - **Nagao 系列 3 个二分类集 (RHC, HHE, HHG)**：不同蛋白标记的 G2/非G2区分；
  - **Cilia (二分类)**：纤毛状态分类；
  - **DIC (三分类)**：微分干涉对比显微镜，非荧光图像。

### 2. 对比基线
- **传统或监督式方法**：
  - 低层卷积网络（自建浅层 CNN）
  - Siamese few-shot 网络
  - Scattering network（基于小波分解的非参数方式）
  - 预训练迁移：MobileNetV2 与 InceptionV3（ImageNet 权重）
- **其他半监督方法**：
  - **Triple-GAN (Li et al., 2017)**  
  - **SPARSE (Manni et al., 2026)**  
  与本文 SGAN 同条件对比。

### 3. 数据量与交叉验证
- 共 28 组配置（4 种标注 × 7 种无标注规模）；
- 对每组进行 5 折交叉验证；
- 另增迁移、再训练与类别不平衡分析实验。

---

## 四、资源与算力
- **硬件环境**：
  - CPU：Intel Xeon Gold 6326 双路（64 核，共 128 线程）；
  - 内存：256 GB；
- **训练耗时**：平均 17 分钟/配置；
- 未明确使用 GPU 训练，显示实验可在 CPU 上完成；
- 推理速度：单细胞图像（64×64）推理时间约 110 ms（≈8.9 cells/s），处理一个 2048×2048 视野需 28 s。

---

## 五、实验数量与充分性
- **数据规模**：主任务测试 28 组；迁移学习覆盖 6 套数据集；
- **评估维度**：
  - 不同标注数量；
  - 不同未标注数量；
  - 跨数据集迁移；
  - 超参变化与训练稳定性；
  - 与监督、半监督同行方法的对比；
- **结论**：实验数量丰富，设置合理且有交叉验证，能说明方法稳定性与泛化性，整体公正度高。

---

## 六、主要结论与发现
- SGAN 在 Mitocheck 五分类任务上，**仅使用每类 80 张标注样本 + 600 张无标注样本** 即可达到 **93 ± 2 % 准确率**；
- 性能随标注数据增加显著提升，未标注数据主要提供正则化作用；
- SGAN 较其他方法在低标注样本条件下优势突出；
- 对无标注类别不平衡表现鲁棒，轻度不均衡不影响精度；
- 在迁移学习场景：
  - **CellCognition（五类）** 迁移准确率 95.7 ± 1.3%；  
  - **Homemade 数据** 94.5 ± 0.5%；  
  - 二分类任务平均约 86–90%；
  - 仅 **DIC 模态** 出现较大性能下降（84%，需完整再训练）。
- 模型小巧，推理快，适合集成到嵌入式“智能显微镜”中实现实时分类。

---

## 七、方法与实验的优点
- **数据效率高**：仅需极少标注即可达高精度；
- **框架通用**：可适用于不同细胞系、标记方式、成像方式；
- **计算轻量**：CPU即可训练推理；
- **鲁棒性好**：对类别不平衡和数据噪声具适应性；
- **迁移学习强**：从 Mitocheck 迁移到多源数据仍有高准确率；
- **系统集成潜能**：可直接嵌入“Roboscope”等自动显微系统，实现实时细胞状态判定。

---

## 八、不足与局限
- **模态迁移能力有限**：  
  在非荧光 DIC 成像下需重新训练，说明在成像物理差异大时，特征泛化受限；
- **生成器质量未深入评估**：  
  未定量展示生成样本的真实性或其对特征边界形成的具体贡献；
- **规模限制**：  
  虽然实验内部充分，但数据集总体样本数仍处于小规模（数千张），尚未验证在百万级真实高通量场景下的稳定性；
- **缺少实时嵌入测试结果**：  
  虽推理速度快，但未实际植入显微镜控制流程的端到端测试；
- **算力受限**：  
  未测试 GPU 加速或更复杂网络，尚难评估可扩展上限。

---

**（完）**
