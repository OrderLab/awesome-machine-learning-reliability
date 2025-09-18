# Awesome Machine Learning Reliability

## Table of Contents

- [Background](#background)
- [High-Level View](#high-level-view)
- [Empirical Studies](#empirical-studies)
- [Silent Errors](#silent-errors)
  - [Empirical Studies](#empirical-studies-1)
  - [Detection & Diagnosis](#detection--diagnosis)
- [Distributed Training](#distributed-training)
- [Diagnosis](#diagnosis)
- [Code Bug Testing](#code-bug-testing)
- [Monitoring](#monitoring)
- [Model Behavior Testing](#model-behavior-testing)
- [Fault Injection Tools](#fault-injection-tools)
- [Industry Post Mortems](#industry-post-mortems)

## Background

- [MLSys: The New Frontier of Machine Learning Systems](https://arxiv.org/pdf/1904.03257.pdf) — Position paper outlining the co-design challenges/opportunities across ML, systems, and hardware.
- [AI Engineering Quick Start](https://ai-engineering.club/docs/quick_start) — Practical guide to end-to-end AI engineering workflows and best practices.

## High-Level View

- [Machine Learning Testing: Survey, Landscapes and Horizons](https://arxiv.org/pdf/1906.10742.pdf), *TSE 2020* — Comprehensive survey of ML testing techniques, tools, and open challenges.
- [Hidden Technical Debt in Machine Learning Systems](https://papers.nips.cc/paper/5656-hidden-technical-debt-in-machine-learning-systems.pdf), *NeurIPS 2015* — Seminal discussion of non-obvious maintenance costs and systemic risks in ML systems.

## Empirical Studies
- [A First Look at Bugs in LLM Inference Engines](https://www.arxiv.org/abs/2506.09713), *arXiv 2025* [Inference] — Early taxonomy and root causes of bugs in LLM inference engines across open-source stacks.
- [Towards Understanding Bugs in Distributed Training and Inference Frameworks for Large Language Models](https://arxiv.org/pdf/2506.10426), *arXiv 2025* [Training] [Inference] — Characterizes bug patterns in distributed LLM frameworks and offers mitigation guidance.
- [Characterization of Large Language Model Development in the Datacenter](https://arxiv.org/abs/2403.07648), *NSDI 2024* [Training] — Cluster-scale study of LLM development workloads and bottlenecks at Shanghai AI Lab. [Review](./reviews/Characterization%20of%20Large%20Language%20Model%20Development%20in%20the%20Datacenter.md)
- [An Empirical Study on Low GPU Utilization of Deep Learning Jobs](https://dl.acm.org/doi/10.1145/3597503.3639232), *ICSE 2024* [Training] — Identifies causes of low GPU utilization in DL jobs and practical optimizations.
- [Toward Understanding Deep Learning Framework Bugs](https://dl.acm.org/doi/10.1145/3587155), *TOSEM 2023* [Kernels] — Analyzes bug types, triggers, and impact across major DL frameworks.
- [Are Machine Learning Cloud APIs Used Correctly?](https://ieeexplore.ieee.org/document/9402073), *ICSE 2021* [Inference] — Studies real-world misuse patterns of ML cloud APIs and their consequences.
- [A Comprehensive Empirical Study on Bug Characteristics of Deep Learning Frameworks](https://linkinghub.elsevier.com/retrieve/pii/S0950584922001306), *IST 2021* [Kernels] — Large-scale analysis of DL framework bug reports to extract categories and trends.
- [An Empirical Study on Program Failures of Deep Learning Jobs](https://dl.acm.org/doi/10.1145/3377811.3380362), *ICSE 2020* [Training] — Characterizes failure modes in production DL jobs at Microsoft focusing on exception-throwing failures.
- [An Empirical Study of Common Challenges in Developing Deep Learning Applications](https://ieeexplore.ieee.org/document/8987482), *IEEE Software 2020* [Training] [Inference] — Surveys and categorizes practical challenges in building correct and accurate DL apps.
- [Taxonomy of Real Faults in Deep Learning Systems](https://arxiv.org/abs/1910.11015), *ICSE 2019* [Training] [Inference] — Builds a taxonomy of real-world DL faults with testing implications.

## Silent Errors

### Empirical Studies
- [Understanding Silent Data Corruption in LLM Training](https://arxiv.org/abs/2502.12340), *arXiv 2025* [Training] — Amazon's study of SDC causes, manifestations, and detection challenges in LLM training.
- [Silent Errors in Large-scale LLM Training: Challenges and Lessons Learned](https://atscaleconference.com/scale-data-ai-infra/?tab=0&item=8#agenda-item-8), *2025* [Training] — NVIDIA experience report on prevalence, sources, and mitigations for silent training errors.

### Detection & Diagnosis
- [Training with Confidence: Catching Silent Errors in Deep Learning Training with Automated Proactive Checks](https://www.arxiv.org/abs/2506.14813), *OSDI 2025* [Training] — TrainCheck automatically infers training invariants and proactively flags silent correctness errors.
- [XPUTIMER: Anomaly Diagnostics for Divergent LLM Training in GPU Clusters of Thousand-Plus Scale](https://arxiv.org/pdf/2502.05413), *arXiv 2025* [Training] — Real-time anomaly diagnostics tailored for large-scale distributed LLM training.

## Distributed Training

- [TrainVerify: Equivalence-Based Verification for Distributed LLM Training](https://www.arxiv.org/abs/2506.15961), *SOSP 2025* [Training] — Verifies distributed training by checking equivalence against a reference to catch silent errors.
- [TTrace: Lightweight Error Checking and Diagnosis for Distributed Training](https://arxiv.org/abs/2506.09280), *arXiv 2025* [Training] — Low-overhead tracing to detect and localize errors in distributed training.

## Diagnosis
- [Defeating Nondeterminism in LLM Inference](https://thinkingmachines.ai/blog/defeating-nondeterminism-in-llm-inference/), *Blog 2025* [Inference] [Kernels] — Blog on ensuring "batch invariance" of kernels by Thinking Machines
- [PerfTracker: Online Performance Troubleshooting for Large-scale Model Training in Production](https://arxiv.org/abs/2506.08528), *arXiv 2025* [Training] — Alibaba Cloud system for online localization of training performance bottlenecks and regressions.
- [Emerging Platforms Meet Emerging LLMs: A Year-Long Journey of Top-Down Development](http://arxiv.org/abs/2404.09151), *arXiv 2024* [Training] — Case study on co-designing software and hardware platforms to support rapidly evolving LLMs.
- [Debugging Machine Learning Pipelines](https://dl.acm.org/doi/10.1145/3329486.3329489), *DEEM 2019* [Training] — Uses decision trees over historical runs to localize ML pipeline performance anomalies. [Review](reviews/Debugging-Machine-Learning-Pipelines.md)

## Code Bug Testing

- [CRADLE: Cross-Backend Validation to Detect and Localize Bugs in Deep Learning Libraries](https://www.cs.purdue.edu/homes/lintan/publications/cradle-icse19.pdf), *ICSE 2019* [Kernels] — Differential testing across DL backends to expose and localize inconsistencies.
- [A Static Analyzer for Detecting Tensor Shape Errors in Deep Neural Network Training Code](https://dl.acm.org/doi/abs/10.1145/3510454.3528638), *ICSE 2022* [Training] — Abstract-interpretation-based static analysis to detect tensor shape errors. [Review](reviews/A-Static-Analyzer-for-Detecting-Tensor-Shape-Errors-in-Deep-Neural-Network-Training-Code.md)
- [AutoTrainer: An Automatic DNN Training Problem Detection and Repair System](https://dl.acm.org/doi/10.1109/ICSE43902.2021.00043), *ICSE 2021* [Training] — Detects training issues and applies automated repairs to improve convergence.
- [Reliability Assurance for Deep Neural Network Architectures against Numerical Defects](https://dl.acm.org/doi/abs/10.1109/ICSE48619.2023.00156), *ICSE 2023* [Kernels] — Identifies and mitigates numerical instability (e.g., NaNs/overflow) in DNN computation.
- [NeuRI: Diversifying DNN Generation via Inductive Rule Inference](https://arxiv.org/abs/2302.02261), *FSE 2023* [Kernels] — Generates diverse DNNs via learned transformation rules to boost test coverage.
- [NNSmith: Generating Diverse and Valid Test Cases for Deep Learning Compilers](http://arxiv.org/abs/2207.13066), *ASPLOS 2023* [Kernels] — Synthesizes semantically valid models to stress and validate DL compilers.
- [Fuzzing Automatic Differentiation in Deep-Learning Libraries](https://arxiv.org/pdf/2302.04351), *ICSE 2023* [Kernels] — Fuzzes autodiff implementations to reveal gradient calculation bugs.
- [Fuzzing Deep-Learning Libraries via Automated Relational API Inference](https://arxiv.org/pdf/2207.05531), *FSE 2022* [Kernels] — Infers API relations to generate relational checks that uncover defects.
- [Free Lunch for Testing: Fuzzing Deep-Learning Libraries from Open Source](http://lingming.cs.illinois.edu/publications/icse2022a.pdf), *ICSE 2022* [Kernels] — Leverages OSS artifacts to derive oracles and fuzz tests for DL libraries.
- [Automated Testing of Software that Uses Machine Learning APIs](https://ieeexplore.ieee.org/document/9793999), *ICSE 2022* [Inference] — Techniques for testing applications that integrate ML APIs and handling API misuses.
- [Keeper: Automated Testing and Fixing of Machine Learning Software](https://www.microsoft.com/en-us/research/publication/keeper-automated-testing-and-fixing-of-machine-learning-software/), *TOSEM 2024* [Training] — End-to-end system to automatically generate tests and propose fixes for ML code.

## Monitoring

- [Training with Confidence: Catching Silent Errors in Deep Learning Training with Automated Proactive Checks](https://www.arxiv.org/abs/2506.14813), *OSDI 2025* [Training] — Proactive runtime monitoring via inferred invariants to detect silent training errors.
- [Self-Checking Deep Neural Networks in Deployment](https://dl.acm.org/doi/abs/10.1109/ICSE43902.2021.00044), *ICSE 2022* [Inference] — Embeds runtime checks to detect anomalies and trigger self-tests during inference.

## Model Behavior Testing

- [DeepXplore: Automated Whitebox Testing of Deep Learning Systems](https://dl.acm.org/doi/10.1145/3132747.3132785), *SOSP 2017* [Inference] — Introduces neuron coverage and differential testing to generate inputs and expose discrepancies.
- [Oracle Issues in Machine Learning and Where to Find Them](https://dl.acm.org/doi/10.1145/3387940.3391490), *ICSEW 2020* [Data] — Identifies and detects issues in ML oracles/labels using entropy and semantic analysis. [Review](reviews/Oracle-Issues-in-Machine-Learning-and-Where-to-Find-Them.md)

## Fault Injection Tools
- [NVBitFI: Dynamic Fault Injection for GPUs](https://ieeexplore.ieee.org/abstract/document/9505068), *DSN 2021* [Kernels] — Injects faults into GPU binaries to evaluate resilience and error propagation in DL workloads.

## Industry Post Mortems
- [Anthropic: A Postmortem of Three Recent Issues](https://www.anthropic.com/engineering/a-postmortem-of-three-recent-issues) — Lessons and mitigations drawn from consecutive reliability incidents in Claude models during Aug 2025.

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
