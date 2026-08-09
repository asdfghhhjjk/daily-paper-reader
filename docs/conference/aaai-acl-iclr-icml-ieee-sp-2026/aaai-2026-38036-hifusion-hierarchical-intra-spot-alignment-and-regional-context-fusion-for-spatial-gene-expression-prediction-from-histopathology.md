---
title: "HiFusion: Hierarchical Intra-Spot Alignment and Regional Context Fusion for Spatial Gene Expression Prediction from Histopathology"
title_zh: HiFusion：面向组织病理学空间基因表达预测的分层斑点内对齐与区域上下文融合
authors: "Ziqiao Weng, Yaoyu Fang, Jiahe Qian, Xinkun Wang, Lee A D Cooper, Weidong Cai, Bo Zhou"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/38036/41998"
tags: ["query:path-xai-sel"]
score: 4.0
evidence: "使用H&E全切片图像进行基因表达预测的计算病理学方法"
tldr: "针对从H&E全切片图像预测基因表达中难以捕获斑点内异质性和易受噪声干扰的问题，本文提出HiFusion框架，通过分层斑点内建模提取细粒度形态表示，并融合区域上下文以抑制形态噪声，从而提升预测精度。实验表明该方法能有效整合多尺度空间信息，为低成本空间转录组学提供新途径。"
source: AAAI-2026-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38036/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1836, \"height\": 871}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38036/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 876, \"height\": 892}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38036/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1796, \"height\": 816}]"
tables_json: "[{\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38036/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1830, \"height\": 491}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38036/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 791, \"height\": 351}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38036/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 810, \"height\": 209}]"
motivation: 现有方法忽略斑点内异质性且易受形态噪声影响。
method: 提出分层斑点内建模模块与区域上下文融合机制。
result: 方法有效整合多尺度空间信息，提升基因表达预测精度。
conclusion: HiFusion为低成本空间转录组学提供了新路径。
---

## Abstract
Spatial transcriptomics (ST) bridges gene expression and tissue morphology but faces clinical adoption barriers due to technical complexity and prohibitive costs. While computational methods predict gene expression from H&E-stained whole-slide images (WSIs), existing approaches often fail to capture the intricate biological heterogeneity within spots and are susceptible to morphological noise when integrating contextual information from surrounding tissue. To overcome these limitations, we propose HiFusion, a novel deep learning framework that integrates two complementary components. First, we introduce the Hierarchical Intra-Spot Modeling module that extracts fine-grained morphological representations through multi-resolution sub-patch decomposition, guided by a feature alignment loss to ensure semantic consistency across scales. Concurrently, we present the Context-aware Cross-scale Fusion module, which employs cross-attention to selectively incorporate biologically relevant regional context, thereby enhancing representational capacity. This architecture enables comprehensive modeling of both cellular-level features and tissue microenvironmental cues, which are essential for accurate gene expression prediction. Extensive experiments on two benchmark ST datasets demonstrate that HiFusion achieves state-of-the-art performance across both 2D slide-wise cross-validation and more challenging 3D sample-specific scenarios. These results underscore HiFusion’s potential as a robust, accurate, and scalable solution for ST inference from routine histopathology.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义
- **研究背景**：空间转录组学（ST）能同时获取基因表达与组织空间位置，但受实验成本高、技术复杂等限制难以大规模临床推广。基于H&E染色全切片图像（WSI）计算预测基因表达成为低成本替代方案。
- **现有方法不足**：
  - 多数方法将每个测序斑点视为均质整体，忽略其内部细胞类型、核纹理等微结构异质性，未能捕捉多尺度形态线索。
  - 简单引入周围组织上下文作为辅助输入，缺少语义相关性建模，易引入无关形态噪声。
- **核心目标**：提出HiFusion框架，通过分层斑内建模和上下文感知跨尺度融合，同时捕获斑点内细粒度形态异质性和组织微环境语义信息，提升从组织病理图像预测空间基因表达的精度与鲁棒性。

### 2. 方法论
- **整体框架**：HiFusion包含两个互补模块——分层斑内建模（HISM）和上下文感知跨尺度融合（CCF）。
- **分层斑内建模 (HISM)**：
  - 将每个斑点图像（224×224）按非重叠方式分解为不同分辨率的子斑块：Level-0（全图，1×1），Level-1（2×2网格），Level-2（7×7网格），以提取从组织级到细胞级的特征。
  - 所有级别图像共享ResNet-18编码器，生成多尺度特征图 \( F_S^0, \tilde{F}_S^1, \tilde{F}_S^2 \)。
  - 引入特征对齐损失 \( L_{\text{align}} = \sum_{s=1}^2 \|\tilde{F}_S^s - F_S^0\|_1 \)，强制细尺度特征与全图语义对齐，保持跨尺度一致性。
- **上下文感知跨尺度融合 (CCF)**：
  - 为每个斑点提取周围448×448区域作为邻域图像，经轻量编码器ResNet-10和全局平均池化得到区域查询向量 \( Q_N^i \)。
  - 多尺度斑内特征通过可学习加权融合（权重由softmax作用于可学习参数 \( \alpha_s \)）得到融合特征，并通过自适应平均池化至2×2 token，重塑为交叉注意力的键和值矩阵 \( K_S^i, V_S^i \)。
  - 采用残差多头交叉注意力：区域查询 \( Q_N^i \) 查询融合后的斑内特征，输出经层归一化和全连接层预测基因表达向量 \( \hat{y}_i \)。残差连接 \( Q_N^i + \phi_{\text{ca}}(Q_N^i, K_S^i, V_S^i) \) 稳定训练。
- **损失函数**：
  - 主回归损失 \( L_{\text{main}} = \frac{1}{n}\sum_i \|\hat{y}_i - y_i\|_2^2 \)。
  - 多尺度辅助预测损失 \( L_{\text{aux}} = \frac{1}{3n}\sum_i\sum_{s=0}^2 \|\hat{y}_i^{(s)} - y_i\|_2^2 \)，其中 \( \hat{y}_i^{(s)} \) 由各尺度特征经共享FC层预测。
  - 总损失：\( L_{\text{total}} = L_{\text{main}} + L_{\text{aux}} + \lambda L_{\text{align}} \)，\( \lambda = 1 \)。
- **训练细节**：Adam优化器（动量0.9，权重衰减1e-5），初始学习率3e-4，余弦退火调度至1e-6，训练50 epoch，batch size 32。

### 3. 实验设计
- **数据集与预处理**：
  - **HER2**：36张HER2阳性乳腺癌WSI，含4例6层切片+4例3层切片，共13,620个斑点。
  - **ST-Data**：乳腺癌数据集，选取16例3层切片，共41,544个斑点。
  - 斑点直径100μm，中心间距200μm。预测基因为平均表达最高的前250个。表达值经斑内总计数归一化后取对数。
- **评估场景**：
  - **2D Slide-wise 交叉验证**：4折交叉验证，按患者分折，避免泄漏。
  - **3D Sample-specific 验证**：每例患者用首层切片训练，其余层测试，评估样本内泛化。
- **对比方法**：ST-Net（局部DenseNet）、HisToGene（ViT+长距离依赖）、Hist2ST（ConvMixer+GNN）、EGN（示例引导的检索对比学习）、TRIPLEX（三分支多分辨率）、ASIGN-2D/3D（图网络对齐相邻切片）。
- **评价指标**：均方误差（MSE）、平均绝对误差（MAE）、皮尔逊相关系数（PCC）。报告平均性能，并注明显著性检验（p<0.05）。

### 4. 资源与算力
- 所有实验在单块NVIDIA RTX 4090 GPU上完成。
- 训练设置为50个epoch，batch size 32。论文未提供具体单次训练时长，但基于数据规模和模型复杂度，在消费级GPU上训练时间应在数小时内，资源需求较为轻量。

### 5. 实验数量与充分性
- **主要对比实验**：在HER2和ST-Data两个数据集上，分别进行2D slide-wise和3D sample-specific两种评估，与7个baseline对比（含SOTA方法ASIGN），表格展示完整指标。
- **消融实验**：
  - 图像分解级别组合（7种，从仅1×1到多级叠加），验证多尺度建模效果。
  - 特征对齐损失的影响（有/无对比）。
  - CCF模块中spot token数量（2×2至7×7）和邻域图像尺寸（224×N，N=1~5）的影响。
  - 癌症标志基因（ERBB2、KRT19、CD74）空间表达可视化与定量比较，展示与ground truth的空间分布一致性。
- **充分性评价**：实验覆盖主流数据集与最新评估范式，对比方法多样，消融实验较系统，能支撑核心主张。对比时基线复现与原文献一致，训练条件相同，较公平客观。但缺少统计显著性多次重复实验的细节（如多次运行的标准差），泛化性测试限于两种乳腺癌数据集，未在其他组织类型验证。

### 6. 主要结论与发现
- HiFusion在HER2和ST-Data上均取得最优MSE、MAE和PCC，显著优于现有方法（如TRIPLEX、ASIGN）。
- 3D样本特异性验证中，HiFusion性能稳健，且表明样本内单层训练即可实现较好的跨层预测，避免复杂3D配准。
- 分层斑内分解（尤其1×1+2×2+7×7组合）和特征对齐能有效捕捉细胞级到组织级异质性。
- 适度的邻域上下文（2倍斑点尺寸）和较少token数量（2×2）可抑制噪声，提升交叉注意力融合效果。
- 癌症标志基因的可视化证实HiFusion能准确定位高表达区域，具有临床可解释性潜力。

### 7. 优点
- **双模块设计新颖**：显式建模斑内多尺度形态并利用区域上下文交叉注意力，兼具细粒度与上下文感知能力。
- **训练策略合理**：特征对齐损失与多尺度辅助监督增强跨尺度语义一致性，提升鲁棒性。
- **评估体系全面**：同时采用2D跨患者和3D样本内两种范式，更贴近真实临床场景。
- **轻量高效**：单张消费级GPU即可训练，推理成本低，利于推广。
- **消融深入**：分析了分解级别、token数量、邻域大小等关键设计，提供实践指导。

### 8. 不足与局限
- **实验数据集局限**：仅使用两种乳腺癌数据集，未在其他组织类型或癌症（如脑、肺、结肠）上验证，泛化性待考证。
- **基因数目受限**：仅预测前250个高表达基因，未覆盖低表达但具生物学意义的标志物，可能遗漏重要信号。
- **邻域融合机制较简单**：采用单分支区域编码和交叉注意力，可能未能充分挖掘复杂组织微环境的多级上下文，未来可探索更高效的上下文提取。
- **评估指标一般**：未报告基因相关性分布等更深入分析，缺乏与外部正交数据（如免疫组化）的对比验证。
- **训练细节透明度**：未说明训练时长、多次实验的稳定性（仅报告p<0.05，未给标准差），复现的可靠性略有不足。
- **可能偏差**：数据预处理（如归一化方式、基因筛选阈值）可能影响结果，不同预处理下的鲁棒性未讨论。

（完）
