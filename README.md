#  Predicting NBA Impact from College Performance

**Repository:** [https://github.com/chouiie/Predicting-NBA-Impact-from-College-Performance./
]

Which college stats actually predict success in the NBA? This project builds a multiple linear regression model on 386 drafted players to find out. It controls for draft position, position, and age so the model measures what college performance adds beyond what scouts already priced in.

**Key finding:** College **Box Plus-Minus (BPM)** is the strongest predictor of NBA impact (β = 0.40, p < 0.001). Effective field goal percentage (eFG%) and college playing time were **not** statistically significant once other factors were controlled for.

---

## Table of Contents

- [Data](#data)
- [Methodology](#methodology)
- [Results](#results)
- [Model Diagnostics](#model-diagnostics)
- [Tech Stack](#tech-stack)
- [Project Structure](#project-structure)
- [Getting Started](#getting-started)
- [Limitations and Future Work](#limitations-and-future-work)

---

## Data

The final dataset contains **386 drafted players**, built by cleaning and merging three sources:

| Source | Description |
|---|---|
| NCAA player statistics | 61,000+ college player-season records |
| NBA draft data | 13 years of draft results (pick number, team, position) |
| FiveThirtyEight RAPTOR | Advanced player ratings used to measure NBA impact |

### Merging and Cleaning

The three sources don't share a common player ID, so merging them meant resolving **entity mismatches**: name spelling variations, suffixes (Jr., III), nicknames, and players with the same name. Players were matched across sources and filtered to those with both a college record and an NBA RAPTOR rating.

---

## Methodology

1. **Data preparation:** Cleaned and merged the three sources with Python and Pandas, then engineered the analysis dataset.
2. **Model:** Fit an Ordinary Least Squares (OLS) multiple linear regression predicting NBA impact from college statistics.
3. **Controls:** Included draft position, player position, and age at draft, so college stat coefficients reflect information beyond what the draft already captured.
4. **Inference:** Evaluated individual features with t-tests and 95% confidence intervals, and the overall model with an F-test.
5. **Validation:** Checked regression assumptions with residual analysis and tested for multicollinearity with Variance Inflation Factors (VIF).

The approach draws on statistical learning theory and linear algebra, including the matrix form of OLS estimation.

---

## Results

| Finding | Detail |
|---|---|
| Overall model | Statistically significant (F-test p < 0.001) |
| Strongest predictor | College Box Plus-Minus (β = 0.40, p < 0.001) |
| Not significant | eFG%, college playing time |

**Interpretation:** A player's overall on-court impact in college (BPM) carries forward to the NBA. Shooting efficiency and minutes played don't add predictive value once draft position and other controls are in the model, which suggests they're either already reflected in where a player is drafted or don't translate cleanly to the pro level.

---

## Model Diagnostics

- **Residual analysis:** Residual plots were checked for linearity, constant variance, and approximate normality.
- **Multicollinearity:** All VIFs < 2.2, well below common thresholds of 5 or 10, so predictors are not redundant enough to distort coefficient estimates.

---

## Tech Stack

- **Language:** Python
- **Data wrangling:** Pandas, NumPy
- **Modeling and inference:** OLS regression, t-tests, F-tests, confidence intervals
- **Visualization:** Matplotlib
- **Environment:** Jupyter Notebook

---

## Project Structure

> Update this to match your repository.

```
Predicting-NBA-Impact-from-College-Performance/
├── data/
│   ├── raw/              # Original NCAA, draft, and RAPTOR files
│   └── processed/        # Merged, cleaned dataset (386 players)
├── notebooks/
│   ├── 01_cleaning_and_merging.ipynb
│   ├── 02_eda.ipynb
│   └── 03_regression_model.ipynb
├── requirements.txt
└── README.md
```

---

## Getting Started

```bash
# Clone the repository
git clone https://github.com/chouiie/Predicting-NBA-Impact-from-College-Performance.git
cd Predicting-NBA-Impact-from-College-Performance

# Install dependencies
pip install -r requirements.txt

# Launch the notebooks
jupyter notebook
```

Run the notebooks in order, starting with data cleaning and merging.

---

## Limitations and Future Work

- **Sample size:** 386 players is enough for inference but limits how many predictors the model can support.
- **Survivorship:** Only drafted players with NBA ratings are included, so the model says nothing about undrafted players.
- **Single outcome metric:** NBA impact is measured with RAPTOR; results could differ with other metrics like Win Shares or VORP.
- **Possible extensions:** Add interaction terms (for example BPM × position), try regularized models (Ridge, Lasso), or test out-of-sample prediction on more recent draft classes.

