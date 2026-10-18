# Yulu_Buisness_case
Data analysis and business case study exploring user demand, rental trends, and operational factors for Yulu micro-mobility services

# Yulu: What Drives Demand for Shared Electric Cycles?
*An Exploratory Data Analysis (EDA) of hourly rental demand to help Yulu understand revenue drivers.*

---

## 🛠️ Badges
![Python](https://img.shields.io/badge/Python-3.x-blue.svg)
![Jupyter/Colab](https://img.shields.io/badge/Jupyter-Colab-orange.svg)
![Pandas](https://img.shields.io/badge/pandas-data_analysis-150458.svg)
![Seaborn](https://img.shields.io/badge/seaborn-visualization-3776AB.svg)
![Statsmodels](https://img.shields.io/badge/statsmodels-statistics-green.svg)
![NumPy](https://img.shields.io/badge/NumPy-013243?style=flat&logo=numpy&logoColor=white)
![Matplotlib](https://img.shields.io/badge/Matplotlib-%23ffffff.svg?style=flat&logo=Matplotlib&logoColor=black)
![ANOVA](https://img.shields.io/badge/ANOVA-Statistical_Test-blue.svg)
![Chi-Square](https://img.shields.io/badge/Chi--Square-Hypothesis_Test-green.svg)
---

## 📌 Project Overview
Yulu has experienced a dip in revenue, motivating a data-driven investigation into what governs shared electric cycle usage. Using hourly rental records spanning from January 2011 to December 2012, this case study identifies the key variables affecting user demand. Through statistical hypothesis testing and data exploration, the analysis uncovers behavioral splits between user types and environmental sensitivities, providing an empirical baseline to optimize fleet operations.

---

## 🎯 Business Problem / Objectives
* Determine if hourly rental demand significantly differs between working and non-working days.
* Quantify the impact of different weather conditions on user demand.
* Assess seasonal variations in rentals across the year.
* Test whether weather conditions and seasons are statistically independent.

---

## 📊 Dataset
* **Source:** [Yulu.csv] 
* **Dimensions:** 10,886 rows and 12 columns.

| Column Name | Data Type | Description |
| :--- | :--- | :--- |
| `datetime` | Datetime | Timestamp for the hourly rental record |
| `season` | String / Integer | Season of the year (spring, summer, fall, winter) |
| `holiday` | Integer | Indicator for whether the day is a holiday (0 or 1) |
| `workingday` | Integer | Indicator for working day vs. weekend/holiday (0 or 1) |
| `weather` | Integer | Weather category rating (1 to 4) |
| `temp` | Float | Actual temperature in Celsius |
| `atemp` | Float | "Feels-like" temperature in Celsius |
| `humidity` | Integer | Relative humidity percentage |
| `windspeed` | Float | Recorded wind speed |
| `casual` | Integer | Count of casual/non-registered users |
| `registered` | Integer | Count of registered/member users |
| `count` | Integer | Total hourly rental demand (casual + registered) |

---

## 🧰 Tools & Libraries
* **Python:** Core programming language.
* **Pandas & NumPy:** Data loading, manipulation, and numerical computations.
* **Matplotlib & Seaborn:** Data visualization, histograms, boxplots, countplots, and correlation heatmaps.
* **SciPy (`stats`):** Statistical testing (Levene's test, independent t-tests, Mann-Whitney U, ANOVA, Kruskal-Wallis, Chi-square).
* **Statsmodels:** Regression modeling and Tukey's HSD post-hoc tests.

---

## ⚙️ Methodology
1. **Data Loading:** Imported hourly logs and parsed datetime features.
2. **Data Cleaning & Integrity Checks:** Verified total row and column dimensions, checking for missing values and duplicate entries.
3. **Handling Outliers & Anomalies:** Inspected distributions via descriptive statistics and boxplots; retained genuine high-demand peaks (rush-hour traffic up to 977) to prevent distorting demand patterns.
4. **Feature Engineering:** Mapped numerical season codes to descriptive labels (`spring`, `summer`, `fall`, `winter`) and created auxiliary tracking variables.
5. **Univariate, Bivariate & Multivariate Analysis:** Evaluated individual feature distributions (noting right-skew in counts, casual, and registered users), correlation matrices (identifying multicollinearity between `temp` and `atemp`), and group segmentations.
6. **Hypothesis Testing & Visualization:** Executed two-sample t-tests, one-way ANOVAs, Kruskal-Wallis tests, Chi-square tests of independence, and visualized distributions with histograms, boxplots, KDE plots, and Q-Q plots.

---

## 💡 Key Insights & Findings
* **Total Demand Across Workdays:** Mean hourly rentals are 193.0 on working days versus 188.5 on non-working days, yielding no statistically significant difference ($t = 1.21, p = 0.23$).
* **User Mix Shift:** Although total demand is similar, customer composition flips; registered users average 167.9 on workdays vs. 129.2 on non-working days, whereas casual users average 25.1 on workdays vs. 59.3 on non-workdays.
* **Weather Impact:** Demand drops significantly as weather worsens; mean hourly rentals are 205.2 for clear skies, 179.0 for mist/cloudy conditions, and 118.8 for light rain/snow ($F = 98.28, p = 5.0 \times 10^{-43}$), representing an approximate 42% reduction during rain.
* **Seasonal Differences:** Rentals vary heavily by season ($F = 236.95, p = 6.2 \times 10^{-149}$), peaking in fall (mean 234.4) and summer (mean 215.3), while registering lowest in spring (mean 116.3).
* **Weather-Season Association:** Weather conditions and seasons are significantly associated ($\chi^2 = 46.10, p = 2.8 \times 10^{-8}$ excluding weather level 4), indicating specific weather distributions per season.
* **Collinearity:** Actual temperature (`temp`) and "feels-like" temperature (`atemp`) exhibit a near-perfect correlation of $0.98$.

---

## 🚀 Recommendations
* **Implement Weather-Based Dynamic Pricing:** Introduce promotions or rain-day discounts to recover demand during adverse weather conditions (light rain/snow).
* **Targeted Marketing by Day Type:** Allocate weekday communications toward commuter/registered user plans, while shifting to leisure-focused weekend offers for casual riders.
* **Optimize Fleet Rebalancing:** Position vehicles near transit hubs and office districts ahead of peak commuting windows (around 8 AM and 5 PM).
* **Align Maintenance Schedules:** Schedule fleet maintenance and repairs during historically low-demand seasons (such as spring).

---

## ⚠️ Limitations & Future Work
* **Dataset Context:** The analysis utilizes a US-style bike-sharing proxy dataset; findings should be cross-validated against real Indian Yulu operational data.
* **Temperature Thresholds:** The dataset caps out at 41°C, failing to capture extreme tropical heat effects relevant to Indian markets.
* **Next Steps:** Incorporate localized real-time traffic, station-level geospatial distribution, and extreme heat data to refine predictive modeling.

---

## 💻 How to Run
To explore the analysis interactively:
1. Open the notebook directly in Google Colab via the repository link: [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/parvezsardar13/Yulu_Buisness_case/blob/main/Yulu_Buisness_case.ipynb)
2. Alternatively, clone the repository locally and ensure the dependencies are installed:
   ```bash
   pip install pandas numpy matplotlib seaborn scipy statsmodels
