# Complexity-Stability Analysis for Software Bug Prediction

This project explores the relationship between **software complexity metrics** and the **stability of feature selection algorithms** in the context of software defect prediction. It combines data from multiple open-source projects and evaluates how dataset-level complexity influences the consistency of feature selection across algorithms such as Chi2, Mutual Information, ReliefF, and Lasso.

---

## Project Steps

The project is organized into 17 structured steps:

### 1 Original Dataset
- CSV files from different open-source software projects are loaded.
- 10 key software metrics (e.g., WMC, CBO, LOC) and the target label `isExistBug` are filtered.
- All valid projects are combined into a single DataFrame (37,630 records).
- Bug rates per project are calculated.
- Outlier projects are detected using Z-scores.

### 2 Computation Dataset Complexity Metrics
- Using the `problexity` library, dataset complexity metrics are computed.
- Example metrics: `f1`, `density`, `clsCoef`, `score`, etc.
- Each project’s metrics are saved as separate CSV files.

### 3 Merge Complexity Metrics
- All complexity metric CSV files are merged into a single CSV file.

### 4 Feature Selection Stability Metrics
- FS is applied using four algorithms:
  - Chi-squared (Chi2)
  - Mutual Information
  - ReliefF
  - Lasso
- 30 iterations are performed for each FS method.
- Selected features are recorded for each iteration.
- Stability scores and confidence intervals (CI) are computed using binary selection matrices.

### 5 Merge Feature Selection Stability Metrics
- Stability scores are merged in a pivot table format.
- Projects are ordered according to a predefined strategy.
- Final stability scores for each FS method are saved in CSV format.

### 6 Merge Complexity Metrics and Stability Measures
- Merged using `project_name`.
- Final combined CSV is created.

### 7 Correlation Analysis between Complexity and Stability
- Pearson correlation is calculated between complexity metrics and FS stability scores.
- Heatmaps are created for visualization.
- Notable findings: `f4`, `lsc`, `t3`, and `clsCoef` show strong correlations with Lasso stability.

### 8 Feature Importance with Random Forest
- Random Forest models are trained for each project (30 iterations each).
- Average feature importance scores are calculated for the 10 metrics.
- Results are saved and visualized with bar plots.

---

## Filtered Dataset Analysis (Top 5 Features)

### 9 Feature Reduction
- Based on importance, a reduced feature set is created:
  - `WMC`, `CBO`, `RFC`, `LOC`, `NPM`

### 10 Re-computation of Complexity Metrics (Filtered)
- Complexity metrics are recalculated using the 5-feature dataset.

### 11 Merge Complexity Metrics (Filtered)
- All filtered complexity metrics are merged into a single CSV file.

### 12 FS Stability Metrics (Filtered)
- Stability scores are recalculated (K = 2) for the reduced dataset using 30 iterations.

### 13 Merge FS Stability (Filtered)
- Merged into a pivot format for all filtered projects.

### 14 Merge Complexity and Stability (Filtered)
- Final combined CSV is created for reduced feature set.

### 15 Correlation Analysis (Filtered)
- Pearson correlation heatmaps generated.
- Strong associations observed between metrics like `f4`, `clsCoef`, `t2`, `t3` and FS methods like Lasso and ReliefF.

### 16 Correlation Analysis After Removing Outliers
- Outlier projects (`Promise_xalan27`, `Promise_log4j`) are excluded.
- Correlation results become more robust and aligned with literature.

---

## Key Technologies & Libraries

- **Python 3.10+**
- `pandas`, `numpy`, `matplotlib`, `seaborn`
- `scikit-learn`, `skrebate`, `problexity`
- Custom FS stability scoring module

---

## Project Objectives

- Apply multiple feature selection (FS) algorithms across several software datasets.
- Calculate the **stability** of FS algorithms using Nogueira’s index.
- Compute software **complexity metrics** using the `problexity` library.
- Correlate complexity with FS stability to identify patterns.
- Determine and compare feature importance using Random Forest.

---

## Pipeline Summary

### 1. Load & Prepare Data
- Load `.csv` files from open-source projects.
- Keep 9 metrics (e.g., `WMC`, `CBO`, `RFC`, etc.) + `isExistBug` label.
- Merge all datasets into one (37,630 records) and remove statistical outliers.

### 2. Compute Complexity Metrics
- Use `problexity` to compute 20+ dataset-level metrics like `f1`, `density`, `clsCoef`, `score`, etc.
- Save results per project and merge.

### 3. Feature Selection & Stability
- Apply FS using: `Chi2`, `Mutual Info`, `ReliefF`, `Lasso`.
- Repeat each algorithm 30 times per project.
- Measure **stability** using binary selection matrix → Nogueira Index.

### 4. Correlation Analysis
- Merge complexity and stability data.
- Compute Pearson correlations.
- Visualize via heatmaps.

### 5. Feature Importance
- Train `RandomForestClassifier` across 30 iterations per project.
- Compute average importance for all 10 features.
- Identify top 5 most impactful: `WMC`, `CBO`, `RFC`, `LOC`, `NPM`.

### 6. Filtered Dataset Analysis
- Redo steps 2–4 with reduced 5-feature datasets.
- Results become more interpretable and aligned with literature.

---

## Outputs

| File / Folder | Description |
|---------------|-------------|
| `summary_feature_importance_mean.csv` | Mean feature importance from Random Forest |
| `merged_complexity_and_stability.csv` | Combined complexity + stability |
| `correlation_complexity_vs_stability.csv` | Pearson correlation table |
| `project.pdf` | Clean output version of Jupyter analysis |
| `project.ipynb` | Full pipeline code with outputs |
| `correlation_complexity_vs_stability.xlsx` | Final coloured combined complexity + stability |

---

## How to Run This Project

Follow the steps below to set up and run the full pipeline from scratch:

### 1. Clone the Repository

```bash
git clone https://github.com/ramazangurpinar/complexity_stability.git
cd complexity_stability
```

### 2. (Optional) Create a Virtual Environment

```bash
python -m venv venv
```

```On macOS/Linux:
source venv/bin/activate
```

```On Windows:
venv\Scripts\activate.bat
```

### 3. Install Dependencies

```bash
pip install -r requirements.txt
```

### 4. Launch the Jupyter Notebook

```bash
jupyter notebook notebooks/project.ipynb
```

## Project Structure

## Project Directory Structure

<details>
<summary>Click to expand the full folder structure</summary>
<br>
  
```plaintext
DissertationProject/
│
├── README.md
│   └── Project description and usage guide (this file)
│
├── requirements.txt
│   └── Python dependencies required to run the project
│
├── notebooks/
│   ├── project.ipynb
│   │   └── Main Jupyter Notebook containing all analysis steps
│   └── stability/
│       └── Custom module for computing Nogueira’s stability index
│
├── code-pdf/
│   └── project.pdf
│       └── Exported PDF version of the Jupyter notebook
│
├── data/
│   ├── original-datasets/
│   │   └── Raw CSV files containing 9 software metrics + target label (`isExistBug`)
│   │
│   ├── originaldata-complexity-metrics/
│   │   └── Computed dataset-level complexity metrics (one file per project)
│   │
│   ├── originaldata-fs-stability-metrics/
│   │   └── Feature selection stability scores from 4 FS algorithms (Chi2, MI, ReliefF, Lasso)
│   │
│   ├── filtered-datasets/
│   │   └── Same datasets as original, reduced to top 5 most important features
│   │
│   ├── filtereddata-complexity-metrics/
│   │   └── Recalculated complexity metrics using filtered datasets
│   │
│   ├── filtereddata-fs-stability-metrics/
│   │   └── FS stability scores computed again using filtered features
│   │
│   └── results/
│       ├── originaldata-results/
│       │   └── Merged results, feature importance and correlation (from original datasets)
│       │
│       ├── filtereddata-results/
│       │   └── Same result structure for the filtered (top-5) datasets
│       │
│       └── overall-results/
│           └── Final combined analysis across all projects and settings

```
