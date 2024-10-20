# Decision Tree: Comprehensive Notes

## 1. Overview

A Decision Tree is a **supervised learning algorithm** used for both classification and regression tasks. It splits the dataset into smaller subsets based on features to make predictions. The goal is to identify splits that result in the purest possible subsets, where each subset contains similar data points.

## 2. Types of Decision Trees

### ID3 (Iterative Dichotomiser 3)
- Allows **multiple splits** at each node (a feature can have more than two categories).
- Uses **Entropy** and **Information Gain** to decide splits.

### CART (Classification and Regression Trees)
- Only allows **binary splits** (each node splits into two parts).
- Uses **GINI Index** for classification and **Variance Reduction** for regression.

## 3. Purity and Splitting Criteria

### 3.1. Purity
A split is **pure** if all the data points in a node belong to the same class. The quality of a split is determined by how **pure** the resulting subsets are.

### 3.2. Feature Selection for Splitting
For each split, we need to decide which feature provides the **most informative** split. The quality of a split is measured using:
- **Entropy** (for classification).
- **GINI Index** (for classification).
- **Variance Reduction** (for regression).

## 4. Entropy and GINI Index: Detailed Examples

### 4.1. Entropy (for classification)

**Entropy** measures the amount of disorder or uncertainty in the dataset. A split with **lower entropy** means the data is more pure after the split.

#### Formula for Entropy:
\[
\text{Entropy}(S) = - \sum_{i=1}^{c} p_i \log_2(p_i)
\]
Where:
- \( p_i \) is the proportion of samples belonging to class \( i \).
- \( c \) is the total number of classes.

#### Example Calculation:

Let's use this dataset with the target variable **Buys_Computer** (Yes/No):

| **Buys_Computer** | **Count** |
|-------------------|-----------|
| Yes               | 9         |
| No                | 5         |

- Total samples \( S = 14 \).
- Probability of "Yes" \( p_{\text{Yes}} = \frac{9}{14} = 0.642 \).
- Probability of "No" \( p_{\text{No}} = \frac{5}{14} = 0.357 \).

Now, plug these values into the entropy formula:
\[
H(S) = - \left( 0.642 \log_2(0.642) + 0.357 \log_2(0.357) \right)
\]
\[
H(S) = - \left( 0.642 \times (-0.644) + 0.357 \times (-1.485) \right)
\]
\[
H(S) = 0.413 + 0.530 = 0.943
\]
- **Entropy of the dataset = 0.943**.

#### Interpretation:
- Entropy \( 0 \) means the node is pure (contains only one class).
- Entropy \( 1 \) means the node is impure (50-50 split between classes).

### 4.2. GINI Index (for classification)

The **GINI Index** measures the probability of misclassifying a randomly chosen sample. A lower GINI index indicates a purer node.

#### Formula for GINI Index:
\[
\text{Gini}(S) = 1 - \sum_{i=1}^{n} p_i^2
\]
Where:
- \( p_i \) is the proportion of samples in class \( i \).

#### Example Calculation:

We will use the same dataset:

| **Buys_Computer** | **Count** |
|-------------------|-----------|
| Yes               | 9         |
| No                | 5         |

- Probability of "Yes" \( p_{\text{Yes}} = \frac{9}{14} = 0.642 \).
- Probability of "No" \( p_{\text{No}} = \frac{5}{14} = 0.357 \).

Now, calculate the GINI Index:
\[
\text{Gini}(S) = 1 - \left( 0.642^2 + 0.357^2 \right)
\]
\[
\text{Gini}(S) = 1 - \left( 0.412 + 0.127 \right) = 1 - 0.539 = 0.461
\]
- **GINI Index = 0.461**.

#### Interpretation:
- GINI \( 0 \) means the node is pure.
- GINI \( 0.5 \) means the node is impure (for binary classification).

### 4.3. Entropy vs. GINI Index

| **Entropy**                      | **GINI Index**                  |
|----------------------------------|----------------------------------|
| More sensitive to data changes.  | Computationally simpler.         |
| Uses logarithms, making it more sensitive to small changes. | Works faster in larger datasets. |
| Preferred for smaller datasets.  | Preferred for larger datasets.   |

### **Entropy and GINI help us to check the impurity so that we can decide if further split is needed, while Information Gain will help us to select the feature for splitting.**

## 5. Information Gain

**Information Gain** measures how much the entropy decreases after a split. The feature with the **highest Information Gain** is chosen as the splitting feature.

#### Formula for Information Gain:
\[
\text{Gain}(S, f) = H(S) - \sum_{v} \left( \frac{|S_v|}{|S|} \cdot H(S_v) \right)
\]
Where:
- \( H(S) \) is the entropy of the parent node.
- \( |S_v| \) is the number of samples in the child node \( v \).
- \( H(S_v) \) is the entropy of child node \( v \).

### Example Calculation:

Let’s calculate **Information Gain** for the feature **Income** using the following data:

| **Income**  | **Buys_Computer = Yes** | **Buys_Computer = No** |
|-------------|-------------------------|------------------------|
| High        | 2                       | 3                      |
| Medium      | 4                       | 2                      |
| Low         | 3                       | 0                      |

We previously calculated the **Entropy of the root node** \( H(S) = 0.943 \).

#### Step 1: Calculate Entropy for Each Split

- **For Income = High:**
  - \( p_{\text{Yes}} = \frac{2}{5} \), \( p_{\text{No}} = \frac{3}{5} \).
  - \( H(\text{High}) = - \left( 0.4 \log_2 0.4 + 0.6 \log_2 0.6 \right) = 0.971 \).

- **For Income = Medium:**
  - \( p_{\text{Yes}} = \frac{4}{6} \), \( p_{\text{No}} = \frac{2}{6} \).
  - \( H(\text{Medium}) = - \left( 0.666 \log_2 0.666 + 0.333 \log_2 0.333 \right) = 0.918 \).

- **For Income = Low:**
  - \( p_{\text{Yes}} = 1 \), \( p_{\text{No}} = 0 \).
  - \( H(\text{Low}) = 0 \).

#### Step 2: Calculate Weighted Entropy

\[
H_{\text{Income}} = \frac{5}{14} \times 0.971 + \frac{6}{14} \times 0.918 + \frac{3}{14} \times 0 = 0.693
\]

#### Step 3: Calculate Information Gain

\[
\text{Gain}(S, \text{Income}) = 0.943 - 0.693 = 0.25
\]
- **Information Gain = 0.25** for the split on **Income**.

---

# Decision Trees with Entropy, Gini, and Information Gain

## Example Dataset

We will use a simple fruit classification dataset with two features: **color** and **size**. The goal is to predict whether the fruit is an **apple** or an **orange**.

| Fruit (Target) | Color   | Size  |
|----------------|---------|-------|
| Apple          | Red     | Small |
| Apple          | Red     | Large |
| Orange         | Orange  | Small |
| Orange         | Orange  | Large |
| Orange         | Red     | Large |

In this example, we will use **color** and **size** as input features to build the decision tree.

## 6. Entropy Calculation for Fruit Dataset

### What is Entropy?

Entropy is a measure of uncertainty or impurity in a dataset. It quantifies how mixed the dataset is with respect to the class labels. Lower entropy means less uncertainty, while higher entropy means more uncertainty.

The formula for entropy is:

\[
Entropy(S) = - \sum_{i=1}^{k} p_i \log_2(p_i)
\]

Where:
- \(p_i\) is the proportion of class \(i\) in the dataset \(S\).

### Calculating Entropy for the Example Dataset

In our fruit dataset:
- Probability of **Apple**: \( p(\text{Apple}) = \frac{2}{5} = 0.4 \)
- Probability of **Orange**: \( p(\text{Orange}) = \frac{3}{5} = 0.6 \)

Entropy of the dataset:

\[
Entropy(S) = - (0.4 \cdot \log_2(0.4)) - (0.6 \cdot \log_2(0.6)) \approx 0.971
\]

## 7. Gini Index Calculation for Fruit Dataset

### What is the Gini Index?

The Gini index is another measure of impurity in a dataset. It ranges from 0 (pure) to 0.5 (completely impure). The formula is:

\[
Gini(S) = 1 - \sum_{i=1}^{k} p_i^2
\]

Where \(p_i\) is the proportion of each class in the dataset.

### Calculating Gini Index for the Example Dataset

For the same dataset:
- Probability of **Apple**: \( p(\text{Apple}) = 0.4 \)
- Probability of **Orange**: \( p(\text{Orange}) = 0.6 \)

Gini Index of the dataset:

\[
Gini(S) = 1 - (0.4^2 + 0.6^2) = 0.48
\]

## 8. Information Gain for Features (Fruit Example)

We calculate the Information Gain for both **color** and **size** features to determine which feature should be used for the first split.

### Information Gain for Color

Split by **color** (Red vs. Orange):

- Subset 1: Color = Red
    - Entropy: \( 0.918 \)
- Subset 2: Color = Orange
    - Entropy: \( 0 \)

Information Gain:

\[
IG(S, Color) = 0.971 - \left(\frac{3}{5} \cdot 0.918 + \frac{2}{5} \cdot 0\right) = 0.42
\]

### Information Gain for Size

Split by **size** (Small vs. Large):

- Subset 1: Size = Small
    - Entropy: \( 1 \)
- Subset 2: Size = Large
    - Entropy: \( 0.918 \)

Information Gain:

\[
IG(S, Size) = 0.971 - \left(\frac{2}{5} \cdot 1 + \frac{3}{5} \cdot 0.918\right) = 0.0202
\]

### Conclusion: Choosing the First Split

The Information Gain for **Color** is higher (0.42) than for **Size** (0.0202), so we would split the data based on the **Color** feature first.

---

## 9. Decision Tree for Regression

In **Decision Tree Regression**, the goal is to predict a **continuous** target value. Instead of using entropy or GINI index, the algorithm minimizes the **variance** in the target variable.

### Key Concept: Variance Reduction

The best split is one that reduces the **variance** of the target values. Variance measures the spread of the target values in a node.

#### Variance Formula:
\[
\text{Variance}(S) = \frac{1}{n} \sum_{i=1}^{n} (y_i - \bar{y})^2
\]
Where \( y_i \) is the target value of the \( i \)-th sample, and \( \bar{y} \) is the mean of all target values.

#### Variance Reduction Formula:
\[
\text{Variance Reduction} = \text{Variance of Parent Node} - \sum_{i} \left( \frac{|S_i|}{|S|} \cdot \text{Variance of Child Node}_i \right)
\]

### Example of Decision Tree for Regression:

Let’s predict the **Price of a House** based on the feature **Size (in square meters)**:

| **Size (sq. meters)** | **Price** |
|-----------------------|-----------|
| 50                    | 150,000   |
| 60                    | 180,000   |
| 75                    | 200,000   |
| 80                    | 220,000   |
| 90                    | 240,000   |
| 100                   | 300,000   |
| 120                   | 330,000   |
| 150                   | 400,000   |

#### Step 1: Sort the Feature
Sort **Size**: {50, 60, 75, 80, 90, 100, 120, 150}.

#### Step 2: Evaluate Possible Splits
Evaluate splits at the midpoints between consecutive values, such as 55, 67.5, 77.5, etc.

#### Step 3: Calculate Variance for Each Split

Let’s calculate the **Variance Reduction** for the split at **Size = 80**.

- **Left Split (Size ≤ 80):**
  - Samples: {50, 60, 75, 80}
  - Prices: {150,000, 180,000, 200,000, 220,000}
  - Mean Price: \( \bar{y}_{\text{left}} = 187,500 \)
  - Variance: \( 875,000,000 \).

- **Right Split (Size > 80):**
  - Samples: {90, 100, 120, 150}
  - Prices: {240,000, 300,000, 330,000, 400,000}
  - Mean Price: \( \bar{y}_{\text{right}} = 317,500 \)
  - Variance: \( 3,875,000,000 \).

#### Step 4: Calculate Weighted Variance
\[
\text{Weighted Variance} = \frac{4}{8} \times 875,000,000 + \frac{4}{8} \times 3,875,000,000 = 2,375,000,000
\]

#### Step 5: Calculate Variance Reduction
Let’s assume the **Variance of the root node** (before splitting) is 3,500,000,000.

\[
\text{Variance Reduction} = 3,500,000,000 - 2,375,000,000 = 1,125,000,000
\]

Thus, splitting the node at **Size = 80** reduces the variance by **1.125 billion**.

## 10. Pruning the Decision Tree

Pruning helps reduce **overfitting** by limiting the depth or complexity of the tree.

### 10.1. Pre-Pruning (Early Stopping)

Pre-pruning stops the tree's growth early by setting constraints such as:
- **Max depth**: The maximum allowable depth of the tree.
- **Min samples per node**: The minimum number of samples required to split a node.

### 10.2. Post-Pruning (Pruning After Tree Construction)

Post-pruning occurs after the tree has been fully built. It removes branches that do not contribute significantly to the tree's performance.

#### Example of Post-Pruning:
Consider a tree with four leaf nodes:

           Size > 80
         /           \
   Yes (Left)        No (Right)
 /       \          /      \


After pruning, the tree may be simplified if some branches don't improve accuracy:

       Size > 80
     /          \
 Leaf         Leaf


By merging leaves or removing unnecessary branches, the tree becomes simpler and less prone to overfitting.

## Summary of Key Concepts:
- **Entropy** and **GINI Index** measure impurity in classification tasks.
- **Information Gain** helps select the best feature to split the dataset.
- **Variance Reduction** is used in regression tasks to find the best splits.
- **Pruning** (pre- and post-pruning) helps prevent overfitting and improves generalization.
