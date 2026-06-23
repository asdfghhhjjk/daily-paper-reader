---
title: "FuseUNet: A Multi-Scale Feature Fusion Method for U-like Networks"
title_zh: FuseUNet：面向U形网络的多尺度特征融合方法
authors: "Quansong He, Xiangde Min, Kaishen Wang, Tao He"
date: 2025-05-01
pdf: "https://openreview.net/pdf?id=KYiynifZUk"
tags: ["query:pathology-ai"]
score: 6.0
evidence: 医学图像分割中的多尺度特征融合
tldr: UNet及其变体在医学图像分割中广泛使用，但跳跃连接缺乏跨尺度交互且仅简单拼接。本文提出FuseUNet，将解码过程视为初值问题，重新设计跳跃连接为多尺度融合机制。该方法增强了不同尺度特征之间的信息流动，在多个医学分割数据集上取得更优性能，可推广至数字病理图像分析。
source: ICML-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-icml-2025-kyiynifzuk/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 529, \"height\": 375, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-kyiynifzuk/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1683, \"height\": 1033, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-kyiynifzuk/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1766, \"height\": 575, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-kyiynifzuk/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 835, \"height\": 522, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-kyiynifzuk/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 782, \"height\": 516, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-kyiynifzuk/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1775, \"height\": 475, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-kyiynifzuk/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1774, \"height\": 474, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-kyiynifzuk/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1777, \"height\": 471, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-kyiynifzuk/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1739, \"height\": 1242, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-icml-2025-kyiynifzuk/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 841, \"height\": 454, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-kyiynifzuk/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1751, \"height\": 347, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-kyiynifzuk/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1627, \"height\": 816, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-kyiynifzuk/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1709, \"height\": 397, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-kyiynifzuk/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 787, \"height\": 250, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-kyiynifzuk/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1142, \"height\": 609, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-kyiynifzuk/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 968, \"height\": 190, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-kyiynifzuk/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1722, \"height\": 186, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-kyiynifzuk/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1120, \"height\": 154, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-kyiynifzuk/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 882, \"height\": 783, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-kyiynifzuk/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 934, \"height\": 284, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-kyiynifzuk/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1761, \"height\": 182, \"label\": \"Table\"}]"
motivation: UNet的跳跃连接缺乏跨尺度交互，限制信息整合效率。
method: 将解码过程建模为初值问题，提出多尺度特征融合方法以增强跳跃连接。
result: 在多个医学分割数据集上取得更优分割精度。
conclusion: FuseUNet改进了UNet的信息流动，适用于医学图像分割。
---

## Abstract
Medical image segmentation is a critical task in computer vision, with UNet serving as a milestone architecture. The typical component of UNet family is the skip connection, however, their skip connections face two significant limitations: (1) they lack effective interaction between features at different scales, and (2) they rely on simple concatenation or addition operations, which constrain efficient information integration. While recent improvements to UNet have focused on enhancing encoder and decoder capabilities, these limitations remain overlooked. To overcome these challenges, we propose a novel multi-scale feature fusion method that reimagines the UNet decoding process as solving an initial value problem (IVP), treating skip connections as discrete nodes. By leveraging principles from the linear multistep method, we propose an adaptive ordinary differential equation method to enable effective multi-scale feature fusion. Our approach is independent of the encoder and decoder architectures, making it adaptable to various U-Net-like networks. Experiments on ACDC, KiTS2023, MSD brain tumor, and ISIC2017/2018 skin lesion segmentation datasets demonstrate improved feature utilization, reduced network parameters, and maintained high performance. The code is available at
https://github.com/nayutayuki/FuseUNet.

---

## 论文详细总结（自动生成）

# 论文总结：FuseUNet: A Multi-Scale Feature Fusion Method for U-like Networks

## 1. 核心问题与整体含义（研究动机和背景）

- **问题**：U-Net系列网络的跳跃连接存在两个主要局限：一是缺乏不同尺度特征之间的有效交互，二是仅依赖简单的拼接或加法操作，制约了信息整合效率。近年来对U-Net的改进多集中在编码器/解码器能力增强上，忽视了跳跃连接本身的缺陷。
- **意义**：本文首次从数值计算角度重新解读U-Net的跳跃连接，将解码过程类比为求解常微分方程初值问题，提出一种基于线性多步法和神经记忆ODE的多尺度特征融合方法，旨在提升特征利用率、降低参数量并保持高性能，且与编码器/解码器结构无关，可推广至各类U形网络。

## 2. 方法论

- **核心思想**：将U-Net中不同尺度的跳跃连接视为离散节点，解码过程视为对初值问题（IVP）的求解。借鉴线性多步法（Adams-Bashforth和Adams-Moulton方法）及预测-校正思想，自适应选择离散阶数实现多尺度特征融合。结合神经记忆常微分方程（nmODEs），将学习神经元和记忆神经元分离，使记忆流可逐步更新而不参与特征提取，从而大幅降低计算开销。
- **关键技术细节**：
  - 定义每个阶段跳跃连接特征 `X_i` 与解码器输出 `Y_i`，建立微分关系 `˙Y_i = -Y_i + f(Y_i + g(X_i))`，其中 `f` 根据网络架构选择（卷积/Transformer/Mamba），`g` 用于对齐形状。
  - 使用预测-校正（P-C）模块：对第 `i` 步，先通过显式Adams-Bashforth方法预测 `Y_{i+1}`，再用隐式Adams-Moulton方法校正，逐步提高精度。初始阶段（`i<4`）使用低阶方法，之后固定使用4步隐式方法；最终阶段使用显式4步方法计算 `Y_final`。
  - 算法流程（Algorithm 1）详细描述了从 `i=1` 到 `L-1` 的更新过程，以及最终计算步骤。
- **公式/算法（文字说明）**：见论文Algorithm 1及附录A，核心是利用多步线性多步法公式，通过已知的 `F_i = ˙Y_i` 序列递推求解 `Y_i`，并保证跨尺度信息充分融入。

## 3. 实验设计

- **数据集**：3D任务：ACDC（心脏MRI，100例）、KiTS2023（肾脏CT，559例）、MSD脑肿瘤（MRI，484例）；2D任务：ISIC2017（皮肤镜，2000张）、ISIC2018（2594张）。均为医学图像分割领域公开基准。
- **Benchmark**：对于每个架构选取代表性骨干网络：CNN型：nn-UNet；Transformer型：UNETR；Mamba型：UltraLight VM-UNet。
- **对比方法**：
  - 3D任务：与CoTr、Swin-UNETR、U-Mamba、STU-Net-L、nn-UNet、UNet3+、TransUNet等对比。
  - 2D任务：与UNet、TransFuse、MALUNet、EGE-UNet、VM-UNet、UltraLight VM-UNet对比。
- **评价指标**：Dice系数（3D任务）；Dice、灵敏度（SE）、特异度（SP）、准确率（ACC）（2D任务）。均采用官方协议（如五折交叉验证）。

## 4. 资源与算力

- **GPU**：所有实验在单张RTX 4090上完成。
- **训练时长**：论文表5给出了KiTS数据集上不同内存容量下的单epoch时间（如2N通道时128秒/epoch），但未提供完整训练总时长。学习率设置为骨干网络的2~3倍，其余超参数与骨干网络一致。
- **说明**：文中未明确报告总训练时间或GPU数量，仅提到单GPU实验。

## 5. 实验数量与充分性

- **实验组数**：
  - 3D任务：三个数据集×五折交叉验证，每个骨干网络各一组实验（共3组主要对比）。
  - 2D任务：两个数据集，一组主要对比。
  - 消融实验：a）特征融合阶数影响（图5，测试了1~4阶，覆盖全部5个数据集）；b）记忆容量影响（表5，在KiTS上测试4种通道数）。
  - 统计检验：表12对ACDC和KiTS进行了配对t检验，显示FuseUNet与nn-UNet无显著差异。
- **充分性判断**：实验覆盖多模态（MRI/CT/皮肤镜）、多任务（2D/3D）、多架构（CNN/Transformer/Mamba），消融实验完整，统计检验合理。对比方法包括近年SOTA，且实验设置与骨干网络原始文献保持一致，较为客观公平。

## 6. 主要结论与发现

- FuseUNet在保持或略微提升分割精度的前提下，显著降低参数量和计算量（3D任务：nn-UNet参数量减少54.9%，GFLOPs减少34.3%；UNETR参数量减少13.6%，GFLOPs减少50%；2D轻量骨干参数量减少29.8%）。
- 可视化结果表明，FuseUNet能更好地识别边缘细节、减少假阳性/假阴性。
- 特征融合阶数越高（4阶最佳），网络性能越好；记忆容量设为2倍目标类数时性价比最优。
- 方法对编码器/解码器结构无关，可灵活适配不同架构的U形网络。

## 7. 优点

- **理论创新**：首次将跳跃连接与线性多步法、预测-校正法建立显式数学联系，为网络结构提供了可解释的数值计算基础。
- **通用性**：方法独立于编码器/解码器，可应用于卷积、Transformer、Mamba等主流U-Net变体。
- **高效性**：通过nmODEs分离记忆与学习，大幅减少解码器参数量和计算开销，尤其适用于轻量级网络。
- **实验充分**：覆盖多数据集多架构，消融实验验证关键设计，统计检验增强可信度。
- **代码开源**：提供GitHub仓库，便于复现和推广。

## 8. 不足与局限

- **内存消耗**：线性多步法需要存储多个历史解（中间状态），当目标类别数较多时内存占用显著增加（表5显示4N时VRAM增至8.7G）。作者也承认这是未来需要改进的方向。
- **计算量增加**：在轻量级网络上，由于插值操作导致GFLOPs略有上升（如UltraLight VM-UNet上GFLOPs从0.060增至0.095），但整体仍属可接受范围。
- **适用场景限制**：方法依赖于跳跃连接的多尺度信息，对于没有明显编码-解码结构的网络可能不适用。
- **未覆盖所有骨干**：虽测试了三种主流架构，但未包含如Swin-UNet、U-Mamba等更多变体，也未在超大规模数据集（如总分割挑战）上验证。
- **统计显著性**：t检验显示与nn-UNet无显著差异，说明性能提升并不绝对，主要优势在于参数压缩而非准确率大幅提升。

（完）
