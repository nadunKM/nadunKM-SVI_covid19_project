# Predicting COVID-19 Deaths in the USA Based on Socioeconomic and Health Risk Factors

![](https://github.com/nadunKM/nadunKM-SVI_covid19_project/blob/main/Images/Covid_deaths.png)

## Introduction 
This project aims to develop a model to predict COVID-19 deaths in the USA based on socioeconomic and health-related factors. For example, this model uses socioeconomic factors such as unemployment, poverty levels, household burden, and demographic data. 
Furthermore, we use health-related factors, such as chronic disease status. These data are available for almost every county in the USA. 

![](https://github.com/nadunKM/nadunKM-SVI_covid19_project/blob/main/Images/unemp.png)

### Dataset
The data for this study was sourced from a reliable and widely used database (CDC): [Census Tract Data (GIS Friendly Format), 2022](https://data.cdc.gov/500-Cities-Places/PLACES-Census-Tract-Data-GIS-Friendly-Format-2022-/shc3-fzig/about_data), [Social Vulnerability Data](https://www.atsdr.cdc.gov/placeandhealth/svi/documentation/SVI_documentation_2022.html). This is a reliable, widely used database for getting the above data. The data are from the Centers for Disease Control and Prevention (CDC), which is a government data source in the USA. I have already checked if the data is available for the features mentioned above, and they do exist. 

## Data Cleaning

[Data Cleaning Report](https://github.com/nadunKM/nadunKM-SVI_covid19_project/blob/main/Data%20Wrangling.ipynb)

First, data was checked for missing, duplicated, and data types. Data was missing for some counties, which were excluded from the model. Also, some numeric data was recorded with string characters and converted to numeric data. Furthermore, the way county FIPS were recorded was inconsistent. Therefore, they were all changed to one format. Finally, groupby was used to aggregate data into specific categories.

## EDA

[EDA Report](https://github.com/nadunKM/nadunKM-SVI_covid19_project/blob/main/EDA.ipynb)

From EDA, we can notice that the higher the poverty, unemployment, and minority percentages, the higher the COVID deaths. Also, it was observed that the areas with high African American and Hispanic populations have high unemployment and poverty.
We can clearly see that the higher the socioeconomic burdens, the higher the health risks as well. Furthermore, when both of the above are higher, the COVID deaths are also high.

![](https://github.com/nadunKM/nadunKM-SVI_covid19_project/blob/main/Images/pow.png)

Another key observation is that health risk factors are linearly related to the number of COVID-19 deaths. The higher the health risk factors, the higher the COVID-19 deaths. 

![](https://github.com/nadunKM/nadunKM-SVI_covid19_project/blob/main/Images/health_iss.png)

#### Principal Component Analysis

![](https://github.com/nadunKM/nadunKM-SVI_covid19_project/blob/main/Images/expl.png)        ![](https://github.com/nadunKM/nadunKM-SVI_covid19_project/blob/main/Images/pca.png)   


The above figures show that two principal components account for 75% of the variance. There is somewhat non-linear separability between the two categories based on the plot of the PCA.

## Modeling

[Modeling Report](https://github.com/nadunKM/nadunKM-SVI_covid19_project/blob/main/Modeling.ipynb)

### Linear Regression

For modeling, I used linear regression, XGBoost, and Random Forest Regressor. For the metrics of success, I used mean squared error and R-squared. The dataset was split into train and test sets (80-20 split). Standard scaling was then used on the train-test split. The train test was used with both models via cross-validation, and the test set was held until the better model was picked. Five-fold cross-validation was used with both models. Overall, the Random Forest Regressor was the best model. The first model used in the analysis is multiple linear regression. The mean squared error (MSE) and R-squared during the five-fold cross-validation steps were calculated. The mean MSE is around 130 and the mean R-squared is around 0.61.


### Random Forest Regressor

The first step with Random Forest Regressor was hyperparameter tuning, Which was done using GridSearchCV. The best parameters for max_depth, max_features, and n_estimators were 13,log2 and 300, respectively. The best MSE during hyperparameter tuning was roughly 134, which is better than linear regression. Therefore, Random Forest Regressor was chosen as the preferred model. 


### Metric Table

| Method            | Mean Squared Error | R-Squared  |
| -------------     |:-------------:| -----:|
| Linear Regression | 17534 | -0.23 |
| XGBoost     | 133     |   0.58 |
| Random Forest Regressor    | 134     |   0.61 |







