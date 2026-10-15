# Machine Learning & Social Network Analysis

As part of a Data Science course project at Toronto Metropolitan University, I explored machine learning performance, data parallelization and recommendation-driven social network connectivity. Using the **DSMP Social Network Simulator**, I conducted experiments, collected performance measurements, created visualizations and analyzed the results to better understand algorithm scalability and social network behaviour.

## At a Glance

| Area | Focus | Dataset | Tools |
| :--- | :--- | :--- | :--- |
| Parallel ML benchmarking | Compare K-Means and SVM execution times using 1, 2, 4 and 8 processing nodes | Provided 57k dataset | DSMP Simulator |
| Social network analysis | Examine Doc2Vec-based recommendations and network connectivity | Provided `Retail.txt` dataset (153 nodes) | DSMP Simulator, Gephi |

## 1. Parallel ML Benchmarking

I ran K-Means and Support Vector Machine (SVM) experiments across four processing-node configurations and recorded the execution times reported by the simulator. The measurements reflect **runtime**, not model accuracy.

### Recorded Results

| Processing nodes | K-Means (ms) | SVM (ms) | K-Means speedup | SVM speedup |
| ---: | ---: | ---: | ---: | ---: |
| 1 | 237,249 | 7,883 | 1.00× | 1.00× |
| 2 | 153,589 | 6,975 | 1.54× | 1.13× |
| 4 | 159,768 | 5,296 | 1.49× | 1.49× |
| 8 | 183,727 | 6,787 | 1.29× | 1.16× |

The measurements are available in [`data/benchmark-results.csv`](data/benchmark-results.csv). Speedup is calculated as `T(1) / T(N)`, where `T(1)` is the single-node runtime and `T(N)` is the runtime with N nodes.

### Performance Visualizations

The following charts were recreated from the recorded measurements, not from additional simulator runs.

<p align="center"><img src="assets/execution-time.png" width="650" alt="Execution time comparison for K-Means and SVM"></p>

<p align="center"><img src="assets/speedup.png" width="650" alt="Parallel processing speedup by node count"></p>

### Original Experimental Graphs

These graphs were created during the original experiment and are retained as part of the project record.

<p align="center"><img src="assets/original-timing-gains.png" width="550" alt="Original timing graph with gain annotations"></p>

<p align="center"><img src="assets/original-timing-comparison.png" width="550" alt="Original K-Means and SVM runtime comparison"></p>

### Benchmark Findings

- **K-Means:** The fastest tested configuration used **2 nodes**, completing in **153,589 ms**, a **35.3% runtime reduction** compared with one node.
- **SVM:** The fastest tested configuration used **4 nodes**, completing in **5,296 ms**, a **32.8% runtime reduction** and approximately **1.49× speedup** compared with one node.
- **Scalability:** More processing nodes did not consistently reduce runtime. Both algorithms became slower beyond their fastest tested configurations.
- **Comparison:** SVM ran faster than K-Means in these experiments, but runtime alone does not establish which algorithm is more accurate or better suited to a different task.

## 2. Recommendation-Driven Social Network Analysis

I used the simulator's **Doc2Vec** recommendation option with the provided `Retail.txt` dataset. I ran the experiment using a single processing node, then inspected the exported social network with **Gephi** to examine connectivity and graph structure.

### Network Visualization

<p align="center"><img src="assets/gephi-network.png" width="500" alt="Gephi visualization of the simulated social network"></p>

### Recorded Gephi Statistics

| Network metric | Reported value |
| :--- | ---: |
| Nodes | 153 |
| Edges | 2 |
| Average degree | 0.026 |
| Connected components | 151 |
| Network diameter | 2 |
| Average path length | 1.333 |

The recorded network was sparse, with most nodes remaining isolated. The experiment illustrated how recommendation-driven connections can affect network structure and provided practical experience interpreting graph metrics.

## 3. Conclusion

These experiments highlighted two complementary aspects of data science: **evaluating computational performance** and **interpreting network structure**.

In the parallelization experiment, adding processing nodes initially improved runtime, but the fastest configuration depended on the algorithm. K-Means performed best with two nodes, while SVM performed best with four. This reinforced that scalability should be evaluated with measurements rather than assuming more resources always lead to better performance. Communication and synchronization overhead are possible explanations for diminishing gains, although they were not measured separately.

In the social network experiment, Doc2Vec-based recommendations provided a way to explore connections within a simulated network. Gephi helped quantify how sparse the resulting graph was through its node, edge and connected-component statistics.

Together, the projects strengthened my experience with **ML benchmarking, data parallelization, performance visualization, recommendation systems and social network analysis**.

## Attribution

The **DSMP Social Network Simulator** and its underlying algorithms were developed by the original contributors. My work focused on configuring and running experiments, collecting measurements, creating charts, examining the exported network with Gephi and interpreting the findings.

**Original simulator:** [d-ibanescu/SocialNetworkSimulatorV3.1](https://github.com/d-ibanescu/SocialNetworkSimulatorV3.1)
