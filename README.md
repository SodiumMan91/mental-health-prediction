# Mental Health Prediction Project

This project aims to predict the prevalence of poor mental health in neighborhoods using demographic, socioeconomic, and environmental factors. By analyzing community-level data, the model identifies key predictors of mental health outcomes and highlights high-risk areas. The project utilizes data processing, exploratory data analysis (EDA), machine learning modeling, and visualization techniques to provide insights into public health challenges and inform targeted interventions.

## Datasets used, preprocessing and joining the datasets.
We briefly explain the datasets we used and the feature engineering in [this document](Datasets_Feature_Engineering.md)

## Tasks performed
1. Identify the most significant factors contributing to poor mental health prevalence. [Report](Feature_Importance.md) [Notebook](notebooks/random_forest_xg_boost.ipynb)
2. Analyze the relationship between proximity to healthcare facilities and mental health rates. [Report](Regression_Analysis.md) [Notebook 1](notebooks/reg_SLD_data_on_mental_health.ipynb) [Notebook 2](notebooks/reg.ipynb)
3. Predict high-risk neighborhoods and recommend facility placement. [Notebook](notebooks/k-means.ipynb)
