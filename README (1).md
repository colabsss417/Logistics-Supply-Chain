# D2P2-GAT

## Dynamic Dual-Path Graph Attention Network for Intelligent Supply Chain Logistics Routing

D2P2-GAT is a graph-based routing framework designed for intelligent supply chain and delivery logistics. The framework models logistics networks as graph structures and incorporates complementary attention mechanisms to support route selection under spatial, relational, temporal, congestion, risk, and delivery-related conditions.

The repository contains the implementation workflow, preprocessing utilities, routing optimization procedures, evaluation scripts, scalability experiments, and ablation-analysis outputs used to evaluate the D2P2-GAT framework.

---

## 1. Project Overview

Modern supply chain logistics involves dynamic interactions among distribution nodes, transportation links, traffic conditions, route risk, congestion, and delivery urgency. Conventional shortest-path routing may not adequately represent these interacting factors.

D2P2-GAT addresses this problem using a graph-attention-based routing framework with three principal attention components:

1. **Edge-Level Attention**  
   Represents characteristics associated with transportation links and route-level costs.

2. **Spatial-Relational Attention**  
   Captures relationships among connected logistics nodes and spatial routing conditions such as risk and congestion.

3. **Temporal-Urgency Attention**  
   Represents time-sensitive delivery conditions, including delivery-time and delay-related information.

The complete model combines these components to obtain an attention-informed routing representation for route optimization.

---

## 2. Main Components

The implementation is organized around the following workflow:

```text
Raw Logistics Dataset
        │
        ▼
Data Loading & Validation
        │
        ▼
Data Preprocessing
        │
        ▼
Logistics Graph Construction
        │
        ▼
Graph Attention Representation
        │
        ├── Edge-Level Attention
        │
        ├── Spatial-Relational Attention
        │
        └── Temporal-Urgency Attention
        │
        ▼
Attention-Aware Route Evaluation
        │
        ▼
Candidate Route Generation
        │
        ▼
Route Optimization
        │
        ▼
Optimal Route Selection
        │
        ▼
Performance Evaluation
        │
        ├── OTDR
        ├── Delivery Time
        ├── Inference Latency
        ├── Routing Cost
        ├── DTEI
        └── Path Deviation
        │
        ▼
Ablation & Scalability Analysis
```

---

## 3. Repository Structure

A recommended repository organization is:

```text
D2P2-GAT/
│
├── README.md
├── requirements.txt
├── LICENSE
│
├── data/
│   ├── raw/
│   └── processed/
│
├── preprocessing/
│   └── data_preprocessing.py
│
├── graph/
│   └── graph_construction.py
│
├── models/
│   ├── edge_attention.py
│   ├── spatial_attention.py
│   ├── temporal_attention.py
│   └── d2p2_gat.py
│
├── routing/
│   ├── candidate_route_generation.py
│   └── route_optimization.py
│
├── evaluation/
│   ├── performance_evaluation.py
│   ├── statistical_validation.py
│   ├── ablation_study.py
│   └── scalability_analysis.py
│
├── experiments/
│   ├── distance_analysis.py
│   └── ten_run_validation.py
│
├── visualization/
│   └── plotting.py
│
└── results/
    ├── candidate_routes.csv
    ├── selected_optimal_route.csv
    ├── route_robustness.csv
    ├── ablation_results.csv
    └── scalability_results.csv
```

> The exact filenames can be adjusted to match the final implementation uploaded to the repository.

---

## 4. Dataset

The framework uses a dynamic supply-chain logistics dataset containing route and logistics-related observations.

The working dataset used during development is:

```text
dynamic_supply_chain_logistics_dataset.csv
```

The local development path used in the experiments was:

```text
F:\.0 Work\dynamic_supply_chain_logistics_dataset.csv
```

For GitHub, the dataset should be placed under:

```text
data/raw/
```

if redistribution of the dataset is permitted.

### Important

Do not commit private, confidential, licensed, or restricted data to a public repository. If the original dataset has redistribution restrictions, provide the official dataset source and instructions for obtaining it instead.

---

## 5. Data Processing

The preprocessing stage prepares the logistics records for graph-based routing.

Typical processing operations include:

- Loading the raw CSV dataset
- Inspecting data types and column structure
- Handling missing values
- Converting numerical variables to numeric format
- Preparing route and node identifiers
- Preparing routing-related attributes
- Validating candidate route information
- Preparing features required for graph construction

The preprocessing scripts should be executed before graph construction and route optimization.

---

## 6. Graph Construction

The logistics network is represented as a graph:

```text
G = (V, E)
```

where:

- `V` represents logistics nodes
- `E` represents transportation connections
- Node attributes represent logistics/network conditions
- Edge attributes represent transportation and routing characteristics

The graph can be stored in GraphML format for subsequent routing and analysis.

Example:

```text
d2p2_gat_attention_graph.graphml
```

---

## 7. D2P2-GAT Attention Mechanisms

### 7.1 Edge-Level Attention

Edge-level attention represents the characteristics of individual transportation links.

It can incorporate route-related information such as:

- Edge cost
- Transportation conditions
- Route risk
- Link-level characteristics

The resulting attention representation contributes to the routing score.

### 7.2 Spatial-Relational Attention

Spatial-relational attention models relationships between connected logistics nodes.

Relevant information can include:

- Network connectivity
- Spatial relationships
- Traffic congestion
- Route risk
- Local network conditions

This component helps the framework distinguish routes according to their network context rather than treating links independently.

### 7.3 Temporal-Urgency Attention

Temporal-urgency attention incorporates time-sensitive delivery information.

Relevant variables can include:

- Delivery-time characteristics
- ETA variation
- Delay probability
- Delivery urgency

This component is intended to improve route selection when delivery timeliness is important.

---

## 8. Candidate Route Generation

Candidate routes are generated from the logistics graph and evaluated using routing-related attributes.

A typical output is:

```text
candidate_routes.csv
```

The candidate-route file may contain variables such as:

```text
route_id
source_node
destination_node
path
distance_km
path_cost
eta_variation
risk
congestion
attention-related scores
```

The exact columns depend on the dataset and implementation version.

---

## 9. Route Optimization

The route optimization stage evaluates candidate routes using the D2P2-GAT attention representation.

The selected route is saved as:

```text
selected_optimal_route.csv
```

A route-robustness analysis can additionally be generated as:

```text
route_robustness.csv
```

The optimization stage should use the same preprocessing, graph representation, and parameter configuration used for the reported experiments.

---

## 10. Evaluation Metrics

The framework is evaluated using multiple logistics performance measures.

### On-Time Delivery Rate (OTDR)

OTDR measures the proportion of deliveries completed within the defined delivery-time requirement.

```text
OTDR (%) =
(On-time deliveries / Total deliveries) × 100
```

An actual delivery-status or on-time ground-truth variable should be used when reporting empirical OTDR.

### Delivery Time

Delivery time represents the time required to complete a selected route, expressed in minutes.

### Inference Latency

Inference latency measures the time required to generate a routing decision.

```text
Inference Latency (ms)
```

### Routing Cost

Routing cost represents the aggregate cost associated with a selected route according to the defined routing objective.

### DTEI

DTEI is used as an additional delivery/routing evaluation indicator in the experimental analysis. Its exact formulation should follow the mathematical definition used in the manuscript and implementation.

### Path Deviation

Path deviation measures the difference between the selected route and the corresponding reference/optimal route according to the implementation's defined path-comparison procedure.

---

## 11. Distance-Wise Evaluation

The routing framework can be evaluated at different route-distance levels:

```text
5 km
10 km
15 km
20 km
25 km
```

For each distance level, the implementation can report:

- Inference Latency (ms)
- OTDR (%)
- P_opt (%)

An average value across the distance levels is also reported.

---

## 12. Statistical Validation

The implementation supports validation across 10 paired experimental runs.

The statistical analysis reports:

- D2P2-GAT Mean ± SD
- Mean Difference
- SD of Differences
- Paired t-statistic
- p-value

The evaluated metrics include:

```text
OTDR (%)
Inference Latency (ms)
DTEI
Path Deviation (%)
```

For paired testing, each D2P2-GAT observation should correspond to the same experimental condition as its comparison observation.

The paired difference is:

```text
d_i = X_D2P2,i - X_baseline,i
```

and the paired t-statistic is:

```text
t = mean(d) / (SD(d) / sqrt(n))
```

with:

```text
n = 10
```

---

## 13. Ablation Study

The contribution of the three attention mechanisms is investigated using four model variants.

| Model Variant | Edge-Level Attention | Spatial-Relational Attention | Temporal-Urgency Attention |
|---|:---:|:---:|:---:|
| D2P2-GAT w/o Edge Attention | ✗ | ✓ | ✓ |
| D2P2-GAT w/o Spatial Attention | ✓ | ✗ | ✓ |
| D2P2-GAT w/o Temporal-Urgency Attention | ✓ | ✓ | ✗ |
| Complete D2P2-GAT | ✓ | ✓ | ✓ |

The ablation analysis reports:

- On-Time Delivery (%)
- Delivery Time (min)
- Inference Latency (ms)
- Routing Cost

The complete D2P2-GAT configuration should use all three attention mechanisms.

---

## 14. Scalability Analysis

The scalability experiment evaluates routing performance under increasing logistics workloads.

| Delivery Tasks/hour | Number of Nodes |
|---:|---:|
| 200 | 1,200 |
| 400 | 2,400 |
| 600 | 3,600 |

The following measures are reported:

- Inference Latency (ms)
- Memory Consumption (MB)
- Processing Time (s)
- Routing Success Rate (%)

### Interpretation

Increasing the number of nodes and delivery tasks provides a stress test of the routing implementation.

The experiment should be performed using graph instances containing the specified number of nodes. If the available graph contains fewer nodes, the experiment should not be labelled as a 1,200-, 2,400-, or 3,600-node experiment without first constructing the corresponding graph instances.

---

## 15. Reproducibility

For reproducible experiments:

1. Use the same dataset version.
2. Use the same preprocessing configuration.
3. Use the same graph-construction procedure.
4. Use the same model configuration.
5. Fix random seeds where stochastic operations are used.
6. Record Python and package versions.
7. Keep the experimental train/validation/test or evaluation partitions fixed where applicable.
8. Preserve the generated candidate-route and evaluation files.
9. Run the statistical analysis on the same paired experimental conditions.

A recommended random seed is:

```python
SEED = 42
```

when stochastic operations are present.

---

## 16. Installation

Create a Python environment and install the required dependencies.

Example:

```bash
python -m venv venv
```

Activate the environment.

### Windows

```bash
venv\Scripts\activate
```

### Linux/macOS

```bash
source venv/bin/activate
```

Install dependencies:

```bash
pip install -r requirements.txt
```

---

## 17. Example Requirements

A typical environment may require:

```text
numpy
pandas
scipy
scikit-learn
networkx
matplotlib
openpyxl
```

If the final neural-network implementation uses a deep-learning framework, add the corresponding framework and version to `requirements.txt`.

For exact reproducibility, pin package versions after confirming the versions used for the final experiments.

---

## 18. Running the Workflow

The recommended execution order is:

```text
1. Data preprocessing
        ↓
2. Graph construction
        ↓
3. D2P2-GAT attention calculation
        ↓
4. Candidate route generation
        ↓
5. Route optimization
        ↓
6. Route robustness analysis
        ↓
7. Distance-wise evaluation
        ↓
8. Statistical validation
        ↓
9. Ablation study
        ↓
10. Scalability analysis
```

Example:

```bash
python preprocessing/data_preprocessing.py
python graph/graph_construction.py
python models/d2p2_gat.py
python routing/candidate_route_generation.py
python routing/route_optimization.py
python evaluation/performance_evaluation.py
python evaluation/statistical_validation.py
python evaluation/ablation_study.py
python evaluation/scalability_analysis.py
```

The exact commands should be updated to match the final filenames committed to the repository.

---

## 19. Output Files

The experiments can generate files such as:

```text
candidate_routes.csv
selected_optimal_route.csv
route_robustness.csv
D2P2_GAT_distance_performance_table.csv
D2P2_GAT_statistical_validation.csv
D2P2_GAT_ablation_results.csv
D2P2_GAT_scalability_results.csv
```

These files contain intermediate and final experimental results used for analysis and manuscript preparation.

---

## 20. Reproducibility and Data Integrity Notes

Performance values should be generated from the experimental data and implementation rather than manually entered into result tables.

In particular:

- OTDR should use actual on-time delivery ground truth where available.
- P_opt should use a clearly defined optimality criterion.
- Inference latency should be measured consistently across model variants.
- Memory consumption should be measured under the same execution conditions.
- Scalability experiments should use graphs with the stated node counts.
- Ablation variants should actually remove the corresponding attention mechanism.
- Statistical tests should use paired observations when the experimental design is paired.

These practices help prevent unsupported performance claims and improve experimental reproducibility.

---

## 21. Citation

If you use this repository in academic work, please cite the associated research publication.

```bibtex
@article{d2p2gat,
  title   = {Dynamic Dual-Path Graph Attention Network for Intelligent Supply Chain Logistics Routing},
  author  = {Author Name},
  journal = {Journal Name},
  year    = {Year},
  volume  = {Volume},
  number  = {Issue},
  pages   = {Pages}
}
```

Replace the placeholder bibliographic information with the final published-paper details.

---

## 22. License

Add the license that applies to the project.

For example:

```text
MIT License
```

Do not claim an open-source license for third-party datasets or code unless their original license permits it.

---

## 23. Contact

For questions regarding the implementation or research:

```text
Author/Research Group: <Name>
Email: <Email Address>
Institution: <Institution Name>
```

---

## 24. Acknowledgement

This repository is intended to support transparent and reproducible research on graph-based intelligent logistics routing, dynamic supply-chain decision support, and attention-aware route optimization.

---

## 25. Project Status

**Status:** Research / Experimental Implementation

The repository is intended for research reproducibility. Experimental configurations and reported results should be synchronized with the final manuscript version before publication.
