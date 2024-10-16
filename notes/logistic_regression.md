# Logistic Regression

Logistic Regression is a supervised learning algorithm used for **classification** problems, particularly when the target variable is binary (e.g., 0 or 1, yes or no). It predicts the probability that an instance belongs to a particular class based on the input features. Below is an in-depth explanation of Logistic Regression, its key components, and evaluation metrics.

---

## 1. Logistic Function (Sigmoid Function)

The **sigmoid function** is the core of logistic regression. It transforms any real-valued number into a range between 0 and 1, representing probabilities.

### Mathematical Definition:

$$
\sigma(z) = \frac{1}{1 + e^{-z}}
$$

Where:
- z = θ<sup>T</sup>x, the linear combination of the input features.
- \( e \) is Euler's number, approximately 2.718.

### Why use the sigmoid function?
It helps in mapping the output to probabilities:
- A value closer to 0 represents class 0.
- A value closer to 1 represents class 1.

### Example:

Consider the problem of predicting whether a student passes or fails based on their study hours. If \( z = 0.8 \) (calculated from input features), then:

$$
P(\text{Pass}) = \frac{1}{1 + e^{-0.8}} \approx 0.69
$$

This means the model predicts a 69% probability that the student will pass.

---

## 2. Logistic Regression Model

The logistic regression model predicts probabilities using the sigmoid function. It uses a **linear combination** of input features, followed by the logistic transformation.

### Model Hypothesis:

$$
h_\theta(x) = \sigma(\theta^T x) = \frac{1}{1 + e^{-\theta^T x}}
$$

Where:
- &theta; represents the model parameters (weights and intercept).
- \( x \) is the vector of features.

### Example Dataset:

| Hours Studied | Attendance Rate | Pass (Y/N) |
|---------------|-----------------|------------|
| 5             | 80%             | Yes        |
| 3             | 50%             | No         |
| 10            | 90%             | Yes        |
| 2             | 40%             | No         |

Here, the target variable "Pass" is binary: Yes (1) or No (0). The model will use hours studied and attendance rate to predict the probability of a student passing.

### Linear Combination:

Suppose we have two features (Hours Studied and Attendance Rate), and our initial model coefficients are:
\[
θ<sub>0</sub> = -4, θ<sub>1</sub> = 0.3, θ<sub>2</sub> = 2
\]

For a student who studied 5 hours and had an 80% attendance rate, the linear combination would be:

$$
z = \theta_0 + \theta_1 \times \text{Hours} + \theta_2 \times \text{Attendance Rate}
$$

$$
z = -4 + (0.3 \times 5) + (2 \times 0.8) = -4 + 1.5 + 1.6 = -0.9
$$

Now, applying the sigmoid function:

$$
P(\text{Pass}) = \frac{1}{1 + e^{0.9}} \approx 0.29
$$

Thus, the model predicts a 29% probability that the student will pass.

---

## 3. Cost Function

In Logistic Regression, we use the **Log-Loss** (or **Cross-Entropy Loss**) to measure the error between the predicted probabilities and the actual class labels. The cost function aims to minimize this error.

### Cost Function Definition:

$$
J(\theta) = -\frac{1}{m} \sum_{i=1}^{m} \left[ y^{(i)} \log(h_\theta(x^{(i)})) + (1 - y^{(i)}) \log(1 - h_\theta(x^{(i)})) \right]
$$

Where:
- \( m \) is the number of training examples.
- y<sup>(i)</sup> is the actual label (0 or 1).
- h<sub>θ</sub>(x<sup>(i)</sup>) is the predicted probability for the i-th example.

### Explanation:
- For a true positive (y = 1), the cost is high if the predicted probability is close to 0.
- For a true negative (y = 0), the cost is high if the predicted probability is close to 1.

---

## 4. Optimization: Gradient Descent

Logistic Regression uses **Gradient Descent** to minimize the cost function by updating the model’s coefficients. The update rule is:

$$
\theta_j := \theta_j - \alpha \frac{\partial}{\partial \theta_j} J(\theta)
$$

Where:
- &alpha; is the learning rate (step size).
- (∂/∂θ<sub>j</sub>) J(θ) is the partial derivative of the cost function with respect to θ<sub>j</sub>.

This process is repeated iteratively until the model converges (i.e., the cost function stops decreasing).

### Example:
If the initial value of θ<sub>1</sub> = 0.3 and the gradient of the cost function is `0.02`, then with a learning rate &alpha; = 0.1, the update would be:

$$
\theta_1 := 0.3 - 0.1 \times 0.02 = 0.298
$$

---

## 5. Decision Boundary

Logistic Regression predicts probabilities, but we need a threshold to assign class labels (0 or 1). Typically, the threshold is set to 0.5.

### Decision Rule:
- If P(Class = 1) &ge; 0.5, predict class 1 (e.g., Pass).
- If P(Class = 1) < 0.5, predict class 0 (e.g., Fail).

### Example:
For the earlier student with a predicted probability of 29% (0.29), we classify them as "Fail" since 0.29 < 0.5.

---

## 6. Evaluation Metrics

Evaluating a logistic regression model requires various classification metrics. These metrics help us assess how well the model performs, especially in binary classification problems. Below are the commonly used metrics:

### 6.1 Accuracy

#### Definition:
Accuracy is the ratio of correctly predicted observations to the total observations. It tells us how often the model is correct overall.

$$
\text{Accuracy} = \frac{\text{True Positives} + \text{True Negatives}}{\text{Total Observations}}
$$

#### When to Use:
- **Use accuracy when the classes are balanced** (i.e., the number of positives and negatives is roughly equal).
- In a balanced dataset, accuracy gives a good overall sense of model performance.

#### Example:
If we have 100 test examples, and the model correctly predicts 90 of them (60 true positives and 30 true negatives), then the accuracy would be:

$$
\text{Accuracy} = \frac{60 + 30}{100} = 0.90 = 90\%
$$

### 6.2 Precision

#### Definition:
Precision measures the proportion of true positive predictions out of all positive predictions made by the model. It answers the question: **Out of all predicted positives, how many were actually positive?**

$$
\text{Precision} = \frac{\text{True Positives}}{\text{True Positives} + \text{False Positives}}
$$

#### When to Use:
- **Use precision when the cost of false positives is high**, i.e., when you want to be very sure that positive predictions are correct.
- This metric is particularly useful in **fraud detection**, **spam email detection**, or **medical diagnoses**, where a false positive could have serious consequences.

#### Example:
If the model predicts 50 cases as positive, but only 40 are actually positive, and 10 are false positives, the precision would be:

$$
\text{Precision} = \frac{40}{40 + 10} = \frac{40}{50} = 0.80 = 80\%
$$

### 6.3 Recall (Sensitivity or True Positive Rate)

#### Definition:
Recall measures the proportion of actual positives that are correctly identified. It answers the question: **Out of all actual positives, how many were correctly predicted?**

$$
\text{Recall} = \frac{\text{True Positives}}{\text{True Positives} + \text{False Negatives}}
$$

#### When to Use:
- **Use recall when the cost of false negatives is high**, i.e., when it’s crucial to catch as many positives as possible.
- This metric is useful in **medical diagnoses** (e.g., detecting diseases), **search and rescue operations**, or **credit card fraud detection**, where missing a positive case can have serious consequences.

#### Example:
If there are 50 actual positive cases, and the model correctly predicts 45 of them (5 false negatives), the recall would be:

$$
\text{Recall} = \frac{45}{45 + 5} = \frac{45}{50} = 0.90 = 90\%
$$

### 6.4 F1 Score

#### Definition:
The **F1 Score** is the harmonic mean of precision and recall. It provides a single measure that balances both precision and recall, especially useful when you want to balance the trade-off between false positives and false negatives.

$$
F1 = 2 \times \frac{\text{Precision} \times \text{Recall}}{\text{Precision} + \text{Recall}}
$$

#### When to Use:
- **Use F1 Score when you need a balance between precision and recall**. This is especially important in cases where the class distribution is imbalanced, and both false positives and false negatives matter.
- The F1 Score is useful in scenarios like **information retrieval** (e.g., search engines) and **natural language processing tasks** (e.g., text classification).

#### Example:
If precision is 80% and recall is 90%, the F1 score would be:

$$
F1 = 2 \times \frac{0.80 \times 0.90}{0.80 + 0.90} = 2 \times \frac{0.72}{1.7} \approx 0.847 = 84.7\%
$$

### 6.5 F-Beta Score

#### Definition:
The **F-Beta Score** is a generalized version of the F1 Score. It allows you to adjust the balance between precision and recall by using a parameter \( \beta \) that weighs recall more heavily when &beta; > 1, or precision more heavily when &beta; < 1.

$$
F_\beta = (1 + \beta^2) \times \frac{\text{Precision} \times \text{Recall}}{(\beta^2 \times \text{Precision}) + \text{Recall}}
$$

#### Explanation:
- **\( \beta = 1 \)** results in the F1 Score, where precision and recall are equally weighted.
- **\( \beta > 1 \)** gives more weight to recall, which is useful when false negatives are more costly.
- **\( \beta < 1 \)** gives more weight to precision, which is useful when false positives are more costly.

#### When to Use:
- **Use F-Beta Score when you need to prioritize either precision or recall more than the other**, depending on the specific problem. For example:
  - **High Recall Priority (&beta; > 1)**: In medical diagnoses, missing a disease (false negative) could have severe consequences, so higher recall is important.
  - **High Precision Priority (&beta; < 1)**: In fraud detection, labeling legitimate transactions as fraud (false positives) can cause user dissatisfaction, so higher precision is crucial.

#### Example:
If you care more about recall and set \( &beta; = 2 \), and if precision is 80% and recall is 90%, the F2 score would be:

$$
F_2 = (1 + 2^2) \times \frac{0.80 \times 0.90}{(2^2 \times 0.80) + 0.90} = 5 \times \frac{0.72}{3.2 + 0.90} = 5 \times \frac{0.72}{4.1} \approx 0.88
$$

### 6.6 ROC Curve (Receiver Operating Characteristic)

#### Definition:
The **ROC curve** is a graphical representation of a model’s performance across different classification thresholds. It plots the **True Positive Rate** (Recall) against the **False Positive Rate** (FPR):

$$
\text{False Positive Rate} = \frac{\text{False Positives}}{\text{False Positives} + \text{True Negatives}}
$$

#### When to Use:
- **Use the ROC curve when you need to evaluate the model’s performance at different classification thresholds**. It’s especially useful for binary classification problems where the output is a probability.
- The ROC curve is commonly used in **medical decision-making**, **binary classification**, and **credit scoring**.

#### Interpreting ROC:
- A perfect model would have a ROC curve that passes through the top-left corner (TPR = 1, FPR = 0).
- The area under the ROC curve (**AUC-ROC**) gives an overall measure of the model’s ability to distinguish between classes. **AUC** values closer to 1 indicate better performance.

### 6.7 AUC (Area Under the Curve)

#### Definition:
The **AUC (Area Under the ROC Curve)** is a single scalar value representing the model’s performance across all possible classification thresholds. It ranges from 0 to 1.

- **AUC = 1**: Perfect model.
- **AUC = 0.5**: The model is as good as random guessing.
- **AUC < 0.5**: The model performs worse than random guessing.

#### When to Use:
- **Use AUC when you want a single metric to represent the performance of a model across all thresholds**. This is especially useful when you don’t know which threshold to choose.
- It’s often used in **medical diagnostics** and **binary classification problems**.

#### Example:
If a model’s AUC is 0.85, it means that there’s an 85% chance that the model will correctly distinguish between a positive class and a negative class.

---

## 7. Regularization in Logistic Regression

Regularization helps prevent **overfitting** by penalizing large coefficients. Two common forms of regularization are:

### L2 Regularization (Ridge):
Adds a penalty proportional to the square of the coefficients.

$$
J(\theta) = -\frac{1}{m} \sum \text{Log-Loss} + \frac{\lambda}{2m} \sum_{j=1}^{n} \theta_j^2
$$

### L1 Regularization (Lasso):
Adds a penalty proportional to the absolute value of the coefficients.

$$
J(\theta) = -\frac{1}{m} \sum \text{Log-Loss} + \frac{\lambda}{m} \sum_{j=1}^{n} |\theta_j|
$$

---

## 8. Multiclass Classification

Logistic regression can be extended to multiclass classification using methods like:

- **One-vs-Rest (OvR)**: Train multiple binary classifiers, one for each class.
- **Softmax Regression**: Generalizes logistic regression to multiple classes using the softmax function.

---

## 9. Assumptions of Logistic Regression

- **Linearity**: Logistic regression assumes a linear relationship between the independent variables and the log-odds.
- **Independence**: Observations should be independent of each other.
- **No Multicollinearity**: Independent variables should not be highly correlated.

---

## 10. Applications of Logistic Regression

- **Medical Diagnosis**: Predicting disease presence.
- **Fraud Detection**: Identifying fraudulent transactions.
- **Email Classification**: Predicting whether an email is spam or not.
- **Customer Retention**: Predicting customer churn.

---

## 11. Selecting the Right Metric

Choosing the right metric depends on the problem you're solving and the importance of different types of errors.

### 1. If the classes are balanced and all errors are equally important:
- **Use Accuracy**: It gives a good overall measure of performance.

### 2. If you want to reduce false positives:
- **Use Precision**: Especially useful in problems like **email spam detection** or **fraud detection**, where false positives are costly (e.g., labeling a legitimate email as spam).

### 3. If you want to reduce false negatives:
- **Use Recall**: Ideal for problems where missing a positive instance is costly (e.g., **disease detection**, **fraud detection** in financial systems, **search and rescue**).

### 4. If you need to balance precision and recall:
- **Use F1 Score**: This is useful when you care about both false positives and false negatives, especially in imbalanced datasets (e.g., **information retrieval**, **text classification**).

### 5. If you want to prioritize either precision or recall more:
- **Use F-Beta Score**: Choose \( \beta > 1 \) if recall is more important, and \( \beta < 1 \) if precision is more important.
