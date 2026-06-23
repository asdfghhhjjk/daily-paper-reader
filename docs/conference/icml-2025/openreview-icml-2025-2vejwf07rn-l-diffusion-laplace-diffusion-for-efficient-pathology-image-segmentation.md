---
title: "L-Diffusion: Laplace Diffusion for Efficient Pathology Image Segmentation"
title_zh: "L-Diffusion: 用于高效病理图像分割的拉普拉斯扩散模型"
authors: "Weihan Li, Linyun Zhou, YangJian, Shengxuming Zhang, Xiangtong Du, Xiuming Zhang, Jing Zhang, ChaoqingXu, Mingli Song, Zunlei Feng"
date: 2025-05-01
pdf: "https://openreview.net/pdf?id=2veJwf07RN"
tags: ["query:cellseg"]
score: 7.0
evidence: 病理图像分割，数字病理
tldr: 针对病理图像分割中标注成本高和长尾类别识别精度低的问题，提出L-Diffusion框架，利用多个拉普拉斯分布代替高斯分布建模不同成分，理论上增强特征分解能力。实验表明在病理分割数据集上显著提升了尾部类别准确性且更高效。
source: ICML-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-icml-2025-2vejwf07rn/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 854, \"height\": 630, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-2vejwf07rn/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1745, \"height\": 1026, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-2vejwf07rn/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1764, \"height\": 452, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-2vejwf07rn/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1693, \"height\": 1119, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-2vejwf07rn/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1770, \"height\": 508, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-2vejwf07rn/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1157, \"height\": 617, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-2vejwf07rn/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1731, \"height\": 1695, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-2vejwf07rn/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1591, \"height\": 2180, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-2vejwf07rn/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1547, \"height\": 2154, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-2vejwf07rn/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1653, \"height\": 2070, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-2vejwf07rn/fig-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1569, \"height\": 1651, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-icml-2025-2vejwf07rn/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1777, \"height\": 718, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-2vejwf07rn/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1777, \"height\": 718, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-2vejwf07rn/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 850, \"height\": 252, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-2vejwf07rn/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 836, \"height\": 261, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-2vejwf07rn/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 850, \"height\": 227, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-2vejwf07rn/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 851, \"height\": 178, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-2vejwf07rn/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1205, \"height\": 264, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-2vejwf07rn/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1544, \"height\": 689, \"label\": \"Table\"}]"
motivation: 病理图像标注耗时且长尾分布导致尾部类别分割精度低。
method: 提出拉普拉斯扩散模型，用多个拉普拉斯分布建模特征空间的不同成分。
result: 在多个病理分割任务上提升了尾部类别准确率，并降低了标注需求。
conclusion: 拉普拉斯扩散能有效处理病理图像的长尾分布问题。
---

## Abstract
Pathology image segmentation plays a pivotal role in artificial digital pathology diagnosis and treatment. Existing approaches to pathology image segmentation are hindered by labor-intensive annotation processes and limited accuracy in tail-class identification, primarily due to the long-tail distribution inherent in gigapixel pathology images. In this work, we introduce the Laplace Diffusion Model, referred to as L-Diffusion, an innovative framework tailored for efficient pathology image segmentation. L-Diffusion utilizes multiple Laplace distributions, as opposed to Gaussian distributions, to model distinct components—a methodology supported by theoretical analysis that significantly enhances the decomposition of features within the feature space. A sequence of feature maps is initially generated through a series of diffusion steps. Following this, contrastive learning is employed to refine the pixel-wise vectors derived from the feature map sequence.  By utilizing these highly discriminative pixel-wise vectors, the segmentation module achieves a harmonious balance of precision and robustness with remarkable efficiency. Extensive experimental evaluations demonstrate that L-Diffusion attains improvements of up to  7.16\%,  26.74\%,  16.52\%, and  3.55\% on tissue segmentation datasets, and  20.09\%,  10.67\%,  14.42\%, and  10.41\% on cell segmentation datasets, as quantified by DICE, MPA, mIoU, and FwIoU metrics. The source are available at https://github.com/Lweihan/LDiffusion.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 核心问题与整体含义（研究动机和背景）
- **问题**：病理图像（gigapixel级别）存在长尾分布，导致尾部类别标注成本高、分割精度低。现有方法在尾部类别识别上表现有限。
- **整体含义**：论文提出 **L-Diffusion（拉普拉斯扩散模型）**，利用拉普拉斯分布替代传统高斯分布来建模不同组织/细胞成分，从理论上增强特征空间中的成分分离能力，结合对比学习进一步拉大成分间的分布差异，最终实现高效、精准的病理图像分割。

## 2. 方法论：核心思想与技术细节
- **核心思想**：使用多个独立的拉普拉斯分布（而非高斯分布）对图像的 N 个不同成分建模；利用扩散过程生成中间重建特征图序列；沿着扩散步数轴提取每个像素的潜在向量（1×T）；通过对比学习优化这些向量，使同类像素向量聚集、异类像素向量分离；最后用分割网络（ConvNeXT）基于增强后的特征图序列生成分割结果。
- **关键技术细节**：
  - **拉普拉斯扩散**：正向和反向扩散步骤中，噪声分布采用拉普拉斯分布。理论分析表明，拉普拉斯分布的梯度变化更陡（`∇pL(x) ∝ -sign(x)/b`），对噪声更敏感，能更好分离不同成分的分布。
  - **像素潜在向量对比学习**：每个像素对应一个 T 维向量（由 T 步扩散的灰度特征图组成）。对于有标注的少量样本，使用对比损失函数 `L_{CRT}` 拉近同类样本的向量、推远异类样本的向量。超参数 τ 设为 0.05~0.1。
  - **分割模块**：将对比学习增强后的特征图序列拼接，输入 ConvNeXT 网络，用 DICE 损失训练。
- **公式/算法流程（文字说明）**：
  1. 输入图像 x0，通过 VAE 编码到潜在空间。
  2. Laplace Scheduler 将噪声按拉普拉斯分布添加到潜在表示，经 U-Net 预测噪声并逐步去噪，经 DAE 解码回原始尺寸，得到 T 张中间重建特征图 [r1,...,rT]。
  3. 每张特征图转为灰度图 [ˆr1,...,ˆrT]，沿扩散步骤轴提取每个像素的潜在向量 v ∈ R^(1×T)。
  4. 使用对比学习损失（仅对部分有标注的像素对）优化向量，使不同成分的向量差异最大化。
  5. 将优化后的特征图序列输入 ConvNeXT 进行分割，训练使用 DICE 损失。

## 3. 实验设计
- **数据集**：
  - **组织分割**：CRCD（结直肠癌，1764张，9种组织）、PUMA（黑色素瘤，151张，6种组织）、BCSS（乳腺癌，151张，22种组织）。
  - **细胞分割**：PanNuke（多类细胞，481张，19种细胞）。
  - **泛化实验**：Massachusetts‑Building 遥感图像分割数据集。
- **Baseline 与对比方法**：FastFCN、U‑Net++、Swin‑UNet、SAMUS、SAMed、SAMPath、DeepLabv3/v3+、DenseASPP、UN‑SAM、BONUS 等 11 种主流方法。
- **评价指标**：DICE、MPA（平均像素准确率）、mIoU（平均交并比）、FwIoU（频率加权交并比）。细胞分割中仅对前景细胞计算指标以消除背景主导影响。
- **实验规模**：
  - 在 4 个数据集上与 11 种方法比较（定量 + 定性）。
  - 在 PUMA 数据集上进行了不同标注比例（10%‑100%）的消融。
  - 消融对比学习 + 拉普拉斯分布（四个组合，平均 3 个组织数据集结果）。
  - 不同噪声分布（Cauchy、Student's t、Laplace）对比。
  - 遥感图像泛化实验（与 U‑Net、Uniformer、UANet、GLGF‑Net 对比）。

## 4. 资源与算力
- **未明确说明**：文中没有提及 GPU 型号、数量或总训练时长。
- **间接信息**：扩散模型训练 batch size = 1，分割网络训练 batch size = 32；在噪声分布对比实验中，Laplace 的运行时为 8882 秒（学生 t 为 20440 秒，Cauchy 为 7325 秒），但未说明硬件环境。

## 5. 实验数量与充分性
- **数量充分**：论文覆盖了组织分割、细胞分割、遥感分割三大场景，包含了定量、定性、消融（分布选择、对比学习有无、标注比例）、泛化性、不同成分性能分析等多组实验。
- **客观性与公平性**：使用了公开数据集和开源代码，对比方法均为近期 SOTA；评价指标多样。但未提供置信区间或多次重复实验的标准差，可能存在随机性影响；遥感泛化仅一个数据集，泛化能力验证有限。

## 6. 主要结论与发现
- L‑Diffusion 在所有病理分割数据集上 **显著优于** 现有方法，组织分割 DICE 提升最高 7.16%（PUMA），细胞分割 DICE 提升最高 20.09%（PanNuke）。
- 拉普拉斯分布比高斯分布 **更利于区分不同成分**，尤其对尾部类别（低比例成分）效果突出。
- **对比学习** 与拉普拉斯分布结合后，像素潜在向量的类间分离度和类内紧凑度同步提升。
- **仅需 30% 标注样本** 即可达到接近全标注的性能，大幅降低标注成本。
- 在遥感图像分割任务中也有良好表现，说明方法具有一定 **跨领域泛化能力**。

## 7. 优点
- **理论创新**：首次将拉普拉斯分布引入扩散模型用于分割任务，并从梯度角度理论论证其优势。
- **方法简洁高效**：通过扩散步骤构建像素潜在向量 + 对比学习，无需复杂网络结构即可显著提升分割性能。
- **缓解长尾问题**：对低比例成分（如凋亡细胞、少组织类型）的分割精度提升明显（雷达图所示）。
- **数据高效**：仅需少量标注即可训练对比学习，适合标注成本高的医疗场景。
- **实验全面**：覆盖多种数据集、多种对比方法、多角度消融，并做了泛化验证。

## 8. 不足与局限
- **仍需部分标注**：对比学习依赖于少量带标注的像素对，并非完全无监督。
- **硬件成本**：扩散模型训练/推理步骤（T=5~15）相比直接分割网络额外增加计算开销，文中未提供完整的训练时间与硬件对比。
- **泛化验证有限**：仅在遥感一个额外数据集上验证，未在更多非医学大尺度图像（如卫星、航拍）上测试。
- **潜在偏差与可靠性**：论文伦理声明提及可能存在算法偏见、可解释性不足、患者隐私等风险，并强调当前版本仅用于学术研究，未经临床部署验证。
- **无置信区间**：实验未报告多次运行的标准差或置信区间，结果的稳健性有待进一步确认。

（完）
