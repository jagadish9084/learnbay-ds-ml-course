# Model Performance and Evaluation

## Contents
1. [Residuals](#residuals)
2. [Mean Squared Error (MSE)](#mean-squared-error-mse)
3. [R-Squared (R²)](#r-squared-r)
4. [Adjusted R-Squared (Adjusted R²)](#adjusted-r-squared-adjusted-r)
5. [Bias and Variance](#bias-and-variance)
6. [Underfitting](#underfitting)
7. [Overfitting](#overfitting)
8. [Noise in Data](#noise-in-data)
9. [P-Values](#p-values)
10. [Variance Inflation Factor (VIF)](#variance-inflation-factor-vif)
11. [Multicollinearity](#multicollinearity)

---

## Residuals

**Definition:**  
Residuals are the differences between the actual values and the values predicted by the model. They represent the error in the model’s predictions.

**Formula:**

\[
\text{Residual}_i = y_i - \hat{y}_i
\]

- **\(y_i\):** Actual value of the target variable.
- **\(\hat{y}_i\):** Predicted value of the target variable.

**Interpretation:**
- **Residuals Plot:** A plot of residuals versus predicted values can help identify patterns such as non-linearity or heteroscedasticity.
- **Normal Distribution of Residuals:** Residuals should be normally distributed around zero. If they are not, it might indicate issues with the model.

**Summary:**  
Residuals help to assess the accuracy of the model by indicating how far off the predictions are from the actual values. Analyzing residuals can provide insights into potential improvements for the model.

---

## Mean Squared Error (MSE)

Mean Squared Error (MSE) is a common metric used to evaluate the performance of regression models. It measures the average squared difference between the actual values and the predicted values.

**Formula:**

\[
\text{MSE} = \frac{1}{n} \sum_{i=1}^n (y_i - \hat{y}_i)^2
\]

- **\(n\):** Number of observations in the dataset.
- **\(y_i\):** Actual value of the target variable.
- **\(\hat{y}_i\):** Predicted value of the target variable.

**How It Works:**
1. **Calculate the Error:** For each observation, find the difference between the actual value and the predicted value (\(y_i - \hat{y}_i\)).
2. **Square the Error:** Square each of these differences to ensure they are positive and to penalize larger errors more heavily.
3. **Average the Squared Errors:** Sum all the squared differences and divide by the number of observations to get the average squared error.

**Interpretation:**
- **Lower MSE:** Indicates that the model’s predictions are closer to the actual values. A lower MSE means better model performance.
- **Higher MSE:** Indicates that there is a greater discrepancy between predicted and actual values, suggesting that the model isn’t performing as well.

**Advantages:**
- **Penalizes Larger Errors:** Because errors are squared, larger discrepancies between predicted and actual values have a bigger impact on MSE. This helps in focusing on improving the model where the predictions are furthest off.

**Disadvantages:**
- **Sensitivity to Outliers:** Since errors are squared, MSE can be disproportionately affected by outliers or extreme values, which might not always be desirable.

**Example:**

Suppose you have the following actual and predicted values for a small dataset:

- **Actual values:** [3, 5, 2.5, 7]
- **Predicted values:** [2.8, 5.2, 2.7, 6.8]

1. **Calculate Errors:**
   - \((3 - 2.8)^2 = 0.04\)
   - \((5 - 5.2)^2 = 0.04\)
   - \((2.5 - 2.7)^2 = 0.04\)
   - \((7 - 6.8)^2 = 0.04\)

2. **Sum of Squared Errors:** \(0.04 + 0.04 + 0.04 + 0.04 = 0.16\)

3. **Mean Squared Error:** \(0.16 / 4 = 0.04\)

In this case, the MSE is 0.04, which indicates the average squared difference between the actual and predicted values.

**Summary:**  
MSE is a key metric for evaluating regression models, helping to quantify the average squared deviation of predictions from actual values. Lower MSE values generally indicate better model performance, though it is important to consider its sensitivity to outliers.

---

## R-Squared (R²)

R-Squared (R²), also known as the coefficient of determination, is a statistical measure that represents the proportion of the variance in the dependent variable that is predictable from the independent variables.

**Formula:**

\[
R^2 = 1 - \frac{\text{SS}_{\text{res}}}{\text{SS}_{\text{tot}}}
\]

- **\(\text{SS}_{\text{res}}\):** Sum of Squares of Residuals (the sum of squared differences between the actual and predicted values).
- **\(\text{SS}_{\text{tot}}\):** Total Sum of Squares (the sum of squared differences between the actual values and their mean).

**Interpretation:**
- **\(R^2 = 1\):** The model explains all the variability in the target variable. Perfect fit.
- **\(R^2 = 0\):** The model does not explain any of the variability in the target variable. The predictions are no better than the mean of the target values.
- **\(R^2 < 0\):** The model performs worse than a model that simply predicts the mean of the target values.

**Summary:**  
R² indicates the proportion of the variance in the dependent variable that is predictable from the independent variables. A higher R² value indicates a better fit of the model to the data.

---

## Adjusted R-Squared (Adjusted R²)

**Definition:**  
Adjusted R-Squared adjusts the R-Squared value to account for the number of predictors in the model. It provides a more accurate measure of model fit when multiple predictors are used.

**Formula:**

\[
\text{Adjusted } R^2 = 1 - \left(\frac{1 - R^2}{n - 1}\right) \times (n - k - 1)
\]

- **\(R^2\):** R-Squared value.
- **\(n\):** Number of observations.
- **\(k\):** Number of predictors.

**Interpretation:**
- **Higher Adjusted R²:** Indicates a better fit of the model when accounting for the number of predictors. It penalizes the addition of irrelevant predictors.
- **Lower Adjusted R²:** May suggest that the model is not capturing the underlying patterns effectively, even when more predictors are added.

**Summary:**  
Adjusted R² provides a more reliable measure of model performance by accounting for the number of predictors. It helps to evaluate whether additional predictors improve the model's explanatory power.

---
## Bias and Variance

   Bias and variance are two sources of error in machine learning models, including linear regression. They help explain the model's performance in terms of overfitting, underfitting, and generalization.

### Bias:

- Bias refers to the error due to overly simplistic assumptions in the learning model. A high bias model may not capture the underlying patterns of the data well
- In linear regression, bias is high when the model is too simple (e.g., missing important variables, not capturing non-linear relationships)

### Variance:

- Variance refers to the error due to the model's sensitivity to small fluctuations in the training data. A high variance model pays too much attention to the noise in the training set, making it less generalizable to unseen data.
- In linear regression, variance increases as the model becomes more complex (e.g., using too many features, overfitting to the training data).

### Bias-Variance Tradeoff in Linear Regression

| **Scenario**      | **Bias**        | **Variance**     | **Model Behavior**  | **Example in Linear Regression**                  |
|-------------------|-----------------|------------------|---------------------|---------------------------------------------------|
| **Overfitting**   | Low Bias        | High Variance    | Model too complex   | Too many predictors or polynomial terms           |
| **Underfitting**  | High Bias       | Low Variance     | Model too simple    | Missing important predictors or relationships     |
| **Generalized**   | Optimal Bias    | Optimal Variance | Good balance        | Right set of predictors, simple but effective     |

---

## Underfitting

**Definition:**  
Underfitting occurs when a model is too simple to capture the underlying patterns in the data. It doesn’t perform well on either the training data or new data.

**Signs:**
- **Low Accuracy:** The model has poor performance on both training and test data.
- **Simple Model:** The model might have too few parameters or a too simplistic form.

**Example:**  
Using a linear model to fit data that has a non-linear relationship.

**Bias-Variance relationship:**  

- High Bias, Low Variance: The model makes strong assumptions, leading to underfitting because it is too simple to capture the actual trends. Both training and test error are high.
- In linear regression: This occurs when not enough predictors are included, or important relationships between variables are not captured.

**How to Address Underfitting:**
- **Increase Model Complexity:** Use a more complex model with more parameters or features.
- **Add More Features:** Include additional relevant features that might capture more of the data’s variability.
- **Decrease Regularization:** If using regularization, reduce its strength to allow the model to fit the training data better.

---

## Overfitting

**Definition:**  
Overfitting occurs when a model is too complex and learns the noise or random fluctuations in the training data rather than the underlying patterns. It performs well on the training data but poorly on new, unseen data.

**Signs:**
- **High Training Accuracy, Low Test Accuracy:** The model performs very well on the training data but poorly on the validation or test data.
- **Complex Model:** The model may have too many parameters, or it might be overly flexible.

**Example:**  
A very complex polynomial regression model that fits the training data perfectly but fails to generalize to new data.

**Bias-Variance relationship:**  

- Low Bias, High Variance: The model captures almost every detail and noise in the training data. This results in very low training error but high test error.
- In linear regression: Overfitting happens when you use too many predictors or the model is too complex, resulting in high variance.
  
**How to Address Overfitting:**
- **Simplify the Model:** Reduce the complexity of the model by using fewer parameters or a simpler algorithm.
- **Use Regularization:** Apply techniques like L1 or L2 regularization to penalize overly complex models.
- **Increase Training Data:** More data can help the model generalize better and reduce the risk of overfitting.
- **Cross-Validation:** Use cross-validation techniques to ensure that the model performs well on different subsets of the data.

**Summary:**
- **Underfitting:** Model is too simple, not capturing the data’s patterns. It performs poorly on both training and test data.
- **Overfitting:** Model is too complex, capturing noise rather than patterns. It performs well on training data but poorly on test data.

The goal is to find a balance where the model is complex enough to capture the underlying patterns but not so complex that it fits the noise in the training data. This balance is often achieved through techniques like cross-validation and careful model selection.

---

## Noise in Data

**Definition:**  
Noise consists of random, unpredictable errors or variations in the data that do not represent real patterns. 

**Impact:**  
- **Obscures True Relationships:** Noise can obscure the true relationship between variables, making it harder for the model to learn meaningful patterns.
- **Overfitting Risk:** If a model learns to fit the noise, it might perform well on the training data but poorly on new data.

**Examples of Noise:**
- **Measurement Errors:** Inaccuracies in measurement tools.
- **Data Entry Errors:** Mistakes made when entering data into a database.
- **Random Fluctuations:** Variations that are not systematic or meaningful.

**How Models Deal with Noise:**
- **Overfitting:** A model that overfits the training data may have learned to capture this noise as if it were a pattern.
- **Generalization:** The goal is to build a model that captures the true underlying patterns and relationships while ignoring the noise.

**Strategies to Mitigate Noise:**
- **Data Cleaning:** Remove or correct errors and inconsistencies.
- **Robust Algorithms:** Use algorithms that are less sensitive to noise.
- **Feature Selection:** Focus on the most relevant features and exclude those more likely to contain noise.
- **Cross-Validation:** Use techniques to assess how well the model generalizes to new data.

**Summary:**  
Noise refers to random errors and variations in the data. Effective modeling involves distinguishing between true patterns and noise, ensuring that the model learns from relevant patterns without being misled by random fluctuations.

---

## P-Values

**Definition:**  
P-values are used to determine the statistical significance of the predictors in the model. They indicate whether the effect observed in the data is likely to be due to chance.

**Interpretation:**
- **Low P-Value (typically < 0.05):** Suggests that the predictor has a significant effect on the target variable.
- **High P-Value:** Suggests that the predictor may not be significantly related to the target variable.

**Summary:**  
P-values help in assessing whether the predictors in the model are statistically significant. Predictors with low p-values are considered significant and are likely contributing to the model.

---

## Variance Inflation Factor (VIF)

**Definition:**  
Variance Inflation Factor (VIF) measures how much the variance of an estimated regression coefficient increases due to multicollinearity.

**Formula:**

\[
\text{VIF}_i = \frac{1}{1 - R_i^2}
\]

- **\(R_i^2\):** R-Squared value of the regression of the \(i\)-th predictor on all other predictors.

**Interpretation:**
- **VIF < 10:** Indicates that multicollinearity is not a severe problem.
- **VIF > 10:** Indicates high multicollinearity, which might be problematic.

**Summary:**  
VIF is used to detect multicollinearity among predictors. High VIF values suggest that a predictor is highly correlated with other predictors, which can affect the stability and interpretation of the model.

---

## Multicollinearity

**Definition:**  
Multicollinearity occurs when two or more predictors in a regression model are highly correlated. This can lead to unreliable estimates of the regression coefficients.

**Detection:**
- **Correlation Matrix:** Check the correlation between predictors. Acceptable threshold is generally below 0.8 for feature correlation.
- **VIF Values:** High VIF values indicate multicollinearity.

**Impact:**
- **Unstable Coefficients:** High multicollinearity can cause large changes in the coefficients with small changes in the model or data.
- **Reduced Interpretability:** Makes it difficult to assess the individual effect of each predictor on the target variable.

**How to Address Multicollinearity:**
- **Remove Highly Correlated Predictors:** Identify and remove predictors with correlation above 0.8.
- **Combine Predictors:** Combine correlated predictors into a single feature.
- **Regularization:** Use techniques like L1 regularization (Lasso) to penalize and potentially eliminate redundant predictors.

**Summary:**  
Multicollinearity can affect the reliability and interpretability of a regression model. Detecting and addressing multicollinearity is essential for building stable and interpretable models.

