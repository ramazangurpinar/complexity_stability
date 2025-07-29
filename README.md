# Complexity-Stability Analysis for Software Bug Prediction

This project aims to investigate the relationship between software complexity metrics and the stability of feature selection (FS) algorithms in the context of software defect (bug) prediction.

---

## Project Structure

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

## 📄 Outputs

- `summary_feature_importance_mean.csv`
- `merged_complexity_and_stability.csv`
- Multiple correlation heatmaps
- Stability and complexity CSVs (original and filtered)

---
