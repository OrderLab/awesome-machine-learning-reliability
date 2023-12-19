# Awesome Machine Learning Reliability

A curated list of awesome machine learning reliability resources.

## TODOs

- [ ] Add more papers, blogs, and presentations.
- [ ] Try to provide a short summary for each paper. Copy my reviews to this repo.

## Table of Contents

TODO:

## Background

- [MLSys: The New Frontier of Machine Learning Systems](https://arxiv.org/pdf/1904.03257.pdf) - The white paper that you must read.
- [AI Engineering Quick Start](https://ai-engineering.club/docs/quick_start) - A great, approachable of machine learning engineering workflow and practices.

## High-Level View

- [Hidden Technical Debt in Machine Learning Systems](https://papers.nips.cc/paper/5656-hidden-technical-debt-in-machine-learning-systems.pdf), *NeurIps 2015* - A seminal paper on the hidden technical debt in machine learning systems.

## Empirical Studies on Machine Learning Bugs & Challenges

- [A comprehensive empirical study on bug characteristics of deep learning frameworks](https://linkinghub.elsevier.com/retrieve/pii/S0950584922001306), *Information and Software Technology 2021* - TODO: Add summary.
- [An Empirical Study on Program Failures of Deep Learning Jobs](https://dl.acm.org/doi/10.1145/3377811.3380362), *ICSE 2020* - An empirical study on **failure characteristics** of industry deep learning jobs from Microsoft. The study focuses on **job failures** that throw explicit exceptions.
- [An Empirical Study of Common Challenges in Developing Deep Learning Applications](https://ieeexplore.ieee.org/document/8987482), *IEEE Software 2020* - An empirical study on **challenges** in developing correct and accurate deep learning applications. It categorizes the types of issues and investigates the difficulty of debugging them.

## ML Bug Detection

- [DeepXplore: Automated Whitebox Testing of Deep Learning Systems](https://dl.acm.org/doi/10.1145/3132747.3132785), *SOSP 2017* (Best paper award) - Introduces **Neuron Coverage** to guide input generation and **Differential Testing** to detect bugs across autonomous driving systems.
- [A Static Analyzer for Detecting Tensor Shape Errors in Deep Neural Network Training Code](https://dl.acm.org/doi/abs/10.1145/3510454.3528638), *ICSE 2022* - A static analyzer for detecting **tensor shape errors** in deep neural network training code. The analyzer is based on **abstract interpretation** and **constraint solving** and it used Z3 SMT Solver to detect conflicts. [Review (TBD)](reviews/A-Static-Analyzer-for-Detecting-Tensor-Shape-Errors-in-Deep-Neural-Network-Training-Code.md)


- [Oracle Issues in Machine Learning and Where to Find Them](https://dl.acm.org/doi/10.1145/3387940.3391490), *ICSEW 2020* - An introduction to machine learning oracles (i.e. the labels of validation and test data) and how to detect issues within them using *Shannon Entropy* and *Semantic Analysis*. [Review](reviews/Oracle-Issues-in-Machine-Learning-and-Where-to-Find-Them.md)
- [CRADLE: Cross-Backend Validation to Detect and Localize Bugs in Deep Learning Libraries](https://www.cs.purdue.edu/homes/lintan/publications/cradle-icse19.pdf), *ICSE 2019* - Using **differential testing** to find bugs in different libraries' implementations of the same deep learning utilities.

- [AutoTrainer: An Automatic DNN Training Problem Detection and Repair System](https://dl.acm.org/doi/10.1109/ICSE43902.2021.00043), *ICSE 2021*

- [Reliability Assurance for Deep Neural Network Architectures against Numerical Defects](https://dl.acm.org/doi/abs/10.1109/ICSE48619.2023.00156), *ICSE 2023*

## Monitoring

- [Self-Checking Deep Neural Networks in Deployment](https://dl.acm.org/doi/abs/10.1109/ICSE43902.2021.00044), *ICSE 2022*

## ML Bug Debugging

- [Debugging Machine Learning Pipelines](https://dl.acm.org/doi/10.1145/3329486.3329489), *DEEM 2019* - Localizing root causes of ML performance anomalies in (i.e. hyperparameter, software version, data, etc.) with **decision trees** and existing runs of the same pipeline. [Review](reviews/Debugging-Machine-Learning-Pipelines.md)

## TODO:

- Beyond Accuracy: Behavioral Testing of NLP Models with CheckList
- add more papers from zotero
