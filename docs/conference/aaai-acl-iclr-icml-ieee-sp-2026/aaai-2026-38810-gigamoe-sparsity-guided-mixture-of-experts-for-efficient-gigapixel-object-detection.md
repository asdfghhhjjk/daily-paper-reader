---
title: "GigaMoE: Sparsity-Guided Mixture of Experts for Efficient Gigapixel Object Detection"
title_zh: GigaMoE：稀疏性引导混合专家的高效十亿像素对象检测
authors: "Xiang Li, Wenxi Li, Yuetong Wang, Chenyang Lyu, Haozhe Lin, Guiguang Ding, Yuchen Guo"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/38810/42772"
tags: ["query:path-xai-sel"]
score: 8.0
evidence: 稀疏性引导的混合专家架构在十亿像素图像中选择重要区域，可类比全切片图像的区域选择
tldr: 针对十亿像素对象检测中区域复杂度差异被忽略的问题，提出稀疏引导的混合专家架构GigaMoE，自适应地为重要区域分配差异化计算，兼顾检测精度与效率。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38810/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 874, \"height\": 351, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38810/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1829, \"height\": 732, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38810/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1831, \"height\": 518, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38810/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 861, \"height\": 696, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38810/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 873, \"height\": 400, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38810/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1844, \"height\": 778, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38810/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 873, \"height\": 214, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38810/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 769, \"height\": 218, \"label\": \"Table\"}]"
motivation: 现有稀疏方法对所有选中区域使用统一计算模型，未考虑区域复杂度差异。
method: 用混合专家模块替换标准前馈网络，由共享和专家网络自适应处理不同区域。
result: 在多个十亿像素检测基准上达到最优性能与效率平衡。
conclusion: GigaMoE为十亿像素图像中的高效精确检测提供了新范式，可推广至病理全切片图像分析。
---

## Abstract
Object detection in High-Resolution Wide (HRW) shots, or gigapixel images, presents unique challenges due to extreme object sparsity and vast scale variations. State-of-the-art methods like SparseFormer have pioneered sparse processing by selectively focusing on important regions, yet they apply a uniform computational model to all selected regions, overlooking their intrinsic complexity differences. This leads to a suboptimal trade-off between performance and efficiency. In this paper, we introduce GigaMoE, a novel backbone architecture that pioneers adaptive computation for this domain by replacing the standard Feed-Forward Networks (FFNs) with a Mixture-of-Experts (MoE) module. Our architecture first employs a shared expert to provide a robust feature baseline for all selected regions. Upon this foundation, our core innovation---a novel Sparsity-Guided Routing mechanism---insightfully repurposes importance scores from the sparse backbone to provide a "computational bonus,'' dynamically engaging a variable number of specialized experts based on content complexity. The entire system is trained efficiently via a loss-free load-balancing technique, eliminating the need for cumbersome auxiliary losses. Extensive experiments show that GigaMoE sets a new state-of-the-art on the PANDA benchmark, improving detection accuracy by 1.1% over SparseFormer while simultaneously reducing the computational cost (FLOPs) by a remarkable 32.3%.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义
- **核心问题**：高分辨率宽幅（HRW）或十亿像素图像的目标检测面临物体极度稀疏和尺度剧烈变化的挑战。现有稀疏处理方法（如 SparseFormer）虽然通过选择重要区域节省计算，但对所有选中区域施加相同的计算负载（统一的 FFN），忽略了区域间的**内容复杂度差异**，导致性能与效率的权衡不佳。
- **整体含义**：本文提出在计算维度上进一步引入“稀疏性”，**根据区域复杂度动态分配计算资源**。用混合专家（MoE）模块替代传统 FFN，实现自适应计算，从而在提升检测精度的同时显著减少冗余计算。

### 2. 方法论
- **整体架构**
  - 基于 Swin Transformer 的层次化骨干网络（4 个阶段），每阶段包含全局注意力块和局部块。
  - 全局块：对窗口特征进行聚合、全局自注意力，再用轻量级 **ScoreNet** 获取各窗口的重要性分数。
  - 窗口稀疏化：根据分数进行 Top‑K 选择，仅将高分之窗送入局部块。
- **GigaMoE 局部块（核心贡献）**
  - 用 **MoE 模块** 替换标准 FFN，包含 1 个共享专家和 \(N_s\) 个专门专家。每个专家为两层 FFN，隐藏维度设计为原 FFN 的 \(1/(k_{max}+1)\)，确保最大计算量与原 FFN 相当。
  - 共享专家为所有窗口提供统一的特征基线。
  - **稀疏引导路由（Sparsity‑Guided Routing）**
    - 复用 ScoreNet 产生的重要性分数，决定每个窗口分配的专门专家数量 \(k_w\)（0 到 \(k_{max}\)）。
    - 具体做法：对选中的 K 个窗口按分数降序排列，通过预先设定的分布向量 \(P = (p_0,...,p_{k_{max}})\)（如 \(0.4,0.3,0.2,0.1\)）映射排名到专家数（例如前 10% 得 3 个，接着 20% 得 2 个，再 30% 得 1 个，后 40% 得 0 个）。
    - 轻量级路由器（单线性层）根据窗口特征的均值池化选出具体的 \(k_w\) 个专门专家。
    - 窗口的最终输出 = 共享专家输出 + 所选专门专家输出的加权和（权重经 Softmax 归一化）。
- **在线负载均衡**
  - 不使用辅助损失，采用可学习偏置项动态调整专家选择偏好。每个专门专家有一个偏置 \(b_i\)，根据实时负载误差按符号更新，更新步长 \(u_t\) 随训练进程线性或余弦衰减，实现稳定平衡。

### 3. 实验设计
- **数据集与基准**：PANDA 基准（首个十亿像素级人类中心数据集），包含 18 个场景，13 个用于训练，5 个用于测试。
- **评价指标**：FLOPs（按平均处理 1280×800 窗口计算，区分前景/背景/总计），COCO 风格 AP（APₜₒₜₐₗ、APₛ、APₘ、APₗ）。
- **对比方法**
  - 通用两阶段检测器：Faster R‑CNN、RetinaNet、Cascade R‑CNN（ResNet‑101）。
  - 专用十亿像素检测器：ClusDet、DMNet、GigaDet、PAN。
  - 稀疏处理方法：Dynamic‑Head + Swin‑T/DEG/SparseFormer，DINO + ResNet‑50/Swin‑T/DEG/SparseFormer/SparseNet。
  - 本研究提出的 **Dynamic‑Head+GigaMoE** 和 **DINO+GigaMoE**。
- **训练细节**：基于 MMDetection 工具包实现，所有模型均训练 36 个 epoch，骨干的超参数（深度、嵌入维度等）与对比方法保持一致以保证公平。

### 4. 资源与算力
- 论文未明确说明所使用的 GPU 型号、数量或训练时长，仅提到所有模型均训练 36 个 epoch。**算力需求未公开**。

### 5. 实验数量与充分性
- **实验组数**：
  - 主表（Table 1）包含十余种检测器/骨干组合，全面对比 AP 和 FLOPs。
  - 消融实验：专家分配分布（固定数量 vs. 多种自适应策略）、模块组件有效性（稀疏基线 → 传统 MoE → 稀疏引导 → 移除共享专家）、负载均衡策略（无均衡、固定更新率、线性衰减、余弦衰减）。
- **充分性与公平性**：实验覆盖主流检测头和骨干，严格控制结构参数一致，对比客观。消融实验逐步验证设计选择，结论可靠。未在 PANDA 以外的数据集（如其他十亿像素或病理图像）测试，但内部消融实验设计充分。

### 6. 主要结论与发现
- GigaMoE 在 PANDA 上取得 **新 SOTA**：与 DINO 头搭配时 APₜₒₜₐₗ 达 79.1%，比 SparseFormer（78.0%）高 1.1%；同时 **总 FLOPs 降低 32.3%**（从 75.71 降至 51.24 GFLOPs）。
- 动态自适应分配（倒金字塔分布）以极小的精度损失（0.3%）换取了巨大的计算节省（30.8%），验证了“以少数专家换取几乎全部性能”的可行性。
- 共享专家对性能至关重要（移除后 AP 骤降 5.6%），稀疏引导路由优于传统固定路由。
- 无辅助损失的在线负载均衡能有效避免专家崩溃，且自适应更新速率进一步提升稳定性。

### 7. 优点
- **创新性强**：首次将 Mixture‑of‑Experts 引入十亿像素目标检测，并巧妙地将区域选择分数复用为计算预算的指导信号。
- **效率与精度双赢**：不仅刷新 SOTA，还大幅降低计算量，实现了更优的 Pareto 前沿。
- **训练友好**：提出的无损失负载均衡方法避免了额外的超参数调优，简化训练。
- **设计统一**：在保持与现有稀疏方法兼容的同时，易于嵌入各类检测头，实验覆盖 DINO 和 Dynamic‑Head 两种头结构，展示出通用性。
- **消融实验扎实**：逐项验证了分配策略、路由机制和共享专家的必要性。

### 8. 不足与局限
- **数据集单一**：仅在 PANDA 上评估，未在其他十亿像素数据集（如病理全切片图像、遥感大图）或更宽泛的检测基准上验证泛化能力。
- **算力披露不足**：未报告具体 GPU 资源、batch size 或训练时长，难以评估实际部署和复现开销。
- **专家数量与分布预设**：路由分布 \(P\) 和最大专家数 \(k_{max}\) 基于经验选择，缺少对超参数敏感性的深入分析，可能需根据场景重新调整。
- **依赖 ScoreNet**：路由决策完全依赖稀疏选择阶段产生的分数，若 ScoreNet 质量较差，可能导致计算资源分配失当。
- **可能引入额外推理延迟**：虽然 FLOPs 降低，但 MoE 的动态路由和专家切换可能在实际硬件上带来额外通信或调度开销，论文未讨论实际推理速度。
- **模型复杂度**：多个专家小网络增加了参数量和工程实现复杂度，轻量级部署或边缘场景下的实用性待探索。

（完）
