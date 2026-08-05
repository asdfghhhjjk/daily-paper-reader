---
title: Low-rank Interpretable Cell–Cell Hidden Interactions from Embeddings
title_zh: 基于低秩可解释嵌入的细胞间隐藏相互作用发现
authors: "Noga Mudrik, Zoe Piran, Paula Coelho, Linh Thi Thuy Trinh, TAKAMASA KUDO, Aviv Regev"
date: 2025-09-20
pdf: "https://openreview.net/pdf?id=Qu2A8wBTBJ"
tags: ["query:cellseg"]
score: 7.0
evidence: 从嵌入中推断可解释的细胞间相互作用，可用于数字病理中的肿瘤微环境分析。
tldr: 针对活细胞成像中细胞间相互作用的动态建模挑战，该论文提出LICCHIE模型，使用动态多特征向量和低秩点积来推断时变、基于特征的细胞间交互。该方法不依赖于特定生物系统，能够揭示细胞群体在空间和时间上的隐藏相互作用。在数字病理分析中，该模型有望用于解析肿瘤微环境中的细胞通信模式，为从细胞分割结果中构建可解释的空间证据提供新途径。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 现有方法难以建模活细胞成像中复杂的细胞间动态交互。
method: 提出LICCHIE模型，用动态多特征向量表示细胞，低秩点积推断交互关系。
result: 成功识别不同系统和条件下的细胞间相互作用，体现可解释性。
conclusion: 该方法为从细胞成像数据中提取空间交互特征提供了通用工具，可应用于肿瘤微环境分析。
---

## Abstract
Multicellular organisms rely on continuously changing cell–cell interactions that govern critical biological processes as cells modify their internal states and trajectories in space over time. Studying these interactions is critical to understand development, homeostasis, and disease progression. Live-cell imaging provides a unique opportunity to directly observe these dynamical events; however, current computational approaches often fail to model complex, time-varying events involving diverse populations and spatial contexts. Here, we present LICCHIE, a model designed to infer time-changing, feature-based cell-cell interactions, applicable across systems and conditions. Our approach represents each cell with a dynamic multi-feature vector, and interactions are modeled as spatially constrained, directed influences between cell pairs, evolving over time. We optimize the model using an iterative scheme balancing data fidelity, interactions smoothness, and low-rank sparse structure. We validated LICCHIE’s ability to capture cellular interactions across populations in a controlled synthetic setting and applied it to real-world 3D live-cell imaging of patient-derived tumor organoids to (1) identify components with interpretable structures that capture interaction type and directionality, and (2) suggest modulation strategies that may accelerate Natural Killer (NK) polarization and tumor cell death.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义
- **核心问题**：在活细胞成像中，多细胞生物的细胞间相互作用是动态、时变且依赖于空间环境的，但现有的计算方法往往难以建模这类涉及多种细胞群和空间背景的复杂事件。
- **研究动机**：准确理解这些相互作用对于揭示发育、组织稳态和疾病进展等关键生物学过程至关重要。
- **整体含义**：论文试图提供一种通用、跨系统和跨条件的方法，从细胞嵌入中自动推断隐藏的、可解释的细胞间交互模式，尤其面向肿瘤微环境等数字病理场景。

### 2. 论文提出的方法论
- **核心思想**：以**低秩可解释的细胞间隐藏相互作用（LICCHIE）**模型为核心，将每个细胞表示为**动态多特征向量**，并将细胞间相互作用建模为**受空间约束、有方向性、随时间演化**的影响。
- **关键技术细节**：
  - **嵌入表示**：每个细胞用一个随时间变化的特征向量来表征其内部状态。
  - **交互推断**：利用**低秩点积**来推断成对细胞之间基于特征的相互作用，低秩结构兼具稀疏性和可解释性。
  - **优化目标**：通过迭代优化方案，在**数据保真度**、**交互平滑性**和**低秩稀疏结构**之间取得平衡。
- **算法流程（文字说明）**：给定多细胞时空数据，首先为每个细胞提取动态多特征嵌入；然后，在空间邻近性约束下，通过低秩矩阵分解的方式学习细胞对之间的有向影响强度，并确保交互模式随时间是平滑变化的；最后，从分解的组分中解析出具有生物可解释性的交互类型和方向性。

### 3. 实验设计
- **数据集/场景**：
  - **受控合成数据**：用于验证模型在已知交互规则下捕获不同细胞群体间相互作用的能力。
  - **真实世界数据**：患者来源的**3D 活细胞成像肿瘤类器官**，重点分析自然杀伤（NK）细胞与肿瘤细胞之间的动态互动。
- **Benchmark 与对比方法**：**原文摘要未提及具体的对比方法或基准模型**，无法判断是否与已有方法（如 CellChat、NicheNet、图神经网络等）进行过直接比较。
- **任务目标**：
  - 识别具有可解释结构的交互成分，捕捉交互的类型和方向性。
  - 提出可能加速 NK 细胞极化和肿瘤细胞死亡的调节策略。

### 4. 资源与算力
- **文中未明确说明所使用的 GPU 型号、数量、训练时长等算力信息**。由于摘要和元数据中没有提及相关细节，该部分无法评估。

### 5. 实验数量与充分性
- **实验组数**：明确提到的实验场景包括**1 组合成数据实验**和**1 组真实肿瘤类器官实验**。未提及多组不同数据集、跨物种或系统的对比，也未提供消融实验（如去除低秩约束、去除时序平滑项）的相关描述。
- **充分性与公平性**：
  - 基于当前摘要，实验规模较为有限，缺少与前沿方法的横向对比，难以全面证明方法的优越性。
  - 合成实验可控性强，能够验证核心推断能力；真实数据应用展示了潜在转化价值，但整体实验的客观性和泛化性证据尚不充分。

### 6. 论文的主要结论与发现
- LICCHIE 能够**成功识别不同生物系统和条件下细胞间的时变相互作用**。
- 模型推断的**低秩组件具有可解释的结构**，可以明确表征交互的类型和方向性。
- 在肿瘤类器官中，该方法不仅重建了 NK 细胞与肿瘤细胞之间的通信模式，还能为**加速免疫细胞杀伤肿瘤提供可能的调制策略**。
- 总体提供了一个**从细胞成像数据中提取空间交互特征的通用计算工具**，有望拓展到肿瘤微环境分析等数字病理任务。

### 7. 优点
- **动态建模能力**：明确考虑交互随时间演变，契合活细胞成像的特性。
- **可解释性设计**：利用低秩点积和多特征向量，使得交互成分具备生物学解释性，便于下游分析。
- **空间约束集成**：将空间邻近性纳入模型，更符合细胞间接触性信号传递的实际机制。
- **跨系统适用性**：不依赖特定生物系统或标记，具有作为通用分析框架的潜力。

### 8. 不足与局限
- **实验对比缺失**：摘要未提及任何基线方法，无法评估 LICCHIE 相对于现有细胞间相互作用推断工具的性能优劣。
- **验证规模有限**：仅展示了合成数据和单一真实数据集的结果，需要更多不同类型组织、不同扰动的实验来证明稳健性。
- **技术细节缺失**：从摘要难以判断对数据噪声、缺失值、细胞分割质量等的鲁棒性，以及模型超参数的敏感性。
- **应用限制**：虽提及用于肿瘤微环境分析，但当前结果仅基于体外类器官，距离真正的临床病理应用仍有距离。

（完）
