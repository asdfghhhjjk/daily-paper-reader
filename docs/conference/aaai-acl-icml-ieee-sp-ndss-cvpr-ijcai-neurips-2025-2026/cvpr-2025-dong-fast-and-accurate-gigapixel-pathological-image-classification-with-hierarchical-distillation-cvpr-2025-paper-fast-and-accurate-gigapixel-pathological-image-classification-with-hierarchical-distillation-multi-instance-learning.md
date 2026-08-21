---
title: Fast and Accurate Gigapixel Pathological Image Classification with Hierarchical Distillation Multi-Instance Learning
title_zh: 基于层次蒸馏多实例学习的快速准确千兆像素病理图像分类
authors: "Dong, Jiuyang, Jiang, Junjun, Jiang, Kui, Li, Jiahan, Zhang, Yongbing"
date: 2025-06-01
pdf: "https://openaccess.thecvf.com/content/CVPR2025/papers/Dong_Fast_and_Accurate_Gigapixel_Pathological_Image_Classification_with_Hierarchical_Distillation_CVPR_2025_paper.pdf"
tags: ["query:cell-path"]
score: 6.0
evidence: 层次蒸馏多实例学习用于高效WSI病理图像分类
tldr: "针对千兆像素WSI分类中多实例学习推理成本高的问题，提出HDMIL框架，通过动态多实例网络和轻量级实例预筛选网络实现无关补丁剔除，从而加速分类。该方法在保持准确率的同时显著降低推理计算量。其为H&E全切片图像的病理分类提供了高效方案，但未利用细胞级分割与分类特征。"
source: CVPR-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-dong-fast-and-accurate-gigapixel-pathological-image-classification-with-hierarchical-distillation-cvpr-2025-paper/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 838, \"height\": 501, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-dong-fast-and-accurate-gigapixel-pathological-image-classification-with-hierarchical-distillation-cvpr-2025-paper/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1713, \"height\": 659, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-dong-fast-and-accurate-gigapixel-pathological-image-classification-with-hierarchical-distillation-cvpr-2025-paper/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 880, \"height\": 832, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-dong-fast-and-accurate-gigapixel-pathological-image-classification-with-hierarchical-distillation-cvpr-2025-paper/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 863, \"height\": 709, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-dong-fast-and-accurate-gigapixel-pathological-image-classification-with-hierarchical-distillation-cvpr-2025-paper/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1715, \"height\": 707, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-dong-fast-and-accurate-gigapixel-pathological-image-classification-with-hierarchical-distillation-cvpr-2025-paper/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 852, \"height\": 495, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-dong-fast-and-accurate-gigapixel-pathological-image-classification-with-hierarchical-distillation-cvpr-2025-paper/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 863, \"height\": 777, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-dong-fast-and-accurate-gigapixel-pathological-image-classification-with-hierarchical-distillation-cvpr-2025-paper/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1724, \"height\": 319, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-dong-fast-and-accurate-gigapixel-pathological-image-classification-with-hierarchical-distillation-cvpr-2025-paper/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 843, \"height\": 145, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-dong-fast-and-accurate-gigapixel-pathological-image-classification-with-hierarchical-distillation-cvpr-2025-paper/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 867, \"height\": 237, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-dong-fast-and-accurate-gigapixel-pathological-image-classification-with-hierarchical-distillation-cvpr-2025-paper/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 863, \"height\": 221, \"label\": \"Table\"}]"
motivation: 多实例学习处理海量WSI补丁导致推理成本高。
method: 提出HDMIL，结合动态多实例网络与轻量级预筛选网络加速分类。
result: 在病理图像分类上实现快速准确，消除无关补丁。
conclusion: 为WSI分类提供高效MIL框架，是计算病理学的重要基础。
---

## Abstract
Although multi-instance learning (MIL) has succeeded in pathological image classification, it faces the challenge of high inference costs due to processing numerous patches from gigapixel whole slide images (WSIs).To address this, we propose HDMIL, a hierarchical distillation multi-instance learning framework that achieves fast and accurate classification by eliminating irrelevant patches.HDMIL consists of two key components: the dynamic multi-instance network (DMIN) and the lightweight instance pre-screening network (LIPN). DMIN operates on high-resolution WSIs, while LIPN operates on the corresponding low-resolution counterparts.During training, DMIN are trained for WSI classification while generating attention-score-based masks that indicate irrelevant patches.These masks then guide the training of LIPN to predict the relevance of each low-resolution patch.During testing, LIPN first determines the useful regions within low-resolution WSIs, which indirectly enables us to eliminate irrelevant regions in high-resolution WSIs, thereby reducing inference time without causing performance degradation.In addition, we further design the first Chebyshev-polynomials-based Kolmogorov-Arnold classifier in computational pathology, which enhances the performance of HDMIL through learnable activation layers.Extensive experiments on three public datasets demonstrate that HDMIL outperforms previous state-of-the-art methods, e.g., achieving improvements of 3.13% in AUC while reducing inference time by 28.6% on the Camelyon16 dataset.The project will be available.

---

## 论文详细总结（自动生成）

## 1. 论文的核心问题与整体含义

- **研究背景**：多实例学习（MIL）已成为病理全切片图像（WSI）分类的主流方法，但其推理成本很高，主要原因在于需要对千兆像素 WSI 中的大量 patch 逐一进行裁剪和特征提取。
- **核心问题**：现有 MIL 方法必须先提取所有 patch 的特征，才能计算注意力分数并判断哪些 patch 相关，形成“先有鸡还是先有蛋”的困境，导致难以在推理阶段提前剔除无关 patch。
- **论文目标**：通过层次蒸馏框架 HDMIL，在不降低分类性能的前提下，快速识别并剔除无关 patch，从而减少 WSI 推理时间。
- **整体含义**：论文提出了一种新的加速思路：利用低分辨率 WSI 预筛选相关区域，间接决定高分辨率 WSI 中哪些 patch 需要处理，挑战了“速度与性能不可兼得”的传统认知。

## 2. 论文提出的方法论

- **总体框架**：HDMIL 包含两个核心模块：
  - **动态多实例网络（DMIN）**：在高分辨率 WSI 上训练，用于分类并生成 patch 相关性掩码。
  - **轻量级实例预筛选网络（LIPN）**：在低分辨率 WSI 上工作，学习预测每个低分辨率 patch 是否相关。
- **训练阶段分两步**：
  1. **自蒸馏训练 DMIN**：
     - 使用高分辨率 patch 特征，通过投影模块和注意力模块获得注意力分数。
     - 教师分支使用全部实例计算包级表示并分类。
     - 学生分支通过 Gumbel-Sigmoid 和可微二值化，只选择注意力分数较高的实例计算包级表示。
     - 通过自蒸馏损失（L2 和 KL 散度）强制教师和学生分支输出一致，同时约束学生分支选择的实例比例接近预设保留率 \(r\)。
     - 训练完成后，DMIN 可以为每个 patch 生成二元掩码，指示其是否相关。
  2. **跨蒸馏训练 LIPN**：
     - 将低分辨率 patch 输入 LIPN，得到双分支预测矩阵，并二值化为掩码。
     - 使用 DMIN 生成的掩码作为监督信号，通过 L1 损失和保留率约束训练 LIPN，使其学会预测低分辨率 patch 的相关性。
- **推理阶段**：
  - 先对低分辨率 WSI 进行裁剪，输入 LIPN 得到相关区域掩码。
  - 根据掩码选择性裁剪高分辨率 WSI 中对应区域，只对保留的 patch 进行特征提取和 DMIN 分类。
- **CKA 分类器**：
  - 提出基于第一类切比雪夫多项式的 Kolmogorov-Arnold 分类器（CKA），替代传统线性分类层。
  - 通过迭代形式 \(T_K(x) = 2xT_{K-1}(x) - T_{K-2}(x)\) 构造基函数，并与可学习系数相乘得到预测。
  - 使用 tanh 将输入映射到 \([-1,1]\) 以满足多项式要求。
- **关键公式**：
  - 注意力分数：\(A_{i,HR} = [\phi(F_{i,HR}V) \odot \sigma(F_{i,HR}U)]W\)
  - 教师分支包级表示：\(E^{tea}_{i,HR,c} = \varphi(A_{i,HR,c})^\top \otimes F_{i,HR,c}\)
  - 学生分支通过可微二值化掩码 \(M^j_{i,HR,c}\) 加权求和得到包级表示。
  - 混合损失：\(L_{DMIN} = \alpha_1 L^{tea}_{cls} + \alpha_2 L^{tea}_{clu} + \alpha_3 L^{stu}_{dis,1} + \alpha_4 L^{stu}_{dis,2} + \alpha_5 L^{stu}_{rate}\)
  - LIPN 损失：\(L_{LIPN} = \beta_1 \sum_{c=1}^2 L1(M_{i,LR,c}, M_{i,HR,c}) + \beta_2 L2(e_{i,LR}, r)\)

## 3. 实验设计

- **数据集**：
  - **Camelyon16**：乳腺癌淋巴结转移检测，官方训练集按 9:1 划分训练/验证，官方测试集用于测试。
  - **TCGA-NSCLC**：肺癌亚型分类，按 8:1:1 划分训练/验证/测试。
  - **TCGA-BRCA**：乳腺癌亚型分类，按 8:1:1 划分训练/验证/测试。
- **预处理**：使用 CLAM 工具进行 WSI 预处理，提取 20× 高分辨率和 1.25× 低分辨率 patch；高分辨率 patch 大小为 256×256，低分辨率为 16×16。
- **评估指标**：AUC、ACC、平均每 WSI 处理时间（秒）。
- **对比方法**：Max-Pooling、Mean-Pooling、ABMIL、CLAM-SB、CLAM-MB、DSMIL、TransMIL、DTFD-AFS、DTFD-MAS、S4MIL、MambaMIL 等 11 种现有 MIL 方法。
- **交叉验证**：所有实验采用 10 折蒙特卡洛交叉验证，报告均值和标准差。
- **推理时间分解**：将推理过程分为实例预筛选（LIPN）、WSI 裁剪、特征提取、DMIN 分类四个阶段进行对比。

## 4. 资源与算力

- 论文**未明确说明**所使用的 GPU 型号、数量、训练时长或具体算力配置。
- 仅提到：
  - 特征提取器使用 ImageNet 预训练的 ResNet-50。
  - LIPN 使用轻量级 MobileNetV4 变体。
  - 预处理基于 CLAM 工具。
- 因此无法从文中获得计算资源开销的定量信息，这一点是实验可复现性方面的缺失。

## 5. 实验数量与充分性

- **实验数量较多**，主要包括：
  1. 三个数据集的分类性能对比（表 1）。
  2. 推理时间分解与加速分析（表 2）。
  3. 各模块消融实验：DMIN、CKA、自蒸馏、LIPN 的贡献（表 3）。
  4. CKA 分类器深入分析：位置、与其他分类器对比、不同多项式阶数（表 4）。
  5. 自蒸馏效果的线性探测验证（表 5）。
  6. LIPN 不同蒸馏方式对比（表 6）。
  7. 实例保留率 \(r\) 对性能和时间的影响（图 4）。
  8. 数据集规模对性能影响的分析（表 7）。
  9. 可视化分析（图 3）。
- **充分性评价**：实验设计较为全面，覆盖了主要模块的有效性、超参数影响、时间收益和性能对比，且采用 10 折交叉验证，结果具有统计意义。
- **客观性与公平性**：
  - 对比方法较多，涵盖经典和近年 SOTA 方法。
  - 所有实验使用相同预处理流程和评估协议，公平性较好。
  - 但论文未说明对比方法的实现来源（是作者重新实现还是直接引用原论文结果），可能引入实现差异风险。

## 6. 论文的主要结论与发现

- **性能提升**：HDMIL 在三个数据集上均优于现有 SOTA 方法。例如在 Camelyon16 上，HDMIL 的 AUC 达到 90.88%，ACC 达到 88.61%，分别比此前最佳方法提升 3.13% 和 3.18%。
- **推理加速**：HDMIL 在 Camelyon16、TCGA-NSCLC、TCGA-BRCA 上分别减少总推理时间 28.6%、21.8%、7.2%，主要来自裁剪和特征提取阶段的时间节省。
- **自蒸馏有效**：通过自蒸馏让 DMIN 学会聚焦重要实例，提高了分类性能，并可通过线性探测实验验证所选实例质量更高。
- **CKA 分类器有效**：替换传统线性分类器后，AUC 和 ACC 均有显著提升；最佳切比雪夫多项式阶数为 12。
- **掩码蒸馏优于注意力蒸馏**：在 LIPN 训练中，使用离散掩码作为监督信号比使用连续注意力分数效果更好。
- **小数据集效应**：HDMIL 与 HDMIL† 的性能差距在 Camelyon16 上较大，可能是由于验证集规模小导致模型选择偏差，而非算法本身缺陷。

## 7. 优点

- **思路新颖**：通过低分辨率预筛选解决“先提取特征才能判断相关性”的鸡生蛋问题，实现加速而不牺牲性能。
- **层次蒸馏设计巧妙**：自蒸馏让 DMIN 学会聚焦重要 patch，跨蒸馏让 LIPN 学会在低分辨率上快速预筛选，两者结合有效降低计算量。
- **引入 CKA 分类器**：首次将基于切比雪夫多项式的 Kolmogorov-Arnold 网络用于计算病理学，可学习激活函数提升了分类能力。
- **实验丰富**：包含模块消融、超参数分析、时间分解、可视化、数据集规模影响等，多角度验证方法有效性。
- **可解释性较好**：可视化显示 DMIN 注意力分支能区分正常组织和肿瘤组织，LIPN 能丢弃脂肪组织等无关区域。

## 8. 不足与局限

- **未提供算力信息**：缺少 GPU 型号、数量、训练时长等资源细节，影响可复现性和成本评估。
- **数据集规模有限**：Camelyon16 官方训练集不足 400 例 WSI，小数据集导致 HDMIL 在测试集上出现性能波动，削弱了部分结论的稳健性。
- **保留率 \(r\) 是预设超参数**：需要手动调节，且不同数据集最优值可能不同，增加了实际应用的调参负担。
- **评测协议可能引入偏差**：10 折蒙特卡洛交叉验证中，模型选择基于验证集，小验证集可能造成选择偏差，论文虽分析了这一现象，但未提出改进方案。
- **未讨论特征提取器负担**：虽然减少了需要提取特征的 patch 数量，但特征提取器本身仍是计算瓶颈，论文在结论中也承认未来需要进一步减轻特征提取负担。
- **应用范围受限**：仅在三个二分类/亚型分类任务上验证，缺少更多癌症类型、多分类任务或生存预测等场景的评估。

（完）
