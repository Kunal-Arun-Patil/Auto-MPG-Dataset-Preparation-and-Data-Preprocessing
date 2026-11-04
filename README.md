# Machine Learning – CIE 2, Activity 1: Dataset Preparation

**Course:** Machine Learning [ADPC509]
**Class:** T.Y. B.Tech (AI & DS), Semester V, Academic Year 2026–27
**Name:** _<your name>_  **Roll No.:** _<your roll number>_  **Division:** _<A/B/C>_

## Dataset

| Item | Detail |
|---|---|
| Name | Auto MPG |
| Domain | Transport (fuel efficiency of cars, model years 1970–1982) |
| Source | UCI Machine Learning Repository (originally from StatLib, Carnegie Mellon University) |
| Link | https://archive.ics.uci.edu/dataset/9/auto+mpg |
| File type | `auto-mpg.data` (plain text, whitespace-separated, no header row) |
| Size | 398 rows × 9 columns |

The data contains no personal, confidential or restricted information.

## Files in this submission

| File | Description |
|---|---|
| `auto-mpg.data` | Original dataset (not modified) |
| `Activity1_Auto_MPG_Dataset_Preparation.ipynb` | Notebook with all 10 steps, explanations and outputs |
| `Activity1_Auto_MPG_Dataset_Preparation.html` | The same notebook exported as a web page |
| `auto_mpg_cleaned.csv` | Cleaned dataset, readable (not encoded or scaled), 398 × 10 |
| `auto_mpg_prepared.csv` | Final prepared dataset (encoded and scaled, ready for ML), 398 × 10 |
| `README.md` | This file |

## How to run

1. Put `auto-mpg.data` and the notebook in the same folder (or upload both to Google Colab).
2. Open `Activity1_Auto_MPG_Dataset_Preparation.ipynb` in Jupyter Notebook or Colab.
3. Run all cells from top to bottom.

**Libraries needed:** `pandas`, `numpy`, `matplotlib`, `seaborn`, `scikit-learn`

```
pip install pandas numpy matplotlib seaborn scikit-learn
```

## Steps performed

1. **Select a dataset:** Auto MPG from UCI, source and details recorded.
2. **Load and inspect:** loaded with manual column names, shown head and tail, shape, column names and data types.
3. **Data types and statistics:** separated numerical and categorical columns, reviewed summary statistics, chose `mpg` as the possible target.
4. **Identify missing values:** counts and percentages for every column.
5. **Handle missing values:** took a copy of the original, filled `horsepower` with the median, verified no missing values remain.
6. **Duplicates and consistency:** no duplicates found, fixed brand spelling variants, made `origin` and `model_year` readable.
7. **Basic EDA:** summary statistics, frequency counts, histogram, bar chart, box plot, scatter plot and correlation heatmap, with observations.
8. **Encode categorical features:** one-hot encoded `origin`, dropped the identifier `car_name`, explained why `brand` was not one-hot encoded.
9. **Scale numerical features:** standardised the six feature columns (the target `mpg` was not scaled).
10. **Save prepared dataset:** verified shape, no missing values, no duplicates, saved CSV files.

## Data-quality issues found

- 6 missing values (1.5%) in `horsepower`, written as `?` in the source file
- No header row and space-separated format
- Inconsistent brand spellings in `car_name` (for example `chevy`, `chevroelt`, `vw`, `toyouta`, `maxda`, `vokswagen`, `mercedes`)
- `origin` stored as codes 1/2/3 and `model_year` stored as two digits
- Numerical columns on very different scales
- No duplicate rows

## Key decisions

| Decision | Reason |
|---|---|
| Median fill for `horsepower` | The column is right-skewed and only 1.5% is missing, so rows were kept |
| One-hot encoding for `origin` | The regions are nominal, with no natural order |
| `car_name` dropped from the ML-ready data | It is an almost unique identifier |
| Standardisation (z-score) of features | The features are on different scales; `mpg` and the 0/1 `origin` columns were left unscaled |

## Final dataset columns (`auto_mpg_prepared.csv`)

`mpg` (target), `cylinders`, `displacement`, `horsepower`, `weight`, `acceleration`, `model_year` (all standardised), `origin_Europe`, `origin_Japan`, `origin_USA` (one-hot, 0/1)

## Note

No model was trained in this activity. The scaler was fitted on the full dataset for demonstration only. In a real prediction task, the scaler should be fitted on the training data only and then applied to the test data, to avoid data leakage.
