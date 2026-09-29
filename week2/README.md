# Extending "Assessing Model Performance": MAE vs. RMSE on Real Outliers

## Module explored

**Module 5, "Assessing Model Performance"** (Unit 1, Class: AI/ML Algorithms I).

## What this project explores

I explored the Assessing Model Performance module. The module defined MSE, RMSE, MAE, and R², and built a full worked example for classification, but never for regression, and it claimed RMSE is more sensitive to outliers than MAE without demonstrating it numerically. I built that missing regression worked example on the Students Performance dataset (math score predicted from reading score, writing score, and student background features), without altering any data. I found that the worst 5 test points, about 1.7% of the 300-point test set, accounted for 11.1% of total squared error but only 5.4% of total absolute error. This happens because squaring stretches the gap between small and large errors.

## Dataset

[Students Performance in Exams](https://www.kaggle.com/datasets/spscientist/students-performance-in-exams) (Kaggle). 1,000 rows, no missing values. Note: this dataset is widely understood to be simulated for teaching purposes rather than scraped from real school records; the statistical mechanism demonstrated here doesn't depend on that, but it's worth stating plainly.

- **Target:** math score
- **Predictors:** reading score, writing score, gender, race/ethnicity, parental level of education, lunch type, test preparation course (categorical variables dummy-encoded, one category dropped per variable as baseline)

## Approach

1. Load and inspect the data (shape, dtypes, missing values, summary statistics)
2. Encode categorical predictors as dummy variables
3. Visualize the target distribution and its relationship to the main numeric predictor
4. Fit an ordinary linear regression on a 70/30 train-test split
5. Build the train-vs-test metrics table the original module never built for regression: MSE, RMSE, MAE, and R² side by side
6. Rank test-set residuals by squared and absolute error, and measure what share of total error the worst few points carry under each

## Results

**Train vs. test metrics:**

| | MSE | RMSE | MAE | R² |
|---|---|---|---|---|
| Train | 27.54 | 5.25 | 4.20 | 0.875 |
| Test | 30.89 | 5.56 | 4.42 | 0.876 |

**Residual concentration (test set, n = 300):**

| Worst points | Share of test set | Share of total squared error | Share of total absolute error |
|---|---|---|---|
| Top 5 | 1.7% | 11.1% | 5.4% |

The same five points carry roughly twice as much weight under squared error as under absolute error, confirming the module's claim numerically, on real data, with nothing altered.

## Reproducing this

```bash
uv sync
uv run jupyter notebook
Then open week2/linear_regression.ipynb.
```

Open `linear_regression.ipynb` and select the project's virtual environment as the kernel.