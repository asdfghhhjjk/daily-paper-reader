---
title: Weakly Supervised Gland Segmentation with Class Semantic Consistency and Purified Labels Filtration
title_zh: 基于类别语义一致性与纯化标签过滤的弱监督腺体分割
authors: "Siyang Feng, Huadeng Wang, Chu Han, Zhenbing Liu, Hualong Zhang, Rushi Lan, Xipeng Pan"
date: 2025-04-11
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/32306/34461"
tags: ["query:cellseg"]
score: 9.0
evidence: 提出利用语义和类别一致性在组织病理学图像中进行弱监督腺体分割。
tldr: 图像级弱监督语义分割在计算病理中至关重要，但组织病理图像低对比度导致现有基于类激活图的方法在腺体分割上表现不佳。本文分析发现，类别一致性与语义一致性可引导网络区分混淆像素，生成精细伪掩膜。为此提出一致性相关方法及纯化标签过滤策略。实验表明，该方法显著提高了弱监督腺体分割的精度。
source: AAAI-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/aaai-2025-accepted/aaai-2025-32306/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 814, \"height\": 284, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2025-accepted/aaai-2025-32306/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1653, \"height\": 1450, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2025-accepted/aaai-2025-32306/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 834, \"height\": 509, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2025-accepted/aaai-2025-32306/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 860, \"height\": 496, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/aaai-2025-accepted/aaai-2025-32306/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1839, \"height\": 592, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2025-accepted/aaai-2025-32306/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 764, \"height\": 302, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2025-accepted/aaai-2025-32306/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 769, \"height\": 402, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2025-accepted/aaai-2025-32306/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 757, \"height\": 420, \"label\": \"Table\"}]"
motivation: 现有弱监督方法在腺体分割中因组织低对比度而效果差。
method: 提出类别一致性和语义一致性引导的弱监督分割框架，引入纯化标签过滤。
result: 方法生成的伪掩膜更精细，分割精度显著提升。
conclusion: 一致性建模是提升弱监督病理分割的关键技术。
---

## Abstract
Image-level weakly supervised semantic segmentation (WSSS) reduces the dependence on high-quality data annotation, which plays a crucial role in computational pathology. Benefit from the ability to localize the objects with only binary labels, Class Activation Map (CAM) is a widely used method to initial pseudo masks. However, due to the low contrast among different tissues in histopathological images, most existing CAM-based methods perform poorly in gland segmentation. We retrospect this process and find that class consistency and semantic consistency can guide the network to effectively distinguish confusing pixels and generate fine-grained pseudo masks. Specifically, for class consistency, we propose Consistency Correlation Attention (CCA) to encourage the network to focus on the contribution of class features to semantic dependencies. For semantic consistency, we propose Multi-scale Pyramid Fusion Pooling (MPFP) to aggregate coarse-to-fine global semantic information from CAMs at multiple spatial resolutions, thus identifying class localization. Additionally, we introduce a Purified Labels Filtration (PLF) strategy during the segmentation phase to mitigate the noisy supervision signal and improve the segmentation quality of the model. Extensive experiments show that the our method achieves new state-of-the-art results on three publicly available gland datasets. Furthermore, our method demonstrates impressive domain adaptation capability, achieving satisfactory results with only a small portion of samples when faced with unseen domain data.

---

## 论文详细总结（自动生成）

# 论文解析：《基于类别语义一致性与纯化标签过滤的弱监督腺体分割》

## 1. 核心问题与研究动机
- **弱监督语义分割 (WSSS) 的价值**：组织病理图像分析中，密集的像素级标注极为耗时、成本高昂。基于图像级标签的 WSSS 可将标注时间缩短约 60 倍，因此备受关注。
- **现有方法的局限**：主流 WSSS 方法多基于类激活图 (CAM)，但直接在自然图像上设计的 CAM 方法移植到腺体图像时效果不佳。
- **两大核心挑战**：
  - **类别混淆**：腺体图像不同组织间颜色对比度低、目标形状相似，导致边界难以区分，像素易被错误归类。
  - **语义混淆**：自然图像有明确语义先验（如“船在水上”），而腺体组织分布随机、不均匀，会出现“船在铁轨上”式的异常语义关联，干扰模型理解语义关系。
- **本文切入点**：认为保持**类别一致性**（同一类别像素特征应相似，不同类别应差异明显）与**语义一致性**（正确的全局语义对应）是解决混淆、生成精细化伪掩膜的关键。

## 2. 方法论

### 2.1 整体框架
- 图像级标注图像输入分类网络（嵌入 CCA）→ 生成初始 CAM → 经 MPFP 精细化 CAM 并得到伪掩膜 → 基于伪掩膜和 PLF 策略训练分割网络 → 测试时直接使用分割网络推理。
- 分类骨干为 ResNet38，分割网络为 PSPNet + ResNeSt200。

### 2.2 类别一致性：一致性相关注意力 CCA
- **目的**：强制模型关注同一类别像素的长距离依赖，增强类内特征聚合、类间特征分离。
- **结构**：
  - 输入特征图 \(X_{in}\) 先经过第一个 Criss-Cross Attention 获得含上下文信息的特征 \(X'\)。
  - 再通过三个卷积生成 \(H, M, N\)，计算位置注意力图 \(B\)，加权聚合到 \(X'\) 上，最后用第二个 Criss-Cross Attention 获取全局上下文，输出 \(X_{out}\)。
- **部署位置**：分类网络 Stage 4~6 的最后层均嵌入 CCA，以融合多分辨率特征。

### 2.3 语义一致性：多尺度金字塔融合池化 MPFP
- **动机**：传统 CAM 中用全局平均池化 (GAP) 导致空间信息均等贡献，容易仅激活最显著区域而忽略次相关区域，丢失完整语义。
- **关键设计**：
  - 对特征图 \(F\) 以不同池化尺度 \((\tau=2,4,8,16)\) 构建特征金字塔 \(P_{\tau}\)。
  - 设计**符号保持卷积 (S)**：同时强化正、负两个方向的激活特征，以保留类别存在与不存在的语义信息。
  - 从粗到细（由低尺度到高尺度）逐步融合金字塔特征，利用公式 (6)(7)(8) 得到 \(P'_{16}\)。
  - 最终预测由融合后的特征与原始 \(F\) 解耦计算得出（公式 9），再生成精细 CAM。
- **效果**：抑制非相关区域，增强目标完整区域，缓解语义混淆。

### 2.4 分割阶段去噪：纯化标签过滤 PLF
- **问题**：即使经过 CCA 和 MPFP，伪掩膜仍含噪声像素。
- **思路**：不完全丢弃噪声区域，而是通过可靠性评分挑选其中的干净标签信号。
- **方法**：
  - 对标准交叉熵损失 \(L_{ce}\) 乘上一个由置信度指标与损失值指标组成的权值图。
  - 置信度指标：对类别概率做 softmax，用最大 - 最小差值度量。
  - 损失值指标：对损失图沿空间维度做 softmax 并均值归一化，使干净样本获得更高权重。
- **应用条件**：仅对包含多类别的图像使用 PLF，单类图像不适用。

## 3. 实验设计

### 3.1 数据集
- **ProG (前列腺腺体)**：1500 张 H&E 染色 WSIs (150 患者)，切成 224×224 补丁。训练集 36k 张，验证集 8,244 张，测试集 9,756 张。
- **GlaS (结肠腺体分割挑战)**：165 张 H&E 图像，训练 70 张、验证 15 张、测试 80 张。滑动窗口切补丁（112×112，步长 56）。
- **EBHI (肠镜活检组织)**：从结直肠癌肠镜活检数据集中筛选含腺体的 1169 张 224×224 图像，按 7:1:2 划分。

### 3.2 评估指标
- mIoU 与 F1-score（常用 WSSS 与腺体分割指标）。
- 统计分析：独立样本 T 检验，p<0.05 视为显著。

### 3.3 对比方法
- **八种 SOTA 图像级 WSSS 方法**：SEAM, ReCAM, AMR, MLPS, OEEM, AME-CAM, HAMIL, CBFNet。
- **全监督基线**（PSPNet + ResNeSt200）仅做参考，不做弱监督对比。

## 4. 资源与算力
- 硬件：1 块 NVIDIA 4090 GPU。
- 框架：PyTorch 2.0.1。
- 训练细节：
  - 分类阶段：ResNet38 在 ImageNet 预训练，学习率 0.01，多项式衰减，训练 20 epochs。
  - 分割阶段：SGD 优化器，学习率 0.005，动量 0.9，权重衰减 0.0005，批次大小 20，训练 30 epochs。
- 其他数据增强：随机翻转、畸变、高斯模糊。

## 5. 实验数量与充分性
- **主要实验**：在 3 个公开数据集上与 8 种现有方法对比，各报告 mIoU 和 F1-score（表 1），并进行统计显著性检验。
- **消融实验**：
  - 各组件贡献 (Baseline + CCA / MPFP / PLF 逐步叠加) → 表 2 (ProG)。
  - CCA 结构消融 (不同注意力块配置) 和插入阶段研究 → 表 3。
  - MPFP 多尺度策略与融合方式消融 → 表 4。
- **模块兼容性实验**：将 CCA 和 MPFP 插入 OEEM、HAMIL 中验证性能提升。
- **领域适应实验**：ProG ↔ GlaS 小样本微调，对比 OEEM，考察 20%、10%、5%、1% 数据量下的稳定性。
- **总计**：约 7 组以上消融/对比/扩展实验，覆盖不同维度，设计公平、全面，结论可靠。

## 6. 主要结论与发现
- 三个数据集上均达到 SOTA：ProG 87.69% mIoU，GlaS 80.44%，EBHI 77.36%。
- 所提 CCA 有效保持类别一致性，MPFP 改善语义一致性并细化 CAM，PLF 进一步抑制噪声。
- 模型具有优异的领域适应能力，仅用 1% 目标域数据微调仍能保持稳定表现，临床潜力大。

## 7. 优点
- **问题定义清晰**：首次明确分析腺体分割中的“类别一致性”和“语义一致性”两大本质难点。
- **模块创新性强**：CCA 融合位置注意力与十字交叉注意力捕捉长程依赖；MPFP 采用符号保持卷积和金字塔融合保留正负语义，设计精巧。
- **全流程优化**：覆盖伪掩膜生成（分类阶段）和使用（分割阶段），PLF 策略按置信度与损失双重动态过滤，提升训练稳定性。
- **实验扎实**：多数据集、多方法对比，多组细粒度消融，模块兼容性验证及域适应实验，证据充分。
- **代码开源，可复现性强**。

## 8. 不足与局限
- **数据集类型有限**：仅涉及 H&E 染色的腺体影像，未在免疫组化等其他染色或非腺体病理图像上验证。
- **CAM 基础结构**：分类网络固定为 ResNet38，虽已验证与 OEEM 等兼容，但未探索其他分类骨架（如 Transformer）的影响。
- **全监督结果仍有差距**：ProG 上比全监督低约 1.9 个百分点，极限性能待突破。
- **噪声过滤假设**：PLF 依赖模型置信度与损失值可靠，若训练初期噪声过强，筛选效果可能受限，文中未详细讨论极端噪声情景。
- **计算复杂度未分析**：未给出 CCA/MPFP 带来的参数量、推理时间增加等定量分析。

（完）
