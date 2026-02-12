# Sports Analytics Portfolio
**Author:** Jacob Gigliotti
**Background:** Medical Underwriter | Former NCAA Athlete (Salisbury University)
**Tech Stack:** R (tidyverse, survival, zoo), Python, SQL

---

## Project 1: Dynamic TD Prediction (The "Hot Hand" Model)
**File:** `NFL dataset TD prediction.Rmd`

**Objective:** Predict the probability of a Wide Receiver or Tight End scoring a touchdown in their *next* game based on their recent form.

* **The Problem:** Most fantasy projections rely on season-long averages. I wanted to build a "Hot Hand" detector that weights recent performance heavier than distant history.
* **Methodology:**
    * **Data Engineering:** Built a time-series pipeline using `zoo` to calculate **4-game rolling averages** for Targets and Yards.
    * **Leakage Prevention:** Engineered "Lag" features to ensure the model only used data available *before* kickoff to predict the result (preventing data leakage).
    * **Model:** Logistic Regression (Binomial GLM).
* **Key Findings:**
    * Volume (Rolling Targets) is a significantly stronger predictor of future TDs than Efficiency (Yards per Catch).
    * Identified "Buy Low" candidates where Expected TDs (xTD) > Actual TDs using Poisson distribution.

---

##  Project 2: QB Career Survival Analysis
**File:** `QB EPA.Rmd`

**Objective:** Apply actuarial survival models to NFL Quarterbacks to predict career longevity and retirement risk.

* **The Problem:** Draft position is often used as the sole proxy for "career security." I wanted to see if College QBR predicts longevity *independent* of draft capital.
* **Methodology:**
    * **Technique:** **Cox Proportional Hazards Model** (Survival Analysis).
    * **Metric:** Modeled the "Hazard Ratio" of retirement based on College QBR tiers.
* **Key Findings:**
    * **The Mobile Revolution:** Using an interaction model (`EPA_Run * Draft_Year`), I quantified how the draft capital value of Rushing EPA has shifted significantly positive post-2012 (The RG3/Wilson/Newton era).
    * **Longevity:** High QBR (>75) quarterbacks have a statistically significant lower risk of washing out of the league, even when controlling for draft round.

---

##  Project 3: The "SEC Premium" (Conference Bias)
**File:** `Conference Regression.Rmd`

**Objective:** Quantify the "Draft Stock Boost" a player receives simply by playing in the SEC compared to other conferences.

* **Methodology:**
    * Built a Multivariate Linear Regression model to predict **Draft Pick Number**.
    * Controlled for production (Yards, TDs) and physical traits (Height, Weight) to isolate the `Conference` coefficient.
* **Key Findings:**
    * Even with identical stats and size, SEC players are drafted significantly earlier than Group of 5 players, confirming a "Conference Bias" in scouting departments.

---

##  Project 4: WR Physical Profiling & "Bust" Probability
**File:** `NFL dataset Career Stats.Rmd`

**Objective:** Identify outliers who outperformed their physical prototype and predict "Bust" probability for high draft picks.

* **Methodology:**
    * **Gamma Regression:** Used to model Career Yards per Year (right-skewed data) based on BMI, Height, and Weight.
    * **Logistic Regression:** Calculated the probability of a "Bust" (Top 100 pick with <500 career yards).
* **Visuals:** Created a "Prototype Chart" using `ggrepel` to highlight players like Steve Smith or Wes Welker who succeeded despite being "Underweight" outliers.
---

##  Project 5: Medical Insurance Cost Prediction (Risk Modeling)
**File:** `Final Project.Rmd`

**Objective:** Demonstrate the fundamental risk modeling techniques used in my professional underwriting career and how they translate to sports.

* **The Problem:** In both insurance and sports, "risk" is rarely linear. A smoker with a high BMI has a risk profile that is exponentially worse than just "Smoker" + "High BMI."
* **Methodology:**
    * **Linear Regression:** Modeled medical charges based on Age, Sex, BMI, Children, and Region.
    * **Feature Engineering:** Created a custom **Interaction Term** (`BMI * Smoker`) to capture the compounding risk of unhealthy habits combined with high body mass.
* **Key Findings:**
    * **The "Smoker Premium":** Calculated the precise dollar value impact of smoking on annual premiums, isolating the cost for actuarial pricing.
    * **Model Accuracy:** The interaction model significantly outperformed the base model, proving that identifying "compounding risks" is the key to accurate price prediction (a concept directly applicable to "injury prone" labels in sports).
* **Visuals:**
    * Generated an `Actual vs. Predicted` regression plot to validate the model's pricing accuracy.
---


