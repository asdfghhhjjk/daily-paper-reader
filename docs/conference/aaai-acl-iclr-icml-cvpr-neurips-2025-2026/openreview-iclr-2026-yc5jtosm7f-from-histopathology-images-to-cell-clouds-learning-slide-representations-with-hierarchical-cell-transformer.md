---
title: "From Histopathology Images to Cell Clouds: Learning Slide Representations with Hierarchical Cell Transformer"
title_zh: 从组织病理图像到细胞云：用层次化细胞转换器学习切片表示
authors: "Zijiang Yang, Zhongwei Qiu, Tiancheng Lin, Hanqing Chao, Wanxing Chang, Yelin Yang, Yunshuo Zhang, Wenpei Jiao, Yixuan Shen, Wenbin Liu, Dongmei Fu, Dakai Jin, Ke Yan, Le Lu, Hui Jiang, Yun Bian"
date: 2025-09-02
pdf: "https://openreview.net/pdf?id=yC5jtOSm7F"
tags: ["query:cellseg"]
score: 10.0
evidence: 将WSI建模为细胞云，直接利用细胞空间分布进行切片表示学习
tldr: 针对现有方法忽略细胞空间分布的重要性，提出将全切片视为细胞云并通过层次化细胞转换器直接建模细胞分布，结合人机协同标注优化细胞检测，在病理图像分析中捕获了更精细的语义信息。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 传统WSI分析忽略细胞分布，但细胞空间排列具有临床意义。
method: 提出人机协同标签细化方法优化细胞检测，并设计层次化细胞转换器建模细胞云。
result: 在多个WILu测试上，细胞云表示优于标准图像表示，提高了下游任务性能。
conclusion: 直接建模细胞分布为病理图像分析开辟了新范式，尤其适用于微环境分析。
---

## Abstract
It is clinically crucial and potentially beneficial to analyze and directly model the spatial distributions of cells in histopathology whole slide images (WSI). However, existing methods typically analyze WSIs via image representation learning and ignore the importance of cell distributions. Thus, it remains an open question whether deep learning models can directly and effectively analyze WSIs from the semantic aspect of cell distributions. In this work, we argue that each WSI can be regarded as a collection of cells and propose a new scheme consisting of cell detection and cell cloud modeling to tackle these challenges. Firstly, we propose a novel human-in-the-loop label refinement method to finetune the pretrained cell detection and classification model. Then, a novel hierarchical Cell Cloud Transformer (CCFormer) is proposed to model the cell spatial distribution. Specifically, a Neighboring Information Embedding module is proposed to characterize the distribution of cells within the cell neighborhood, and a Hierarchical Spatial Perception module is proposed to learn the spatial relationship among cells in a bottom-up manner. Clinical analysis indicates that clinical evaluation metrics directly based on counting cells can effectively assess patients' survival risk, offering significant potential for analyzing and modeling cell distribution in WSIs. Besides, extensive experiments on survival prediction and cancer staging show that CCFormer achieves state-of-the-art performances and evidently outperforms other competing methods by learning from cell spatial distribution alone.

---

## 论文详细总结（自动生成）

# 论文详细总结：从组织病理图像到细胞云：用层次化细胞转换器学习切片表示

## 1. 论文的核心问题与整体含义

- **研究背景与动机**：在组织病理全切片图像（WSI）分析中，细胞的**空间分布与排列模式**具有重要的临床意义（如肿瘤微环境评估、患者预后判断）。然而，现有主流方法通常将 WSI 视为普通的巨幅图像，通过图像级表示学习提取特征，**忽略了细胞分布这一高层语义信息**。
- **核心问题**：深度学习模型能否**直接、有效地从细胞分布的语义层面**对 WSI 进行分析，而非仅仅依赖像素/图像块特征？这仍是一个开放问题。
- **整体含义**：论文主张将每个 WSI 重新定义为“**细胞云**”（cell cloud）——一个细胞的集合，其空间分布本身就蕴含了丰富的诊断与预后信息。由此提出一种**从细胞检测到细胞云建模**的全新范式，绕过传统图像特征提取路径，直接利用细胞空间位置的集合来实现切片表示学习。

## 2. 论文提出的方法论

### 2.1 总体框架
- 两阶段方案：
  1. **细胞检测与分类**：利用预训练模型获得单个细胞的类别与坐标。
  2. **细胞云建模**：将细胞集合（点云）输入到提出的层次化 Cell Transformer（CCFormer）中进行空间关系学习，产生整张切片的表示。

### 2.2 关键技术细节

- **人机协同标签细化（Human-in-the-loop label refinement）**
  - 目的：细胞检测预训练模型可能存在标注误差或领域偏移，通过少量人工纠正与模型再训练，在细胞级检测与分类上实现更高精度的微调。
  - 过程概览：基于初始预训练模型的输出进行人工审核与修正，形成高质量伪标签，再用以微调检测/分类模型，迭代提升细胞级别的检测质量。

- **层次化细胞云转换器（CCFormer）**
  - **邻近信息嵌入（Neighboring Information Embedding, NIE）模块**：对每个细胞，提取其邻域内其他细胞的空间分布特征，刻画局部细胞环境。
  - **层级空间感知（Hierarchical Spatial Perception, HSP）模块**：以自底而上的方式逐步聚合细胞之间的空间关系：
    - 底层：学习局部细胞群组模式；
    - 中层：从局部组群模式到更大区域的上下文；
    - 顶层：形成全切片级别的空间结构表示。
  - 整体架构可视为一种专门针对细胞点云的层次化 Transformer。

### 2.3 算法流程（文字描述）
1. 将 WSI 输入微调后的细胞检测模型，得到每个细胞的坐标及类别标签（细胞云）。
2. 细胞云经过 NIE 模块，为每个细胞生成局部空间嵌入向量。
3. HSP 模块对局部嵌入进行多层聚合，利用自注意力机制捕捉长、短程空间依赖关系。
4. 最终输出一个全局特征向量，作为该 WSI 的细胞分布表示，用于下游任务（如生存预测、癌症分期）。

## 3. 实验设计

- **数据集/场景**：文中提到**多个 WSI 数据集**（未在摘要中给出具体名称），以及**生存预测**和**癌症分期**两个下游任务，说明实验涵盖预后预测与诊断分期等临床场景。
- **Benchmark 与对比方法**：
  - 与现有**图像表示学习方法**进行对比（即从图像块提取特征的方法），表明仅靠细胞分布即可超越这些方法。
  - 还对比了其他竞争性方法，具体名称未在摘要中列出。
- **量化结果**：CCFormer 在生存预测与癌症分期任务上均取得了**state-of-the-art 性能**，且**明显优于**其他方法。

## 4. 资源与算力

- 摘要与提供的元数据中**未明确说明** GPU 型号、数量、训练时长或单次实验计算开销等信息。因此无法评估其算力需求或资源消耗，需从全文获取更详细数据。

## 5. 实验数量与充分性

- 根据摘要，至少包含以下实验组：
  - 多个数据集上的生存预测、癌症分期任务对比实验；
  - 与标准图像表示方法及其他竞争方法的性能比较；
  - 人机协同标注方法的有效性评估（隐含在细胞检测精度的提升中，但摘要未给出消融细节）；
  - 临床评价指标（如基于计数的细胞指标）与患者生存风险的关联分析。
- **充分性评判**：摘要透露实验覆盖了多任务、多方法对比和临床关联分析，看似较为全面，但**缺少消融实验、跨中心验证、细胞检测误差分析等细节**，无法断定是否完全客观公平。作者称其方法“仅从细胞空间分布学习”即取得优势，这需要更系统的消除混淆因素的实验设计来支持。

## 6. 论文的主要结论与发现

- 临床分析表明，直接基于**细胞计数的评价指标**能够有效评估患者生存风险，验证了细胞分布具有独立于图像纹理的预后价值。
- 提出的 CCFormer 分别以细胞云为唯一输入，在生存预测和癌症分期上达到 SOTA 性能，**显著超越**传统的基于图像块表示的方法。
- **结论**：直接对细胞空间分布进行建模，为组织病理图像分析提供了一种**全新的范式**，特别适用于肿瘤微环境分析等需要精细细胞空间信息的场景。

## 7. 优点

- **范式创新性**：首创将 WSI 建模为“细胞云”并用 Transformer 直接学习空间分布表示，跳出了图像块嵌入的传统框架，开辟了语义级别的新方向。
- **临床相关性**：通过细胞分布与生存风险的关联，赋予方法更强的医学可解释性，与病理学临床实践（如微环境评估）高度契合。
- **技术贡献**：
  - 人机协同标签细化方法，提升细胞检测质量；
  - 为细胞云定制的层次化 Transformer（NIE + HSP）架构，有效捕获局部与全局空间模式。
- **实验说服力**：在多任务、多方法比较下取得 SOTA，且表示学习仅基于细胞分布，显示出方法的潜力。

## 8. 不足与局限

- **信息缺失**：摘要未提供具体数据集、对比方法名称和消融实验结果，难以评估实验的全面性与公平性。
- **依赖细胞检测质量**：整个流程建立在细胞检测/分类精度之上，如果细胞检测不准，细胞云建模将引入噪声，尽管作者提出了标签细化策略，但对检测错误的鲁棒性未在摘要中展示。
- **复杂性与资源需求**：需要先运行细胞检测模型，再于大量细胞点上进行 Transformer 运算，可能带来较高的计算开销和内存需求，但无具体数据支持。
- **通用性未验证**：仅凭摘要无法确认方法在不同器官、不同染色条件的病理切片上的泛化能力，以及是否适用于无细胞分割标注的弱监督场景。

（完）
