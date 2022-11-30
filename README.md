# Advanced Regression Project

## House Price Regression

A US-based housing company named Surprise Housing has decided to enter the Australian market. The company uses data analytics to purchase houses at a price below their actual values and flip them on at a higher price. For the same purpose, the company has collected a data set from the sale of houses in Australia. The data is provided in the CSV file below.

The company is looking at prospective properties to buy to enter the market. You are required to build a regression model using regularisation in order to predict the actual value of the prospective properties and decide whether to invest in them or not.

The company wants to know: Which variables are significant in predicting the price of a house, and how well those variables describe the price of a house.

We also need to determine the optimal value of lambda for ridge and lasso regression.


## Business Goal:  
We are required to model the price of houses with the available independent variables. This model will then be used by the management to understand how exactly the prices vary with the variables. They can accordingly manipulate the strategy of the firm and concentrate on areas that will yield high returns. Further, the model will be a good way for management to understand the pricing dynamics of a new market.


Using GridSearchCV the model arrives at a final optimum lambda to determine the house prices using ridge and lasso regression.



## Steps followed:
1. Data Understanding, Data Cleaning, EDA and Data Preparation
    - All data quality checks are performed, and all data quality issues are addressed in the right way (missing value imputation, removing duplicate data and other kinds of data redundancies, etc.). Data quality issues are clearly explained in comments.
    - Dummy variables are created properly, wherever applicable.
    - New metrics are derived, if applicable, and are used for analysis and modelling.
    - The data is converted to a clean format suitable for analysis.


2. Model Building and Evaluation: Three models were trained, namely, Simple Linear Regression Model and two mOdels with regularization - Ridge Model and Lasso Model
    - Model parameters are tuned using correct principles, and the approach is explained clearly. Both the technical and business aspects are considered while building the model.
    - Correct variable selection techniques are used. A reasonable number of different models are attempted, and the best one is chosen based on key performance metrics.
    - Model evaluation is done using the correct principles, and appropriate evaluation metrics are chosen.
    - The results are on par with the best possible model on the data set.
    - The model is interpreted and explained correctly. The commented code includes a brief explanation of the important variables and the model in simple terms.


## Ridge Model Interpretation
From different variations that I tried (number of features = 40 to 110, num of folds = 5 & 10, scaling method = normalization & standardization, varied values of alpha), I learnt following:

    1. Scaling tecniques: Standardization scaling works better than min-max scaling. This might be because target variable distribution is not exxactly Gaussian, in fact it is a little right skewed. Standardization will scale all features such that mean = 0 and distribution is closer to Gaussian.
    
    2. number of indeppendent features used to predict: There were 176 columns and hence 175 features (as one of the column is for target variable). This is a lot of features and so come to a reasonale conclusion on number, I trained model with N = 40, 50, 55, 60, 65, 70, 75 , 80, 90, 100, 110.
    
    Criteria used to zeroed down to best possible number of predictor variables was to have almost similar r2 score for test and train data ensuring thhere is no overfitting. Number cannot be too small to avoid underfitting.
    While results were improving from 40 to 110, the improvement in r2 score was not significant after N = 70
    After going throght all results, I decided to go with N = 90 which gave r2 score of 0.93 and 0.88 respectively for train and test data, which looks pretty good.
       
    3. number of folds: tried withh 5 and 10 folds. We know that a higher number of folds means that each model is trained on a larger training set and tested on a smaller test fold. In theory, this should lead to a lower prediction error as the models see more of the available data. And thhat is exactl what I observed. Results with 10 fold were better than 5 folds and hence presented that in this code.    
    
    4. Most important features: higher coefficient value indicates more importaqnt is the feature as it contributes more in predicting the target variable. In the above training case, looking at the coefficient values, we can say that top 5 important features are (from higher to lower importance)

        - BsmtCond_2.0	0.360527
        - SaleType_Oth	0.355191
        - Neighborhood_NridgHt	0.345379
        - GarageArea	0.322681
        - FireplaceQu_5.0	0.290445

    5. Metrics that evaluates Model performance:
    
    r2 score of training set =  0.93
    r2 score of testing set =  0.88

    rss value of training set =  64.12
    rss value of testing set =  48.92
        
    MSE value of training set =  0.07
    MSE value of testing set =  0.12
    

## Lasso Model Interpretation
From different variations that I tried (number of features = 40 to 110, num of folds = 5 & 10, scaling method = normalization & standardization, varied values of alpa), I learnt following:

    1. Scaling tecniques: Standardization scaling works better than min-max scaling. This might be because target variable distribution is not exxactly Gaussian, in fact it is a little right skewed. Standardization will scale all features such that mean = 0 and distribution is closer to Gaussian.
    
    2. number of indeppendent features used to predict: criteria used is same as whhat is explained above for Ridge
       
    3. number of folds: tried withh 5 and 10 folds. We know that a higher number of folds means that each model is trained on a larger training set and tested on a smaller test fold. In theory, this should lead to a lower prediction error as the models see more of the available data. However, in this case, results with 5 folds were better than 10 folds and hence presented that in this code. 
        
    4. Most important features: higher coefficient value indicates more importaqnt is the feature as it contributes more in predicting the target variable. In the above training case, looking at the coefficient values, we can say that top 5 important features are (from higher to lower importance)
        - BsmtCond_2.0	0.366245
        - SaleType_Oth	0.345030
        - Neighborhood_NridgHt	0.330837
        - GarageType_CarPort	0.329764
        - GarageFinish_3.0	0.326146

    
    5. Metrics that evaluates Model performance:
    
    r2 score of training set =  0.93
    r2 score of testing set =  0.87

    R-Squared (R² or the coefficient of determination) is a statistical measure in a regression model that determines the proportion of variance in the dependent variable that can be explained by the independent variable. In other words, r-squared shows how well the data fit the regression model (the goodness of fit). FRom the definition it is clear that higher it is , better fit is the model.

       In above model, r2 score for training as well as testing data set is close to each other indicating no overfitting of data. 
    Both values are pretty high too, indicating chosen independent variables and trained coefficients fits well to data and hence as hhigh prediction power

    rss value of training set =  62.36
    rss value of testing set =  50.66
        
    The residual sum of squares (RSS) measures the level of variance in the error term, or residuals, of a regression model. The smaller the residual sum of squares, the better your model fits your data; the greater the residual sum of squares, the poorer your model fits your data.
    
    Considering this is sum of square of errors, 62.36 and 50.66 are quite small values indicating good fit.
    
    MSE value of training set =  0.07
    MSE value of testing set =  0.12
    

    The Mean Squared Error measures how close a regression line is to a set of data points. It is a risk function corresponding to the expected value of the squared error loss. Mean square error is calculated by taking the average, specifically the mean, of errors squared from data as it relates to a function.
    
    Once again 0.07 and 0.12 are prett low values for MSE, reinstating that we have a good model here.

## Comparing three models

1. If we look at thhe performance metrics, there is no major difference between three models and one may think wh not use Simple Linear Regression

2. However, what is interesting is the coefficient values:
If you look closely, Lasso has 7 features with coefficient value = 0

So Lasso has manged to reduce 7  variables' coefficients to zero and hence managed to eliminate 7 features wich are irrelevant, namely - BsmtUnfSF , Exterior1st_AsphShn ,  Exterior2nd_Brk Cmn	,  HeatingQC_1 , HeatingQC_3 , GarageQual_2.0 , GarageQual_5.0 
    
While Ridge and simple LR retained those variables may be with smaller coefficient values.

This shows that Lasso managed to get same performance with less number of features by eliminating irrelevant features and hence it is a simpler model, with lesset features giving same performance on given training / testing data.

When we have two (or three) competing models that fit the data equally well, Occam's razor recommends to 'shave away all but what is necessary'. The concept of parsimony is based on Occam's razor, which also proposes that the model with fewer parameters to be preferred to the one with more. Which means Lasso is the best option out of the three models.



 