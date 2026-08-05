---
title: "Cyto-SSL: A Self-Supervised Pretraining Framework for Cytology Foundation Model"
title_zh: Cyto-SSL：一种用于细胞学基础模型的自监督预训练框架
authors: "Yiming Zhang, Rui Yan, Xiaohua Wan, Yifan Zhao, Shuang Feng, Zhetao Xu, Ying Wang, Fa Zhang, Bin Hu"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/38289/42251"
tags: ["query:cellseg"]
score: 4.0
evidence: 细胞病理学图像的自监督预训练框架，通过核中心扰动学习细胞特征
tldr: 针对细胞学图像缺乏有效预训练基础模型的问题，本文提出了首个面向细胞病理学的自监督框架Cyto-SSL，设计了以细胞核为中心的扰动策略和对比学习来提取判别性细胞特征，可视为从细胞图像中抽取特征的工具。该方法在多个细胞学分类和检测任务上取得了性能提升，验证了其在计算细胞学中迁移学习的价值。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38289/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 870, \"height\": 442, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38289/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1833, \"height\": 734, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38289/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 709, \"height\": 1637, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38289/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 884, \"height\": 825, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38289/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1651, \"height\": 1219, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38289/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 856, \"height\": 519, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38289/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 751, \"height\": 418, \"label\": \"Table\"}]"
motivation: 细胞学图像稀疏且无组织，缺乏有效的预训练基础模型，限制了细胞病理学模型的迁移性。
method: 提出以细胞核为中心的扰动策略和对比学习，从液基薄层细胞学图像中学习细胞核和胞浆特征。
result: 在细胞学分类和检测任务上取得性能提升，验证了预训练的有效性。
conclusion: Cyto-SSL是首个细胞学图像自监督框架，通过核中心扰动学习判别性细胞特征，推动了细胞病理学基础模型发展。
---

## Abstract
Cytological images originate from exfoliated cells, collected via liquid-based slides and digitized into whole slide images (WSIs). Unlike histological WSIs that exhibit continuous and well-structured tissue, cytological WSIs are sparse in spatial distribution and unstructured in cellular relationships. Typically, the nucleus serves as the primary diagnostic feature, while surrounding cytoplasmic information plays a supportive role. These unique characteristics limit the development of effective foundation models and hinder the transferability of histology-based models for cytopathology. To address this, we propose **Cyto-SSL**, the first self-supervised pretraining framework for cytological images. It introduces **Nuclei-Centered Perturbation**, which highlights individual nuclei by perturbing non-nuclear regions. We also design an SR-Transformer module, which complements this by using sparse attention to concentrate on diagnostically relevant scattered cells, while iRPE helps model to capture local spatial relationships and avoids unnecessary attention to irrelevant global structures. Experimental results show that **Cyto-SSL** enhances performance across diverse cytological datasets and Multiple Instance Learning (MIL) methods. On a WSI-level dataset, it achieved 95.67% accuracy and outperformed ImageNet-pretrained ResNet-50 by 11.33%, demonstrating superior feature representation for cytological analysis. Additionally, **Cyto-SSL** modules are plug-and-play, easily integrated into other pretraining frameworks, yielding a 2.6% accuracy gain across different SSL methods.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义

*   **研究背景与动机**
    *   细胞病理学图像（如宫颈、乳腺、血液涂片）在早期癌症检测中至关重要。与传统组织病理学图像不同，细胞学图像具有**细胞空间分布稀疏**和**细胞间关系非结构化**的显著特点。
    *   在诊断中，**细胞核**是核心诊断特征，细胞质起辅助作用（如判断核质比）。
    *   现有的自监督预训练模型（如DINO, MoCo）大多为连续、结构化的组织病理学图像设计，学习全局特征。由于自然图像或组织学图像与细胞学图像差异巨大，这些模型在细胞学任务上迁移效果不佳，导致细胞病理学领域缺乏有效的专用基础模型。

*   **核心问题与整体含义**
    *   本文旨在解决**如何针对细胞学图像的稀疏性和非结构化特性，设计一个专用的自监督预训练框架**，以训练出一个能够聚焦于诊断关键区域（细胞核）的高质量细胞学基础模型。

### 2. 论文提出的方法论

Cyto-SSL 的核心思想是通过**引导模型关注细胞核区域**，并**抑制对无效背景和全局无关结构的关注**，来学习更具判别性的细胞学特征。该框架主要包括两大组件：

*   **整体架构：师生蒸馏**
    *   采用DINO等框架中的师生网络结构，学生网络从教师网络学习，通过最小化两者输出的交叉熵损失来更新参数，避免了负样本需求，适合细胞学图像的语义稀疏性。教师网络通过学生权重的指数移动平均更新。

*   **核心组件一：核中心扰动**
    *   一种新型视图生成策略，旨在生成以细胞核为中心的增强视图，显式引导模型关注诊断相关区域。
    *   **流程**：
        1.  **细胞核检测**：使用预训练的CellViT模型（冻结权重）定位图像中的细胞核位置。
        2.  **背景扰动**：在细胞核周围半径（$r=50$ 像素）之外的区域，随机打乱像素，以破坏无关背景结构，同时保留核及周围关键细胞质信息。
        3.  **视图生成**：以细胞核位置为中心，应用随机缩放、旋转、色彩抖动等增强，生成多尺度视图。

*   **核心组件二：SR-Transformer**
    *   集成到ViT中的即插即用模块，包含两个关键设计来增强特征提取：
    *   **稀疏自注意力**：仅保留查询与键的点积得分矩阵中每行的前$h$（$h=16$）个最大值，其余置为负无穷。这使得注意力强制集中在少数最相关的 token 上，有效抑制了噪声和无关背景，突出稀疏分布的诊断性细胞核。
    *   **图像相对位置编码**：在计算注意力分数时引入了一个可学习的相对位置偏置矩阵$R$，同时对值矩阵也引入相对位置偏置$rV$。这有助于模型捕捉局部细胞的空间关系，而无需依赖导致误导的全局绝对位置结构。

### 3. 实验设计

*   **数据集**
    *   **预训练数据集**：私有的**Cervical Cytologic WSI 数据集**（760张WSI，40倍放大，约80,000 × 80,000像素，二分类标签）。
    *   **下游任务数据集**：
        *   **FNAC 2019**：公开乳腺细胞学图像数据集（212张，良性/恶性）。
        *   **NIH-NLM Thin Blood Smears Pf**：公开疟疾血涂片数据集（965张，阴性/阳性）。

*   **评估基准与对比方法**
    *   **基准模型**：ImageNet 预训练的 ResNet-50、DINO V2、Prov-GigaPath（组织病理学基础模型，用 LoRA 微调）。
    *   **下游MIL分类器**：ABMIL, TransMIL, DTFD-MIL, CLAM-SB, DSMIL, LESS（细胞学专用方法）。
    *   **自监督框架（用于即插即用验证）**：SimCLR, MoCo, DINO。
    *   **评价指标**：AUC, ACC, Recall。

### 4. 资源与算力

*   论文中提到实验基于一台配备 Intel Core i9-14900K CPU 和 **NVIDIA RTX 4090 GPU** 的工作站。预训练阶段使用了包含250万个40倍放大病理块的私有数据集。
*   **未明确说明**：论文未提及使用的GPU数量、具体的预训练总时长或每个epoch的耗时。

### 5. 实验数量与充分性

*   **实验数量**：进行了约 3 组主要类型的实验，覆盖度较好。
    1.  **与主流特征提取器及MIL方法结合的全面对比**：在3个数据集上，将所提方法与3种基准编码器及**6种MIL方法**组合，形成了大量对比实验。
    2.  **消融实验**：在2种MIL方法上，针对“核中心扰动”、“稀疏自注意力”、“iRPE”三个模块单独和组合的作用进行了消融。
    3.  **跨框架即插即用验证**：与**3种主流SSL框架**（SimCLR， MoCo, DINO）集成，验证其通用性。
    4.  **模型注意力可视化分析**：定性展示了模型是否聚焦于关键区域。
*   **充分性与客观性评估**：
    *   **充分**：实验设计系统且全面，覆盖了多个维度（不同数据集、不同MIL方法、不同SSL框架、内部模块消融）。
    *   **客观公平**：对比时固定了其他设置（如MIL分类器配置），仅替换特征提取器，确保了比较的公平性。结果呈现了一致性的提升，证据较为扎实。

### 6. 论文的主要结论与发现

*   Cyto-SSL在所有三个细胞学数据集和多种MIL方法上，性能一致且显著优于基于ImageNet的ResNet-50、组织病理学基础模型Prov-GigaPath和DINO V2。在私有宫颈细胞学WSI数据集上，准确率最高达 **95.67%**，相比ResNet-50提升**11.33%**。
*   其关键模块“核中心扰动”和“SR-Transformer”可以即插即用，集成到SimCLR、MoCo、DINO等不同自监督框架后，均能带来约2.6%的性能提升。
*   注意力图可视化证明，Cyto-SSL成功引导模型将注意力聚焦于诊断相关的细胞核和细胞质区域，而非背景杂质，解释了其性能提升的原因。
*   在细胞学任务中，简单的MIL方法（如ABMIL）表现可能优于为密集组织设计的方法（如TransMIL，DTFD-MIL），凸显了针对细胞学稀疏性特点进行适配的必要性。

### 7. 优点

*   **问题导向性强，创新点明确**：首次系统性针对细胞学图像“稀疏”和“非结构化”两大核心难题设计预训练框架，非简单迁移。
*   **方法论设计精巧互补**：“核中心扰动”从数据增强层面、“SR-Transformer”从模型架构层面，两者协同增强模型对关键特征的学习能力。
*   **泛化性和即插即用特性**：在多个数据集、多种MIL方法和多种SSL框架下均表现鲁棒且有效，证明了其作为通用模块的巨大潜力。
*   **解释性好**：通过注意力图可视化，清晰展示了方法聚焦诊断区域的机制，增强了模型的可信度。

### 8. 不足与局限

*   **预训练数据来源单一**：预训练仅在单一的私立宫颈细胞学数据集上进行，模型的泛化性可能受限于该数据分布，向更多类型细胞学样本（如胸腹水、痰液）的迁移能力有待验证。
*   **模型规模较小**：实验采用的基础模型为ResNet-50或ViT-tiny，未探索在更大参数量模型（如ViT-Base/Large）上的扩展效果，可能限制了其性能上限。
*   **对细胞核分割模型的依赖**：其核心的“核中心扰动”策略强依赖于外部细胞核分割模型（CellViT）的性能。若该模型在某些罕见或异常细胞形态下检测不准，会直接影响预训练质量。
*   **对比基线略显老旧或非最优**：虽然对比了DINO V2和Prov-GigaPath，但作为发表于2026年的会议，未对比同年或更近期提出的其他先进病理基础模型。此外，对于组织病理学模型的迁移，仅使用了LoRA微调，可能不是最有效的域适应策略。

（完）
