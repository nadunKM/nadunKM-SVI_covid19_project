# Predicting COVID-19 Deaths in the USA Based on Socioeconomic and Health Risk Factors

![](https://github.com/nadunKM/nadunKM-SVI_covid19_project/blob/main/Images/Covid_deaths.png)

## Introduction 
This project aims to develop a model to predict COVID-19 deaths in the USA based on socioeconomic and health-related factors. For example, this model uses socioeconomic factors such as unemployment, poverty levels, household burden, and demographic data. 
Furthermore, we use health-related factors, such as chronic disease status. These data are available for almost every county in the USA. 

![](https://github.com/nadunKM/nadunKM-SVI_covid19_project/blob/main/Images/unemp.png)

### Dataset
The data for this study was sourced from a reliable and widely used database (CDC): [Census Tract Data (GIS Friendly Format), 2022](https://data.cdc.gov/500-Cities-Places/PLACES-Census-Tract-Data-GIS-Friendly-Format-2022-/shc3-fzig/about_data), [Social Vulnerability Data](https://www.atsdr.cdc.gov/placeandhealth/svi/documentation/SVI_documentation_2022.html). This is a reliable, widely used database for getting the above data. The data are from the Centers for Disease Control and Prevention (CDC), which is a government data source in the USA. I have already checked if the data is available for the features mentioned above, and they do exist. 

## Data Cleaning

[Data Cleaning Report](https://github.com/nadunKM/Fed_interest_analysis/blob/main/Data%20Wrangling.ipynb)

First, data was checked for missing, duplicated, and data types. There were no missing data, but some numeric data was recorded with string characters and converted to numeric data. Furthermore, the frequency of data was different, as data was recorded weekly, monthly, or quarterly. To be consistent, all data was converted to monthly data (the first day of each month). If the first day of the month is a holiday, the nearest data value was taken. The value of the nearest month was used for missing months in quarterly data.  The data starts on 01 - 01 - 1990 and ends on 03 - 01 - 2024.

## EDA

[EDA Report](https://github.com/nadunKM/Fed_interest_analysis/blob/main/EDA.ipynb)

There are a few notable correlations. GDP, personal consumption expenditure, and S&P500 are highly correlated with each other and also with other variables such as bond yield, m2 money supply, our debt-to-GDP ratio, and CPI. Since GDP is already considered with the debt-to-GDP ratio, we can drop it. Personal consumption expenditure is also highly correlated with CPI and some other features. Therefore, considering all these factors, I decided to drop GDP and personal consumption expenditure and adjusted S&P500.

![](https://github.com/nadunKM/Fed_interest_analysis/blob/main/Images/heatmap.png)

#### Principal Component Analysis

![](https://github.com/nadunKM/Fed_interest_analysis/blob/main/Images/pca_explcum.png)                ![](https://github.com/nadunKM/Fed_interest_analysis/blob/main/Images/pca_comp.png)


The above figures show that three principal components account for 78% of the variance. The first two principal components and the colormap depict federal interest rates. It is clear that about four clusters of interest rates are somewhat separable from each other. Finally, the figures show that bond yield, m2 money supply, CPI, and the debt to GDP ratio are significant features related to the first principal component. Unemployment, the US dollar index, and adjusted CPI are the most represented in the second principal component. The volatility index and the budget surplus/deficit are the highlights of the third principal component.

## Modeling

[Modeling Report](https://github.com/nadunKM/Fed_interest_analysis/blob/main/EDA.ipynb)

### Linear Regression

For modeling, I used linear regression and XGBoost. For the metrics of success, I used mean squared error and R-squared. The dataset was split into train and test sets (80-20 split). Standard scaling was then used on the train-test split. The train test was used with both models via cross-validation, and the test set was held until the better model was picked. Five-fold cross-validation was used with both models. Overall, XGBboost was the best model. The first model used in the analysis is multiple linear regression. The mean squared error (MSE) and R-squared during the five-fold cross-validation steps were calculated, as shown in the following figures. The mean MSE is around 1.2, and the smallest MSE during cross-validation is 0.92. The mean R-squared is around 0.745, and the smallest R-squared during cross-validation is 0.735.

![](https://github.com/nadunKM/Fed_interest_analysis/blob/main/Images/linear_mse.png)

### XGBoost

The first step with XGBoost was hyperparameter tuning, Which was done using GridSearchCV. The best parameters for max_depth, colsample_bytree, and eta were 5,0.45 and 0.1, respectively. The best MSE during hyperparameter tuning was roughly 0.40, which is better than linear regression. Therefore, XGBoost was chosen as the preferred model. Finally, the model was used on the test set for the first time; the MSE was 0.08, and the R-squared was 0.98.

![](https://github.com/nadunKM/Fed_interest_analysis/blob/main/Images/test_solutions.png)

### Metric Table

| Method            | Mean Squared Error | R-Squared  |
| -------------     |:-------------:| -----:|
| Linear Regression | 0.40 | 0.735 |
| XGBoost     | 0.08     |   0.98 |







