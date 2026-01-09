# Film Economics and Macroeconomic Conditions Analysis

*DSA 210 - Introduction to Data Science*
*2025-2026 Fall Term Project*


This project analyzes the relationship between movie industry financial performance (ROI, box office revenue) and macroeconomic conditions (GDP growth, unemployment, inflation).

## Motivation

The movie industry is a multi-billion-dollar ecosystem where financial success is influenced by multiple factors. While most analyses focus on movie-specific features (budget, genre, cast), this project explores a less-studied question: How do macroeconomic conditions affect film industry performance?

Understanding this relationship can help:

- Film studios optimize release timing based on economic cycles
- Investors make data-driven decisions about film financing
- Researchers understand the interplay between entertainment and economics

## Data Sources

This project uses two different types of data, combining movie industry data with economic indicators:

| Source | Description | Link |
| --- | --- | --- |
| IMDb 5000 Movie Dataset | Movie budget, gross revenue, ratings, genres, directors, actors | Kaggle |
| World Bank - World Development Indicators | GDP growth, unemployment rate, inflation, GDP per capita | World Bank |

Data Enrichment:

- Merged movie data with economic indicators by country and year
- Derived new variables: ROI = (gross - budget) / budget
- Created budget categories (Low/Medium/High) and genre classifications (Escapist/Non-Escapist)
- Defined economic periods (2008 Crisis, COVID, Normal)

## Research Questions & Hypotheses

| Hypothesis | Description |
| --- | --- |
| H1 | During high unemployment periods, escapist genres (comedy, fantasy, animation) perform better |
| H2 | The 2008 financial crisis period shows significantly different ROI distribution compared to normal years |


## Methodology

### 1. Data Preparation

- Loaded and cleaned movie metadata (handled missing values, removed invalid entries)
- Transformed World Bank data from wide to long format
- Mapped country names between datasets for merging
- Calculated ROI and created categorical variables

### 2. Exploratory Data Analysis (EDA)

- Distribution analysis of ROI, budget, and gross revenue
- Yearly trends in movie production and profitability
- Genre-wise ROI comparison
- Correlation analysis between movie features and economic indicators
- Visualizations: histograms, scatter plots, heatmaps, bar charts

### 3. Hypothesis Testing

- Mann-Whitney U Test: Non-parametric test for comparing ROI distributions
- Independent t-test: Comparing means between groups
- Pearson & Spearman Correlation: Testing relationships between continuous variables
- Significance level: α = 0.05

### 4. Machine Learning

- Feature Engineering: Label encoding for categorical variables, feature selection
- Linear Regression: Interpretable model for ROI prediction, coefficient analysis
- Random Forest: Feature importance analysis to identify key drivers of ROI
- Model Evaluation: Train-test split, cross-validation, RMSE, R² metrics

## Key Findings

### Hypothesis Test Results

-H1: Escapist genres + High unemployment → Better performance
-Mann-Whitney U test → P_value=0.0143,  We Reject

-H2: 2008 crisis ROI ≠ Normal years ROI
-t-test → P_value=0.4542, We reject


### Machine Learning Results

```text
Linear Regression Coefficients:

Intercept: 0.5806

imdb_score               0.3202
genre_encoded            0.2504
country_encoded          0.2314
gdp_per_capita           0.1669
title_year              -0.1648
inflation                0.1008
budget                  -0.0874
unemployment             0.0843
gdp_growth               0.0404

Feature Importance (Random Forest):

budget               0.2577
imdb_score           0.1976
genre_encoded        0.1035
gdp_per_capita       0.0980
inflation            0.0854
title_year           0.0776
unemployment         0.0708
gdp_growth           0.0660
country_encoded      0.0433

Model Performance:
Linear Regression Performance:
Test RMSE: 2.3662
Test R^2: 0.0423

Random Forest Performance:
Test RMSE: 2.1134
Test R^2: 0.2360
```



##Limitations

- Movie dataset is heavily weighted toward US films
- ROI calculation only includes box office revenue (excludes streaming, DVD, merchandise)
- Economic data may be incomplete for some countries/years


##Future Work
- Include streaming revenue data for more accurate ROI
- Apply time series analysis to predict future trends
```text


```
