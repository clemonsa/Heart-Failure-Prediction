## Introduction

The goal of this case study is to create a heart failure prediction model with at least 90% accuracy using the [Heart Failure Prediction Dataset](https://www.kaggle.com/datasets/fedesoriano/heart-failure-prediction/data?select=heart.csv) by `fedesoriano`.

This case study will follow several common steps of Data Analysis process such as preprocessing, Exploratory Data Analysis (EDA), model building, model evaluation, and model selection.

## Exploratory Data Analysis
For our analysis we will select `HeartDisease` as the outcome (dependent) variable and explore the remaining variables in relation to it.

### Heart Disease Distribution
![](https://github.com/clemonsa/Heart-Failure-Prediction/blob/5cc9eccfeb03444212dc2c2c7d3bd0150db19049/Heart-Failure-Prediction_files/figure-html/Distribution%20of%20Dependent%20Variable-1.png)

As we can see our outcome variable is binary with sufficient counts in each category. Our initial assumption would be that a Logistic Regression model would be best for creating a predictive model.

There several other assumptions which must be met to perform a Logistic Regression model:

1)  Our observations must be independent, based on the data source this appears to be true.

2)  There is low multicollinearity among our independent (predictor) variables. This we will be testing to confirm.

3)  Linearity of the log-odds of the dependent variable and the continuous independent variables.

4)  A large enough sample size, with our sample size of 918 observations we're confident that we meet this requirement. Using [Peduzzi Formula](https://pubmed.ncbi.nlm.nih.gov/8970487/) $N =\frac {10 \times k}{p}$ confirms that a sample size of at least `r signif(((ncol(hf_data) - 1) * 10) / (sum(hf_data$HeartDisease == "0") / nrow(hf_data)), 1)` is enough.

### Continuous Predictors
![](https://github.com/clemonsa/Heart-Failure-Prediction/blob/fa1429968369df0283a92774a1780b30f4413338/Heart-Failure-Prediction_files/figure-html/Correlation%20of%20Continuous%20Predictors-1.png)

The above correlation matrix information suggests that there is little collinearity between the predictors. We will further confirm this by obtaining the **Variance Inflation Factor** (VIF) after fitting our model.

![](https://github.com/clemonsa/Heart-Failure-Prediction/blob/main/Heart-Failure-Prediction_files/figure-html/Distribution%20of%20Continuous%20Predictors-1.png)

Next we will visualize the distribution of our continuous predictors by the outcome.

We can see that for those who do not have heart disease:

1)  Tend to be younger

2)  Most serum cholesterol levels \~227 mm/dl

3)  A higher maximum heart rate

4)  Lower ST Depression (Old Peak)

Noticeably the resting blood pressure seems to be very similar between the groups.

### Categorical Predictors

Finally are the Categorical Predictors

![](https://github.com/clemonsa/Heart-Failure-Prediction/blob/main/Heart-Failure-Prediction_files/figure-html/Distribution%20of%20Categorical%20Predictors-1.png)

We can see that for those who do not have heart disease:

1)  They are mostly non-asymptomatic for chest pain.

2)  The majority lack exercise-induced angina.

3)  Few have a fasting blood sugar level greater than 120 mg/dl

4)  Fewer resting ECG with probable or definite left ventricular hypertrophy

5)  Demonstrate major upsloping of the peak exercise ST segment, in contrast those who are positive show a flatter slope.

Notably most cases who are positive for heart disease are overwhelmingly male. Furthermore Fasting Blood Sugar levels are a big vague as a categorical variable in contrast to a continuous variable as there are similar amounts of participants within both outcome groups with blood sugar equal or lesser than 120 mg/dl.

## Final Model Build

### Metrics

Now we will do a final evaluation of our model using several additional metrics based on the predictions as well as check for collinearity between the predictors.

1.  Using `car::vif()` we can see there are only two predictors of some moderate concern for collinearity within our model, `ST_Slope_Flat` and `ST_Slope_Up` with values \~ 4. Conventionally values of 4 - 5 are considered acceptable in prediction models.

2.  Additional metrics used shows that our model is good.

3.  Outlier data points which could improve our model if removed.

### Visualizations

![](https://github.com/clemonsa/Heart-Failure-Prediction/blob/main/Heart-Failure-Prediction_files/figure-html/Final%20Model%20Visualizations-1.png)
![](https://github.com/clemonsa/Heart-Failure-Prediction/blob/main/Heart-Failure-Prediction_files/figure-html/Final%20Model%20Visualizations-2.png)
![](https://github.com/clemonsa/Heart-Failure-Prediction/blob/main/Heart-Failure-Prediction_files/figure-html/Final%20Model%20Visualizations-3.png)
Our visualizations provide several outliers or influential observations that we should consider removing before refitting our model.

## Next Steps

Unfortunately our final model does not meet the 90% accuracy goal we have set at the beginning of this Case Study. A suggestion would be to use another classification model such as a Regularized Logistic Regression model, Support Vector Machine, k-Nearest Neighbors and Decision Trees.

We could also remove data points with high influence or outliers to see if that improves our fit.

We will approach this again in another Case Study.
