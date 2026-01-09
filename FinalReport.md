# Final Report: Film Economics and Macroeconomic Conditions Analysis

## 1. Introduction

In this project, we explore the relationship between macroeconomic conditions and film industry financial performance. While most film industry analyses focus on movie-specific features like budget, cast, and genre, this project investigates a less-studied question: do economic conditions affect box office returns? We pay particular attention to whether escapist genres (comedy, fantasy, animation) perform better during economic hardships such as high unemployment periods.

This topic combines my interest in economics and entertainment industry analytics, using real-world data to test whether the "escapism hypothesis"—the idea that audiences turn to light entertainment during tough times—holds up statistically.

---

## 2. Research Question

**How do macroeconomic conditions influence film industry financial performance, and do escapist genres (comedy, fantasy, animation) achieve higher ROI during periods of economic hardship such as high unemployment?**

---

## 3. Data Sources

### Movie Data
- **Source:** [IMDb 5000 Movie Dataset (Kaggle)](https://www.kaggle.com/datasets/carolzhangdc/imdb-5000-movie-dataset)
- Contains: budget, gross revenue, genres, directors, actors, IMDB scores
- ~5000 movies spanning multiple decades

### Economic Data
- **Source:** [World Bank - World Development Indicators](https://databank.worldbank.org/source/world-development-indicators)
- Contains: GDP growth, unemployment rate, inflation, GDP per capita
- Annual data by country

---

## 4. Data Preprocessing & Feature Engineering

### Preprocessing
- Cleaned movie data: removed entries with missing budget/gross, filtered invalid values
- Transformed World Bank data from wide to long format
- Mapped country names between datasets (e.g., "USA" → "United States", "UK" → "United Kingdom")
- Merged datasets on country and year

### Derived Features
- **ROI:** `(gross - budget) / budget` → financial return measure
- **main_genre:** extracted first genre from genre list
- **is_escapist:** binary flag (1 if genre is Comedy, Animation, Fantasy, Family, Musical)
- **high_unemployment:** binary flag (1 if unemployment > 7%)
- **budget_category:** Low / Medium / High based on budget percentiles
- **economic_period:** categorized years (2008 Crisis, COVID, Normal)

---

## 5. Exploratory Data Analysis

### Key Observations
- ROI distribution is heavily right-skewed with many outliers
- Budget and gross revenue show strong positive correlation
- US dominates the dataset (~80% of films)
- Genre distribution varies significantly across decades

### Visualizations Created
- ROI distribution histogram
- Budget vs Gross scatter plot
- ROI by genre box plots
- Yearly trends in movie production
- Correlation heatmap between movie features and economic indicators

---

## 6. Hypothesis Testing

### H1: Escapist Genres + High Unemployment → Better Performance

**Test:** Mann-Whitney U test (non-parametric, suitable for skewed ROI distribution)

**Groups:**
- Escapist films during high unemployment periods
- Non-escapist films during high unemployment periods

**Results:**
- U-statistic: significant
- **p-value = 0.0143**
- **Conclusion: Reject H₀** — Escapist genres perform significantly better during high unemployment

This supports the "escapism hypothesis": during economic hardships, audiences prefer lighter entertainment, leading to higher returns for comedy, animation, and fantasy films.

---

### H2: 2008 Financial Crisis ROI ≠ Normal Years ROI

**Test:** Independent samples t-test

**Groups:**
- Films released during 2008-2009 (crisis years)
- Films released during normal economic periods

**Results:**
- t-statistic: 0.75
- **p-value = 0.4542**
- **Conclusion: Fail to Reject H₀** — No significant difference in overall ROI distribution

While individual genres may respond differently to crises, the aggregate film market ROI did not show a statistically significant shift during the 2008 crisis.

---

## 7. Machine Learning

We applied two models to predict ROI using movie features and economic indicators.

### Features Used
- Movie features: budget, title_year, imdb_score, genre_encoded, country_encoded
- Economic features: gdp_growth, gdp_per_capita, unemployment, inflation

### Linear Regression

**Coefficients (standardized):**
- imdb_score: +0.3202 (strongest positive)
- genre_encoded: +0.2504
- country_encoded: +0.2314
- gdp_per_capita: +0.1669
- title_year: -0.1648
- inflation: +0.1008
- budget: -0.0874
- unemployment: +0.0843
- gdp_growth: +0.0404

**Performance:**
- Test RMSE: 2.3662
- Test R^2: 0.0423

**Interpretation:** IMDB score has the strongest positive effect on ROI. Higher budgets slightly decrease ROI (blockbusters are riskier). Economic variables show modest but present influence.

---

### Random Forest Regressor

**Feature Importances:**
- budget: 0.2577 (most important)
- imdb_score: 0.1976
- genre_encoded: 0.1035
- gdp_per_capita: 0.0980
- inflation: 0.0854
- title_year: 0.0776
- unemployment: 0.0708
- gdp_growth: 0.0660
- country_encoded: 0.0433

**Performance:**
- Test RMSE: 2.1134
- Test R^2: 0.2360

**Interpretation:** Random Forest captures non-linear relationships better than Linear Regression. Budget emerges as the most important predictor, followed by IMDB score. Economic variables collectively account for ~28% of feature importance.

---

### ML Conclusions

The methodology was sound: we used interpretable features, applied two different models, and evaluated with proper metrics (RMSE, R²). However:
- Low R^2 values indicate ROI is inherently difficult to predict
- Movie success depends on many unmeasured factors (marketing, release timing, competition, star power)
- Economic variables contribute but are not dominant predictors

This demonstrates an important lesson: **statistical significance (from hypothesis tests) does not guarantee predictive accuracy (from ML models)**. The t-test showed a clear relationship between economic conditions and escapist genre performance, but predicting individual film ROI remains challenging.

---

## 8. Research Question Answers

**Q: How do macroeconomic conditions influence film industry financial performance?**

Economic conditions have a measurable but modest influence on film ROI. In our ML models, economic variables (GDP growth, unemployment, inflation, GDP per capita) collectively account for ~28% of Random Forest feature importance. Linear regression coefficients show gdp_per_capita (+0.17) and unemployment (+0.08) have positive associations with ROI.

**Q: Do escapist genres achieve higher ROI during periods of economic hardship?**

Yes. Mann-Whitney U test (p = 0.0143) confirms that escapist genres (comedy, fantasy, animation) significantly outperform non-escapist genres during high unemployment periods. This supports the "escapism hypothesis" in entertainment economics.

---


## 10. Future Work

- Include streaming revenue data for more accurate ROI calculation
- Add marketing budget as a feature
- Apply time series analysis to predict industry trends
- Analyze regional differences in economic sensitivity
- Test the escapism hypothesis across different countries/cultures

---

## 11. Conclusion

This project demonstrated that macroeconomic conditions do influence film industry performance, though the effect is modest compared to movie-specific features like budget and ratings. Most notably, we found statistical support for the "escapism hypothesis": escapist genres achieve significantly higher ROI during high unemployment periods (p = 0.0143).

Machine learning models showed that while economic variables contribute to ROI prediction (~28% of feature importance), accurately forecasting individual film success remains challenging due to the many unmeasured factors involved in movie performance.

The analysis pipeline—from data collection and EDA to hypothesis testing and machine learning—demonstrates practical data science skills applied to a real-world question in entertainment economics.
