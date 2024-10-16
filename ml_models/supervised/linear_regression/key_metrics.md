# Key Error Metrics: MSE, MAE, RMSE

In machine learning, error metrics like MSE, MAE, and RMSE are essential for evaluating model performance by quantifying prediction errors. Here’s a breakdown:

## 1. Mean Squared Error (MSE)

**MSE** measures the average squared difference between actual and predicted values, commonly used for optimization.

### Formula:
\[
\text{MSE} = \frac{1}{n} \sum (y_i - \hat{y_i})^2
\]

### Advantages:
- **Fast convergence**: MSE often leads to quicker model optimization due to its smooth, differentiable nature.
- **Differentiable at all points**: This property makes it easier for optimization algorithms like gradient descent to minimize the error.

### Disadvantages:
- **Highly sensitive to outliers**: Squaring the errors amplifies large differences, pulling the model's predictions toward outliers, which distorts results.
- **Units mismatch**: The error is in squared units of the target variable, making interpretation less intuitive.

---

## 2. Mean Absolute Error (MAE)

**MAE** calculates the average absolute difference between actual and predicted values. It is robust to outliers, unlike MSE.

### Formula:
\[
\text{MAE} = \frac{1}{n} \sum |y_i - \hat{y_i}|
\]

### Advantages:
- **Robust to outliers**: Unlike MSE, MAE doesn’t square the errors, reducing the impact of outliers.
- **Easy interpretation**: The error remains in the same unit as the target variable, making it simple to interpret.

### Disadvantages:
- **Slower convergence**: Since MAE is not differentiable at zero, optimization algorithms may take longer to converge.
- **Complex optimization**: The absolute value function complicates the optimization process, leading to increased computational cost.

---

## 3. Root Mean Squared Error (RMSE)

**RMSE** is the square root of MSE, bringing the error back to the same units as the target variable while retaining the properties of MSE.

### Formula:
\[
\text{RMSE} = \sqrt{\frac{1}{n} \sum (y_i - \hat{y_i})^2}
\]

### Advantages:
- **Same units**: Like MAE, the error is in the same units as the target variable, making it more interpretable than MSE.

### Disadvantages:
- **Sensitive to outliers**: Since RMSE is derived from MSE, it shares MSE’s sensitivity to large errors.

---

## Choosing the Right Metric

- **Use MSE** if you prioritize faster optimization and can tolerate outliers.
- **Use MAE** when you want to minimize the effect of outliers and require easier error interpretation.
- **Use RMSE** for balanced measurement when you want the error in the same unit but also benefit from the properties of MSE.

---

## What Does "Differentiable" Mean?

A function is **differentiable** if you can compute its slope (derivative) at every point. In machine learning, this property is essential for optimization algorithms, which adjust model parameters by calculating the gradient (slope) of the error function to minimize the error.
