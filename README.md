# What Drives the Price of a Used Car?

Identify which vehicle attributes most strongly predict price and quantify their impact, enabling a used car dealership to price inventory more accurately.

## Findings

**What drives price up:**
- Clean title (+49%)
- Porsche (+72%), Tesla (+47%), RAM (+39%), GMC (+24%)
- Diesel fuel (+38%)
- Pickup trucks and convertibles (+25%)
- Rear-wheel or 4-wheel drive

**What drives price down:**
- High mileage and age (nonlinear — accelerates at extremes)
- Parts-only title (-48%)
- Saturn (-48%), Mercury (-36%), Fiat (-36%)
- Sedans and hatchbacks (-23%)
- Front-wheel drive (-21%)

**Key caveats:** Brand coefficients are collinear with vehicle age — Tesla's premium partly reflects a narrow, recent model-year distribution rather than brand alone. A single global depreciation slope cannot capture brand-specific curves. Title status and odometer are the most actionable signals at the individual vehicle level.

## Model Performance

| Model | Train RMSE | Val RMSE | Test RMSE | Test R² |
|---|---|---|---|---|
| Linear Regression | 0.397 | 0.397 | 0.394 | 0.761 |
| Ridge | 0.397 | 0.397 | 0.394 | 0.761 |
| Lasso | 0.397 | 0.397 | 0.394 | 0.761 |
| **Polynomial Ridge** | **0.372** | **0.370** | **0.368** | **0.791** |

Polynomial Ridge is the final model. RMSE is on log-price scale. The model explains ~79% of price variance; meaningful uncertainty remains at the individual vehicle level due to missing features (condition, trim, color).

## Next Steps

- Incorporate `condition`, `model`, and `color` — likely high-value predictors
- Fit brand-specific depreciation curves to separate age effects from brand premium
- Build a pricing tool backed by the trained model for real-time valuation

## Notebook

[prompt_II.ipynb](prompt_II.ipynb)

## Data

`data/vehicles.csv` — 426,880 used vehicle listings (18 features, target: `price`)
