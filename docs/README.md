<div class="dpr-home-notice-card">
  <h3 class="dpr-home-notice-title">🚀 Start Here</h3>
  <ul class="dpr-home-notice-list">
    <li><a href="#/tutorial/README">使用教程</a></li>
  </ul>
</div>

## 每次日报
- 最新运行日期：2026-05-27 ~ 2026-06-25
- 运行时间：2026-06-25 08:17:22 UTC
- 运行状态：成功
- 本次总论文数：18
- 精读区：10
- 速读区：8

### 今日简报（AI）
今日聚焦病理AI前沿：精读18篇论文中，基础模型SegTME-UNI2和参数高效ViT分别拿下10分与9分，揭示通用细胞分割与多任务学习新范式。  
最值得关注：LLM正从组织微环境表征渗入疤痕临床分析，且上下文多示例学习、可学习Token稀疏化让十亿像素WSI推理更高效。  
建议读者紧随“基础模型+LLM+高效推理”三角趋势，重点实验SegTME-UNI2和子空间解耦策略在自家病理数据上的迁移效果。
- 详情：[/20260527-20260625/README](/20260527-20260625/README)

### 精读区论文标签
1. [SegTME-UNI2: A Foundation Model-Based Framework for Generalisable Multiclass Cell Segmentation and LLM-Driven Tumour Microenvironment Characterisation in Histopathology](/20260527-20260625/2606.17702v2-segtme-uni2-a-foundation-model-based-framework-for-generalisable-multiclass-cell-segmentation-and-llm-driven-tumour-microenvironment-characterisation-in-histopathology)  
   标签：评分：10.0/10、query:cellseg
   evidence：双头解码器统一框架，同时进行六类语义分割和基于分水岭的核实例分离，联合预测细胞类别标签和边界
2. [Parameter-Efficient Subspace Decoupling ViT for Mitigating Multi-Task Negative Transfer in Histological Scoring](/20260527-20260625/2605.29852v1-parameter-efficient-subspace-decoupling-vit-for-mitigating-multi-task-negative-transfer-in-histological-scoring)  
   标签：评分：9.0/10、query:profile
   evidence：使用子空间解耦ViT对形态学特征进行多任务组织学评分
3. [Symb-xMIL: Symbolic Explanations for Multiple Instance Learning in Digital Pathology](/20260527-20260625/2606.06224v1-symb-xmil-symbolic-explanations-for-multiple-instance-learning-in-digital-pathology)  
   标签：评分：9.0/10、query:wsi-mil
   evidence：数字病理学中多实例学习的符号解释
4. [Symb-xMIL: Symbolic Explanations for Multiple Instance Learning in Digital Pathology](/20260527-20260625/2606.06224v2-symb-xmil-symbolic-explanations-for-multiple-instance-learning-in-digital-pathology)  
   标签：评分：9.0/10、query:wsi-mil
   evidence：通过符号规则量化MIL证据组合方式，实现图块重要性估计和判别区域识别
5. [Stain-Aware Wavelet Regularization for Instant Adversarial Purification in Histopathology](/20260527-20260625/2606.08745v1-stain-aware-wavelet-regularization-for-instant-adversarial-purification-in-histopathology)  
   标签：评分：9.0/10、query:pathology-ai
   evidence：用于计算病理学管道中组织病理学图像的对抗性净化框架
6. [Predicting Immune Biomarkers with MultiModal Mixture-of-Expert Pathology Foundation Models Empowers Precision Oncology](/20260527-20260625/2606.18123v2-predicting-immune-biomarkers-with-multimodal-mixture-of-expert-pathology-foundation-models-empowers-precision-oncology)  
   标签：评分：9.0/10、query:pathfeat
   evidence：整合病理基础模型，从H&E图像中提取图像块级表示，用于像素级和切片级免疫生物标志物预测
7. [Performance and Interpretability of Convolutional, Transformer, and Hybrid Deep Learning Models in Colorectal Histology Classification](/20260527-20260625/2606.23744v1-performance-and-interpretability-of-convolutional-transformer-and-hybrid-deep-learning-models-in-colorectal-histology-classification)  
   标签：评分：9.0/10、query:pathology-ai
   evidence：对结直肠组织学分类中CNN、Transformer和混合模型的比较评估
8. [A Leakage-Aware Comparative Benchmark of Machine Learning, Deep Learning, and Transformer Models for Reliable Leukemia Detection](/20260527-20260625/2606.24944v1-a-leakage-aware-comparative-benchmark-of-machine-learning-deep-learning-and-transformer-models-for-reliable-leukemia-detection)  
   标签：评分：9.0/10、query:cellseg
   evidence：对从外周血涂片显微镜图像中分类急性淋巴细胞白血病的机器学习与深度学习模型进行基准测试
9. [C2RM-Seg: Causal Counterfactual Reasoning with Structural-Semantic Priors for Weakly Supervised Histopathological Tissue Segmentation](/20260527-20260625/2606.25508v1-c2rm-seg-causal-counterfactual-reasoning-with-structural-semantic-priors-for-weakly-supervised-histopathological-tissue-segmentation)  
   标签：评分：9.0/10、query:wsi-mil
   evidence：通过因果类激活图优化的弱监督组织病理学组织分割，识别判别区域
10. [AutoMedBench: Towards Medical AutoResearch with Agentic AI Models](/20260527-20260625/2606.01961v1-automedbench-towards-medical-autoresearch-with-agentic-ai-models)  
   标签：评分：8.0/10、query:pathology-ai
   evidence：面向医学自主AI智能体的基准测试，包含分割等长期任务，能够评估自主特征发现能力

### 速读区论文标签
1. [When LLMs Analyze Scars: From Images to Clinically-Meaningful Features](/20260527-20260625/2606.18063v1-when-llms-analyze-scars-from-images-to-clinically-meaningful-features)  
   标签：评分：8.0/10、query:pathology-ai
   evidence：利用LLM作为知识驱动的特征工程器从疤痕图像中提取临床有意义特征
2. [In-Context Multiple Instance Learning](/20260527-20260625/2606.06458v1-in-context-multiple-instance-learning)  
   标签：评分：7.0/10、query:wsi-mil
   evidence：上下文MIL袋级分类，适用于计算病理学
3. [Learnable Token Sparsification for Efficient Gigapixel Whole Slide Image Reasoning](/20260527-20260625/2606.08641v1-learnable-token-sparsification-for-efficient-gigapixel-whole-slide-image-reasoning)  
   标签：评分：7.0/10、query:wsi-mil
   evidence：可学习标记稀疏化用于千兆像素全切片图像，学习选择重要视觉标记，类似判别性图块选择
4. [DANTE: A Reference-Guided Unsupervised Pipeline for Extended-Transient Anomaly Characterization in LIGO O4a](/20260527-20260625/2606.25702v1-dante-a-reference-guided-unsupervised-pipeline-for-extended-transient-anomaly-characterization-in-ligo-o4a)  
   标签：评分：7.0/10、query:wsi-mil
   evidence：使用多实例学习(MIL) top-k池化进行频谱图异常表征，展示了图块重要性估计
5. [Multimodal Brain Tumour Classification Using Feature Fusion](/20260527-20260625/2606.11107v1-multimodal-brain-tumour-classification-using-feature-fusion)  
   标签：评分：6.0/10、query:pathfeat
   evidence：融合CNN图像特征与手工放射组学特征的多模态脑肿瘤分类
6. [Essential Subspace Merging for Multi-Task Learning](/20260527-20260625/2606.19164v2-essential-subspace-merging-for-multi-task-learning)  
   标签：评分：6.0/10、query:cellseg
   evidence：通过本质子空间分解实现多任务模型合并
7. [Robust Image-Driven Phenotyping of Ovarian Tumor Cells using Optimized Dynamic Features in Hyperbolic Channels](/20260527-20260625/2606.20703v1-robust-image-driven-phenotyping-of-ovarian-tumor-cells-using-optimized-dynamic-features-in-hyperbolic-channels)  
   标签：评分：6.0/10、query:pathology-ai
   evidence：基于图像的细胞力学表型分析，提取形态动力学与运动学特征
8. [Contrastive and Adaptive Multi-modal Masked Autoencoder for Spatial Transcriptomics](/20260527-20260625/2606.21156v1-contrastive-and-adaptive-multi-modal-masked-autoencoder-for-spatial-transcriptomics)  
   标签：评分：6.0/10、query:pathfeat
   evidence：利用掩码自编码器从H&E组织学图像中预测基因表达，实现图块级表征学习


<div class="dpr-home-promo-card">
  <h3 class="dpr-home-promo-title">💬 社区与支持</h3>
  <ul class="dpr-home-promo-list">
    <li>欢迎 Star / Fork / Issue / PR</li>
    <li>QQ群：583867967（欢迎交流，已有：1151人）</li>
  </ul>
</div>
