### Motivation & Goal

- **What problem is this work addressing?**  
  This work addresses the development and execution patterns of Large Language Model (LLM) workloads in data center scenarios, specifically focusing on the reliability and efficiency aspects of these workloads.

- **Why the problem is important?**  
  Large Language Models (LLMs) have gained significant popularity, especially with the advent of tools like ChatGPT. Due to their enormous sizes and relatively fixed model architectures, LLM workloads present unique reliability and efficiency challenges compared to traditional ML workloads, which have smaller model sizes and more diverse architectures (e.g., LSTM, CNN). Additionally, the high cost of the necessary computational infrastructure restricts detailed insights into LLM development to a few wealthy companies. Sharing this information is crucial for academic researchers to make meaningful contributions.

- **What goals does this work aim to achieve?**  
  This work aims to provide a deep empirical study of the development and execution patterns of LLM workloads. It uses data from a company's internal data center and conducts an extensive study, investigating discrepancies between LLMs and prior task-specific Deep Learning (DL) workloads, exploring resource utilization patterns, and identifying the impact of various job failures.

### Related Work

- **What are the state-of-the-art solutions addressing this problem?**  
  Several studies have addressed DL workloads before the rise of LLMs:
  - Microsoft's work based on data collected from Philly (2017)
  - SenseTime's work based on data collected from Helios (2020)
  - Alibaba's work based on data collected from PAI (2020)

- **Why are they inadequate?**  
  The authors argue that the unique characteristics of LLMs have rendered these traditional DL workload studies obsolete:
  - **Paradigm Transition:** Traditional DL workloads typically adopt a task-specific paradigm, training models on domain-specific data. In contrast, LLMs undergo large-scale **pretraining** to create foundation models, which are then adapted to specific tasks through **alignment** on task-specific data.
  - **Tailored Software Stack:** New software like DeepSpeed, Megatron, and Alpa has emerged to accelerate training, and Orca & vLLM for efficient scheduling and memory management during inference.
  - **Unified Model Architecture:** Traditional DL workloads employ various architectures (e.g., CNN, RNN). In contrast, LLMs predominantly use the transformer architecture, leading to high uniformity in the LLM development pipeline.
  - **Shorter Job Duration & Unfair Queuing Delay:** LLM workloads, despite their large sizes, are often shorter than traditional DL workloads, which may reflect changes in workload type distribution or advancements in hardware.

### Key Contributions and Findings

- **Empirical Study:** The paper provides an in-depth study of a six-month LLM development workload trace collected from a GPU datacenter named Acme. This study highlights several key findings:
  - **Shorter Job Duration:** LLM workloads have significantly shorter job durations compared to traditional DL workloads.
  - **Imbalanced Resource Usage:** Pretraining jobs, while fewer in number, consume the majority of compute resources, whereas evaluation jobs, though numerous, use minimal resources.
  - **High GPU Utilization:** LLM workloads exhibit high GPU utilization, underscoring their computational intensity.
  - **Frequent Job Failures:** Infrastructure and hardware failures are common, particularly in long-term pretraining jobs, significantly impeding training efficiency.

- **System Efforts:**
  - **Fault-Tolerant Pretraining:** This system enhances fault tolerance through frequent model saving, failure diagnosis using heuristic rules and LLM, and automatic recovery.
  - **Decoupled Scheduling for Evaluation:** This system achieves timely performance feedback by decoupling model loading and metric computation, balancing the workload across GPUs.

### Reliability Issues

#### **Frequent Job Failures**
One of the central reliability issues in LLM development is the frequent occurrence of job failures. The paper categorizes these failures into three primary groups:

1. **Infrastructure-Related Failures:**
   - **NVLink Errors:** These errors occur due to communication issues between GPUs, often resulting from hardware malfunctions.
   - **CUDA Errors:** These errors arise from problems in the CUDA environment, often due to driver issues or hardware faults.
   - **Node Failures:** These can be caused by various hardware issues, including overheating and power supply failures.
   - **ECC Errors:** Errors related to memory corruption, which are critical in maintaining data integrity during large-scale computations.
   - **Network Errors:** Failures due to network instability, affecting data transfer between nodes.
   - **S3 Storage Errors:** Problems with accessing or writing to remote storage, impacting the retrieval or saving of model checkpoints.

2. **Framework-Related Failures:**
   - **Dataloader Killed:** Issues with the data loading process, often due to data corruption or insufficient memory.
   - **Out of Memory Errors:** These occur when the memory requirements of the model exceed the available GPU memory.
   - **Runtime Errors:** These can arise from bugs in the training script or unexpected behaviors during execution.
   
3. **Script-Related Failures:**
   - **File Not Found Errors:** These are usually due to incorrect file paths or missing data files.
   - **Permission Errors:** Issues with access rights, often due to misconfigured permissions on files or directories.
   - **Syntax Errors:** Errors in the code syntax, typically due to programming mistakes.

#### **Impact on Training Efficiency**
- **High Restart Costs:** Infrastructure-related failures, especially those involving hardware faults, require significant time and effort to diagnose and fix. This often necessitates manual intervention, leading to high restart costs and prolonged downtimes.
- **Loss of Training Progress:** Frequent job failures result in the loss of training progress. Although frequent checkpointing mitigates this to some extent, the interruption still hampers overall efficiency.
- **Resource Imbalance:** The imbalance in resource utilization, with pretraining jobs consuming most of the resources, exacerbates the impact of job failures. Evaluation jobs, although numerous, are given lower priority, leading to longer queuing delays and inefficient resource allocation.

### System Solutions

1. **Fault-Tolerant Pretraining**
   - **Asynchronous Checkpointing:** This technique reduces the overhead associated with frequent checkpointing by decoupling the checkpointing process from the training process. Checkpoints are stored in CPU memory and saved to persistent storage by a separate thread, minimizing the disruption to training.
   - **Failure Diagnosis:** The system employs a combination of heuristic rules and LLMs to accurately diagnose the root causes of failures. This approach improves the accuracy and efficiency of failure detection compared to purely rule-based methods.
   - **Automatic Recovery:** The system includes a toolkit for fast fault detection and recovery, which identifies and isolates faulty nodes, and restarts training from the last healthy checkpoint.

2. **Decoupled Scheduling for Evaluation**
   - **Decoupling Remote Model Loading:** This approach separates the model loading process from the evaluation process, reducing contention and speeding up the overall evaluation.
   - **Decoupling Metric Computation:** By decoupling metric computation from the GPU inference workload, the system minimizes GPU idle time and accelerates the evaluation process.
   - **Prior-based Elastic Scheduling:** This technique uses prior knowledge about trial runtimes to balance the workload across GPUs, optimizing resource utilization and reducing trial switch overhead.

### Critical Analysis

- **Strengths:**
  - The study provides valuable empirical data and insights into the unique challenges of LLM workloads.
  - It identifies specific inefficiencies and proposes practical solutions to improve reliability and efficiency.
  - The release of traces and system codes contributes to the academic community, enabling further research and optimization of LLM systems.

- **Weaknesses:**
  - The study does not include workload analysis for deployment and serving stages, which are crucial for comprehensive LLM lifecycle management.
  - The paper mentioned that LLM workloads suffers a super high cancellation rate. Specifically, cancelled jobs (~6% of all jobs) contributed to ~63% total GPU time in the cluster. 
  > Beyond the common cancellation motives cited in prior studies (e.g., achieving desired model performance sooner than expected, early recognition of poor hyperparameter configuration) our experience with LLM pretraining has identified two additional frequent causes: (1) Users pausing jobs to adjust parameters in response to performance anomalies, such as loss spikes. (2) Jobs stalling due to infrastructure issues without throwing error messages, only to be addressed upon manual inspection by users, leading to significant resource wastage. 
  The paper mainly explained (2), and it is a pity that (1) is not studied to show what kind of challenges the developers face despite infrastructure issues.

### Conclusion

This work makes a significant contribution by providing a detailed empirical study of LLM workloads in a data center environment, highlighting the unique challenges and inefficiencies associated with LLM development. The proposed systems for fault-tolerant pretraining and decoupled scheduling for evaluation offer practical solutions to enhance the reliability and efficiency of LLM development. The insights and resources provided by this study will be valuable for both academic researchers and industry practitioners working on optimizing LLM systems and GPU cluster management.