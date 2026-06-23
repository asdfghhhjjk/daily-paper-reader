---
title: Subobject-level Image Tokenization
title_zh: 子对象级图像标记化
authors: "Delong Chen, Samuel Cahyawijaya, Jianfeng Liu, Baoyuan Wang, Pascale Fung"
date: 2025-05-01
pdf: "https://openreview.net/pdf?id=imkFoKwFwd"
tags: ["query:cellseg"]
score: 6.0
evidence: 子对象级图像标记化，结合边界检测与分水岭分割
tldr: 针对基于块的图像标记化忽略视觉对象形态的问题，该论文提出子对象级自适应标记分割方法EPOC。它使用紧凑模型进行边界检测，并结合分水岭分割确保无像素遗漏，将图像分割为子对象级区域作为标记。在5个数据集上，EPOC的分割与人类对象级和部件级形态标注高度一致，并提升了标记的单语义性。该方法可直接迁移至细胞实例分割等任务，为个体细胞识别提供有效的分割基础。
source: ICML-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-icml-2025-imkfokwfwd/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 809, \"height\": 890, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-imkfokwfwd/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 809, \"height\": 510, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-imkfokwfwd/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1742, \"height\": 769, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-imkfokwfwd/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1730, \"height\": 791, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-imkfokwfwd/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1708, \"height\": 439, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-imkfokwfwd/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 859, \"height\": 247, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-imkfokwfwd/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1765, \"height\": 246, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-imkfokwfwd/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1764, \"height\": 568, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-imkfokwfwd/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1764, \"height\": 1235, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-imkfokwfwd/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1763, \"height\": 681, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-imkfokwfwd/fig-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1749, \"height\": 1512, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-imkfokwfwd/fig-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1729, \"height\": 415, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-imkfokwfwd/fig-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 1750, \"height\": 794, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-imkfokwfwd/fig-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 310, \"height\": 759, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-imkfokwfwd/fig-015.webp\", \"caption\": \"\", \"page\": 0, \"index\": 15, \"width\": 1733, \"height\": 901, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-icml-2025-imkfokwfwd/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 834, \"height\": 590, \"label\": \"Table\"}]"
motivation: 现有基于块的标记化忽视对象形态，限制了图像理解的效率和有效性。
method: 提出EPOC图像标记器，结合边界检测与分水岭分割得到子对象级区域作为标记。
result: EPOC的分割与人类形态标注高度一致，标记单语义性优于基线，且推理效率更高。
conclusion: 子对象级标记化可提升图像理解性能和效率，为实例分割提供新范式。
---

## Abstract
Patch-based image tokenization ignores the morphology of the visual world, limiting effective and efficient learning of image understanding. Inspired by subword tokenization, we introduce subobject-level adaptive token segmentation and explore several approaches, including superpixel, SAM, and a proposed Efficient and PanOptiC (EPOC) image tokenizer. Our EPOC combines boundary detection--a simple task that can be handled well by a compact model--with watershed segmentation, which inherently guarantees no pixels are left unsegmented. Intrinsic evaluations across 5 datasets demonstrate that EPOC's segmentation aligns well with human annotations of both object- and part-level visual morphology, producing more monosemantic tokens and offering substantial efficiency advantages. For extrinsic evaluation, we designed a token embedding that handles arbitrary-shaped tokens, and trained VLMs with different tokenizers on 4 datasets of object recognition and detailed captioning. The results reveal that subobject tokenization enables faster convergence and better generalization while using fewer visual tokens.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 核心问题与整体含义（研究动机和背景）

- **核心问题**：当前主流的图像标记化（tokenization）方法采用固定大小的方形图像块（patch），这种非自适应的分割方式忽略了视觉世界中的形态结构，导致两个关键缺陷：一是大图像块内可能包含多个语义（多语义性，polysemanticity），不利于模型学习；二是小图像块虽然语义更纯净，但会导致标记数量过多，计算效率低下。这类似于自然语言处理中“字符级”标记化的困境。
- **研究背景与动机**：在NLP中，子词（subword）标记化通过合并频繁共现的字符，实现了更好的语义单义性、对罕见词的泛化能力以及序列长度压缩。受此启发，论文提出在图像领域引入**子对象级（subobject-level）**自适应标记分割，即将图像分割为介于对象和像素之间的语义连贯区域（如对象部件、子部件等），以期在保持语义纯净性的同时控制标记数量。认知科学中的“识别-组件理论”也支持这种思路：人类通过对象的组成部分来识别物体。

## 2. 方法论：核心思想、关键技术细节

- **核心思想**：用自适应分割替代固定网格分割，将图像划分为语义上有意义的子对象区域作为视觉标记。论文探索了三种自适应分割思路：对象级（基于全景分割）、超像素（基于像素聚类）、以及提出的EPOC。
- **EPOC方法细节**：
  1. **边界检测**：采用极紧凑的SegFormer-b0模型（仅3.7M参数）预测像素级边界概率图 \( P \in [0,1]^{H \times W} \)。这比SAM（641M参数）的掩码生成任务简单得多，可以在单次前向传播中完成。
  2. **分水岭分割**：将边界概率图视为地形表面，概率高的区域为“山脊”（边界），概率低的区域为“盆地”（内部）。通过阈值 \( t \) 确定种子区域（低于阈值的像素），然后“淹没”过程从种子开始向外扩展，直到不同种子相遇时形成分水岭（即分割边界）。该算法天然保证所有像素都被分割（全景覆盖），且复杂度为 \( O(1) \)，与生成的标记数无关。
  3. **粒度控制**：通过调节阈值 \( t \) 可灵活控制分割粒度——\( t \) 越高，种子越少，分割越粗糙；\( t \) 越低，分割越细致。
- **与现有方法的区别**：不同于SAM需要多次通过掩码解码器生成独立掩码（复杂度O(N)），EPOC的单次边界预测+快速分水岭算法极大提升了效率，且避免了SAM的未分割区域问题。

## 3. 实验设计

- **内在评估（Intrinsic Evaluation）**：
  - **数据集**：5个数据集，覆盖对象级和子对象级标注。包括COCO（COCONut重标注验证集）、ADE-20K（对象级）、Pascal Panoptic Parts (PPP)、PartImageNet++ (PIN++)、SA-1B（子对象级）。
  - **评估指标**：
    - **形态对齐**：使用边界精确率-召回率（Boundary Precision-Recall），衡量分割与语义边界的匹配程度。
    - **标记单义性分数（Token Monosemanticity Score）**：计算有多少比例的预测标记完全位于单个真实语义区域内。
    - **计算效率**：测量最大FPS和GPU利用率。
  - **对比方法**：
    - 静态patch（patch size 2~32）
    - 对象级：Mask2Former、OneFormer（COCO/ADE20K训练）
    - 子对象级：SLIC超像素、SAM（ViT-B/H）、FastSAM、MobileSAMv2、EPOC
- **外在评估（Extrinsic Evaluation）**：
  - **任务与数据集**：训练视觉语言模型（VLM）在4个数据集上：
    - ImageNet-1K（物体识别）
    - ShareGPT4V（详细描述）
    - Pixmo-cap（丰富密集描述）
    - CLEVR-cap（新合成数据集，含计数、空间推理、属性识别）
  - **模型架构**：采用冻结的图像特征提取器（如DINOv2/CLIP/VAE）+可训练的MLP投影+LLM（Llama架构，最大1.7B参数）。针对自适应分割设计了内容嵌入（平均池化段内像素特征）和位置嵌入（盒-掩码分解，包含边界框和裁剪掩码）。
  - **对比方法**：patch、SLIC、Mask2Former、EPOC（不同粒度超参数）
  - **评估指标**：验证集困惑度（perplexity），训练损失下降速度，标记效率（不同标记数下的性能）。

## 4. 资源与算力

- **明确说明的算力**：
  - EPOC的边界检测模型（SegFormer-b0）在SA-1B数据集上训练了2个epoch，使用单台**8×A100**机器，有效批量大小64，学习率1e-4，5000步预热。
  - 推理效率测试在**NVIDIA V100 (32GB)** 和**30 CPU核心**上进行。
  - 外在评估中VLM训练：CLEVR-cap训练30 epoch，ImageNet-1k、ShareGPT4V、Pixmo-cap分别训练1、1、3 epoch，批量大小分别为512、256、256、256。使用AdamW，混合精度（bf16）。但论文未说明训练这些VLM的具体GPU型号和总计算量。
- **说明**：论文未详细给出外在评估中VLM训练的总GPU小时数或节点数，这部分算力信息较为模糊。

## 5. 实验数量与充分性

- **实验数量**：
  - 内在评估：5个数据集 × 多种方法（约10种），涵盖不同粒度遍历，生成大量数据点。
  - 外在评估：4个下游任务数据集，每个任务对多种标记器（patch、SLIC、Mask2Former、EPOC）在不同粒度下进行训练，并测试了多种图像特征提取器（DINOv2、CLIP、VAE、RGB像素）和不同规模LLM（最大1.7B）。
  - 额外消融实验：标记截断鲁棒性、不同位置嵌入/内容嵌入策略等。
- **充分性与公平性**：
  - **充分**：内在评估使用边界PR和单义性分数，从形态对齐、语义纯度、效率三个维度系统比较；外在评估覆盖了物体识别、详细描述、合成推理等任务，并进行了多种超参数扫描。
  - **客观公平**：对比方法均为公开成熟模型（SAM、FastSAM、SLIC等），且在同一框架下调整粒度参数，避免了偏向性。但外在评估中EPOC与SAM的直接对比未包含SAM（SAM因效率太低未训练VLM），这在一定程度削弱了公平性。不过论文给出了内在评估中SAM的性能作为参考。

## 6. 主要结论与发现

1. **子对象级标记化显著优于静态patch**：在所有外在评估数据集上，自适应标记化（尤其是EPOC和SLIC）在使用更少标记的情况下，达到或超过了小patch的验证困惑度，并实现更快收敛。
2. **EPOC内在性能突出**：EPOC的分割与人类标注的形态对齐度接近SAM ViT-H，且优于SAM ViT-B和所有对象级模型；标记单义性分数接近100%（在子对象级数据上），而对象级模型仅约60%。
3. **计算效率极高**：EPOC（3.7M参数）最大FPS达17.1，GPU利用率低于10%，远优于所有SAM变体（SAM ViT-H仅0.4 FPS，GPU利用率92.4%）。
4. **与弱特征兼容**：在使用VAE嵌入时，patch-based模型无法收敛，而EPOC仍可有效学习，表明自适应分割简化了图像理解任务。
5. **对标记截断鲁棒**：由于EPOC产生长尾分布（有许多小标记），丢弃最小标记对性能影响很小，而随机丢弃patch会导致显著下降。

## 7. 优点

- **方法新颖且自然**：将NLP中的子词思想引入图像标记化，提出了明确的“子对象”概念，并设计了实用高效的EPOC方法。
- **兼顾效率与质量**：通过简化任务（边界检测替代掩码生成）和使用轻量模型，大幅降低了计算开销，同时保持了与SAM相当的分割质量。
- **完整的评估体系**：同时进行内在和外在评估，从多个维度验证方法的有效性，包括形态对齐、语义纯度、效率、下游任务性能等。
- **开放性和可迁移性**：EPOC可作为即插即用的图像标记器，适用于各种需要图像标记化的场景（如VLM、视频处理等），且已开源。

## 8. 不足与局限

- **细粒度结构局限**：边界预测模型基于SegFormer，特征图分辨率仅为输入的1/4，导致非常细或薄的物体（如头发、小字体）可能无法精确分割。
- **外在评估规模有限**：使用的LLM最大仅1.7B参数，远小于当前主流大模型（如70B+）。在更大模型上是否保持优势存疑。
- **额外预处理开销**：EPOC仍需一个独立的分割步骤（即使较轻量），在延迟敏感的实时应用中可能成为瓶颈。论文承认此问题，但认为在重型VLM训练/推理中可被抵消。
- **缺少与SAM的直接外部对比**：由于SAM效率太低，论文未在VLM训练中直接比较SAM与EPOC，削弱了“子对象级”优势的说服力。
- **可解释性和信息损失**：自适应分割本质上是丢弃了段内空间结构（如纹理细节），这可能在需要像素级编辑或超精细分辨率任务中造成信息丢失。论文类比了子词在字符级任务中的劣势。
- **语种与场景偏差**：所有评估集中在自然场景（COCO、SA-1B等），未涉及医学图像、卫星图像等特殊领域，通用性有待验证。

（完）
