# Ridge Regression

Ridge regression is a technique used to address the issue of multicollinearity in linear regression models. Multicollinearity occurs when predictor variables are highly correlated, leading to unstable estimates of regression coefficients and making the model's predictions unreliable. Ridge regression adds a penalty term to the standard linear regression cost function to stabilize the coefficient estimates.

## Ridge Regression Model

In standard linear regression, the objective is to minimize the sum of squared residuals:

\[
\text{Objective Function} = \sum_{i=1}^n (y_i - \hat{y}_i)^2
\]

Where:
- \(y_i\) is the actual value.
- \(\hat{y}_i\) is the predicted value.

Ridge regression modifies this by adding a penalty term proportional to the square of the magnitude of the coefficients. The modified objective function becomes:

\[
\text{Objective Function} = \sum_{i=1}^n (y_i - \hat{y}_i)^2 + \lambda \sum_{j=1}^p \beta_j^2
\]

Where:
- \( \lambda \) is the regularization parameter.
- \( \beta_j \) represents the coefficients of the predictors.

## Key Components

1. **Penalty Term**: The penalty \( \lambda \sum_{j=1}^p \beta_j^2 \) discourages the model from fitting the data too closely by penalizing large coefficients.
2. **Regularization Parameter (\( \lambda \))**: Controls the strength of the penalty. A higher \( \lambda \) shrinks the coefficients, while \( \lambda = 0 \) makes Ridge regression equivalent to ordinary least squares (OLS).

## Example

Consider a dataset with one predictor variable \( x \) and a response variable \( y \):

| \( x \) | \( y \) |
|--------|--------|
| 1      | 2      |
| 2      | 4      |
| 3      | 6      |
| 4      | 8      |

The linear model is \( y = \beta_0 + \beta_1 x \).

### Standard Linear Regression
Ordinary least squares (OLS) would calculate the coefficients by minimizing the sum of squared residuals without any penalty.

### Ridge Regression
The objective function to minimize becomes:

\[
\text{Objective Function} = \sum_{i=1}^4 (y_i - \beta_0 - \beta_1 x_i)^2 + \lambda \beta_1^2
\]

Assume \( \lambda = 1 \). Ridge regression will shrink the coefficient \( \beta_1 \), reducing model complexity and mitigating overfitting.

### Solving for Coefficients
The coefficients are computed by solving the modified normal equation:

\[
(\mathbf{X}^T \mathbf{X} + \lambda \mathbf{I}) \mathbf{\beta} = \mathbf{X}^T \mathbf{y}
\]

Where:
- \( \mathbf{X} \) is the matrix of predictors.
- \( \mathbf{I} \) is the identity matrix.
- \( \mathbf{\beta} \) is the vector of coefficients.

## Advantages of Ridge Regression

1. **Reduces Variance**: Shrinking coefficients reduces the variance of the model, making it robust to multicollinearity.
2. **Improves Stability**: Provides more stable estimates when predictors are highly correlated.

## Disadvantages

1. **Bias**: Ridge regression introduces bias into the coefficient estimates.
2. **Does Not Perform Feature Selection**: Ridge regression does not set coefficients exactly to zero, unlike Lasso regression.

## Conclusion

Ridge regression is a valuable tool to handle multicollinearity and stabilize model predictions by adding a regularization term to the objective function. It helps improve model reliability, especially when dealing with highly correlated predictors.

