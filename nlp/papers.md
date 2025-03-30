# Papers

## Word Vectors and Embeddings
- **Efficient Estimation of Word Representations in Vector Space**
  - **发表年份**: 2013
  - **引用**: 30701
  - **作者及所属实验室**:  
    - Tomas Mikolov: Google Inc.  
    - Kai Chen: Google Inc.  
    - Greg Corrado: Google Inc.  
    - Jeffrey Dean: Google Inc.  
  - **核心贡献**:  
    1. 提出了**CBOW（Continuous Bag-of-Words）**和**Skip-gram**两种高效模型架构，用于从大规模语料库中学习高质量词向量。  
    2. 在保持低计算成本（如1.6亿词数据集训练时间小于1天）的同时，显著提升了词向量在句法和语义相似性任务上的性能。  
    3. 设计了综合性测试集验证词向量的线性规律性（如"King - Man + Woman ≈ Queen"），并开源了模型实现以推动后续研究。

- **Distributed Representations of Words and Phrases and their Compositionality**
  - **发表年份**: 2013
  - **引用**: 32961
  - **作者及所属实验室**:  
    - Tomas Mikolov: Google Inc.  
    - Ilya Sutskever: Google Inc.  
    - Kai Chen: Google Inc.  
    - Greg Corrado: Google Inc.  
    - Jeffrey Dean: Google Inc.  
  - **核心贡献**:  
    1. 提出了**高频词子采样**方法，显著提升训练速度并改善低频词的向量质量；引入**负采样（Negative Sampling）**作为分层softmax的高效替代方案。  
    2. 开发了一种基于统计的短语识别方法，成功将Skip-gram模型扩展到短语表示，解决了组合语义（如"Air Canada"）无法通过单词向量简单叠加表达的问题。  
    3. 首次系统验证了词向量的**线性组合特性**（如vec("Germany") + vec("capital") ≈ vec("Berlin")），揭示了分布式表示在语义组合上的数学可解释性。
  
- **GloVe: Global Vectors for Word Representation**
  - **发表年份**: 2014
  - **引用**: 31381
  - **作者及所属实验室**:  
    - Jeffrey Pennington: 斯坦福大学计算机科学系  
    - Richard Socher: 斯坦福大学计算机科学系  
    - Christopher D. Manning: 斯坦福大学计算机科学系  
  - **核心贡献**:  
    1. 提出了**全局对数双线性回归模型（GloVe）**，结合了矩阵分解（如LSA）和局部上下文窗口方法（如skip-gram）的优势，通过词-词共现矩阵的全局统计信息生成词向量。  
    2. 设计了**加权最小二乘损失函数**，有效利用稀疏共现矩阵的非零元素，解决了传统方法对低频/高频词处理不佳的问题。  
    3. 在词类比任务上达到75%准确率（SOTA），并在词相似度任务和命名实体识别（NER）任务中优于同类模型。


## Transformer

- **Attention Is All You Need**
  - **发表年份**: 2017
  - **引用**: 120644
  - **作者及所属实验室**:  
    - Ashish Vaswani: Google Brain  
    - Noam Shazeer: Google Brain  
    - Niki Parmar: Google Research  
    - Jakob Uszkoreit: Google Research  
    - Llion Jones: Google Research  
    - Aidan N. Gomez: 多伦多大学（参与时在Google Brain）  
    - Łukasz Kaiser: Google Brain  
    - Illia Polosukhin: Google Research  
  - **核心贡献**:  
    1. 提出了**Transformer**架构，首次完全基于自注意力机制（self-attention）实现序列建模，摒弃了传统的循环神经网络（RNN）和卷积神经网络（CNN）。  
    2. 设计了**多头注意力机制**（multi-head attention）和位置编码（positional encoding），显著提升了并行计算效率和长距离依赖建模能力。  
    3. 在WMT 2014英德和英法机器翻译任务中取得新的SOTA结果（BLEU 28.4和41.8），并验证了模型在句法解析等任务的泛化能力。

## Models And Pre-trained Models

- **Deep contextualized word representations**
  - **发表年份**: 2018
  - **引用**: 11337
  - **作者及所属实验室**:  
    - Matthew E. Peters, Mark Neumann, Mohit Iyyer, Matt Gardner: Allen Institute for Artificial Intelligence  
    - Christopher Clark, Kenton Lee, Luke Zettlemoyer: Paul G. Allen School of Computer Science & Engineering, University of Washington  
  - **核心贡献**:  
    1. 提出了**ELMo（Embeddings from Language Models）**，通过预训练的双向语言模型（biLM）生成深层上下文相关的词表示，解决了传统词向量无法建模多义词和复杂语境的问题。  
    2. 首次将双向语言模型的多层隐藏状态进行线性组合，证明不同层捕获不同粒度的语言特征（如底层编码语法，高层编码语义），并通过任务自适应的权重分配显著提升了模型性能。  
    3. 在六项NLP任务（如问答、文本蕴含、语义角色标注）中实现当时最先进的结果，最高相对错误率降低达24.9%，并开源了预训练模型和代码。

### BERT 系列

- **BERT: Pre-training of Deep Bidirectional Transformers for Language Understanding**
  - **发表年份**: 2019
  - **引用**: 89161
  - **作者及所属实验室**:  
    - Jacob Devlin: Google AI Language  
    - Ming-Wei Chang: Google AI Language  
    - Kenton Lee: Google AI Language  
    - Kristina Toutanova: Google AI Language  
  - **核心贡献**:  
    1. 提出了**BERT**模型，通过掩码语言模型（MLM）和下一句预测（NSP）任务，首次实现了基于双向Transformer的深度上下文表示预训练。  
    2. 在11项自然语言处理任务（包括GLUE、SQuAD、SWAG等）上刷新了当时的最优性能，其中GLUE基准得分提升7.7%，SQuAD v1.1 F1值提升1.5%。  
    3. 开源了预训练模型和微调代码，推动了后续大规模预训练语言模型的研究与应用。

- **RoBERTa: A Robustly Optimized BERT Pretraining Approach**
  - **发表年份**: 2019  
  - **引用**: 23022
  - **作者及所属实验室**:  
    - Yinhan Liu, Myle Ott, Naman Goyal, Jingfei Du, Mandar Joshi, Danqi Chen, Omer Levy, Mike Lewis, Luke Zettlemoyer, Veselin Stoyanov: Facebook AI  
    - Mandar Joshi, Luke Zettlemoyer: Paul G. Allen School of Computer Science & Engineering, University of Washington  
  - **核心贡献**:  
    1. 提出了**RoBERTa**模型，通过系统优化BERT的预训练策略（包括**动态掩码**、**移除NSP目标**、**更大批次训练**和**更长序列训练**），显著提升了模型性能。  
    2. 验证了**数据规模**和**训练时长**对模型效果的关键作用，并通过新数据集CC-NEWS（76GB新闻文本）证明了数据多样性的重要性。  
    3. 在GLUE、SQuAD和RACE等基准任务上达到SOTA，重新确立了掩码语言模型（MLM）训练目标的竞争力，且无需多任务微调或额外数据增强。


### GPT 系列

- **Improving Language Understanding by Generative Pre-Training**
  - **发表年份**: 2018
  - **引用**: 10900
  - **作者及所属实验室**:  
    - Alec Radford: OpenAI  
    - Karthik Narasimhan: OpenAI  
    - Tim Salimans: OpenAI  
    - Ilya Sutskever: OpenAI  
  - **核心贡献**:  
    1. 提出了**生成式预训练（Generative Pre-Training）与判别式微调（Discriminative Fine-Tuning）结合**的框架，通过大规模无标签文本预训练语言模型后，在特定任务上微调。  
    2. 首次将**Transformer架构**应用于预训练语言模型，解决了长程依赖建模问题，并在12项NLP任务中的9项刷新了SOTA（如常识推理任务提升8.9%，问答任务提升5.7%）。  
    3. 设计了**任务无关的输入转换方法**，将结构化输入（如句子对、问答三元组）统一编码为连续序列，最小化模型架构调整需求。

- **Language Models are Unsupervised Multitask Learners**
  - **发表年份**: 2019
  - **引用**: 21174
  - **作者及所属实验室**:  
    - Alec Radford: OpenAI  
    - Jeffrey Wu: OpenAI  
    - Rewon Child: OpenAI  
    - David Luan: OpenAI  
    - Dario Amodei: OpenAI  
    - Ilya Sutskever: OpenAI  
  - **核心贡献**:  
    1. 提出了**GPT-2**模型（1.5B参数），首次证明大规模语言模型在无监督训练下可通过零样本（zero-shot）方式直接执行多种NLP任务（如问答、翻译、摘要），无需任务特定微调。  
    2. 构建了**WebText**数据集（800万网页文本，40GB），展示了数据多样性和规模对模型多任务泛化能力的关键作用。  
    3. 改进了Transformer架构（如层归一化位置调整、扩展上下文窗口至1024 tokens），在7/8个语言建模基准测试中达到零样本SOTA性能。

- **Language Models are Few-Shot Learners**
  - **发表年份**: 2020
  - **引用**: 37261
  - **作者及所属实验室**:  
    - Tom B. Brown, Benjamin Mann, Nick Ryder, Melanie Subbiah 等: OpenAI  
  - **核心贡献**:  
    1. 提出了**GPT-3**，一种拥有1750亿参数的自回归语言模型，规模是先前非稀疏模型的10倍，展示了模型规模的显著扩展对任务无关的少样本学习能力的提升。
    2. 在零样本、单样本和少样本设置下，GPT-3在多种NLP任务（如翻译、问答、常识推理）中表现出色，部分任务达到或接近微调模型的性能，验证了大规模预训练模型的通用性。
    3. 首次系统性研究了语言模型在少样本学习中的表现，揭示了模型规模与上下文学习能力的关系，并探讨了数据污染、伦理影响（如生成内容的真实性、偏见问题）及社会应用风险。

- **GPT-4 Technical Report**
  - **发表年份**: 2023  
  - **引用**: 11302
  - **作者及所属实验室**:  
    - OpenAI团队: OpenAI  
  - **核心贡献**:  
    1. 提出了**GPT-4**——首个支持多模态输入（图像和文本）的大规模Transformer模型，通过后训练对齐显著提升了生成内容的**事实准确性和行为可控性**。  
    2. 在多项专业和学术基准测试中展现出接近人类水平的性能，例如模拟律师考试得分超过90%的考生。  
    3. 开发了可扩展的**基础设施与优化方法**，首次实现基于千分之一计算量的小模型准确预测GPT-4部分性能的缩放规律。  

### Llama 系列
- **LLaMA: Open and Efficient Foundation Language Models**
  - **发表年份**: 2023
  - **引用**: 11046
  - **作者及所属实验室**:  
    - Hugo Touvron, Thibaut Lavril, Gautier Izacard 等: Meta AI  
  - **核心贡献**:  
    1. 提出了**LLaMA系列模型**（7B至65B参数），首次证明仅使用公开数据集（如CommonCrawl、C4、GitHub等）即可训练出与闭源模型性能匹敌的大语言模型。  
    2. LLaMA-13B在多数基准测试中超越GPT-3（175B），而LLaMA-65B与Chinchilla-70B和PaLM-540B性能相当，同时模型参数量显著减少，推理效率更高。  
    3. 开源所有模型权重及训练方法，推动大语言模型研究的可复现性和社区协作。

- **Llama 2: Open Foundation and Fine-Tuned Chat Models**
  - **发表年份**: 2023
  - **引用**: 10020
  - **作者及所属实验室**:  
    - Hugo Touvron: GenAI, Meta  
    - Louis Martin†, Kevin Stone†, 及其他多位作者: Meta  
  - **核心贡献**:  
    1. 提出了**Llama 2**系列模型，包括7B到70B参数的预训练模型及对话优化版本**Llama 2-Chat**，在多数基准测试中超越开源对话模型。  
    2. 通过监督微调（SFT）、基于人类反馈的强化学习（RLHF）及安全对齐技术（如Ghost Attention），显著提升了模型的安全性和有用性，并在人类评估中接近闭源模型（如ChatGPT）。  
    3. 开源了模型权重、微调代码及详细的安全改进方法，推动社区对LLM负责任开发的贡献，并提供碳排放透明度和数据污染分析。  

- **The Llama 3 Herd of Models**
  - **发表年份**: 2024
  - **引用**: 3227
  - **作者及所属实验室**:  
    - Llama Team: AI @ Meta  
  - **核心贡献**:  
    1. 提出了**Llama 3系列模型**，包含8B、70B和405B参数的密集Transformer模型，支持**128K上下文窗口**，并原生集成多语言、代码生成、复杂推理及工具使用能力。
    2. 在多项基准测试（如MMLU、HumanEval、GSM8K）中达到与GPT-4相当的性能，同时通过改进数据质量（15T多语言token训练）和训练方法（4D并行策略）实现高效扩展。
    3. 开源了预训练和微调版本，包括**Llama Guard 3安全模型**，并实验性地通过组合方法整合图像、视频和语音能力，初步在多模态任务中达到SOTA水平（相关模型仍在开发中）。

### Qwen 系列
- **Qwen2 Technical Report**
  - **发表年份**: 2024
  - **引用**: 640
  - **作者及所属实验室**:  
    Qwen Team, Alibaba Group  
  - **核心贡献**:  
    1. 提出了**Qwen2系列模型**，包含0.5B到72B参数的密集模型和57B总参数/14B激活参数的MoE模型，性能超越多数开源模型（包括前代Qwen1.5）并在多项基准测试中与专有模型竞争。
    2. 在语言理解、代码生成（HumanEval 64.6）、数学推理（GSM8K 89.5）和多语言能力（支持约30种语言）上表现突出，72B模型在MMLU和GPQA分别达到84.2和37.9。
    3. 开源了模型权重、量化/微调工具及长上下文支持（通过YARN和DCA技术扩展至131k tokens），推动社区应用与研究创新。

- **Qwen2.5 Technical Report**
  - **发表年份**: 2025
  - **引用**: 279
  - **作者及所属实验室**:  
    - Qwen Team: 阿里巴巴云Model Studio等  
  - **核心贡献**:  
    1. 提出了**Qwen2.5系列模型**，通过将预训练数据从7万亿token扩展到18万亿token，显著增强了模型的常识、专业知识和推理能力。  
    2. 在训练后阶段引入了复杂的监督微调（含超百万样本）和多阶段强化学习（包括离线DPO和在线GRPO），显著提升了人类偏好对齐、长文本生成和结构化数据分析能力。  
    3. 开源了从0.5B到72B参数的密集模型和MoE变体（Qwen2.5-Turbo/Qwen2.5-Plus），其中Qwen2.5-72B-Instruct在多项基准测试中性能接近Llama-3-405B-Instruct（参数量仅为后者的1/5），并支持百万token级长上下文处理。

### DeepSeek 系列
- **DeepSeek-V3 Technical Report**
  - **发表年份**: 2024
  - **引用**: 187
  - **作者及所属实验室**:  
    - DeepSeek-AI: DeepSeek人工智能研究院
  - **核心贡献**:  
    1. 提出了**首个无辅助损失的专家负载均衡策略**，通过动态偏置调整实现通信效率与模型性能的平衡，同时引入**多令牌预测目标**增强模型推理能力。
    2. 实现了**FP8混合精度训练框架**，首次验证了极大规模模型的低精度训练可行性，并通过算法-框架-硬件协同设计突破跨节点MoE通信瓶颈，使训练效率提升至每万亿token仅需18万H800 GPU小时。
    3. 在14.8万亿token预训练后，模型在数学推理（MATH-500 90.2%）、代码生成（LiveCodeBench 40.5%）等核心任务上超越所有开源模型，并在MMLU-Pro（75.9%）、GPQA（59.1%）等学术基准上达到闭源模型GPT-4o/Claude-3.5水平，全流程训练成本仅278.8万GPU小时（约557万美元）。

- **DeepSeek-R1: Incentivizing Reasoning Capability in LLMs via Reinforcement Learning**
  - **发表年份**: 2025
  - **引用**: 391
  - **作者及所属实验室**:  
    - DeepSeek-AI团队  
  - **核心贡献**:  
    1. 提出了**DeepSeek-R1-Zero**，首次通过纯强化学习（RL）无需监督微调（SFT）直接训练基模型，使模型自然涌现出自我验证、反思和长链推理等能力，在AIME 2024等推理任务中性能提升显著（从15.6%提升至71.0%）。  
    2. 开发了**DeepSeek-R1**，通过多阶段训练（冷启动数据+RL优化）解决了DeepSeek-R1-Zero的可读性和语言混杂问题，在数学、代码等推理任务上性能与OpenAI-o1-1217相当，并在知识型任务（如MMLU、GPQA）中表现优异。  
    3. 开源了基于Qwen和Llama的蒸馏模型（1.5B-70B规模），验证了从小模型直接蒸馏大模型推理能力的有效性（如14B模型超越QwQ-32B-Preview），为社区提供了高效推理模型的新范式。

## Prompting

- **Chain-of-Thought Prompting Elicits Reasoning in Large Language Models**
  - **发表年份**: 2022
  - **引用**: 7475
  - **作者及所属实验室**:  
    - Jason Wei, Xuezhi Wang, Dale Schuurmans, Maarten Bosma, Brian Ichter, Fei Xia, Ed H. Chi, Quoc V. Le, Denny Zhou: Google Research, Brain Team
  - **核心贡献**:  
    1. 提出了**链式思维提示（chain-of-thought prompting）**方法，通过在提示中提供逐步推理的示例，显著提升了大型语言模型在复杂推理任务（如算术、常识和符号推理）上的性能。
    2. 证明了链式思维推理能力是模型规模的**涌现特性**，仅在参数量级达到约100B的模型中有效，并在GSM8K数学基准上超越此前基于微调的SOTA方法（如PaLM 540B模型通过8个示例提示达到57%准确率）。
    3. 方法具有**广泛适用性**，无需任务特定微调或大量标注数据，且在不同标注风格和示例集上表现鲁棒，为语言模型的推理能力提供了可解释性窗口。

## Miscellaneous 

- **Language Modeling with Gated Convolutional Networks**
  - **发表年份**: 2017
  - **引用**: 2293
  - **作者及所属实验室**:  
    - Yann N. Dauphin: Facebook AI Research  
    - Angela Fan: Facebook AI Research  
    - Michael Auli: Facebook AI Research  
    - David Grangier: Facebook AI Research  
  - **核心贡献**:  
    1. 提出了**Gated Linear Units (GLU)**，一种简化的门控机制，通过线性路径缓解梯度消失问题，同时保留非线性建模能力。  
    2. 在WikiText-103和Google Billion Words等大规模语言建模任务上首次实现非循环模型（卷积架构）与强循环模型（如LSTM）的竞争性能，并在WikiText-103上刷新了当时的最佳结果。  
    3. 通过卷积架构的并行化优势，将句子评分延迟降低了一个数量级，显著提升了计算效率。
  
- **Improving Language Understanding by Generative Pre-Training**
  - **发表年份**: 2018
  - **引用**: 10900
  - **作者及所属实验室**:  
    - Alec Radford: OpenAI  
    - Karthik Narasimhan: OpenAI  
    - Tim Salimans: OpenAI  
    - Ilya Sutskever: OpenAI  
  - **核心贡献**:  
    1. 提出了**两阶段训练框架**，通过无监督生成式预训练（基于大规模文本）和监督判别式微调（基于特定任务）提升语言理解能力。  
    2. 采用**Transformer架构**替代传统RNN/LSTM，有效捕捉长距离依赖关系，并通过任务特定的输入序列化方法实现跨任务迁移，最小化模型结构调整。  
    3. 在12项NLP基准任务中9项刷新SOTA，包括常识推理（Stories Cloze Test +8.9%）、问答（RACE +5.7%）和文本蕴含（MultiNLI +1.5%）等任务。  

- **Universal Language Model Fine-tuning for Text Classification**
  - **发表年份**: 2018
  - **引用**: 3515
  - **作者及所属实验室**:  
    - Jeremy Howard: fast.ai & 旧金山大学  
    - Sebastian Ruder: Insight Centre (NUI Galway) & Aylien Ltd.  
  - **核心贡献**:  
    1. 提出了**ULMFiT**（通用语言模型微调方法），首次在NLP领域实现了类似CV的通用迁移学习框架，无需任务特定架构修改即可应用于任意NLP任务。  
    2. 创新性地引入**判别式微调**（不同层差异化学习率）、**斜三角学习率调度**（快速收敛与稳定训练平衡）和**渐进解冻**（逐层微调防灾难性遗忘）三大关键技术。  
    3. 在6个文本分类任务上实现18-24%的错误率显著下降，仅用100标注样本即可达到传统方法万级数据量性能，并开源模型与代码推动NLP迁移学习发展。
 
- **Language Models as Knowledge Bases?**
  - **发表年份**: 2019
  - **引用**: 2488
  - **作者及所属实验室**:  
    - Fabio Petroni: Facebook AI Research  
    - Tim Rocktäschel: Facebook AI Research & University College London  
    - Patrick Lewis: Facebook AI Research & University College London  
    - Anton Bakhtin: Facebook AI Research  
    - Yuxiang Wu: Facebook AI Research & University College London  
    - Alexander H. Miller: Facebook AI Research  
    - Sebastian Riedel: Facebook AI Research & University College London  
  - **核心贡献**:  
    1. 发现**未经微调的BERT**在关系知识抽取任务上的表现与使用传统关系抽取方法（含实体链接Oracle）的知识库相当，且在开放领域QA任务中接近监督基线（57.1% P@10 vs 63.5%）。  
    2. 揭示了语言模型通过预训练更易学习某些类型的事实知识（如1-to-1关系），但对N-to-M关系的表达能力有限。  
    3. 提出了**LAMA探针**框架，首次系统评估了预训练语言模型存储事实和常识知识的能力，展示了其作为无监督开放领域QA系统的潜力。
  
- **Exploring the Limits of Transfer Learning with a Unified Text-to-Text Transformer**
  - **发表年份**: 2020
  - **引用**: 18500
  - **作者及所属实验室**:  
    - Colin Raffel: Google, Mountain View, CA  
    - Noam Shazeer: Google, Mountain View, CA  
    - Adam Roberts: Google, Mountain View, CA  
    - Katherine Lee: Google, Mountain View, CA  
    - Sharan Narang: Google, Mountain View, CA  
    - Michael Matena: Google, Mountain View, CA  
    - Yanqi Zhou: Google, Mountain View, CA  
    - Wei Li: Google, Mountain View, CA  
    - Peter J. Liu: Google, Mountain View, CA  
  - **核心贡献**:  
    1. 提出了**统一文本到文本转换框架（T5）**，将各类NLP任务（如翻译、分类、问答等）统一为文本生成形式，简化了模型架构和训练流程。  
    2. 通过系统实验对比了不同预训练目标、模型架构、数据集和迁移策略，揭示迁移学习的关键影响因素，并基于大规模训练（1万亿token）在多个基准任务上达到SOTA性能。  
    3. 发布了**C4数据集**（Colossal Clean Crawled Corpus）和预训练模型，为后续研究提供标准化工具和可复现基础。

- **Training language models to follow instructions with human feedback**
  - **发表年份**: 2022
  - **引用**: 11022
  - **作者及所属实验室**:  
    - Long Ouyang, Jeff Wu, Xu Jiang, Diogo Almeida, Carroll L. Wainwright, Pamela Mishkin, Chong Zhang, Sandhini Agarwal, Katarina Slama, Alex Ray, John Schulman, Jacob Hilton, Fraser Kelton, Luke Miller, Maddie Simens, Amanda Askell, Peter Welinder, Paul Christiano, Jan Leike, Ryan Lowe (全部来自OpenAI)  
  - **核心贡献**:  
    1. 提出了基于人类反馈的强化学习（RLHF）方法，通过监督微调（SFT）、奖励模型（RM）训练和近端策略优化（PPO）三个阶段，显著提升了语言模型与用户意图的对齐能力。  
    2. 开发的InstructGPT模型（1.3B参数）在人类评估中优于175B参数的GPT-3，减少了生成内容的虚假信息（TruthfulQA基准上真实性提升约2倍）和毒性（毒性输出降低25%），同时保持了公共NLP任务的性能。  
    3. 通过混合预训练梯度更新（PPO-ptx）缓解了传统RLHF微调导致的性能退化问题，验证了人类反馈对齐技术的可扩展性和低对齐税（alignment tax）特性。
 

- **PaLM: Scaling Language Modeling with Pathways**
  - **发表年份**: 2022
  - **引用**: 5684
  - **作者及所属实验室**:  
    - Aakanksha Chowdhery, Sharan Narang, Jacob Devlin 等（共107位作者）: Google Research  
    - 部分作者来自Alphabet X和Moonshot Factory
  - **核心贡献**:  
    1. 提出了**Pathways系统**，首次在6144个TPU v4芯片上高效训练5400亿参数的密集激活Transformer模型，实现46.2%的模型FLOPs利用率。
    2. 在数百个语言理解和生成任务上刷新了few-shot学习的SOTA，在BIG-bench等复杂推理任务中首次超越人类平均表现，并展示了模型规模带来的"能力突变"现象。
    3. 展示了在代码生成（HumanEval 88.4% pass@100）和多语言任务上的突破性能力，同时系统分析了训练数据记忆、偏见和毒性等伦理问题。


- **Large Language Models are Zero-Shot Reasoners**
  - **发表年份**: 2022
  - **引用**: 3702
  - **作者及所属实验室**:  
    - Takeshi Kojima: 东京大学  
    - Shixiang Shane Gu: Google Research, Brain Team  
    - Machel Reid: Google Research  
    - Yutaka Matsuo: 东京大学  
    - Yusuke Iwasawa: 东京大学  
  - **核心贡献**:  
    1. 提出了**Zero-shot Chain of Thought (Zero-shot-CoT)**方法，通过添加如“Let’s think step by step”的单一通用提示，无需任务示例即可激发大语言模型（LLM）的多步推理能力。  
    2. 在算术（MultiArith、GSM8K）、符号推理（Last Letter、Coin Flip）和逻辑任务（Date Understanding）等多样化基准上，Zero-shot-CoT显著超越标准零样本方法（如MultiArith准确率从17.7%提升至78.7%）。  
    3. 展示了该方法在InstructGPT、PaLM等不同规模模型上的泛化性，揭示了LLM未开发的零样本推理潜力，挑战了传统依赖任务特定示例或微调的研究范式。

- **Direct Preference Optimization: Your Language Model is Secretly a Reward Model**
  - **发表年份**: 2023
  - **引用**: 2820
  - **作者及所属实验室**:  
    - Rafael Rafailov: 斯坦福大学  
    - Archit Sharma: 斯坦福大学  
    - Eric Mitchell: 斯坦福大学  
    - Stefano Ermon: 斯坦福大学 & CZ Biohub  
    - Christopher D. Manning: 斯坦福大学  
    - Chelsea Finn: 斯坦福大学  
  - **核心贡献**:  
    1. 提出了**Direct Preference Optimization (DPO)**，一种无需显式奖励建模或强化学习的偏好学习算法，通过简单的分类损失直接优化语言模型策略。  
    2. 通过理论分析揭示了语言模型策略与奖励函数之间的隐式映射关系，证明了DPO优化目标与RLHF的一致性，同时避免了RL训练的复杂性。  
    3. 实验表明DPO在情感控制、摘要生成和对话任务中性能优于或匹配PPO等RLHF方法，且训练稳定性更高、计算开销更低。
