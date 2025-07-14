# Awesome Machine Learning Reliability

## Background

- [MLSys: The New Frontier of Machine Learning Systems](https://arxiv.org/pdf/1904.03257.pdf) – The white paper that you must read.
- [AI Engineering Quick Start](https://ai-engineering.club/docs/quick_start) – A great, approachable of machine learning engineering workflow and practices.

## High-Level View

- [Machine Learning Testing: Survey, Landscapes and Horizons](https://arxiv.org/pdf/1906.10742.pdf), *TSE'20*
- [Hidden Technical Debt in Machine Learning Systems](https://papers.nips.cc/paper/5656-hidden-technical-debt-in-machine-learning-systems.pdf), *NeurIps 2015* – A seminal paper on the hidden technical debt in machine learning systems.

## Empirical Studies

- [Towards Understanding Bugs in Distributed Training and Inference Frameworks for Large Language Models](https://arxiv.org/pdf/2506.10426), *2025*
- [Characterization of Large Language Model Development in the Datacenter](https://arxiv.org/abs/2403.07648), *NSDI'24* – An empirical study of LLM-specific workloads in Shanghai AI Lab's cluster. [Review](./reviews/Characterization%20of%20Large%20Language%20Model%20Development%20in%20the%20Datacenter.md)
- [An Empirical Study on Low GPU Utilization of Deep Learning Jobs](https://dl.acm.org/doi/10.1145/3597503.3639232) *ICSE 2024*
- [Toward Understanding Deep Learning Framework Bugs](https://dl.acm.org/doi/10.1145/3587155), *TOSEM 2023*
- [Are Machine Learning Cloud APIs Used Correctly?](https://ieeexplore.ieee.org/document/9402073) *ICSE 2021*
- [A comprehensive empirical study on bug characteristics of deep learning frameworks](https://linkinghub.elsevier.com/retrieve/pii/S0950584922001306), *Information and Software Technology 2021*
- [An Empirical Study on Program Failures of Deep Learning Jobs](https://dl.acm.org/doi/10.1145/3377811.3380362), *ICSE 2020* – An empirical study on **failure characteristics** of industry deep learning jobs from Microsoft. The study focuses on **job failures** that throw explicit exceptions.
- [An Empirical Study of Common Challenges in Developing Deep Learning Applications](https://ieeexplore.ieee.org/document/8987482), *IEEE Software 2020* – An empirical study on **challenges** in developing correct and accurate deep learning applications. It categorizes the types of issues and investigates the difficulty of debugging them.
- [Taxonomy of Real Faults in Deep Learning Systems](https://arxiv.org/abs/1910.11015), *ICSE'19*

## Silent Errors

### Empirical Studies
- [Understanding Silent Data Corruption in LLM Training](https://arxiv.org/abs/2502.12340), *2025* – from Amazon.
- [Silent Errors In Large-scale LLM Training: Challenges and Lessons Learned](https://atscaleconference.com/scale-data-ai-infra/?tab=0&item=8#agenda-item-8), *2025* – from Nvidia.

### Detection & Diagnosis 
- [Training with Confidence: Catching Silent Errors in Deep Learning Training with Automated Proactive Checks](https://www.arxiv.org/abs/2506.14813), *OSDI 2025* – Introduces TrainCheck, a proactive runtime monitoring framework that automatically infers and checks training invariants to detect silent correctness errors in DL training pipelines.
- [XPUTIMER: Anomaly Diagnostics for Divergent LLM Training in GPU Clusters of Thousand-Plus Scale](https://arxiv.org/pdf/2502.05413), *2025* - Introduces XPUTIMER, a real-time anomaly diagnostic framework tailored for distributed large language model (LLM) training in extensive GPU clusters


## Distributed Training

- [TrainVerify: Equivalence-Based Verification for Distributed LLM Training](https://www.arxiv.org/abs/2506.15961), *SOSP 2025*
- [TTrace: Lightweight Error Checking and Diagnosis for Distributed Training](https://arxiv.org/abs/2506.09280), *2025*

## Diagnosis
- [PerfTracker: Online Performance Troubleshooting for Large-scale Model Training in Production](https://arxiv.org/abs/2506.08528), *2025* - Performance troubleshooting system from Alibaba Cloud.
- [Emerging Platforms Meet Emerging LLMs: A Year-Long Journey of Top-Down Development](http://arxiv.org/abs/2404.09151), *2024*
- [Debugging Machine Learning Pipelines](https://dl.acm.org/doi/10.1145/3329486.3329489), *DEEM 2019* – Localizing root causes of ML performance anomalies in (i.e. hyperparameter, software version, data, etc.) with **decision trees** and existing runs of the same pipeline. [Review](reviews/Debugging-Machine-Learning-Pipelines.md)


## Code Bug Testing

- [CRADLE: Cross-Backend Validation to Detect and Localize Bugs in Deep Learning Libraries](https://www.cs.purdue.edu/homes/lintan/publications/cradle-icse19.pdf), *ICSE 2019* – Using **differential testing** to find bugs in different libraries' implementations of the same deep learning utilities.
- [A Static Analyzer for Detecting Tensor Shape Errors in Deep Neural Network Training Code](https://dl.acm.org/doi/abs/10.1145/3510454.3528638), *ICSE 2022* – A static analyzer for detecting **tensor shape errors** in deep neural network training code. The analyzer is based on **abstract interpretation** and **constraint solving** and it used Z3 SMT Solver to detect conflicts. [Review](reviews/A-Static-Analyzer-for-Detecting-Tensor-Shape-Errors-in-Deep-Neural-Network-Training-Code.md)
- [AutoTrainer: An Automatic DNN Training Problem Detection and Repair System](https://dl.acm.org/doi/10.1109/ICSE43902.2021.00043), *ICSE 2021*
- [Reliability Assurance for Deep Neural Network Architectures against Numerical Defects](https://dl.acm.org/doi/abs/10.1109/ICSE48619.2023.00156), *ICSE 2023*
- [NeuRI: Diversifying DNN Generation via Inductive Rule Inference](https://arxiv.org/abs/2302.02261) *FSE 2023*
- [NNSmith: Generating Diverse and Valid Test Cases for Deep Learning Compilers](http://arxiv.org/abs/2207.13066) *ASPLOS 2023*
- [Fuzzing Automatic Differentiation in Deep-Learning Libraries](https://arxiv.org/pdf/2302.04351) *ICSE 2023*
- [Fuzzing Deep-Learning Libraries via Automated Relational API Inference](https://arxiv.org/pdf/2207.05531) *FSE 2022*
- [Free Lunch for Testing: Fuzzing Deep-Learning Libraries from Open Source](http://lingming.cs.illinois.edu/publications/icse2022a.pdf) *ICSE 2022*
- [Automated Testing of Software that Uses Machine Learning APIs](https://ieeexplore.ieee.org/document/9793999) *ICSE 2022*
- [Keeper: Automated Testing and Fixing of Machine Learning Software](https://www.microsoft.com/en-us/research/publication/keeper-automated-testing-and-fixing-of-machine-learning-software/) *TOSEM 2024*

## Monitoring

- [Training with Confidence: Catching Silent Errors in Deep Learning Training with Automated Proactive Checks](https://www.arxiv.org/abs/2506.14813), *OSDI 2025*
- [Self-Checking Deep Neural Networks in Deployment](https://dl.acm.org/doi/abs/10.1109/ICSE43902.2021.00044), *ICSE 2022*

## Model Behavior Testing

- [DeepXplore: Automated Whitebox Testing of Deep Learning Systems](https://dl.acm.org/doi/10.1145/3132747.3132785), *SOSP 2017* (Best paper award) – Introduces **Neuron Coverage** to guide input generation and **Differential Testing** to detect bugs across autonomous driving systems.
- [Oracle Issues in Machine Learning and Where to Find Them](https://dl.acm.org/doi/10.1145/3387940.3391490), *ICSEW 2020* – An introduction to machine learning oracles (i.e. the labels of validation and test data) and how to detect issues within them using *Shannon Entropy* and *Semantic Analysis*. [Review](reviews/Oracle-Issues-in-Machine-Learning-and-Where-to-Find-Them.md)



<!-- 
TBD:
- @misc{zhang2024surveydeeplearninglibrary,
      title={A Survey of Deep Learning Library Testing Methods}, 
      author={Xiaoyu Zhang and Weipeng Jiang and Chao Shen and Qi Li and Qian Wang and Chenhao Lin and Xiaohong Guan},
      year={2024},
      eprint={2404.17871},
      archivePrefix={arXiv},
      primaryClass={cs.SE},
      url={https://arxiv.org/abs/2404.17871}, 
}

-  -->