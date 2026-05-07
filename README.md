# What Drives the Price of a Used Car?

Identify which vehicle attributes most strongly predict price and quantify their impact, enabling a used car dealership to price inventory more accurately.

## Findings

**What drives price up:**
- Clean title (meaningful premium over rebuilt; salvage/parts-only excluded from model scope)
- Porsche (+86%), Tesla (+66%)
- Diesel fuel (+53%)
- Pickup trucks (+23%), convertibles (+15%)
- Rear-wheel or 4-wheel drive

**What drives price down:**
- High mileage and age (nonlinear; penalty accelerates at extremes)
- Saturn (-29%), Fiat (-31%)
- Hatchbacks (-27%), sedans (-25%)
- Front-wheel drive (-19%)

**Key caveats:** Brand coefficients are collinear with vehicle age. For instance, Tesla's premium partly reflects a narrow, recent model-year distribution rather than brand alone. A single global depreciation slope cannot capture brand-specific curves. Title status and odometer are the most actionable signals at the individual vehicle level.

## Model Performance

| Model | Train RMSE | Val RMSE | Test RMSE | Test R² |
|---|---|---|---|---|
| Linear Regression | 0.397 | 0.397 | 0.394 | 0.761 |
| Ridge | 0.397 | 0.397 | 0.394 | 0.761 |
| Lasso | 0.397 | 0.397 | 0.394 | 0.761 |
| **Polynomial Ridge** | **0.372** | **0.370** | **0.368** | **0.791** |

Polynomial Ridge is the final model. RMSE is on log-price scale. The model explains ~79% of price variance; meaningful uncertainty remains at the individual vehicle level due to missing features (condition, trim, color).

## Next Steps

- Incorporate `condition`, `model`, and `color` (likely high-value predictors)
- Fit brand-specific depreciation curves to separate age effects from brand premium
- Build a pricing tool backed by the trained model for real-time valuation

## Notebook

[2026-05-07-Pasero-UCBMLAI-Submission2.ipynb](2026-05-07-Pasero-UCBMLAI-Submission2.ipynb)

## Data

`data/vehicles.csv` — 426,880 used vehicle listings (18 features, target: `price`)

Source: [Craigslist Used Cars Dataset](https://www.kaggle.com/datasets/austinreese/craigslist-carstrucks-data) via Kaggle
