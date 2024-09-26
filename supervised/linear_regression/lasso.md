# Lasso Regression

Lasso Regression (Least Absolute Shrinkage and Selection Operator) is a regression technique that performs both variable selection and regularization to enhance the prediction accuracy and interpretability of the statistical model it produces.

## Key Concepts

### 1. Feature Selection
- Lasso Regression automatically selects important features by shrinking the coefficients of less important features to zero, effectively removing them from the model.
- This process is crucial when dealing with high-dimensional datasets with many features, as it helps in simplifying the model and reducing overfitting.

### 2. Cost Function Formula
The Lasso Regression cost function is defined as:

Cost Function= 1/2n * ∑ (Residuals**2)+λ∑ ∣Coefficients∣

- The first part, 1/2n * ∑ (Residuals**2), represents the sum of the squared residuals, measuring how well the model fits the data.
- The second part, λ∑ ∣Coefficients∣, is the regularization term that penalizes the absolute values of the coefficients, shrinking them towards zero.

### 3. Impact of Lambda (λ)
- As the value of λ increases, the penalty on the coefficients increases, causing them to decrease in magnitude.
- At a certain point, some coefficients may become zero, effectively removing those features from the model. This property makes Lasso Regression a great tool for feature selection.
- Unlike Ridge Regression, which shrinks coefficients but never reduces them to zero, Lasso Regression can eliminate features entirely.

### 4. When to Use Lasso Regression
- Lasso is particularly useful when working with datasets with hundreds or thousands of features, many of which may not be correlated with the target variable.
- It helps streamline the model by focusing on the most relevant features, enhancing interpretability and performance.

## Example with Dataset

Consider a dataset with 5 features predicting the target variable `Sales`:

| Feature          | Description                  |
|------------------|------------------------------|
| `TV`             | Advertising budget spent on TV (in thousands of dollars) |
| `Radio`          | Advertising budget spent on Radio (in thousands of dollars) |
| `Newspaper`      | Advertising budget spent on Newspaper (in thousands of dollars) |
| `SocialMedia`    | Advertising budget spent on Social Media (in thousands of dollars) |
| `OnlineAds`      | Advertising budget spent on Online Ads (in thousands of dollars) |
| `Sales`          | Sales generated (in thousands of units) |

Suppose the following data points are provided:

| TV | Radio | Newspaper | SocialMedia | OnlineAds | Sales |
|----|-------|-----------|-------------|-----------|-------|
| 230 | 37   | 69        | 80          | 40        | 22    |
| 44  | 39   | 45        | 15          | 25        | 10    |
| 17  | 45   | 69        | 23          | 14        | 9     |
| 151 | 41   | 58        | 65          | 42        | 18    |
| 180 | 10   | 12        | 40          | 22        | 15    |

### Applying Lasso Regression
Assuming the Lasso Regression model is fitted with (λ = 0.5), the coefficients may look like this:

| Feature          | Coefficient |
|------------------|-------------|
| `TV`             | 0.045       |
| `Radio`          | 0.030       |
| `Newspaper`      | 0           |
| `SocialMedia`    | 0.015       |
| `OnlineAds`      | 0           |

### Interpretation:
- The coefficients for `Newspaper` and `OnlineAds` are zero, meaning these features are not contributing significantly to the prediction of `Sales`.
- The model retains only the most impactful features (`TV`, `Radio`, `SocialMedia`), thus simplifying the model and reducing overfitting.

## Advantages of Lasso Regression
- Performs feature selection automatically.
- Reduces model complexity, enhancing interpretability.
- Helps prevent overfitting by penalizing large coefficients.

## Limitations
- When features are highly correlated, Lasso may arbitrarily choose one and ignore others.
- May struggle with selecting variables correctly in scenarios with high multicollinearity.

---

Lasso Regression is a powerful tool when dealing with high-dimensional data and offers both regularization and feature selection in one go. By understanding how \(\lambda\) affects the coefficients, you can tailor your model to be both effective and interpretable.
