# Linear Regression Overview

## 1. Types of Linear Regression
- **Simple Linear Regression (SLR)**: Involves one independent variable (input feature) to predict a dependent variable (output).
- **Multiple Linear Regression (MLR)**: Involves two or more independent variables to predict the dependent variable.

---

## 2. Simple Linear Regression (SLR)

### Best Fit Line
- The goal is to find a line that minimizes the prediction error, measured as the vertical distance from each data point to the line.

### Mathematical Equation
\[
y = mx + c
\]
- **c (Intercept)**: The value of \(y\) when \(x = 0\), indicating where the line intersects the y-axis.
- **m (Slope)**: Indicates how much \(y\) changes for a one-unit increase in \(x\). It reflects the strength and direction of the relationship between \(x\) and \(y\).

### Predicted Values
- **\(Y^ (Y\hat)\)**: Represents the predicted output based on the input \(x\).

### Error Calculation
- **Error**: The difference between the actual value and the predicted value.
\[
\text{Error} = y - \hat{y}
\]

### Creating the Best Fit Line
- Start with an initial guess for the line and iteratively adjust \(c\) and \(m\) to minimize the overall error using optimization techniques like gradient descent.

### Learning Rate (\(\alpha\))
- The learning rate controls how quickly the model adjusts the coefficients. A too-large \(\alpha\) can cause overshooting, while a too-small \(\alpha\) can lead to slow convergence.

### Convergence Algorithm
- The optimization algorithm continues to adjust the parameters until it reaches a point where further changes yield negligible improvements (i.e., convergence to the global minimum error).

---

## 3. Multiple Linear Regression (MLR)
- MLR extends SLR by incorporating multiple independent variables:
\[
y = b_0 + b_1x_1 + b_2x_2 + ... + b_nx_n
\]
- Each \(x_i\) has a corresponding coefficient \(b_i\) that quantifies its influence on \(y\).

---

## 4. Performance Metrics

### R-Squared (\(R^2\))
- **Definition**: \(R^2\) quantifies the proportion of variance in the dependent variable that can be predicted from the independent variables.
\[
R^2 = 1 - \frac{SS_{res}}{SS_{tot}}
\]
  - **Residual Sum of Squares (\(SS_{res}\))**: The sum of squared differences between actual and predicted values.
  \[
  SS_{res} = \sum{(y - \hat{y})^2}
  \]
  - **Total Sum of Squares (\(SS_{tot}\))**: The total variance in the dependent variable.
  \[
  SS_{tot} = \sum{(y - \bar{y})^2}
  \]
  - \(R^2\) ranges from 0 to 1. A higher \(R^2\) indicates a better fit, meaning a greater proportion of variance is explained by the model.

### Adjusted R-Squared
- **Definition**: Adjusted \(R^2\) modifies \(R^2\) to account for the number of predictors in the model, preventing overfitting.
\[
\text{Adjusted } R^2 = 1 - \frac{(1 - R^2)(N - 1)}{N - P - 1}
\]
  - **N**: Number of observations (data points).
  - **P**: Number of independent variables.
- Adjusted \(R^2\) can decrease if unnecessary predictors are added, even if \(R^2\) increases.

### When to Use \(R^2\) vs. Adjusted \(R^2\):
- **Use \(R^2\)**: 
  - When you have a simple model with one or very few predictors.
  - When the focus is on the goodness of fit for models where you expect all predictors to be relevant.
  
- **Use Adjusted \(R^2\)**:
  - When comparing models with different numbers of predictors.
  - When you suspect some predictors may not be significant, and you want a measure that penalizes adding irrelevant predictors.

---

## 5. Error Metrics

### Mean Squared Error (MSE)
- **Definition**: Measures the average of the squares of the errors, providing a larger penalty for larger errors.
\[
\text{MSE} = \frac{1}{n} \sum{(y - \hat{y})^2}
\]

#### Advantages
- **Fast Convergence**: Especially useful in optimization algorithms that rely on gradient descent.
- **Differentiable**: Allows for smooth updates of coefficients.

#### Disadvantages
- **Sensitive to Outliers**: Larger errors have disproportionately higher effects due to squaring.
- **Units Mismatch**: The output is in squared units of the target variable, complicating interpretation.

---

### Mean Absolute Error (MAE)
- **Definition**: Measures the average of the absolute errors, providing a more straightforward interpretation.
\[
\text{MAE} = \frac{1}{n} \sum{|y - \hat{y}|}
\]

#### Advantages
- **Robust to Outliers**: Less sensitive to extreme values than MSE.
- **Intuitive Units**: The error is in the same units as the target variable.

#### Disadvantages
- **Slower Convergence**: Can take longer to optimize due to its non-differentiable nature at zero.
- **Complex Optimization**: Involves more computation in optimization processes.

---

### Root Mean Squared Error (RMSE)
- **Definition**: The square root of MSE, converting the error back to the original units.
\[
\text{RMSE} = \sqrt{\text{MSE}}
\]

#### Advantages
- **Intuitive Units**: Provides an error measure in the same units as the target variable.

#### Disadvantages
- **Sensitive to Outliers**: Inherits the sensitivity of MSE to large errors.

---

## 6. Key Concepts

### Differentiability
- A function is **differentiable** if it has a defined slope (derivative) at every point. This property is crucial for optimization methods that adjust parameters to minimize error based on gradients.

---

### Summary of When to Use Each Metric:
- **MSE**: Use when computational speed is essential and you're willing to handle outlier influence.
- **MAE**: Use when robustness to outliers is required and interpretability is important.
- **RMSE**: Use when you want to measure error in the same unit and are okay with some sensitivity to outliers.
- **\(R^2\)**: Use in simpler models where predictor relevance is assumed.
- **Adjusted \(R^2\)**: Use in more complex models to prevent overfitting and assess the importance of predictors.

---
