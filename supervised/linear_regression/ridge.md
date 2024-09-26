# Ridge Regression

## Introduction
Ridge Regression is an extension of linear regression that handles multicollinearity and reduces overfitting in models. It is also known as **L2 Regularization** because it adds a penalty equal to the square of the magnitude of coefficients to the loss function. This technique prevents the model from fitting too closely to the training data, thereby improving its generalization on unseen data.

## Purpose of Ridge Regression
- The primary goal of Ridge Regression is to improve the model's ability to generalize by shrinking the coefficients of less important features, reducing model complexity.
- It is particularly effective when the number of predictors is large or when predictors are highly correlated.

## Mathematical Formulation

In standard linear regression, the objective is to minimize the sum of squared residuals:

\[
\text{Objective Function} = \sum_{i=1}^n (y_i - \hat{y}_i)^2
\]

Where:
- \(y_i\) is the actual value.
- \(\hat{y}_i\) is the predicted value.

Ridge Regression modifies the cost function used in ordinary least squares (OLS) by adding a regularization term (penalty).

The modified cost function is given by:

\[
\text{Cost Function} = \frac{1}{2n} \sum_{i=1}^{n} (y_i - \hat{y}_i)^2 + \lambda \sum_{j=1}^{p} \beta_j^2
\]

Where:
- \( n \): Number of observations.
- \( y_i \): Actual values.
- \( \hat{y}_i \): Predicted values.
- \( \beta_j \): Coefficients of the model.
- \( \lambda \) (Lambda): Regularization parameter (hyperparameter).
- \( \sum_{j=1}^{p} \beta_j^2 \): Sum of squares of the coefficients.

## Role of Lambda (λ) in Ridge Regression
- **Lambda (λ)** is a hyperparameter that controls the extent of shrinkage applied to the coefficients:
  - When λ = 0, Ridge Regression behaves the same as OLS regression, with no regularization.
  - As λ increases, the penalty on the coefficients becomes larger, reducing their magnitude and shrinking the slope values.
- A higher value of λ forces the coefficients of less significant features (those not correlated with the target variable) to shrink towards zero, thereby reducing their impact.

## Effect on Overfitting
- Ridge Regression helps reduce overfitting by adding a penalty term, preventing the model from fitting the noise present in the training data.
- By penalizing large coefficients, Ridge Regression ensures the model focuses on the most relevant predictors, improving its performance on new, unseen data.

## Practical Insight
- As λ increases, the coefficients shrink, reducing the impact of features that are not significantly correlated with the target variable.
- The slope (coefficient) will decrease as λ increases, effectively reducing the impact of less significant features.

## Example with Dataset

Let's consider a simple dataset with three features (`X1`, `X2`, `X3`) and a target variable (`Y`).

| Observation | X1 | X2 | X3 | Y   |
|-------------|----|----|----|-----|
| 1           | 1  | 2  | 3  | 10  |
| 2           | 2  | 3  | 4  | 12  |
| 3           | 3  | 4  | 5  | 14  |
| 4           | 4  | 5  | 6  | 16  |
| 5           | 5  | 6  | 7  | 18  |

**Step 1: OLS Regression**
- Using OLS, the model fits the line that minimizes the residual sum of squares without any regularization.
- Coefficients might be larger, especially when features are highly correlated.

**Step 2: Ridge Regression with λ = 1**
- Ridge Regression modifies the cost function by adding the penalty term.
- Suppose we set λ = 1; the cost function now includes the sum of the squared coefficients multiplied by λ.

Let's compute Ridge Regression with λ = 1:

\[
\text{Cost Function} = \frac{1}{2 \times 5} \sum_{i=1}^{5} (Y_i - \hat{Y}_i)^2 + 1 \times (\beta_1^2 + \beta_2^2 + \beta_3^2)
\]

- The coefficients will be shrunk compared to OLS, reducing overfitting.
- The model with λ = 1 will penalize larger coefficients, shrinking them towards zero but not fully to zero.

**Effect on Coefficients:**
- Suppose the original OLS coefficients were β1 = 3, β2 = 2, β3 = 1. With Ridge Regression (λ = 1), they might reduce to β1 = 2.5, β2 = 1.8, β3 = 0.9, showing the shrinkage effect.

**Step 3: Increasing λ**
- If λ is increased further, for example, λ = 10, the penalty becomes more significant:
  
\[
\text{Cost Function} = \frac{1}{2 \times 5} \sum_{i=1}^{5} (Y_i - \hat{Y}_i)^2 + 10 \times (\beta_1^2 + \beta_2^2 + \beta_3^2)
\]

- The coefficients will shrink even more, showing how Ridge Regression controls overfitting by reducing the influence of non-significant features.

## Advantages of Ridge Regression
- **Reduces Overfitting:** By adding a penalty to the cost function, Ridge Regression reduces the risk of overfitting, making the model perform better on unseen data.
- **Handles Multicollinearity:** When predictors are highly correlated, Ridge Regression can effectively handle this by penalizing large coefficients.
- **Keeps All Features:** Unlike Lasso Regression, Ridge Regression does not reduce coefficients to zero, ensuring that all features contribute to the model to some extent.
- **Stability of Coefficients:** It helps stabilize coefficients by reducing the impact of less relevant features, making the model more robust.

## Disadvantages of Ridge Regression
- **Interpretability:** Ridge Regression can make the model harder to interpret since it does not perform feature selection, and all features are retained.
- **Not Suitable for Sparse Models:** Since it does not set coefficients to zero, it is not ideal for models where feature selection is desired.
- **Effectiveness Dependent on λ:** Choosing the correct λ value is crucial; a poorly chosen λ can still lead to either overfitting (if too small) or underfitting (if too large).
- **Cannot Eliminate Irrelevant Features:** Unlike Lasso, it does not eliminate features completely, which can be a drawback if feature selection is necessary.

## Comparison with Other Regularization Techniques
- Unlike Lasso Regression, which can shrink some coefficients to zero, Ridge Regression only reduces coefficients towards zero but never fully to zero.
- Ridge Regression is particularly useful when all predictors contribute to some extent but with varying significance levels.

## Conclusion
Ridge Regression is a powerful tool for reducing overfitting and handling multicollinearity, making it an essential technique in the toolkit of machine learning practitioners. Its ability to shrink coefficients without setting them to zero allows for better generalization and improved model performance on unseen data.
