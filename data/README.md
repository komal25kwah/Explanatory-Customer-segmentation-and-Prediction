# Customer feature input

Provide a CSV with one row per customer. The original customer dataset is not included.

| Column | Expected value |
|---|---|
| customer_id | Unique, non-null customer identifier |
| recency | Numeric elapsed time since the last order |
| frequency | Numeric order count |
| monetary | Numeric spending measure |
| adaptive_recency | Numeric precomputed adaptive-recency feature |

Use consistent units and the same aggregation/window definitions as your experiment. The notebook does not reconstruct these features from raw transactions.

Default input: `data/customer_features.csv`. Override with the `CUSTOMER_DATA_CSV` environment variable, or edit `INPUT_CSV` in the notebook configuration.

Default generated output directory: `outputs/`. Override with `CUSTOMER_OUTPUT_DIR`.

For example, in Windows PowerShell before launching Jupyter:

```powershell
$env:CUSTOMER_DATA_CSV = "C:\Data\customer_features.csv"
jupyter notebook final-working.ipynb
```

Use only data you are authorized to process. Local input files and generated customer-level outputs are excluded from Git. Prediction inputs have a separate behavioral schema that must be documented with the original prediction notebook when uploaded.
