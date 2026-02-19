# What Drives the Price of a Used Car?

## Overview

This project analyzes a dataset of **426,000+ used car listings** from Kaggle to identify the key factors that influence used car prices. The goal is to provide actionable recommendations to a used car dealership on what consumers value most — helping them optimize inventory and pricing strategy.

The analysis follows the **CRISP-DM** framework (Cross-Industry Standard Process for Data Mining) through all six phases: Business Understanding, Data Understanding, Data Preparation, Modeling, Evaluation, and Deployment.

## Findings

Using Ridge, Lasso, and Linear Regression models, I found that the following features have the strongest influence on used car prices:

| Rank | Feature            | Effect on Price | Interpretation                                                         |
| ---- | ------------------ | --------------- | ---------------------------------------------------------------------- |
| 1    | **Age**            | ↓ $7,989        | The single strongest driver — newer cars sell for significantly more   |
| 2    | **Fuel (gas)**     | ↓ $5,396        | Gas vehicles are worth less than diesel — diesel trucks hold value     |
| 3    | **Miles per year** | ↓ $3,367        | Cars driven harder depreciate faster, even at the same age             |
| 4    | **Drive (FWD)**    | ↓ $2,556        | Front-wheel drive (sedans/compacts) commands lower prices than 4WD/RWD |
| 5    | **Type (pickup)**  | ↑ $1,759        | Pickups sell at a premium over other vehicle types                     |
| 6    | **Type (truck)**   | ↑ $1,495        | Trucks also command higher prices                                      |

### Model Performance

| Model             | Test RMSE | Test R² |
| ----------------- | --------- | ------- |
| Linear Regression | $8,976    | 0.6326  |
| Ridge (α=10.0)    | $8,976    | 0.6326  |
| Lasso (α=0.1)     | $8,976    | 0.6326  |

All three models performed identically — the data is well-conditioned and regularization provides no additional benefit. The model explains **63.3%** of price variance with an average prediction error of **±$8,976**.

### Recommendations for Dealers

1. **Prioritize newer, low-mileage inventory** — Age and miles-per-year are the two largest price drivers
2. **Stock diesel trucks and pickups** — These command the highest premiums
3. **Highlight 4WD/AWD in listings** — Front-wheel drive reduces price by ~$2,500 vs. 4WD/RWD
4. **Avoid over-investing in budget brands** — Nissan, Hyundai, and Kia sell for ~$1,000 less than average

### Limitations & Next Steps

- The model explains 63% of price variance; the remaining 37% is driven by factors not in our dataset (photos, condition, local demand)
- `condition` and `cylinders` were dropped due to ~41% missing data — imputing these could improve accuracy
- I removed `model` because it had 29K unique values. A frequency-based encoding or grouping into broader categories could recover some of that signal:
  - **Frequency:** Use how popular a model is in the dataset as the feature (e.g., f-150 appears 8,009 times → high-demand model)
  - **Grouping:** Keep the top 20–50 most common models and lump everything else into "other"

## Notebook

📓 [View the full analysis notebook](prompt_II.ipynb)

## Data

- **Source:** [Kaggle — Used Cars Dataset](https://www.kaggle.com/datasets/austinreese/craigslist-carstrucks-data)
- **Size:** 426,880 rows × 18 columns
- **Target variable:** `price` (continuous)

## Repository Structure

```
├── README.md              ← You are here
├── prompt_II.ipynb         ← Main analysis notebook
└── images/
    └── crisp.png        ← Crisp-DM framework image
    └── kurt.jpeg        ← Kurt Vonnegut image
└── data/
    └── vehicles.csv        ← Raw dataset (426K listings)
```

## Acknowledgments

- [Kaggle](https://www.kaggle.com/) for the dataset
- [CRISP-DM](https://en.wikipedia.org/wiki/Cross-industry_standard_process_for_data_mining) for the framework
- [Kurt Vonnegut](https://en.wikipedia.org/wiki/Kurt_Vonnegut) for the image
