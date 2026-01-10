## Introduction

The goal of this case study is to create a heart failure prediction model with at least 90% accuracy using the [Heart Failure Prediction Dataset](https://www.kaggle.com/datasets/fedesoriano/heart-failure-prediction/data?select=heart.csv) by `fedesoriano`.

This case study will follow several common steps of Data Analysis process such as preprocessing, Exploratory Data Analysis (EDA), model building, model evaluation, and model selection.

## Exploratory Data Analysis

![](Heart-Failure-Prediction_files\figure-html\Distribution-of-Dependent-Variable-1.png)

As we can see our outcome variable is binary with sufficient counts in each category. Our initial assumption would be that a Logistic Regression model would be best for creating a predictive model.

There several other assumptions which must be met to perform a Logistic Regression model:

1)  Our observations must be independent, based on the data source this appears to be true.

2)  There is low multicollinearity among our independent (predictor) variables. This we will be testing to confirm.

3)  Linearity of the log-odds of the dependent variable and the continuous independent variables.

4)  A large enough sample size, with our sample size of 918 observations we're confident that we meet this requirement. Using [Peduzzi Formula](https://pubmed.ncbi.nlm.nih.gov/8970487/) $N =\frac {10 \times k}{p}$ confirms that a sample size of at least `r signif(((ncol(hf_data) - 1) * 10) / (sum(hf_data$HeartDisease == "0") / nrow(hf_data)), 1)` is enough.
