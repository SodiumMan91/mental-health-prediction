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

# Goals
In our project we try to answer the following two questions:
1. Identify the most significant factors contributing to poor mental health prevalence. | [Notebook](https://github.com/SodiumMan91/mental-health-prediction/blob/main/notebooks/random_forest_xg_boost.ipynb)
2. Analyze the relationship between living conditions and mental health rates. | [Notebook](https://github.com/SodiumMan91/mental-health-prediction/blob/main/notebooks/reg_SLD_data_on_mental_health.ipynb)

# Feature Importance

Feature importance analysis aims to identify the most significant predictors of mental health outcomes, specifically the crude prevalence of mental health issues (MHLTH_CrudePrev) at the census tract level. By uncovering these key features, we can guide policymakers in designing targeted interventions and allocating resources efficiently. Additionally, this analysis improves the interpretability of machine learning models, bridging the gap between complex algorithms and actionable insights.

## Methodology

To determine feature importance, we employed both tree-based machine learning models and interpretability tools. The two machine learning models we used are:

Random Forest Regressor - A robust ensemble learning method that uses decision trees to identify the contribution of each feature by its reduction in impurity.

XGBoost Regressor - A gradient-boosted tree model optimized for predictive performance and capable of handling high-dimensional data.

The interpretability tool we used is SHAP (SHapley Additive exPlanations. It is a model-agnostic interpretability framework that calculates the marginal contribution of each feature to individual predictions, providing both global and local explanations.

The dataset was preprocessed through imputation for missing values, encoding for categorical variables, and standardization of numerical features. The final dataset consisted of 69 features and 5,289 rows after cleaning, imputation, and dimensionality reduction.

## Key Findings

### Top Features Identified:

- `COGNITION_CrudePrev`: Emerged as the most influential predictor in both Random Forest and XGBoost models, with significantly higher importance scores compared to other features. This highlights the critical role of cognitive health in understanding overall mental health prevalence.
- `DEPRESSION_CrudePrev`: Ranked second, indicating its direct relevance to the target variable.
- `CASTHMA_CrudePrev` and `BINGE_CrudePrev`: Features related to comorbid conditions such as asthma and binge drinking showed moderate importance, suggesting their indirect association with mental health issues.
- `OBESITY_CrudePrev` and `DIABETES_CrudePrev`: These features were less influential but still noteworthy, underscoring the relationship between physical and mental health.

### Model-Specific Observations:

- Random Forest attributed over 87% of the importance to `COGNITION_CrudePrev`, followed by smaller contributions from other features such as depression prevalence and asthma prevalence.
- XGBoost, while agreeing on the top-ranked feature, showed a more distributed importance across the top predictors.

### SHAP Value Insights:

- SHAP summary plots provided nuanced insights into the directionality of feature contributions. For instance, high values of `COGNITION_CrudePrev` consistently corresponded to higher predicted prevalence of mental health issues.
- `DEPRESSION_CrudePrev` and `BINGE_CrudePrev` also displayed strong positive correlations with the target variable, reinforcing their importance.

### Visualizations

**Bar Plots**:

- Comparative bar plots of feature importances from Random Forest and XGBoost highlighted **`COGNITION_CrudePrev`** as the dominant predictor, followed by **`DEPRESSION_CrudePrev`** and others.
![image](https://github.com/user-attachments/assets/b7672131-bc5b-46cc-9d7e-0fea71b9a535)

**SHAP Summary Plots**:

- Visualizations of SHAP values illustrated the global and local impacts of top predictors, providing interpretable and actionable insights for decision-makers.
![image](https://github.com/user-attachments/assets/fbda5e58-8ff9-4b30-b648-6635362bb327)

### Implications

The analysis underscores the critical role of cognitive health and comorbidities in shaping mental health outcomes. Interventions aimed at improving cognitive function and addressing co-occurring conditions like depression and binge drinking could have a substantial impact on reducing the prevalence of mental health issues.

### Actionable Insights

The feature importance analysis highlights actionable areas to improve mental health outcomes at the census tract level. The following insights can guide public health interventions:

#### Focus on Cognitive and Mental Health Comorbidities:

Cognitive Health (`COGNITION_CrudePrev`): As the strongest predictor of mental health prevalence, programs targeting cognitive health improvement—such as memory training, mental agility exercises, and support for individuals with cognitive impairments—should be prioritized.

Depression Prevalence (`DEPRESSION_CrudePrev`): Depression remains a critical determinant. Expanding access to mental health services, promoting early diagnosis, and ensuring community support systems are in place are crucial steps.

#### Address Behavioral and Physical Health Factors:

Asthma and Binge Drinking (`CASTHMA_CrudePrev` and `BINGE_CrudePrev`): Behavioral health issues indirectly impact mental health. Educational campaigns and behavioral intervention programs can mitigate their influence.

Physical Health (`OBESITY_CrudePrev` and `DIABETES_CrudePrev`): The link between physical and mental health warrants integrated care models that address both simultaneously, such as programs encouraging healthy eating and physical activity.

### Regional Insights for Targeted Interventions:

Geospatial analysis suggests variation in feature influence across regions. Localized interventions, tailored to the health profiles and environmental factors of specific census tracts, can maximize impact.

## Limitations and Future Work

While the models provide robust insights, further validation using external datasets and longitudinal studies is recommended to ensure generalizability. Additionally, incorporating spatial analysis could help identify region-specific patterns and hotspots for targeted action.

# Feature Importance and Regression Analysis for Mental Health Prevalence
This analysis examines the relationship between various socio-economic, housing, and mobility features and the prevalence of mental health distress (MHLTH_CrudePrev). Using regression models, the study identifies key factors that either exacerbate or alleviate mental distress, helping policymakers target specific risk factors for intervention.

## Key Findings from Feature Importance and Regression Models
### Regression Models Employed:

1. Linear Regression: Baseline model to understand simple relationships between predictors and mental health outcomes.
2. Ridge Regression: Applies L2 regularization to prevent overfitting by addressing multicollinearity.
3. Lasso Regression: Uses L1 regularization for feature selection, focusing on significant predictors and reducing less important ones.
4. Preprocessing and Assumptions: The dataset, containing 5,289 rows and 76 features, was cleaned and standardized. Categorical variables were one-hot encoded, and multicollinearity was addressed through regularization techniques. Assumptions for linearity, homoscedasticity, and normality were verified.

### Coefficients and Variable Analysis
The regression analysis revealed several key insights:

#### Negative Coefficients (Factors that reduce mental distress):
1. `Pct_AO1`: Percent of one-car households in the census block group (CBG) in 2018.
2. `Pct_AO2p`: Percent of two-plus-car households in CBG in 2018.
3. `R_HiWageWk`: Count of workers earning $3333/month or more in 2017.
4. `D4d`: Aggregate frequency of transit service [D4c] per square mile.
5. `D4c`: Frequency of transit service within 0.25 miles of CBG boundary during evening peak periods (2020).
6. `D5ar`: Jobs within 45 minutes of auto travel time, weighted by time-decay in 2020.
These variables, which reflect household wealth and mobility, show a negative relationship with mental distress, suggesting that higher income, car ownership, and proximity to work are associated with better mental health outcomes.

#### Positive Coefficients (Factors that increase mental distress):
1. `P_WrkAge`: Percent of the working-age population (18 to 64 years).
2. `D3AMM`: Network density in terms of multi-modal facility miles per square mile.
3. `D3APO`: Network density in terms of pedestrian-oriented facility miles per square mile.
4. `D4a`: Distance from population-weighted centroid to nearest transit stop (2020).
5. `D5cr`: Proportional accessibility to regional destinations (auto).
6. `D5cri`: Regional centrality index based on accessibility to regional destinations (auto).
These variables, associated with urban density, mobility, and centrality, indicate that living in more densely populated and developed urban areas increases the risk of mental distress. The negative effects of urbanization, including long commutes, transit service density, and high pedestrian activity, seem to contribute to higher levels of mental health issues.

### Conclusion and Implications
The analysis highlights how socio-economic factors, such as income, car ownership, and proximity to work, contribute to lower mental health distress, emphasizing the importance of household wealth and mobility in promoting mental well-being. Conversely, urbanization and high-density living are linked to higher mental distress, suggesting that factors like crowded environments, limited access to open spaces, and long commutes may have adverse effects on mental health.

These insights can guide public health interventions by focusing on:

1. Improving economic conditions: Programs to increase income and promote car ownership may reduce mental distress.
2. Addressing urban density: Urban planning policies that reduce crowding, improve access to green spaces, and provide better public transport may mitigate the negative effects of living in densely populated areas.

![image](https://github.com/user-attachments/assets/a6242e1d-177b-4ff3-83de-2c4240e8c68f)
