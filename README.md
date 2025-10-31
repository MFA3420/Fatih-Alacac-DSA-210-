# Fatih-Alacac-DSA-210-
This project analyzes  economics of cinema for next movie directors and investors. Analyzing ROI, Genre Trends, and Star Power in the Film Industry.



# Motivation
The movie industry is a multi-billion-dollar ecosystem where financial success is influenced by multiple factors — from actors and directors to genres and release timing.  
This project aims to explore what truly drives a movie’s financial success by analyzing:

-  The impact of **actors and directors (Star Power)** on box office performance  
-  The **evolution of film genres** over the past two decades  
-  The **return on investment (ROI)** across different types of movies  

The results of this study can guide **film studios, investors, and streaming platforms** in making more data-driven decisions.

---

# Dataset
Two main datasets are used and enriched:

/ Source / Description / Link 

/ **IMDb 5000 Movie Dataset** / Contains movie budget, gross revenue, ratings, actors, directors, and genres | [Kaggle](https://www.kaggle.com/datasets/carolzhangdc/imdb-5000-movie-dataset) 
/ **The Movies Dataset (TMDb)** / Includes extended metadata such as cast popularity, vote counts, and release dates / [Kaggle](https://www.kaggle.com/datasets/rounakbanik/the-movies-dataset) 

**Data Enrichment:**
- Merged IMDb and TMDb datasets on movie title
- Derived new variables: `ROI = (revenue - budget) / budget`, `Star Power`, `Genre Popularity Index`

---

##  Methodology

###  Data Preparation
- Loaded CSVs with `pandas`
- Handled missing values (`dropna`, `fillna`)
- Converted JSON-like columns (for cast and genres) into lists
- Normalized monetary columns (converted to USD millions)

###  Exploratory Data Analysis (EDA)
- Overview statistics (mean, median, std for `budget`, `revenue`, `rating`)
- Outlier detection for unusually high budgets or revenues
- Correlation heatmap for numeric variables (`budget`, `revenue`, `rating`, `popularity`)

###  Star Power Analysis
- Calculated **average box office revenue per actor/director**
- Created a custom **Star Power Score** based on:
  - Mean IMDb rating of actor’s films
  - Number of lead appearances
  - Average ROI of their movies
- Visualized:
  ...(to be detailed)  

###  Genre Trend Analysis
- Grouped data by `genre` and `release_year`
- Computed:
  - Average `revenue` and `rating` per year
  - Genre frequency by decade
- Visualized:
   ...(to be detailed)  

###  ROI Analysis
- Calculated ROI for each film: `(revenue - budget) / budget`
- Analyzed:
  - Distribution of ROI across genres
  - Relationship between `budget` and `ROI`
- Visualized:
  ...(to be detailed)  

---




