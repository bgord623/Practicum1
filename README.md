**Practicum I summary - Statistical analysis and prediction of Major League Baseball earnings**

**Overview**

The purpose of this project was to analyze baseball batting and fielding statistics and attempt to predict a player’s combined earnings based on their individual statistics. The data was obtained, cleaned, and prepared. Exploratory data analysis (EDA), visualization, and feature selection were performed. The final stage involved implementing machine learning (ML) techniques to make earnings predictions and analyzing the results.

**Table of contents**

1.	Description of data
2.	Scoring metrics
3.	Data cleaning and preparation
4.	Exploratory data analysis and visualization
5.	Feature importance and selection
6.	Machine learning modeling & evaluation
7.	Final analysis

**Description of data**

CSV files downloaded from the seanlahman.com archive 

**Scoring metrics**

For each ML model utilized, a R-squared (R^2) value and Mean Absolute Error (MSE) or Negative Mean Absolute Error (NMAE) will be provided:
- R^2 represents the proportion of the variance in the target variable that is explained by the ML model. Ranging from 0 to 1, with higher values indicating a better fit
- MAE measured the average absolute difference between the predicted and actual earnings totals

**Data cleaning and preparation**

-	The timeframe was set to 1985-2016 to coincide with the available salary data
-	Feature engineering led to the creation of 4 new columns (POS, SLG, OBP, PA)
-	Earnings were adjusted to reflect annual payroll inflation
-	Dataframes were merged and missing values dealt with
-	Finalized dataframe had ~2500 rows, down from 140K (fielding file)

**Exploratory data analysis and visualization**

Correlation matrix shows strong correlation with many features and target variable (column 1). Multicollinearity was also present:
![image](https://user-images.githubusercontent.com/102693978/223831830-b62a7007-b7e4-4f91-b92d-c43f1528b587.png)

Columns with high correlation with the target variable were cumulative statistics, including runs & RBIs:
 
 
**Feature importance and selection**

I relied on the results of the `RandomForestRegressor()` to determine feature importance and dropped columns below the .02 threshold (blue arrow). The red arrow is a random number column

 
‘PA’ was dropped reduce multicollinearity, and the finalized dataset included 4 features + the target:

 
**Machine learning and evaluation** 

The final stage was fitting the data to various ML models and evaluating the results with R^2 and MAE values. The ML models used include:

-	Simple Linear Regression
-	Multiple Linear Regression
-	K-nearest Neighbors (random k, tuned k)
-	K-Fold Cross-Validation 
        - 5 folds ~ 500 rows each
        - Scaled & unscaled data
        - Models used:
            - Regression:
                - Linear Regression
                - Lasso, LassoCV
                - RidgeCV
                - ElasticNet
            - Ensemble:
                - Ada Boost Regressor (AB)
                - Gradient Boosting Regressor (GBM)
                - Random Forest Regressor (RF)
                - Extra Trees Regressor (ET).
                
**Evaluation** 

The highest R^2 value was from the Kfold GBM model, and the lowest MAE was from the tuned KNN model (k=26). The Kfold method (highlighted blue) had higher R^2 values and MAEs with the exception being the standalone KNN regressor.

Machine learning results for all models:

My final thought on this topic is that it is logical for higher statistical totals to translate to higher salaries. Players who put up significant stats in at least one of the feature columns (RBI, R, H, IBB) are likely to have played multiple seasons, received multiple contracts, and thus receive higher earnings. 
