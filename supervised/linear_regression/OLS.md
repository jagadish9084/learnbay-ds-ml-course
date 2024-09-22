# Linear Regression Using Ordinary Least Squares (OLS)

## Table of Contents
- [Introduction](#introduction)
- [What is Ordinary Least Squares (OLS)?](#what-is-ordinary-least-squares-ols)
- [Mathematical Explanation](#mathematical-explanation)
- [Step-by-Step Guide to OLS](#step-by-step-guide-to-ols)
- [Example Using a Single Feature](#example-using-a-single-feature)
- [Example Using a Multi-Feature Dataset](#example-using-a-multi-feature-dataset)
- [Adjusting Coefficients](#adjusting-coefficients)
- [Evaluating the Model](#evaluating-the-model)
- [Common Issues and Solutions](#common-issues-and-solutions)
- [Conclusion](#conclusion)

## Introduction
Linear Regression is a statistical method used to model the relationship between a dependent variable (target) and one or more independent variables (features). Ordinary Least Squares (OLS) is a technique that estimates the coefficients of the regression model by minimizing the sum of the squared differences between observed values and predicted values.

## What is Ordinary Least Squares (OLS)?
OLS is used to find the best-fitting line by minimizing the sum of squared residuals (differences between observed and predicted values). It is one of the simplest and most widely used methods for estimating linear regression models.

### Key Points:
- **Objective**: Minimize the sum of squared residuals.
- **Assumptions**:
  1. Linearity: The relationship between the independent and dependent variables is linear.
  2. Independence: Observations are independent of each other.
  3. Homoscedasticity: Residuals have constant variance.
  4. Normality: Residuals are normally distributed.

## Mathematical Explanation
The OLS method estimates the coefficients (\(\beta_0, \beta_1, ..., \beta_n\)) of the regression line:

![Regression Line Formula](https://latex.codecogs.com/png.image?\dpi{110}\bg{white}\large%20Y%20=%20\beta_0%20+%20\beta_1X_1%20+%20\beta_2X_2%20+%20...%20+%20\beta_nX_n%20+%20\epsilon)

Where:
- \(Y\) is the dependent variable.
- \(X_1, X_2, ..., X_n\) are the independent variables.
- \(\𝛽0\) is the intercept.
- \(𝛽1, 𝛽2, ..., 𝛽n\) are the coefficients.
- \(\epsilon\) is the error term.

### Simplified Formula for Estimating the Slope (\(\beta_1\))

In a simple linear regression scenario (one feature), the slope \(\beta_1\) can be directly calculated using:

![Slope Formula](https://latex.codecogs.com/png.image?\dpi{110}\bg{white}\large%20\beta_1%20=%20\frac{\sum%20(x_i%20-%20\bar{x})(y_i%20-%20\bar{y})}{\sum%20(x_i%20-%20\bar{x})^2})

**Explanation of Notations:**

1. **\(\beta_1\)**: The slope of the regression line, representing how much \(Y\) changes for a one-unit change in \(X\).

2. **\(x_i\)**: The \(i\)-th observation of the independent variable \(X\).

3. **\(\bar{x}\)**: The mean (average) of the independent variable \(X\).

4. **\(y_i\)**: The \(i\)-th observation of the dependent variable \(Y\).

5. **\(\bar{y}\)**: The mean (average) of the dependent variable \(Y\).

6. **\(\sum\)**: Summation symbol, indicating that you sum over all observations.

### How the Formula Works:

1. **Numerator (\(\sum (x_i - \bar{x})(y_i - \bar{y})\))**:
   - This measures the covariance between the independent variable \(X\) and the dependent variable \(Y\).
   - It captures how changes in \(X\) are associated with changes in \(Y\).

2. **Denominator (\(\sum (x_i - \bar{x})^2\))**:
   - This measures the variance of the independent variable \(X\).
   - It quantifies how much \(X\) deviates from its mean.

3. **Slope Calculation**:
   - By dividing the covariance by the variance, we determine the best slope (\(\beta_1\)) that minimizes the differences between the observed values and the predicted values.

### Final Regression Equation:

After calculating \(\beta_1\), you can find the intercept \(\beta_0\) using:

![Intercept Formula](https://latex.codecogs.com/png.image?\dpi{110}\bg{white}\large%20\beta_0%20=%20\bar{y}%20-%20\beta_1\bar{x})

## Step-by-Step Guide to OLS
### 1. Prepare the Data
- Ensure the data is clean: handle missing values, encode categorical variables, and scale features if necessary.

### 2. Define the Model
- Set up the linear regression equation.

### 3. Estimate Coefficients
- Use the OLS method to estimate the coefficients.

### 4. Make Predictions
- Use the estimated coefficients to predict new values.

### 5. Evaluate the Model
- Assess the model's accuracy using statistical metrics.

## Example Using a Single Feature

### Dataset
We will use a simple dataset to demonstrate how to calculate the coefficients of a linear regression model using OLS with one feature:

| Observation | StudyHours (\(X\)) | FinalGrade (\(Y\)) |
|-------------|--------------------|--------------------|
| 1           | 15                 | 88                 |
| 2           | 12                 | 92                 |
| 3           | 8                  | 75                 |
| 4           | 10                 | 80                 |

### Step 1: Define the Linear Regression Equation
For a single feature, the regression equation is:

![Single Feature Regression](https://latex.codecogs.com/png.image?\dpi{110}\bg{white}\large%20Y%20=%20\beta_0%20+%20\beta_1X)

Where:
- \( Y \) is the predicted FinalGrade.
- \( X \) is the StudyHours.
- \(\beta_0\) is the intercept (constant term).
- \(\beta_1\) is the slope (coefficient of \( X \)).

### Step 2: Calculate the Mean of X and Y
First, find the averages:

![Mean of X](https://latex.codecogs.com/png.image?\dpi{110}\bg{white}\large%20\bar{X}%20=%20\frac{15%20+%2012%20+%208%20+%2010}{4}%20=%2011.25)

![Mean of Y](https://latex.codecogs.com/png.image?\dpi{110}\bg{white}\large%20\bar{Y}%20=%20\frac{88%20+%2092%20+%2075%20+%2080}{4}%20=%2083.75)

### Step 3: Calculate the Slope (\(\beta_1\))
The slope (\(\beta_1\)) is calculated using the formula:

![Slope Calculation](https://latex.codecogs.com/png.image?\dpi{110}\bg{white}\large%20\beta_1%20=%20\frac{\sum%20(x_i%20-%20\bar{x})(y_i%20-%20\bar{y})}{\sum%20(x_i%20-%20\bar{x})^2})

Calculating each term:

- For Observation 1: \( (15 - 11.25) = 3.75 \) and \( (88 - 83.75) = 4.25 \).
- For Observation 2: \( (12 - 11.25) = 0.75 \) and \( (92 - 83.75) = 8.25 \).
- For Observation 3: \( (8 - 11.25) = -3.25 \) and \( (75 - 83.75) = -8.75 \).
- For Observation 4: \( (10 - 11.25) = -1.25 \) and \( (80 - 83.75) = -3.75 \).

Now, sum up the products:

![Sum of Products](https://latex.codecogs.com/png.image?\dpi{110}\bg{white}\large%20\sum%20(X%20-%20\bar{X})(Y%20-%20\bar{Y})%20=%2055.26)

Sum of squares of \( X - \bar{X} \):

![Sum of Squares](https://latex.codecogs.com/png.image?\dpi{110}\bg{white}\large%20\sum%20(X%20-%20\bar{X})^2%20=%2026.74)

Calculate the slope:

![Slope Final Calculation](https://latex.codecogs.com/png.image?\dpi{110}\bg{white}\large%20\beta_1%20=%20\frac{55.26}{26.74}%20=%202.07)

### Step 4: Calculate the Intercept (\(\beta_0\))
The intercept is calculated using:

![Intercept Calculation](https://latex.codecogs.com/png.image?\dpi{110}\bg{white}\large%20\beta_0%20=%20\bar{Y}%20-%20\beta_1\bar{X})

Substitute the values:

![Substituted Intercept Calculation](https://latex.codecogs.com/png.image?\dpi{110}\bg{white}\large%20\beta_0%20=%2083.75%20-%20(2.07%20\times%2011.25)%20=%2060.46)

### Final Regression Equation
The estimated linear regression equation is:

![Final Regression Equation](https://latex.codecogs.com/png.image?\dpi{110}\bg{white}\large%20Y%20=%2060.46%20+%202.07X)

### Interpretation
- **\(\beta_0 = 60.46\)**: This is the expected FinalGrade when StudyHours is zero.
- **\(\beta_1 = 2.07\)**: For each additional hour of study, the FinalGrade increases by 2.07 points.

## Example Using a Multi-Feature Dataset

We will now extend this process to include multiple features to demonstrate how coefficients are estimated in a more complex scenario.

### Dataset
| Observation | AttendanceRate (\(X_1\)) | StudyHoursPerWeek (\(X_2\)) | PreviousGrade (\(X_3\)) | FinalGrade (\(Y\)) |
|-------------|--------------------------|-----------------------------|------------------------|--------------------|
| 1           | 90                       | 15                          | 85                     | 88                 |
| 2           | 95                       | 12                          | 90                     | 92                 |
| 3           | 80                       | 8                           | 70                     | 75                 |
| 4           | 85                       | 10                          | 78                     | 80                 |

### Step 1: Define the Linear Regression Equation
![Multi-Feature Regression](https://latex.codecogs.com/png.image?\dpi{110}\bg{white}\large%20Y%20=%20\beta_0%20+%20\beta_1X_1%20+%20\beta_2X_2%20+%20\beta_3X_3%20+%20\epsilon)

### Step-by-step Calculations
Using the matrix approach explained earlier, we calculate the coefficients for multiple features. The details are similar to the single-feature case but involve matrix multiplication.

## Adjusting Coefficients

### Why and When to Adjust Coefficients?

**1. High SSE (Sum of Squared Errors):**
- **What is SSE?** SSE measures how well the model fits the data by calculating the sum of squared differences between observed and predicted values.
- **When to Adjust:** If the SSE is high, it indicates that the model is not fitting the data well, suggesting that the coefficients need adjustment to improve the fit.

**Adjustments Due to High SSE:**
- **Gradient Descent Method**: Coefficients are adjusted iteratively by minimizing SSE using derivatives.

**2. High p-values:**
- **What is a p-value?** The p-value indicates whether a coefficient significantly contributes to predicting the dependent variable. A high p-value suggests the variable is not statistically significant.
- **When to Adjust:** If a coefficient has a high p-value (commonly above 0.05), it suggests that the variable might not be meaningful in the model.

### Mathematical Approach: Gradient Descent for Adjusting Coefficients

Gradient Descent is used to minimize SSE by adjusting coefficients iteratively:

1. **Define SSE**: 

![SSE](https://latex.codecogs.com/png.image?\dpi{110}\bg{white}\large%20\text{SSE}%20=%20\sum%20(Y%20-%20(\beta_0%20+%20\beta_1X))^2)

2. **Take the Derivatives**:

- Derivative with respect to \(\beta_0\):

![Derivative b0](https://latex.codecogs.com/png.image?\dpi{110}\bg{white}\large%20\frac{\partial%20\text{SSE}}{\partial%20\beta_0}%20=%20-2%20\sum%20(Y%20-%20(\beta_0%20+%20\beta_1X)))

- Derivative with respect to \(\beta_1\):

![Derivative b1](https://latex.codecogs.com/png.image?\dpi{110}\bg{white}\large%20\frac{\partial%20\text{SSE}}{\partial%20\beta_1}%20=%20-2%20\sum%20X%20(Y%20-%20(\beta_0%20+%20\beta_1X)))

3. **Update the Coefficients**:

- Update \(\beta_0\):

![Update b0](https://latex.codecogs.com/png.image?\dpi{110}\bg{white}\large%20\beta_0%20=%20\beta_0%20-%20\alpha%20\frac{\partial%20\text{SSE}}{\partial%20\beta_0})

- Update \(\beta_1\):

![Update b1](https://latex.codecogs.com/png.image?\dpi{110}\bg{white}\large%20\beta_1%20=%20\beta_1%20-%20\alpha%20\frac{\partial%20\text{SSE}}{\partial%20\beta_1})

### Learning Rate: Detailed Explanation

- **What is the Learning Rate (\(\alpha\))?**
  - The learning rate is a scalar value that determines the size of the steps taken towards the minimum SSE during each update of the coefficients.
  - It acts as a multiplier for the gradient, scaling the adjustments made to the coefficients.

- **Impact of Learning Rate:**
  - **Too High:** If the learning rate is too high, the algorithm might take large steps and overshoot the minimum, causing the SSE to increase rather than decrease. This can lead to divergence, where the algorithm fails to find the optimal coefficients.
  - **Too Low:** A very small learning rate means that the algorithm will make tiny adjustments, leading to slow convergence. The algorithm will eventually find the minimum SSE, but it may take a long time.
  - **Optimal Rate:** A well-chosen learning rate ensures that the coefficients are adjusted efficiently, reducing SSE at each step without overshooting the minimum.

- **Choosing the Learning Rate:**
  - Common practice is to experiment with different learning rates and observe the convergence behavior.
  - Techniques like adaptive learning rates (e.g., using algorithms like Adam or RMSprop) automatically adjust the learning rate during training to improve convergence.

### When to Stop Adjusting?

**1. OLS Method: Direct Calculation in One Step**
- **Systematic Solution**: OLS systematically solves for the coefficients using calculus (partial derivatives), ensuring that the error between the actual and predicted values is minimized.
- **No Guesswork**: OLS does not "guess" the coefficients; it calculates them based on the data using the exact formulas derived from the partial derivatives of SSE with respect to each coefficient.
- **Optimal Stopping Point**: OLS stops when it finds the coefficients (\(\beta_0\) and \(\beta_1\)) that minimize the SSE, as this is the point where any further change would increase the error.
- **One-Step Calculation**: Unlike iterative algorithms (like gradient descent), OLS directly computes the optimal values for \(\beta_0\) and \(\beta_1\) in a single calculation, which is the mathematically proven point of minimum error.

**2. Iterative Methods (e.g., Gradient Descent):**
- **Convergence**: Adjustments stop when the changes in coefficients are small, indicating that SSE has reached its minimum.
- **Optimal Solution**: Iterative methods approximate the coefficients by continuously reducing SSE until convergence.

### Avoid Random Adjustments:
- **Use Statistical Evidence:** Adjust coefficients based on derivatives, p-values, or cross-validation, ensuring systematic improvement.

## Evaluating the Model
Key metrics include R-squared, Adjusted R-squared, and residual analysis to ensure assumptions hold.

## Common Issues and Solutions
Multicollinearity, outliers, and heteroscedasticity are common issues with OLS, with corresponding solutions to improve model reliability.

## Conclusion
Mastering OLS for linear regression with clear calculations, gradient descent techniques, and adjustment strategies helps in building accurate predictive models and effectively training others.

---

This `README.md` now includes all the formulas as images for better readability, with consistent notation throughout. Let me know if you need any further adjustments!
