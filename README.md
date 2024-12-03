# Mental Health Prediction Project

This project aims to predict the prevalence of poor mental health in neighborhoods using demographic, socioeconomic, and environmental factors. By analyzing community-level data, the model identifies key predictors of mental health outcomes and highlights high-risk areas. The project utilizes data processing, exploratory data analysis (EDA), machine learning modeling, and visualization techniques to provide insights into public health challenges and inform targeted interventions.

## Datasets used, preprocessing and joining the datasets.
**Datasets and Feature Engineering**

This project used 3 datasets:

1. [CDC Places](https://www.cdc.gov/places/about/index.html) : Contains census tract-level data regarding diseases and demographic 
2. [Smart Location](https://www.epa.gov/smartgrowth/smart-location-mapping#SLD) : Contains census tract-level data regarding land use, transportation, and more
3. [New York Government Hospital Data](https://www.epa.gov/smartgrowth/smart-location-mapping#SLD) : Contains information about each hospital in New York

The CDC Places dataset and the SLD dataset were joined using GeoPandas. This was done by combining the region boundary column of the SLD dataset (a list of points making up the region boundary) and the lat/long points in the CDC dataset. This information suffices for GeoPandas to identify which CDC points fit within which SLD regions. The NY Hospital dataset was not explicitly joined to the remaining data but was instead used to create a new feature, "Distance to Nearest Hospital". Using the latitude and longitude for each hospital as well as the lat/long for each county, the Haversine formula was used to exhaustively find the nearest hospital to each county to populat the Distance to Nearest Hospital feature. 

In addition to combining the three datasets, our pre-processing work included:

1. Filtering SLD and CDC datasets down to the state of New York, our desired scope
2. Dropped highly correlated features using correlation plots for SLD and CDC datasets
3. Dropped features populated primarily with meaningless NA values (insufficient sample)
4. Performed one hot encoding and min-max scaling as appropriate for categorical and numeric features respectively
5. Log-transformed our target variable to have a more normal shaped target

These details about preprocessing can be found [here](https://github.com/SodiumMan91/mental-health-prediction/blob/main/Preprocessing_Details.pdf)

# Goals | [Detailed Report](https://github.com/SodiumMan91/mental-health-prediction/blob/main/Report.md)
In our project we try to answer the following two questions:

1. Identify the most significant factors contributing to poor mental health prevalence.  [Notebook](https://github.com/SodiumMan91/mental-health-prediction/blob/main/notebooks/random_forest_xg_boost.ipynb)
2. Analyze the relationship between living conditions and mental health rates. | [Notebook](https://github.com/SodiumMan91/mental-health-prediction/blob/main/notebooks/reg_SLD_data_on_mental_health.ipynb)

## Feature Importance Analysis | [Notebook](https://github.com/SodiumMan91/mental-health-prediction/blob/main/notebooks/random_forest_xg_boost.ipynb)
The analysis aimed to identify key predictors of mental health issues, specifically crude prevalence (MHLTH_CrudePrev) at the census tract level, using tree-based machine learning models and interpretability tools. Random Forest Regressor and XGBoost Regressor were employed to determine feature importance, while SHAP (SHapley Additive exPlanations) provided model-agnostic insights into the contributions of each feature.

The dataset, after preprocessing and dimensionality reduction, included 69 features and 5,289 rows. Key findings revealed that Cognition Crude Prevalence (COGNITION_CrudePrev) was the most significant predictor, followed by Depression Crude Prevalence (DEPRESSION_CrudePrev). Other notable predictors included comorbid conditions like Asthma (CASTHMA_CrudePrev) and Binge Drinking (BINGE_CrudePrev), as well as physical health factors like Obesity (OBESITY_CrudePrev) and Diabetes (DIABETES_CrudePrev).

Random Forest highlighted COGNITION_CrudePrev as the dominant predictor, while XGBoost provided a more distributed importance across multiple features. SHAP summary plots revealed strong positive correlations between the top features and mental health outcomes.

![image](https://github.com/user-attachments/assets/8b8502d3-8816-417b-9cc1-35dcdac130b5)


## Regression Analysis for Mental Health Prevalence | [Notebook](https://github.com/SodiumMan91/mental-health-prediction/blob/main/notebooks/reg_SLD_data_on_mental_health.ipynb)
This analysis explores the relationship between socio-economic, housing, and mobility features and the prevalence of mental health distress (MHLTH_CrudePrev). Using linear, ridge, and lasso regression models, the study identifies key factors that influence mental distress, with the goal of informing public health interventions.

#### Key Findings:
##### Negative Coefficients (Factors reducing mental distress):

1. Higher income, car ownership, and proximity to work (e.g., Pct_AO1, Pct_AO2p, R_HiWageWk).
2. Better access to transit services (D4d, D4c) and more jobs within travel time (D5ar).

These factors indicate that wealth and mobility are associated with improved mental health outcomes.

##### Positive Coefficients (Factors increasing mental distress):

1. Urban density and infrastructure, including factors like population age (P_WrkAge), network density (D3AMM, D3APO), and proximity to transit (D4a, D5cr).

These factors suggest that living in more developed and densely populated areas increases the risk of mental distress, likely due to crowded environments and long commutes.

![image](https://github.com/user-attachments/assets/a6242e1d-177b-4ff3-83de-2c4240e8c68f)

#### Conclusion:
Socio-economic factors like income and car ownership are linked to better mental health, while urban density and long commutes are associated with increased mental distress. Public health interventions could focus on improving economic conditions and addressing urban density to reduce mental health issues.

Key actionable insights include focusing on cognitive health, expanding access to depression treatment, and addressing comorbid behaviors like asthma and binge drinking. Regional interventions tailored to specific census tract health profiles are recommended for maximum impact. Further validation and spatial analysis are needed to enhance the generalizability of the findings.

