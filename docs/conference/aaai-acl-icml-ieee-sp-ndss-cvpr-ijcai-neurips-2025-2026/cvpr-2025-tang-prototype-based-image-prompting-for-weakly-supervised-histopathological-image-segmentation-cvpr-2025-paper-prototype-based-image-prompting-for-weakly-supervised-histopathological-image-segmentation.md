---
title: Prototype-Based Image Prompting for Weakly Supervised Histopathological Image Segmentation
title_zh: 基于原型的图像提示用于弱监督组织病理图像分割
authors: "Tang, Qingchen, Fan, Lei, Pagnucco, Maurice, Song, Yang"
date: 2025-06-01
pdf: "https://openaccess.thecvf.com/content/CVPR2025/papers/Tang_Prototype-Based_Image_Prompting_for_Weakly_Supervised_Histopathological_Image_Segmentation_CVPR_2025_paper.pdf"
tags: ["query:cell-graph"]
score: 4.0
evidence: 弱监督组织病理图像分割，基于原型提示
tldr: 本文针对组织病理图像像素级标注昂贵的问题，提出基于原型的图像提示框架用于弱监督分割。该方法通过聚类构建图像库，提取每类多个原型特征以捕捉类内异质性，并设计匹配损失来生成更完整的掩码。实验表明该方法优于传统CAM方法，有望降低组织病理分割的标注成本。
source: CVPR-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-tang-prototype-based-image-prompting-for-weakly-supervised-histopathological-image-segmentation-cvpr-2025-paper/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 844, \"height\": 413}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-tang-prototype-based-image-prompting-for-weakly-supervised-histopathological-image-segmentation-cvpr-2025-paper/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1785, \"height\": 743}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-tang-prototype-based-image-prompting-for-weakly-supervised-histopathological-image-segmentation-cvpr-2025-paper/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 865, \"height\": 359}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-tang-prototype-based-image-prompting-for-weakly-supervised-histopathological-image-segmentation-cvpr-2025-paper/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 849, \"height\": 445}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-tang-prototype-based-image-prompting-for-weakly-supervised-histopathological-image-segmentation-cvpr-2025-paper/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 873, \"height\": 543}]"
tables_json: "[{\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-tang-prototype-based-image-prompting-for-weakly-supervised-histopathological-image-segmentation-cvpr-2025-paper/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 867, \"height\": 211}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-tang-prototype-based-image-prompting-for-weakly-supervised-histopathological-image-segmentation-cvpr-2025-paper/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1804, \"height\": 976}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-tang-prototype-based-image-prompting-for-weakly-supervised-histopathological-image-segmentation-cvpr-2025-paper/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 867, \"height\": 621}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-tang-prototype-based-image-prompting-for-weakly-supervised-histopathological-image-segmentation-cvpr-2025-paper/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 870, \"height\": 204}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-tang-prototype-based-image-prompting-for-weakly-supervised-histopathological-image-segmentation-cvpr-2025-paper/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 865, \"height\": 180}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-tang-prototype-based-image-prompting-for-weakly-supervised-histopathological-image-segmentation-cvpr-2025-paper/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 866, \"height\": 277}]"
motivation: 组织病理图像像素级标注成本高，现有弱监督方法如CAM只突出最判别区域导致掩码不完整。
method: 提出基于原型的图像提示框架，通过聚类从训练集构建图像库，提取每类多个原型特征以捕获类内异质性，并设计匹配损失。
result: 摘要未完整给出，预计在组织病理分割上获得更完整的掩码。
conclusion: 该方法有望提升弱监督组织病理图像分割的精度，减少标注依赖，为组织表征提供基础。
---

## Abstract
Weakly supervised image segmentation with image-level labels has drawn attention due to the high cost of pixel-level annotations. Traditional methods using Class Activation Maps (CAMs) often highlight only the most discriminative regions, leading to incomplete masks. Recent approaches that introduce textual information struggle with histopathological images due to inter-class homogeneity and intra-class heterogeneity. In this paper, we propose a prototype-based image prompting framework for histopathological image segmentation. It constructs an image bank from the training set using clustering, extracting multiple prototype features per class to capture intra-class heterogeneity. By designing a matching loss between input features and class-specific prototypes using contrastive learning, our method addresses inter-class homogeneity and guides the model to generate more accurate CAMs. Experiments on four datasets (LUAD-HistoSeg, BCSS-WSSS, GCSS, and BCSS) show that our method outperforms existing weakly supervised segmentation approaches, setting new benchmarks in histopathological image segmentation.

---

## 论文详细总结（自动生成）

# 论文总结：基于原型的图像提示用于弱监督组织病理图像分割

## 1. 核心问题与整体含义

- **研究背景**：组织病理图像分割对计算机辅助诊断、肿瘤微环境定量、肿瘤分级与预后预测等十分关键。但像素级标注需要大量专业知识和时间，成本极高。
- **核心问题**：弱监督学习（仅使用图像级标签）可降低标注成本，但主流方法存在明显缺陷：
  - 基于 **CAM 的方法**通常只激活最具判别性的区域，导致伪掩码不完整。
  - 近期引入**文本提示**的弱监督方法在自然图像上有效，但在组织病理图像中受困于 **类间同质性（不同组织类型外观相似）** 和 **类内异质性（同一组织类型在染色、形状、纹理上差异大）**。
- **整体含义**：本文提出一种**基于原型的图像提示框架（Prototype-Based Image Prompting, PBIP）**，不再依赖文本描述，而是利用训练图像本身构建视觉原型，以更细粒度地指导弱监督分割，提升伪掩码质量，从而减少对像素级标注的依赖。

## 2. 方法论

### 2.1 总体框架

PBIP 由两个主网络组成：

- **ClassNet（分类网络）**：基于 SegFormer，输入病理图像和原型特征，生成初始伪分割掩码 \(M\)，并通过分类损失优化。
- **ImgMatchNet（图像特征匹配网络）**：利用训练集构建的图像库提取类别原型特征 \(P\)，并结合 ClassNet 生成的伪掩码进行前景/背景分离与相似性匹配，进一步优化伪掩码。

最终第一阶段生成的伪掩码被用作第二阶段全监督分割模型（DeepLab-v2）的训练标签。

### 2.2 图像库构建

- 从训练集中挑选**仅含单类组织**的图像 patch，并剔除白色区域过多的图像。
- 对每个类别使用 **K-Means 聚类**，划分为 \(K\) 个子类，以捕捉类内异质性。
- 每个子类选择距离聚类中心最近的 \(N_K\) 张图像作为原型图像。
- 聚类距离基于 CLIP 图像编码器提取特征的余弦距离：
  \[
  D_t(x_1,x_2)=1-\frac{\phi_e(x_1)\cdot \phi_e(x_2)}{\|\phi_e(x_1)\|\|\phi_e(x_2)\|}
  \]

### 2.3 ClassNet：初始伪掩码生成

- 使用 SegFormer 提取多尺度特征 \(F_i\)（\(i=1,2,3\)）。
- 将每个像素特征与对应类别的原型特征 \(P_i\) 计算余弦相似度，并**对每个类的 \(K\) 个原型取平均**，得到像素属于类别 \(n\) 的置信度：
  \[
  M_i(p,n)=\frac{1}{K}\sum_{k=1}^{K}\frac{F_i(p)\cdot P_i(n,k)}{\|F_i(p)\|\|P_i(n,k)\|}
  \]
- 这样可以利用多个原型覆盖类内差异，避免单个原型无法代表整个类别。

### 2.4 ImgMatchNet：原型特征与前景/背景匹配

- 使用 **MedCLIP 图像编码器**（在医学图像-文本对上预训练）对图像库中的原型图像编码，得到原型特征 \(P\in \mathbb{R}^{N\times K\times d}\)。
- 通过 MLP 将原型特征投影到与 ClassNet 各层级特征相同的维度，得到 \(P_i\in\mathbb{R}^{N\times K\times C_i}\)。
- **前景/背景分离模块**：
  - 将多尺度伪掩码上采样并求和：\(M'=\sum_{i=1}^3 \text{Up}(M_i)\)。
  - 使用自适应阈值 \(\tau=\delta\cdot \max(M)\) 二值化，得到前景与背景 mask。
  - 分离前景与背景图像：
    \[
    X_{FG}=b\cdot M\cdot X,\quad X_{BG}=(1-b)\cdot(1-M)\cdot X
    \]
- 再用 MedCLIP 编码器和 MLP 提取前景、背景特征，用于相似性损失。

### 2.5 优化目标

总损失：
\[
L_{total}=\alpha L_{CLS}+\beta L_{SIM}
\]

- **分类损失 \(L_{CLS}\)**：
  - 对每个层级伪掩码做全局平均池化得到图像级预测，使用二值交叉熵与图像级标签对比。

- **相似性损失 \(L_{SIM}\)**：
  - 分为前景相似性损失 \(L_{FGS}\) 和背景相似性损失 \(L_{BGS}\)。
  - \(L_{FGS}\)：鼓励前景特征与**同类原型**相似，同时远离**其他类别原型**（对比学习形式）。
  - \(L_{BGS}\)：鼓励背景特征与**对应背景原型**相似，远离前景原型。
  - 使用温度参数 \(\tau\)、权重 \(\theta_1,\theta_2\) 调节。

## 3. 实验设计

### 3.1 数据集

论文在四个组织病理数据集上验证：

- **BCSS-WSSS**：乳腺癌，4 类，弱监督版本，23,422 训练 patch，3,418 验证，4,986 测试。
- **LUAD-HistoSeg**：肺腺癌，4 类（肿瘤上皮、间质、坏死、淋巴细胞），16,678 训练，306 验证，307 测试。
- **GCSS**：胃癌，4 类，20,000 训练，2,500 验证，2,500 测试。
- **BCSS**：乳腺癌，4 类（肿瘤、间质、淋巴细胞浸润、坏死），30,000 训练，2,500 验证，2,500 测试。

其中 BCSS-WSSS 和 LUAD-HistoSeg 是专门的弱监督分割基准（训练仅图像级标签，验证/测试有像素级 mask）。

### 3.2 Baseline 方法

对比了多类方法：

- **弱监督方法**：HistoSegNet、TransWS、OEEN、MLPS、TPRO、CLIMS、QA-CLIMS、Proto2Seg。
- **全监督/半监督方法**：SSPCL、SAM-Path、SAM2-Path。
- 特别比较了**文本提示方法**：TPRO、CLIMS、QA-CLIMS，以及**原型方法** Proto2Seg。

### 3.3 评估指标

使用四种标准分割指标：mIoU、Frequency Weighted IoU（FwIoU）、Boundary IoU（bIoU）、Dice 系数。对部分结果进行了 t 检验（p 值 < 0.05）。

## 4. 资源与算力

- 论文明确说明：所有模型在**单张 4090 GPU** 上训练。
- 其他算力细节：batch size=10，第一阶段训练 10 个 epoch，使用 AdamW 优化器。
- **未提及**具体训练总时长、GPU 内存占用或推理时间。

## 5. 实验数量与充分性

### 5.1 实验数量

论文进行了大量实验，包括：

- **4 个数据集**上的主结果对比（Table 1）。
- **损失函数组合消融**（Table 2）：检验分类损失、前景相似性损失、背景相似性损失等组合。
- **超参数敏感性分析**（Figure 3）：分析 \(\beta/\alpha\) 和 \(\theta_2/\theta_1\) 比率。
- **图像库原型数量消融**（Figure 4）：比较随机选择与聚类选择、不同原型数量。
- **聚类簇数 \(K\) 消融**（Table 4）：在 4 个数据集上测试 \(K=1\ldots5\)。
- **图像编码器与 backbone 组合**（Table 3）：MedCLIP、CLIP、PLIP、DINOv2 与 SegFormer、ResNet18/38/50、TransUNet 的组合。
- **SIM 模块与自适应阈值模块消融**（Table 5）。
- **文本提示 vs 图像提示的零样本分类实验**（Table 6）。

### 5.2 充分性与客观性

- **充分性较高**：从模块、损失、超参数、编码器选择、数据集等多个维度进行了验证，且多数实验使用多次随机种子并报告标准差，具备一定统计可靠性。
- **公平性存在局限**：
  - CLIMS 和 QA-CLIMS 原本为自然图像设计，在组织病理上性能较差，作为对比基准可能不完全公平。
  - Proto2Seg 原本依赖人工反馈，作者用自动选择 patch 替代，可能**提高**了 Proto2Seg 的性能，但主结果中 PBIP 仍然胜出。
  - 部分方法（如 SSPCL、TransWS）直接使用原文报告结果，而非重新训练，存在一定不一致性。

## 6. 主要结论与发现

- PBIP 在四个数据集上均取得**当前弱监督分割的最佳结果**：
  - BCSS-WSSS：mIoU 69.54%
  - LUAD-HistoSeg：mIoU 76.44%
  - GCSS：mIoU 55.10%
  - BCSS：mIoU 55.28%
- 相比第二好的弱监督方法 Proto2Seg，mIoU 提升了 1.53%–1.87%。
- 统计检验显示在 BCSS-WSSS 和 LUAD-HistoSeg 上的提升显著（p<0.05）。
- 可视化结果表明 PBIP 能生成更完整的目标区域、抑制更多背景误激活。
- 零样本实验证明：在组织病理中，**图像提示显著优于文本提示**，文本提示难以描述复杂组织结构。

## 7. 优点

- **新颖性**：首次在组织病理弱监督分割中引入图像提示（原型）机制，区别于此前主流的文本提示路线。
- **针对性设计**：
  - 使用聚类生成多个原型，显式建模类内异质性。
  - 对比学习式匹配损失缓解类间同质性。
- **两阶段架构清晰**：ClassNet 生成伪掩码，ImgMatchNet 用原型和前景/背景分离进行细化。
- **系统实验**：多数据集、多指标、大量消融，包含统计显著性检验，论证较扎实。
- **可复现性**：作者提供代码仓库链接；关键超参数均明确列出。

## 8. 不足与局限

- **图像库构建依赖单类 patch**：
  - 训练时需选择仅含单类组织的 patch，这可能利用了比一般图像级标签更强的信息。
  - 如果数据集中缺乏单类 patch，或图像级标签为多标签，方法适用性可能受限。
- **

- **图像库构建依赖单类 patch**：
  - 训练时需选择仅含单类组织的 patch，这可能利用了比一般图像级标签更强的信息。
  - 如果数据集中缺乏单类 patch，或图像级标签为多标签，方法适用性可能受限。
- **对预训练编码器依赖较强**：PBIP 依赖 MedCLIP/CLIP 等大规模预训练图像编码器来构建原型和提取特征，编码器选择对性能影响较大（Table 3），且这些编码器可能未充分适应组织病理的染色多变与复杂纹理。
- **多阶段流程与调参复杂度较高**：整体流程包含图像库构建、ClassNet、ImgMatchNet 以及后端全监督分割模型，涉及多个超参数（如 \(\alpha,\beta,\theta_1,\theta_2,K,N_K,\delta\) 等），实际使用和调参成本较高。
- **前景/背景分离的鲁棒性**：自适应阈值 \(\delta\cdot\max(M)\) 依赖于最大置信度，若伪掩码中存在极端高响应或噪声，可能影响前景/背景划分；作者虽做了消融，但未深入分析失败案例。

总体来看，PBIP 通过视觉原型替代文本提示，在组织病理弱监督分割中取得了明显提升，但其对单类 patch 的依赖和预训练编码器的敏感性仍需进一步研究。未来工作可探索无单类 patch 约束的原型构建、端到端训练以及更鲁棒的匹配策略。

（完）
