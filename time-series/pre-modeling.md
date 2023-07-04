# Pre-modeling requirements

## Explanatory variables 

Explanatory variables (or, also called predictor variables, regressors or x) are used to predict or explain variations that occur in dependent variable (or target variable). Based on the estimated relationship between those variables, the analyst can understand correlations and perform forecasts.  

 As an example, suppose we are interested in predicting energy consumption (dependent variable) in a certain city. The possible explanatory variables could be: number of people residing in this city, maximum and minimum temperature. 

## Dependent variable 

Dependent variable (also called target variable, outcome or y) is the output variable in an experiment, or simply the variable of interest in the model. 

Data frequency - concept + no more than 1 observation per frequency period 

The algorithm automatically identifies the data frequency of the dataset. The data frequency is defined according to the difference (measured in days) within values of date column. For a given date sequence, the algorithm computes the difference between them and calculates the median. If, for example, the median value falls within the range [20,…,39] the code assumes data has monthly frequency. 

Once the frequency is determined, it is possible to check whether there is more than one row for each frequency period. For instance, for monthly frequency, the algorithm will not allow two rows with different days in the same month. 

## Minimum data point per frequency  

Depending on the frequency of the provided data, the algorithm needs a certain amount of valid data points (number of rows) to perform the modelling and provides the best results possible. Note that some of the original rows may be dropped out before this instant, if they lack data (e.g. excess of missing values), thus decreasing the number of valid data points. After the removal, the dataset must have at least the minimum data point displayed in the table below per frequency. 

A table containing the minimum data points per frequency can be seen below: 

Frequency              | Minimum data points
:---:                  | :---:
Daily                  | 180 
Weekly                 | 52 
Fortnightly (biweekly) | 24 
Monthly                | 36 
Bimonthly              | 24 
Quarterly              | 24 
Half-year              | 24
Annual                 | 12 

## Lagged variables - definition  

A lag variable is a variable constructed such that its values are the numbers coming from earlier period in the time series. The table below displays an example of lagged variables for sales. We can lag a variable as much as we have time periods for that, but it is important to note that, at each time you lag a variable, you lose the oldest observation. If you would like to lag two times, you would lose the two oldest observations. The number of periods in the past you would like to lag is called “lag order”. The table below shows the example for lag orders one (l1_sales) and two (l2_sales). 

Lag variables are important when we want to consider the direct influence of the past in the model. For example, when you decide the stock level of a product in a store for the next month, you consider the sales of that product in the previous month. 

   

Date | Sales | l1_sales | l2_sales 
:---: | :---: | :---: | :---:   
December/2021 | 100 | - | - 
January/2022 | 108 | 100| - 
February/2022 | 110 | 108 | 100 
March/2022 | 105 | 110 | 108 
May/2022 | 106 | 105 | 110 
April/2022 | 100 | 106 | 105 
June/2022 | 112 | 100 | 106 
July/2022 | 115 | 112 | 100 

Lagged variables in our pipeline + Warning insufficient data points for lags 

You now have the option to add lagged versions of explanatory variables into your modeling dataset automatically in our platform. Throughout the pipeline, the algorithm will choose the lag order with higher correlation with the dependent variable and add it in the dataset. This dataset will proceed to our regular feature selection (if appropriate) and modeling steps.  

There are a few rules that you should keep in mind: 

Lagged variables are added to dataset with the prefix 'l' followed by the lag number and the original variable name. For example, by applying lag 2 to variable 'x1', the variable 'l2_x1' will be created. 

Currently, it is not possible to add lagged versions of categorical or indicator variables (see 'Categorical variables' to understand which variables fall into this category). 

Lagged variables are added to dataset once all imputation and preprocessing have been applied, meaning that if the original variable had missing values, their lagged version will have the same imputed values for them.  

Missing values added due to lagging variables are not filled by any method. This implies that if lag 'x' (e.g. 5) was added to your dataset, the first 'x' rows of the dataset will be dropped.  

When working with datasets near the limit of required data points (see 'Minimum data point per frequency'), there might be a limitation to the number of lags of explanatory variables you can add to the dataset. You will only be able to add lag orders which do not make the number of data points fall below the minimum required data points. If the lag selected is higher than the maximum allowed, a warning pop out.  

For all lags of each explanatory variable, a lag search is performed choosing the lag order with higher correlation with the dependent variable. Unless the lagged variable is chosen as a Golden Variable, there is no guarantee that it will appear in the models, since the regular feature/model selection (if appropriate) are done. 

If one or more lagged variables are chosen as Golden Variables, the lag search for that explanatory variable is skipped, and the lagged variables work as any Golden Variable (see 'Golden variables - when and why'). However, the variables will not be included if the lagged variables are not available (due to minimum data points or other preprocessing detail). 

Any lagged variable included in dataset can be used as Exclusions. 

Feature selection - general idea  

Feature selection intends to select the most relevant continuous features (variables) from the set of available ones, reducing regressors matrix dimensionality, which is typically a problem for model convergence. FaaS performs an exhaustive search for the best combination of features (that grows exponentially with the number of variables), and by reducing dimensionality, it allows a more focused model search. Lastly, in many cases, there are more features than observed values, which can be a problem in identifying model parameters, feature selection reduces the chance of such a problem. 

## Feature selection – methods 

Random Forest - After fitting a random forest, features are shuffled, one by one, and the increase in Mean Squared Error (MSE) is computed. Variables leading to greater variations in MSE are taken as more important than others. A ranking is generated and trimmed to select the desired number of variables. 

Pearson Correlation Filter - It works by first filtering variables with absolute correlation greater than 0.2 with the dependent (response) variable. With this subset, it starts a pairwise analysis of most correlated features, getting the most correlated pair, eliminating the feature with lower absolute correlation with the dependent variable, repeating this process until the number of features is reduced to the desired one.  

Lasso - Runs a Lasso model with standardized data. Since data is standardized, coefficients can be used to measure "variable relevance", and by sorting the coefficients it can select the top N features. Lasso is interesting since it returns a coefficient equal to zero for the less “prominent” features. 

## Preprocessing: Rows dropped   

Data points can be dropped from a dataset due to missing values in the dependent or the explanatory variables: 

- Any missing value of the dependent variable before its first occurrence is removed from the dataset (consequently dropping the entire row). Missing values between the first and last occurrence are filled using Kalman's Filter with matrices derived from univariate ARIMA, except for datasets with daily frequency, in which case the observation is dropped.  

- Rows in the beginning of the dataset with more than 20% of missing values for the explanatory variables are trimmed out from the dataset. 

Preprocessing: Columns dropped + Warning of high % of missing   

Aiming to avoid the imputation of a high percentage of missing values, variables with more than 20% of missing values in the modeling period (i.e., data points in which values for the dependent variable are available) are dropped from the dataset. If you have such variables in your dataset, you will receive a warning indicating the variables that were removed from dataset due to a high percentage of missing values. 

Preprocessing: Data imputation methods + Warning of misleading imputation   

Warning: redundant variables - linear dependency  

Our platform automatically removes redundant variables from the dataset. Redundant variables are features which information is already fully contained in other variables. Technically, they are called linear dependent variables. Linear dependency is a mathematical concept that states that a variable is linear dependent if we can compose that variable with one or any linear combination of other time series within the dataset. It is important to drop them out, as it speeds up processing time and, also, to perform the estimation of some models, which rely on methods that require matrix inversion. You can check in the platform the variables that have been excluded from the dataset through a warning message that pops up on your screen when you click in “Modeling”. 

## Log - when and why?   

Log is the abbreviation for natural logarithm. Log transformation is a data transformation in which the original value is replaced by its natural logarithm. To apply the log transformation, the variable must have only strictly positive values, that is, neither zeros, nor negative numbers.   

It is frequently used in quantitative modeling due to its convenient mathematical properties. When applied, natural logarithm reduces the scale of the variable without changing the relations between the observations within and between series. An advantage of log transformation is the tendency to decrease the impact of outliers and reduce the variance of the series. 

For linear models, such as ARIMA, log transformation implies that we interpret the estimated coefficients as elasticities, when both the dependent and independent variables are in log (also called log-log models), or semi-elasticity, when just the dependent variable are in log (also called log-linear model).  

* Outliers may bias the estimation of the coefficients. 

** Reduction in variable’s variance may help in the statistical hypothesis tests. 

 

Log - our rules (talk about prefix ‘z_’)   

In the platform, there exists the possibility to apply the log transformation to the variables in the dataset. The default is to try to apply the log transformation to all allowed variables, that is, time series without zeros or negative numbers. If you have both types of variables in the dataset, it applies only to the allowed ones. For the variables without log transformation, it adds the prefix “z_” to the name (e.g., z_gap). In that way, you can easily identify the variables treated in the original format. It is important to highlight that it does not apply log transformation to indicator variables, such as outlier, seasonal dummies, or any type of 0-1 dichotomous variable.     

 

Categorical and indicator variables   

If a variable has few distinct values, they are considered indicator or categorical variables for feature selection purposes. All such variables are included in every ARIMA model, and therefore cannot be used as 'exclusions' or 'golden_variables'. 

The number of distinct values that a variable can assume to be considered a categorical variable depends on the data frequency: 

- For daily, weekly, and monthly data, variables with at most 5 distinct values are considered categorical variables. 

- For fortnightly, bimonthly, quarterly, and half-year data, variables with at most 4 distinct values are considered categorical variables. 

- For annual data, variables with at most 3 distinct values are considered categorical variables. 

Variables that only assume values 0 or 1 are called indicator variables. Any indicator variable is also a categorical variable. 

Seasonality (additive, d4i_)   

Within the pipeline, the seasonality is treated as additive, with the inclusion of categorical explanatory variables for each period of the data (with the prefix 'd4i_'). 

Additive seasonality assumes that the effect of the seasonal windows remains constant over time. For example, modeling a monthly dependent variable with this approach assumes that despite changes in trend, the size of the effect in the variable every December is about the same through the years. 

The seasonal dummies added in dataset will appear with the prefix 'd4i_', and the type of dummies depend on the frequency of the data, such as: 

- For monthly, weekly and fortnightly data, it is added an indicator variable for each month of the year. 

- For bimonthly data, it is added an indicator variable for each bimester of the year. 

- For quarterly data, it is added an indicator variable for each quarter of the year. 

- For half-year data, it is added an indicator variable for each semester of the year. 

- For annual data, no indicator variable is added. 

- For daily data, it is added an indicator variable for each month of the year, as well as a indicator for each day of the week (this is called multiple seasonality). 

Apart from Random Forest model, a baseline is always removed from the seasonal indicator variables, avoiding linear dependency among the explanatory variables with the intercept. 

Cross-validation (what is and how we do it)   

Cross-validation is a technique used to ensure that the models can generalize well, to avoid what is called overfitting (when a model performs well with known data, but poorly when exposed to new data). This technique consists of resampling the provided data into different training and testing samples to evaluate how the model performs in these different combinations of subsamples.  

There are multiple types of cross-validation, but for time series we use rolling cross-validation, where the samples are taken in order and the model is trained and predicts N steps ahead, where N is the forecast horizon provided. The process of subdividing the original dataset can be seen below: 

 

 

After all the iterations are done, the accuracy measures are summarized either by the mean or median of the results obtained in each iteration (what we call window), and these are the results provided for each model in the final forecast. 

Forecast Horizon (n_steps) + Test window (n_windows) 

Forecast Horizon, or n_steps, is the size of the cross-validation test set, which should be based on the number of observations to be forecasted. On the other hand, the test window, or n_windows, parameter describes how many times the model will apply the cross validation on the dataset. 

## Accuracy measures - MAPE   

The mean absolute percent error (MAPE) is the mean of absolute errors in percentage terms, for this reason, it can be used to compare series on different scales. However, MAPE is not a desirable choice when we are dealing with observed values ([Equation]) close to zero because the closer to zero the observed value is, the worse the MAPE result will be. MAPE also cannot be used for observed values ([Equation]) equal to zero, as MAPE formula includes a division and it is undefined when [Equation] is zero. 


## Accuracy measures - MPE  

The mean percentage error (MPE) is the mean error in percentage terms. It is very similar to MAPE, the only difference is that it doesn’t  use the absolute value, leading to potential positive and negative forecast errors, which can offset each other and/or result in negative values. If the model, on average, overestimates the series, MPE is negative, and vice-versa. It can be interpreted as a measure of the forecasting bias. 

## Accuracy measures - WMAPE  

The weighted mean absolute percentage error (WMAPE) is a weighted variant of MAPE. It is not sensitive to big distortions and is preferred over MAPE when series have values close to zero (since it reduces the chance of a denominator near zero) and can be used to increase weight of MAPE for larger values, which is a desired feature in many cases, as the same forecast error in higher levels could be more serious than in lower values. 

## Accuracy measures – RMSE 

The Root Mean Squared Error is an error metric that calculates the standard deviation between the observable and the forecast values. It takes the difference between these values and squares it, then the mean is calculated, and its square root is the RMSE. Because the errors are squared, larger ones are penalized. It is useful to identify how much outliers impact predictions. 

 

[Equation] 

## Accuracy measures – MASE 

The Mean Absolute Scaled Error (MASE) is an accuracy measure that compares the forecasts of a model and the forecasts of a naive approach. The naive forecasts are the last observed value of the target variable. This measure is independent of the forecast scale, since it calculates the ratio between the model and the naive forecasts errors. MASE targets values lower than 1, which indicates that the model forecasts errors were lower than the naive forecasts errors, on the other hand, if the result is greater than one, the model performed worse than the naive guessing. When trying to measure the accuracy of a forecast horizon (n_steps)  forecast, the value [Equation] used to calculate the naïve equation is always the last observed value.  

[Equation] 

 

## Accuracy measures – MASEs 

The Mean Absolute Scaled Error Seasonal is a variant of the MASE. In this approach the naive forecast errors are calculated by the mean of the differences between the target value in the time i and the target value in time i - m, where m is the seasonal length, i.e., the naïve forecast is the last value observed for the respective period. 

 

[Equation] 

cv_summary - when and why 

The parameter cv_summary stands for cross-validation summary, which determines how the accuracy measures for each window of the cross-validation process will be aggregated and summarized. This parameter can be chosen between two values, mean and median. Choosing mean will take all values from each window in the cross-validation and return the mean values between them (calculated separately for each different accuracy measure), whilst the median option will do the same process, but outputing the median value. 

The default value for the cv_summary is mean, but if it is expected that certain windows in the cross-validation will have poorer performance due to external events in the period (such as the COVID-19 pandemic for example). As those events are not expected to happen again and they can be considered outliers, median can provide a more accurate portrait of the model’s performance, as it is more robust to outlier values. 

Avoid collinearity - what is collinearity + why avoid it 

Collinearity or Multicollinearity occurs when two or more explanatory variables are highly correlated and it can also happen if an explanatory variable is a linear combination of others. Therefore, if there is collinearity between some explanatory variables, it means that they are remarkably similar/redundant and share the same information for the estimation of the desired model. 

Collinearity is a problem because it increases the standard errors of the estimated model coefficients, leading to less reliable hypothesis tests due to high variance, and potentially harming coefficients interpretation. The increase in standard error can make some explanatory variables not statistically significant when in fact they are significant (type II error). One way to correct collinearity or multicollinearity problem is to identify the variables that are correlated and remove one of them from the model as they are almost similar. 

Auto forecast - how to, when and why 

The auto forecast option helps users that do not have predicted values for explanatory variables to use them in projections. To explore the relationship in the forecast period between the response variable and an explanatory variable, it is necessary to have forecasted values for the latter.  

By selecting the option to "auto forecast", the platform will use a SARIMA model to forecast each series that has missing values in the predicted set. Importantly, the algorithm does not fill in missing values for indicator variables (or "Categorical and indicator variables" - check the definition on this help page). Also, if there is a point with a missing value in the forecast period, no prediction will occur from that point on.  

So, when to use this option? When you do not have prediction for your explanatory variable and are not willing to model such variable as a dependent variable beforehand. Otherwise, there exists the possibility of ending up with fewer predicted values than expected. However, one should keep in mind that a simple model is used to perform forecasts for those missing values and that the forecasts obtained for the response variable may depend a lot on a variable that was automatically forecasted without human supervision. 

Exclusions - when and why 

The Exclusion option is used to avoid two or more variables entering together in the same model. It is commonly applied when you include variables that represent the same economic factor (e.g. two different measures of price indexes). With the exclusion option, those variables will be tested in a final model, but they will not be included together, avoiding potential issues with collinearity. Adding variables to exclusions does not guarantee that they will be in a final model. To do that, use the Golden Variable option. 

Golden variables - when and why 

Golden variables are useful to tell the model those features that you consider extremely important. The algorithm will force this subset in a couple of ways: 

There will exist at least one model containing each golden variable (but it does not necessarily mean one model for each golden variable, e.g., golden variables are "x1", "x2" and "x3", there could be one model with "x1" and "x2", another with only "x3").  

The code will force a model with all golden variables + features that enter in all models (i.e. categorical variables). 

It will guarantee the existence of at least one model with all golden variables + other covariates, if this is possible (it may be that the only possibility is the one cited in 2) 

Prefixes added during modeling ('z_', ‘do_’, ‘d4i_’) 

During modeling it is possible that one of the following prefixes will be added to existing or created variables: 

'z_': prefix added to existing variables to indicate that the variables have values less than or equal to 0, and therefore log could not be applied; 

'do_': prefix of outlier indicator variables. This prefix can be followed by a date or 'c1', 'c2', ..., 'c7' if the outlier dates were grouped in clusters; 

'd4i_': prefix of seasonal indicator variables. This prefix is added to all seasonal indicator variables included in dataset during modeling; 