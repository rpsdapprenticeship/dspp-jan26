---
layout: default
title: Ryan Dempsey Portfolio
---

# Portfolio

## Project: Predicting Depression in Teenagers Using Social Media and Lifestyle Factors

### Executive Summary
The UK Government recently announced a ban on social media for under-16s in an attempt to improve children’s online safety (Department for Science, Innovation and Technology, 2026). This project aims to investigate the relationships between social media and teen mental health by exploring two questions: firstly, can depression in teenagers be predicted through their social media usage; and secondly, does the relationship between social media and depression differ for those aged under-16 and those aged 16-19?
Using a public dataset containing information on the lifestyle and mental health of 1200 people aged 13-19, a Logistic Regression model was built to predict depression based on social media, demographic and lifestyle variables. An interaction feature was also included to explore whether the effect of social media varies across age groups. The model demonstrated strong predictive performance despite a significant class imbalance. Results indicated a statistically significant relationship between social media usage and depression, however found insufficient evidence that this relationship differs for under-16s compared to those aged 16+. This would suggest that social media is associated with depression risk, and this risk appears to extend across all adolescents, not just those under 16.


### Data Infrastructure & Tools
This project was completed using Python. While the dataset was small enough to be handled in other tools such as Excel, Python and its packages provide an end-to-end workflow from data ingestion, cleaning and exploratory analysis, through to preprocessing, modelling, evaluation and statistical testing. VS Code and Jupyter Notebooks were used to enable iterative development, and the project took place within a project-specific virtual environment to support reproducibility and package compatibility. Pandas was used to organise the data because of its compatibility with downstream modelling packages. Sklearn and Statsmodels were used for modelling – Sklearn handled the preprocessing, modelling, tuning and evaluation of predictive performance, and Statsmodels was then used for significance testing of the relationships. This split was chosen because sklearn is optimised for prediction whereas Statsmodels is optimised for statistical testing. Matplotlib and Seaborn were used for visualisations as these are standard Python packages for data visualisation.

### Data Engineering
The data was obtained as a static dataset, therefore the ingestion was treated as a singular import with no ongoing extraction process required. A data quality audit was conducted and found no missing values, no duplicate records, all values were within expected domain ranges and categories, and all data types were correct and consistent within columns. This meant that no data cleaning was required for ensuring data quality. If this data were collected continuously, or if future inferencing was expected, then an ETL pipeline containing data cleaning steps would be appropriate regardless to ensure data quality is maintained even for future unknown data – however that is not the case for this project.
Preprocessing was required for the purposes of modelling, however. The data was first split into training and test sets to reduce leakage and enable evaluation of the model using unseen data to determine whether the model generalises well (James et al., 2023). The numeric features were of differing scales so these were normalised using a StandardScaler to improve model training (James et al., 2023). StandardScaler was chosen because the distributions of the numeric features showed no significant skew or outliers. RobustScaler could be considered as an alternative but was not required given the lack of outliers.
The categorical variables were encoded with OneHotEncoder. This is required to enable them to be readable by the model during fitting and inferencing. The interaction feature was added manually after the preprocessing pipeline – this is inefficient for prediction workflows as including it in the pipeline ensures consistency and reproducibility, however creating it after the pipeline ensures the feature remains intuitively interpretable which supports the objective of evaluating the interaction.
After initial model fitting and evaluation, cross-validation was performed to tune the model. In hindsight, cross-validation should have included preprocessing within the pipeline. This is because preprocessing on the full training dataset before cross-validation can introduce data leakage across the folds (Moscovich and Rosset, 2019). However, the preprocessing is fit using unsupervised training data and the model is evaluated using holdout test data. This helps reduce the impact of the leakage on model performance.

### Data Visualisation
Visualisations were used alongside aggregations during the exploratory analysis to help understand data characteristics and identify relationships between candidate features and the target variable.
A heatmap was used to visualise the correlation matrix between numeric fields. This helped identify which features correlate with the target and if there was potential multicollinearity.
![Correlation_Heatmap](images/Correlation_heatmap.png)

Histograms and boxplots were used to visualise the distributions of numeric columns, which later informed decisions such as scaling strategy. 
 

To explore relationships between candidate features and the target variable, bar charts with overlaid confidence intervals were used for categorical variables and kernel density estimate plots were used for numeric variables.
 
 

A linear model plot was also used to assess whether the relationship between social media and depression varies across age groups and informed the decision to include an interaction feature to test this relationship formally.
  

For the purposes of model evaluation, confusion matrices and ROC curves were visualised.
