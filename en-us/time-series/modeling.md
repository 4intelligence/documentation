 # Modeling types

## ARIMA  

ARIMA is an acronym for Autoregressive Integrated Moving Average model. This model allows the influence of the past values of the dependent variables in the present values, also called autocorrelation. So, it is applied to estimate dynamic models. We can divide the ARIMA into three parts: i) the autoregressive part (AR); ii) the moving average (MA) and; iii) integration part. Generally, the ARIMA(p,d,q) can be expressed as the function below:  

*add formula*

in which, p is the order of the AR part, q is the order of the MA part, d is the order of integration of the series, that is, the number of differences needed to make the time series stationary. The intercept, represented by c in the equation, is also called drift in this model. The MA represents the autocorrelation in the residuals, which, if not control may bias the estimation of the parameters. ARIMA may also include exogenous variables to increase forecasting power. When so, ARIMA is known as ARIMAX. 

To perform the estimation and forecast, FaaS applies regression model with ARMA errors which estimates the two equations: 

*add formula*

In the first equation, it estimates the exogenous variables parameters (impacts) and, in the second one, it controls the autocorrelation of the residuals, that may harm the estimation of the standard errors of the parameters. Both methods, (ARIMA and regression with ARMA errors, are similar and there is no difference in their forecasting ability, but the latter has the advantage of keeping the interpretation of the estimated parameters like in ordinary (non-dynamic) regressions. 

## Forecast Combination  

As defined by the name, forecast combination methods combine predicted values by different models, either linearly or using more sophisticated techniques, to generate new forecasts. Currently, the combination of the top 10 models according to the accuracy criterion chosen by the user (as “MAPE”) is tested, such that model numbers 1 and 2 are combined and metrics are computed, then 1, 2, and 3 are combined, and so on. All methods are performed for every combination. For each technique, the combination with the best criterion chosen by the user is chosen.  

To simplify the explanation of used methods, they were divided in 3 blocks: A) Simple Methods; B) Regression Methods; C) Eigenvector Approach; 

A) Simple Methods 

1) Bates/Granger (1969) - comb_BG 

Main idea: weight forecasts using the inverse of mean squared error prediction (mean of squared difference between forecast and actual values).  

2) Inverse Rank Forecast Combination - comb_invW 

Main idea: Rank the model with the lowest mean squared prediction as 1, the second lowest as 2, etc. Then take the inverse rank and check its weight dividing the inverse rank by the sum of inverse ranks.  

3) Median Forecast Combination - comb_MED 

Main idea: Use the median of the forecasts at each point in time. 

4) Simple Average Forecast Combination - comb_SA 

Main idea: Use the mean of the forecasts at each point in time.  

5) Trimmed Mean Forecast Combination - comb_TA 

Main idea: Trim a desired number of models based on ranking (MAE, MAPE or RMSE) and take the mean forecast. Currently, RMSE is used.  

6) Winsorized Mean Forecast Combination - comb_WA 

Main idea: Use the Winsorized mean of the forecasts at each point in time. The idea of Winsorized mean is to substitute the largest and smallest values with their nearest observations.   

7) Newbold/Granger (1974) Forecast Combination - comb_NG 

Main idea: Like “4) Standard Eigenvector Forecast Combination” but imposing the linear restriction e’w = 1, where 'e' is a vector of ones.  

B) Regression Methods  

1) Ordinary Least Squares Forecast Combination - comb_OLS 

Main idea: The OLS method runs a simple linear model with intercept using as regressors the forecasts and as dependent variable the actual values. 

2) Constrained Least Squares Forecast Combination - comb_CLS 

Main idea: Works like Ordinary Least Squares forecast combinations but add the restrictions: (1) Weights must be non-negative; (2) Weights must sum up to one; 

3) Least Absolute Deviation Forecast Combination - comb_LAD 

Main idea: It works similarly to a combination via Ordinary Least Squares but minimizes the absolute value of errors instead of squared errors. This method is more robust to outliers since the magnitude of penalization is lower than squared errors.  

C) Eigenvector approach  

1) Standard Eigenvector Forecast Combination - comb_EIG1 

Main idea: Minimize the mean squared prediction error (v) through a linear combination (w'*((v*v’)*w, where w is the weight vector). If the restriction imposed is of the format w’w = 1, the solution is one of finding the smallest eigenvector, which in turn is associated with the smallest eigenvalue.   

2) Bias-Corrected Eigenvector Forecast Combination - comb_EIG2 

Main idea: Very similar to 1) but now each vector of prediction error is subtracted from its mean, eliminating possible bias.   

3) Trimmed Eigenvector Forecast Combination - comb_EIG3 

Main idea: Very similar to 1) but pre-selects the best models that will enter in combination according to an optimization criterion: MAE, MAPE, or RMSE and keep the number of models defined by the inbuilt optimization algorithm.  Currently, RMSE is used. 

4) Trimmed Bias-Corrected Eigenvector Forecast Combination - comb_EIG4 

Main idea: Combines 2 and 3. 


## Elementary  

There currently are three distinct types of elementary models, the STL, Arima model with seasonal additive indicator variables (ARIMA_SEASD) and Seasonal Arima model (ARIMA_SEASM), which treats the seasonality in a multiplicative way. Elementary models receive such name because they only include information about the response variable itself, without the inclusion of any explanatory variables, except for those that account for seasonality or outlier observations.  

### ARIMA_SEASD 

The Arima models with additive seasonal and outlier indicator variables have the same structure as described in the Arima section, where the indicator variables are included in the model as explanatory variables. The seasonal indicator variables are included considering the data frequency, for example, for monthly dataset, variables indicating the month of the year are included; for bimonthly, indicator variables of the bimester are included. For daily dataset, on the other hand, two sets of indicator variables are added, those that account for the day of the week and another for the month of the year. The optimal order of the Arima terms is identified considering the entire modeling dataset.  

### ARIMA_SEASM 

The Seasonal Arima model accounts for seasonality within its seasonal arima order and can include outlier indicator variables, if they are identified. Differently from a regular Arima model, a Seasonal Arima model is of the form ARIMA(p,d,q)x(P,D,Q)m, where P, D and Q are the seasonal auto-regressive, differencing and moving average terms, and m indicates the data frequency. This model treats the seasonality considering it is multiplicative, ie.  the seasonal patterns change through time, while the additive seasonality (modelled through ARIMA_SEASD) assumes that the patterns remain constant. 

### STL 

The Seasonal and Trend decomposition using Loess (STL) is a method for estimating patterns within the response variable. A time series decomposition consists of separating the effects in the data into a trend, seasonality and an error, this way it is possible to see clearly each of these effects individually and identify important aspects of the data. The SLT Decomposition estimates these components iteratively, using Loess’ interpolation to smooth the estimation of the seasonal components and to find the trend estimation. 

## Regularized Regression 

Regularized regressions are methods designed to shrink coefficients toward zero by penalizing larger coefficients in the loss function. The idea is that this kind of model generalizes better, since each regressor contributes a little bit to the result, getting “smoother” results. Regularizations can be of type L1 (Lasso) or L2 (Ridge), with ElasticNet combining both.  

L1 and L2 types impose a penalty in the loss function, which is proportional to the size of the absolute coefficients for L1 and is quadratic to L2. The Lasso model represents L1 regularization and L2 Ridge, whereas Lasso may shrink coefficients to zero, Ridge may shrink them toward zero, but never reaching it. There is a parameter, lambda, which controls the degree of this penalty, if it goes to infinity, coefficients move toward  ElasticNet combines L1 and L2 and has an additional parameter, “alpha”, which is a kind of weight given for L1, with its “counterpart” weight proportional to 1 - alpha for L2. 

## Random Forest 

Random forests, or random decision forests, is a model proposed by Ho in 1995 based on decision trees. It aims to reduce the decision tree problem of not generalizing well to new data (overfitting) by making an ensemble of multiple trees using a method called bagging (bootstrap aggregating). 

The method works by extracting subsamples of features from the original dataset and training different trees with these subsamples. The results from each tree are then averaged for regression problems (which is the case for time series forecasting) or the majority vote for classification. 

As a non-parametric model, Random Forest has no parameters, but rather hyperparameters, from which we test two: 

- mtry: number of predictors sampled for spliting at each node; 
- ntree: Number of trees to grow. 
