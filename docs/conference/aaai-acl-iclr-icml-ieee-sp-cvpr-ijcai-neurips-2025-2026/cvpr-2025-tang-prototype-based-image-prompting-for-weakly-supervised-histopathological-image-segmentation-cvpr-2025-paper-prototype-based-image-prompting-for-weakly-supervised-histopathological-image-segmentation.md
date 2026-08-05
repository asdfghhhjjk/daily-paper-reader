---
title: Prototype-Based Image Prompting for Weakly Supervised Histopathological Image Segmentation
title_zh: 基于原型的图像提示用于弱监督组织病理图像分割
authors: "Tang, Qingchen, Fan, Lei, Pagnucco, Maurice, Song, Yang"
date: 2025-06-01
pdf: "https://openaccess.thecvf.com/content/CVPR2025/papers/Tang_Prototype-Based_Image_Prompting_for_Weakly_Supervised_Histopathological_Image_Segmentation_CVPR_2025_paper.pdf"
tags: ["query:cellseg"]
score: 6.0
evidence: 基于原型提示的弱监督组织病理图像分割
tldr: 针对组织病理图像弱监督分割中CAM不完整问题，提出基于原型的图像提示框架，利用聚类构造图像库提取多原型特征，增强分割精度。
source: CVPR-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-tang-prototype-based-image-prompting-for-weakly-supervised-histopathological-image-segmentation-cvpr-2025-paper/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 844, \"height\": 413, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-tang-prototype-based-image-prompting-for-weakly-supervised-histopathological-image-segmentation-cvpr-2025-paper/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1785, \"height\": 743, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-tang-prototype-based-image-prompting-for-weakly-supervised-histopathological-image-segmentation-cvpr-2025-paper/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 865, \"height\": 359, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-tang-prototype-based-image-prompting-for-weakly-supervised-histopathological-image-segmentation-cvpr-2025-paper/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 849, \"height\": 445, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-tang-prototype-based-image-prompting-for-weakly-supervised-histopathological-image-segmentation-cvpr-2025-paper/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 873, \"height\": 543, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-tang-prototype-based-image-prompting-for-weakly-supervised-histopathological-image-segmentation-cvpr-2025-paper/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 867, \"height\": 211, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-tang-prototype-based-image-prompting-for-weakly-supervised-histopathological-image-segmentation-cvpr-2025-paper/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1804, \"height\": 976, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-tang-prototype-based-image-prompting-for-weakly-supervised-histopathological-image-segmentation-cvpr-2025-paper/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 867, \"height\": 621, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-tang-prototype-based-image-prompting-for-weakly-supervised-histopathological-image-segmentation-cvpr-2025-paper/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 870, \"height\": 204, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-tang-prototype-based-image-prompting-for-weakly-supervised-histopathological-image-segmentation-cvpr-2025-paper/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 865, \"height\": 180, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-tang-prototype-based-image-prompting-for-weakly-supervised-histopathological-image-segmentation-cvpr-2025-paper/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 866, \"height\": 277, \"label\": \"Table\"}]"
motivation: 弱监督分割中CAM只关注最判别区域，导致掩膜不完整。
method: 构建原型图像提示框架，通过聚类捕捉类内异质性。
result: 实验证明该方法优于现有弱监督分割方法。
conclusion: 为组织病理图像分割提供有效弱监督方案。
---

## Abstract
Weakly supervised image segmentation with image-level labels has drawn attention due to the high cost of pixel-level annotations. Traditional methods using Class Activation Maps (CAMs) often highlight only the most discriminative regions, leading to incomplete masks. Recent approaches that introduce textual information struggle with histopathological images due to inter-class homogeneity and intra-class heterogeneity. In this paper, we propose a prototype-based image prompting framework for histopathological image segmentation. It constructs an image bank from the training set using clustering, extracting multiple prototype features per class to capture intra-class heterogeneity. By designing a matching loss between input features and class-specific prototypes using contrastive learning, our method addresses inter-class homogeneity and guides the model to generate more accurate CAMs. Experiments on four datasets (LUAD-HistoSeg, BCSS-WSSS, GCSS, and BCSS) show that our method outperforms existing weakly supervised segmentation approaches, setting new benchmarks in histopathological image segmentation.

---

## 论文详细总结（自动生成）

## 1. 论文的核心问题与整体含义

- **问题背景**：组织病理图像分割在计算机辅助诊断中意义重大，但像素级标注成本极高，需要大量专家和时间。
- **弱监督分割的挑战**：使用图像级标签的弱监督分割（WSS）通常借助类激活图（CAM）生成伪标签，但CAM往往仅激活最判别区域，导致掩膜不完整。
- **文本提示方法的局限**：近期引入文本信息（如通过CLIP）的方法在自然图像上表现良好，但在组织病理图像中面临两大难题：
  - **类间同质性**：不同组织类别在染色、纹理上可能非常相似，导致误激活。
  - **类内异质性**：同一组织类别内部差异极大（染色、形状等），使文本描述难以精准对齐。
- **核心动机**：提出一种**基于原型的图像提示框架**，用图像本身而非文本作为提示，更好地捕捉细微视觉差异，从而生成更准确的CAM，最终提升弱监督组织病理分割的性能。

## 2. 方法论：PBIP 框架

### 2.1 整体架构
- **两阶段框架**：
  1. **第一阶段**：分类网络（ClassNet）与图像特征匹配网络（ImgMatchNet）联合生成高质量CAM作为伪标签。
  2. **第二阶段**：用生成的伪标签训练全监督分割模型（DeepLab-v2）得到最终分割结果。
- **核心组件**：ClassNet、ImgMatchNet 及外部图像库。

### 2.2 图像库构建
- **数据筛选**：仅使用图像级标签为单一类别的图像，并自动排除含大量白色区域的图像。
- **聚类生成原型**：
  - 对每个类别，用K-Means聚类将图像分为K个子类。
  - 距离度量基于CLIP图像编码器提取的特征，采用余弦距离。
  - 每个子类选取离聚类中心最近的NK张图像作为原型候选。
- **原型特征提取**：使用预训练MedCLIP图像编码器提取所有图像库特征，计算每个子类的平均特征向量作为该子类的原型特征 \( P \in \mathbb{R}^{N \times K \times d} \)。

### 2.3 分类网络（ClassNet）
- **主干网络**：SegFormer（Mix Transformer），预训练于ImageNet-1K，提取多尺度特征图 \( F_i \)。
- **初始伪掩膜生成**：
  - 对每一像素，计算其特征向量与各类别所有子类原型特征的**余弦相似度**，并在K个子类上取平均，获得类别置信度 \( M_i \)。
  - 特征维度不匹配时，用MLP将原型特征投影到与特征图\( F_i \)相同的通道数。

### 2.4 图像特征匹配网络（ImgMatchNet）
- **多尺度伪掩膜聚合**：将各层\( M_i \)上采样至原图分辨率并求和，得到综合伪掩膜 \( M' \)。
- **自适应阈值分割**：
  - 阈值 \( \tau = \delta \cdot \max(M') \)，\( \delta \)为可调参数。
  - 生成二值掩膜 \( b \)，分离出前景区域 \( X_{FG} \) 和背景区域 \( X_{BG} \)。
- **前景/背景特征提取**：用MedCLIP编码器和MLP从前/背景区域中提取特征 \( F_{FG}^i, F_{BG}^i \)。
- **相似度匹配损失（\( L_{SIM} \)）**：
  - **前景相似度损失（\( L_{FGS} \)）**：鼓励前景特征与对应类别的前景原型相似，同时与背景原型拉开距离（使用软对比损失）。
  - **背景相似度损失（\( L_{BGS} \)）**：鼓励背景特征与背景原型相似，与前景原型拉开距离。
  - 采用温度和求和/均值计算相似度分数，总相似度损失为两者加权和。

### 2.5 联合优化
- **总体损失**：\( L_{total} = \alpha L_{CLS} + \beta L_{SIM} \)，其中\( L_{CLS} \)为多尺度全局平均池化后的二元交叉熵分类损失。

## 3. 实验设计

### 3.1 数据集
- **BCSS-WSSS**（乳腺癌，4类）：训练集23422张，验证集3418张，测试集4986张，仅训练集使用图像级标签。
- **LUAD-HistoSeg**（肺腺癌，4类）：训练集16678张，验证集306张，测试集307张。
- **GCSS**（胃癌，4类）：训练集20000张，验证集2500张，测试集2500张。
- **BCSS**（乳腺癌，4类）：全监督基准，30000张训练，各2500张验证/测试。

### 3.2 对比方法
- **弱监督方法**：HistoSegNet、TransWS、OEEN、MLPS、TPRO、CLIMS、QA-CLIMS、Proto2Seg。
- **全/半监督方法**：SSPCL、SAM-Path、SAM2-Path（仅作为参考上限）。
- 所有可复现的方法均用5次随机种子重训练以确保稳健性，报告平均指标和标准差，并进行t检验。

### 3.3 评估指标
- mIoU、FwIoU、bIoU、Dice系数。

## 4. 资源与算力
- **硬件**：单张NVIDIA RTX 4090 GPU。
- **训练设置**：第一阶段训练10个epoch，batch size 10；第二阶段DeepLab-v2训练细节文中未详细说明，但通常为标准设置。

## 5. 实验数量与充分性
- **主实验对比**：在4个数据集上与超过10种方法比较，提供了详细的统计检验（p值<0.05），十分充分。
- **消融实验**：
  - 损失函数组合对mIoU的影响。
  - 损失系数比例 \( \beta/\alpha \) 和 \( \theta_2/\theta_1 \) 的影响。
  - 相似度计算模块（SIM）与自适应阈值模块（AT）的作用。
  - 图像库中原型图像数量的影响（随机选取 vs 聚类选取）。
  - 聚类数K的影响（K=1-5）。
  - 图像编码器（CLIP、MedCLIP、PLIP、DINOv2）和主干网络（SegFormer、ResNet变体、TransUNet）的组合。
  - 零样本分类实验：比较文本提示与图像提示的有效性。
- **充分性评价**：实验设计系统、覆盖面广，对关键模块和超参数均进行了消融，且使用了统计显著性检验，保证了对比的客观与公平。

## 6. 主要结论与发现
- PBIP在所有四个数据集上均取得最佳弱监督分割性能，在BCSS-WSSS上mIoU超出第二好的Proto2Seg 1.68%，p值均小于0.05。
- 聚类选取的原型比仅增加图像数量更能捕获类内异质性，提升伪掩膜质量。
- 图像提示显著优于文本提示（零样本分类F1分数上，图像提示大幅领先），说明组织病理图像中文本难以准确描述复杂模式。
- 相似度损失（同时使用前景和背景项）和自适应阈值模块对性能提升至关重要。

## 7. 优点
- **首个在组织病理WSS中引入图像提示的工作**，切实解决了类间同质性和类内异质性问题。
- **无额外人工标注**，完全自动化构建图像库和原型。
- **方法设计完整**：从图像库构建、原型特征聚合、动态阈值分离到对比学习损失，形成闭环，可有效提升CAM质量。
- **实验扎实**：涵盖多个数据集、多种backbone和预训练编码器的组合，统计检验充分。

## 8. 不足与局限
- **对预训练模型的依赖**：原型特征提取和相似度计算依赖于MedCLIP/CLIP等预训练模型，若预训练分布与目标病理图像差异过大可能影响效果；文中显示DINOv2等视觉编码器效果较差，可能限制通用性。
- **图像库构建的限制**：仅使用标签为单类的图像，排除了多标签或混合组织区域，可能遗漏复杂的上下文信息。
- **超参数敏感性**：聚类数K和阈值参数δ需要针对不同数据集调优（最优K值随数据集变化），增加了落地成本。
- **计算与存储开销**：需要维护图像库并提取特征，尽管文中未详细分析推理开销，但对于大规模数据或实时应用可能存在负担。
- **仅验证HE染色图像**：所有数据集均为H&E染色，未验证其他染色类型或更复杂的多重免疫荧光场景。
- **缺乏失败案例分析**：未展示在极具挑战性案例（如严重类间模糊区域）上的表现，难以评估鲁棒性边界。

（完）
