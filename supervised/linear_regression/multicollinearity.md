# **Linear Regression Model: Addressing Multicollinearity and Evaluating Model Performance**

## **Overview**

This document provides a comprehensive guide to understanding and addressing multicollinearity in linear regression models. It also covers key aspects of evaluating model performance, including R-squared values, residual analysis, and Mean Squared Error (MSE).

## **Contents**
- [Understanding Multicollinearity and its Impact](#understanding-multicollinearity)
- [Variance Inflation Factor (VIF) Calculation](#variance-inflation-factor-vif-calculation)
- [Steps to Address Multicollinearity](#steps-to-address-multicollinearity)
- [Ridge Regression as a Solution](#ridge-regression-as-a-solution)
- [Principal Component Analysis (PCA) and Partial Least Squares Regression (PLSR)](#principal-component-analysis-pca-and-partial-least-squares-regression-plsr)
- [Model Performance Evaluation (Residual Mean, MSE, R-squared)](#model-performance-evaluation)

## **1. Understanding Multicollinearity**

**Definition**:  
Multicollinearity occurs when two or more predictor variables in a regression model are highly correlated, causing issues such as unstable coefficient estimates and inflated standard errors. High VIF values (> 5 or 10) indicate severe multicollinearity.

## **2. Variance Inflation Factor (VIF) Calculation**

**Steps to Calculate VIF**:
1. **Select a Predictor Variable**: Regress it against all other predictors.
2. **Compute the R-squared Value**: From the regression of the selected predictor on others.
3. **Calculate VIF**: 
   \[
   \text{VIF}_i = \frac{1}{1 - R^2_i}
   \]
   - **VIF < 5**: Low multicollinearity.
   - **5 ≤ VIF < 10**: Moderate multicollinearity.
   - **VIF ≥ 10**: High multicollinearity.

## **3. Steps to Address Multicollinearity**

**Approaches**:
1. **Remove or Combine Predictors**: Simplify or combine correlated predictors.
2. **Use Regularization Techniques**: Apply Ridge or Lasso regression.
3. **Principal Component Analysis (PCA)**: Transform correlated predictors into uncorrelated components.
4. **Partial Least Squares Regression (PLSR)**: Create components strongly related to the dependent variable.

## **4. Ridge Regression as a Solution**

**Python Implementation**:
```python
import numpy as np
import pandas as pd
from sklearn.linear_model import Ridge
from sklearn.model_selection import train_test_split
from sklearn.metrics import mean_squared_error, r2_score

# Prepare Data
X = df.drop(columns=['dependent_variable'])
y = df['dependent_variable']
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)

# Apply Ridge Regression
ridge_model = Ridge(alpha=1.0)
ridge_model.fit(X_train, y_train)
y_pred = ridge_model.predict(X_test)

# Evaluate the Model
mse = mean_squared_error(y_test, y_pred)
r2 = r2_score(y_test, y_pred)
print(f"Mean Squared Error: {mse}")
print(f"R-squared: {r2}")

# Check Coefficients
coefficients = ridge_model.coef_
coef_df = pd.DataFrame({'Feature': X.columns, 'Coefficient': coefficients})
print(coef_df)
