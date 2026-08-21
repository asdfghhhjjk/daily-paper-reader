---
title: Towards Effective and Efficient Context-aware Nucleus Detection in Histopathology Whole Slide Images
title_zh: 迈向有效且高效的组织病理学全切片图像上下文感知细胞核检测
authors: "Zhongyi Shui, Honglin Li, Yunlong Zhang, Yuxuan Sun, Yiwen Ye, Pingyi Chen, Ruizhe Guo, Lei Cui, Chenglu Zhu, Lin Yang"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/37860/41822"
tags: ["query:cell-graph"]
score: 8.0
evidence: 组织病理学WSI中的上下文感知细胞核检测
tldr: "针对组织病理学WSI中滑动窗口独立处理导致上下文缺失的问题，提出有效且高效的上下文感知细胞核检测方法。现有方案通过额外大视野补丁提取上下文特征但增加推理延迟；本文设计新机制，在不显著增加延迟的情况下利用上下文信息提升检测精度。该方法对H&E切片中的细胞核检测至关重要，为下游细胞级分析奠定基础。"
source: AAAI-2026-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-37860/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 875, \"height\": 537}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-37860/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 862, \"height\": 456}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-37860/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1826, \"height\": 463}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-37860/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 878, \"height\": 576}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-37860/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1819, \"height\": 850}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-37860/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 849, \"height\": 409}]"
tables_json: "[{\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-37860/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1822, \"height\": 538}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-37860/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1823, \"height\": 508}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-37860/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 871, \"height\": 252}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-37860/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 465, \"height\": 285}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-37860/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 424, \"height\": 287}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-37860/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 435, \"height\": 229}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-37860/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 343, \"height\": 211}]"
motivation: 现有细胞核检测按滑动窗口独立处理，忽略全局上下文且检测不准确。
method: 提出无需大幅增加推理延迟的上下文感知细胞核检测方法。
result: 在组织病理学WSI上实现更准确的细胞核检测且保持高效。
conclusion: "为H&E全切片图像的细胞核检测提供高效方案，支撑细胞级病理分析。"
---

## Abstract
Nucleus detection in histopathology whole slide images (WSIs) is crucial for a broad spectrum of clinical applications. The gigapixel size of WSIs necessitates the use of sliding window methodology for nucleus detection. However, mainstream methods process each sliding window independently, which overlooks broader contextual information and easily leads to inaccurate predictions. To address this limitation, recent studies additionally crop a large Filed-of-View (LFoV) patch centered on each sliding window to extract contextual features. However, such methods substantially increase whole-slide inference latency. In this work, we propose an effective and efficient context-aware nucleus detection approach. Specifically, instead of using lFoV patches, we aggregate contextual clues from off-the-shelf features of historically visited sliding windows, which greatly enhances the inference efficiency. Moreover, compared to lFoV patches used in previous works, the sliding window patches have higher magnification and provide finer-grained tissue details, thereby enhancing the classification accuracy. To develop the proposed context-aware model, we utilize annotated patches along with their surrounding unlabeled patches for training. Beyond exploiting high-level tissue context from these surrounding regions, we design a post-training strategy that leverages abundant unlabeled nucleus samples within them to enhance the model's context adaptability. Extensive experimental results on three challenging benchmarks demonstrate the superiority of our method.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义

- **研究背景**：组织病理学全切片图像（WSI）具有千兆像素级别尺寸，细胞核检测通常必须采用滑动窗口策略。
- **核心问题**：主流滑动窗口方法独立处理每个窗口，忽略窗口周围的更大范围组织上下文信息，容易导致细胞核分类错误。
- **已有方案与不足**：近期工作通过额外裁剪大视野（LFoV）补丁来提取上下文特征，但带来两点问题：
  - 需要额外准备 LFoV 补丁，显著增加整张 WSI 推理延迟；
  - LFoV 补丁来自低放大倍率，缺少细粒度组织细节，影响性能提升空间。
- **本文目标**：提出一种有效且高效的上下文感知细胞核检测方法，在不大幅增加推理开销的前提下，利用周围滑动窗口的高分辨率特征增强检测精度。

### 2. 论文提出的方法论

- **核心思想**：
  - 不再使用 LFoV 补丁，而是聚合历史上已经访问过的周围滑动窗口的特征，作为上下文线索；
  - ROI 补丁与周围补丁处于相同放大倍率，因此可以共享同一个图像编码器。
- **上下文特征提取**：
  - 对每个标注补丁 \(x_i\)，提取特征图 \(F_i \in \mathbb{R}^{h \times w \times d}\)；
  - 对其周围补丁 \(\{x_{i,j,k} \mid j,k \in \{-\delta,\dots,\delta\}\}\) 提取上下文特征图 \(F_{i,j,k}\)；
  - \(\delta\) 表示上下文邻域大小，例如 \(\delta=1\) 时对应 \(3 \times 3\) 邻域。
- **选择性梯度计算**：
  - 同时编码 \((2\delta+1)^2\) 个补丁会带来高显存压力；
  - 每个训练迭代随机选择 \(k\) 个周围补丁参与反向传播，其余补丁只做前向特征提取，降低显存占用。
- **空间冗余压缩**：
  - 对每个上下文特征图做 \(s \times s\) 网格平均池化，将空间分辨率从 \(h \times w\) 压缩到 \(s^2\)；
  - 拼接后得到上下文特征 \(F_i^{ctx} \in \mathbb{R}^{(2\delta+1)^2 \times s \times s \times d}\)。
- **上下文注入方式**：
  - 通过交叉注意力将上下文特征注入 ROI 特征：
    \[
    F_i' = \text{CrossAttn}(Q = F_i, K = F_i^{ctx}, V = F_i^{ctx})
    \]
  - 不加位置编码，因为病理切片具有空间连续性，相邻补丁边界内容连贯，隐式包含相对位置关系。
- **利用周围未标注细胞核增强上下文适应性**：
  - 先用预训练检测器检测周围补丁中的细胞核，并生成伪类别标签；
  - 提出 **交叉标注（cross-labeling）** 策略，避免自训练中的确认偏差：
    - 将点标注转换为伪掩码标签；
    - 训练一个轻量级多类细胞核分割辅助模型；
    - 用辅助模型对周围补丁生成伪标签，再用于训练分类头。
- **补偿核形态感知能力**：
  - 发现引入高层上下文特征会稀释模型对低层核形态细节的注意力；
  - 从辅助分割模型的最后一层输入特征图中提取形态丰富特征 \(m\)；
  - 将分类头输入从 \(e\) 替换为 \([e; m]\)，融合上下文特征与形态特征。

### 3. 实验设计

- **数据集**：
  - **BRCA**：乳腺癌数据集，120 个 \(20\times\) 放大倍率补丁，来自 113 名患者，训练/验证/测试为 80/10/30；细胞核分为肿瘤、炎症、间质三类。
  - **OCELOT**：来自 303 张 WSI 的 664 个 \(40\times\) 补丁，训练/验证/测试为 400/137/126；细胞核区分为肿瘤与非肿瘤（或背景）。
  - **PUMA**：黑色素瘤组织，206 个 \(40\times\) 补丁，按 6:2:2 随机划分训练/验证/测试；细胞核分为肿瘤、TILs、其他三类。
- **评价指标**：
  - 细胞核检测：F1 分数，BRCA 匹配距离 \(\sigma=6\) 像素，OCELOT 和 PUMA 为 \(\sigma=15\) 像素；
  - 实例分割：Panoptic Quality，PQ；
  - 所有实验重复 5 次，报告均值和 95% 置信区间。
- **对比方法**：
  - 包括 Hover-Net、MCSpatNet、P2PNet、Semi-P2PNet、AC-Former、SMILE、PointNu-N
