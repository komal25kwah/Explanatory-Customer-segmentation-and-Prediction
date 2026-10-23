# Explainable Customer Segmentation and Prediction

Research on customer segmentation and behavioral segment prediction for food-delivery engagement, developed during my MS Data Science at NUST.

The research framework combines **RFM clustering**, **Formal Concept Analysis (FCA)** and **supervised segment prediction**. The uploaded notebook covers clustering experiments and FCA-style explanations; the separate prediction training notebook is not yet included.

## Research overview

- Experimental window: **1 March–24 April 2024**.
- Final study population reported in the research: **314,786 customers**.
- Segmentation uses Recency, Frequency and Monetary features.
- An adaptive-recency extension was evaluated against standard RFM.
- Behavioral prediction experiments compare Random Forest, XGBoost and MLP.

The notebook starts from precomputed customer features. Some exploratory runs used an earlier data snapshot; input size depends on the supplied CSV. Original transaction-level preprocessing and the source dataset are not distributed here.

## Methodology

1. Load customer-level RFM and adaptive-recency features.
2. Standardize features and compare clustering configurations.
3. Evaluate cluster separation using silhouette, Calinski–Harabasz and Davies–Bouldin scores.
4. Preserve RFM-only cluster assignments and join them to customers by ID.
5. Discretize RFM into quintiles and calculate cluster-to-attribute support and confidence.
6. Build a cluster-level concept lattice from selected rules using `concepts` and Graphviz.

The uploaded code includes HDBSCAN, K-Means++, BIRCH and a sampled Agglomerative comparison. FCA-style confidence rules describe associations; they are not causal explanations.

Adaptive recency was investigated as:

$$AR = e^{-d/\mu}$$

where `d` is elapsed time since the previous order and `μ` is the mean inter-order interval used in the study. The current notebook reads this precomputed feature.

## Recorded research results

These are historical results, not newly rerun benchmarks. Cleanup clears notebook outputs to avoid presenting stale outputs alongside edited code.

| Configuration | Silhouette | Calinski–Harabasz | Davies–Bouldin |
|---|---:|---:|---:|
| RFM + K-Means++ | 0.5036 | 333,622.55 | 0.7539 |
| RFM + adaptive recency + K-Means++ | 0.4207 | 242,682.54 | 0.8212 |

The original saved evaluations used a 20,000-row resample for silhouette and full input for the other two metrics. Standard RFM performed better in these experiments.

Interpreted research segments: **Loyal**, **At-Risk**, **Frequent Buyers** and **Premium**. Numeric cluster labels must be interpreted from each fitted model's profiles; they are not fixed business categories across arbitrary reruns.

### Prediction results reported in the research

| Model | Accuracy |
|---|---:|
| Random Forest | 55.13% |
| XGBoost | 57.23% |
| MLP | 55.30% |
| Tuned MLP | 55.32% |

These results are retained from the research summary. **The prediction implementation is not yet uploaded**, so this repository currently cannot reproduce these prediction figures. Prediction uses behavioral inputs rather than RFM; the final feature list should accompany that notebook.

## Run the notebook

1. Clone the repository and create a Python environment.
2. Install dependencies:

```bash
python -m pip install -r requirements.txt
```

3. Install the **Graphviz system application** if rendering lattice diagrams; its `dot` executable must be on PATH. The Python package alone does not provide the executable.
4. Place your authorized customer feature CSV at `data/customer_features.csv`, or set `CUSTOMER_DATA_CSV` to its path before starting Jupyter.
5. Open `final-working.ipynb` and run cells in order.

```bash
jupyter notebook final-working.ipynb
```

The first cell validates the input schema and creates the output directory. Set `CUSTOMER_OUTPUT_DIR` to change the default `outputs/` location. See [data requirements](data/README.md).

HDBSCAN, hierarchical clustering and large silhouette samples can be expensive on hundreds of thousands of customers. This notebook is a research workflow, not a deployed real-time service.

## Repository files

| Path | Contents |
|---|---|
| `final-working.ipynb` | Clustering and FCA experiments |
| `requirements.txt` | Notebook dependencies; exact original environment versions were not recorded here |
| `data/README.md` | Input schema and configuration |
| `.gitignore` | Excludes private datasets, generated outputs and local environments |

Generated outputs include cluster assignments, FCA confidence tables and lattice diagrams. Customer data is not committed.

## Verification and remaining work

The cleanup was checked by compiling all Python code cells and exercising ID-aligned label export and FCA rule generation on synthetic data. Full experiments require the original authorized data and have not been rerun as part of this cleanup.

Remaining work: upload the original prediction notebook, document its feature schema and split, and add the transaction-to-customer feature-engineering implementation.

## Author

**Komal Wahid**  
MS Data Science, National University of Sciences and Technology (NUST)

Research title: *An Explainable Customer Segmentation and Prediction Framework for Real-Time Customer Engagement*.
