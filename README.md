# Mental Health Prediction Project

This project aims to predict the prevalence of poor mental health in neighborhoods using demographic, socioeconomic, and environmental factors. By analyzing community-level data, the model identifies key predictors of mental health outcomes and highlights high-risk areas. The project utilizes data processing, exploratory data analysis (EDA), machine learning modeling, and visualization techniques to provide insights into public health challenges and inform targeted interventions.

## Datasets used, preprocessing and joining the datasets.
**Datasets and Feature Engineering**

This project used 3 datasets:

1. CDC Places: Contains census tract-level data regarding diseases and demographic 
2. Smart Location: Contains census tract-level data regarding land use, transportation, and more
3. New York Government Hospital Data: Contains information about each hospital in New York

The CDC Places dataset and the SLD dataset were joined using GeoPandas. This was done by combining the region boundary column of the SLD dataset (a list of points making up the region boundary) and the lat/long points in the CDC dataset. This information suffices for GeoPandas to identify which CDC points fit within which SLD regions. The NY Hospital dataset was not explicitly joined to the remaining data but was instead used to create a new feature, "Distance to Nearest Hospital". Using the latitude and longitude for each hospital as well as the lat/long for each county, the Haversine formula was used to exhaustively find the nearest hospital to each county to populat the Distance to Nearest Hospital feature. 


## Goals
In our project we try to answer the following two questions:
1. Identify the most significant factors contributing to poor mental health prevalence. [Report](Feature_Importance.md) [Notebook](notebooks/random_forest_xg_boost.ipynb)
2. Analyze the relationship between proximity to healthcare facilities and mental health rates. [Report](Regression_Analysis.md) [Notebook 1](notebooks/reg_SLD_data_on_mental_health.ipynb) [Notebook 2](notebooks/reg.ipynb)
