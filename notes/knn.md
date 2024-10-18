# K-Nearest Neighbors (KNN) Algorithm

## Overview
K-Nearest Neighbors (KNN) is a simple, non-parametric, and lazy learning algorithm used for both **classification** and **regression** tasks. It works by identifying the 'k' nearest data points in the feature space and predicting the target variable based on these neighbors.

---

## KNN for Classification

### Initialization of k value
- The value of 'k' is a **hyperparameter** that controls the number of nearest neighbors to consider when making predictions. It is typically selected through cross-validation.

### Steps for Classification
1. For each test data point, find the 'k' nearest neighbors from the training data.
2. Among these 'k' neighbors, count how many belong to each class.
3. The class with the **maximum count** among the neighbors is assigned as the predicted class for the test point.

### Distance Metric
- **Euclidean Distance**:  
  $$
\sqrt{(x_2 - x_1)^2 + (y_2 - y_1)^2}
 $$

  
- **Manhattan Distance**:  
  \[
  |x_2 - x_1| + |y_2 - y_1|
  \]

---

## Example: KNN for Classification

**Dataset**: Iris dataset, which consists of three types of flowers: Setosa, Versicolor, and Virginica. We will use two features, petal length and petal width, to classify the flower species.

| Petal Length (cm) | Petal Width (cm) | Species      |
|-------------------|------------------|--------------|
| 1.4               | 0.2              | Setosa       |
| 4.7               | 1.4              | Versicolor   |
| 5.1               | 1.8              | Virginica    |
| 1.3               | 0.2              | Setosa       |
| 4.5               | 1.5              | Versicolor   |
| 5.0               | 1.7              | Virginica    |

**Step-by-step Classification**:
- Suppose we are given a test flower with **Petal Length = 4.8 cm** and **Petal Width = 1.6 cm**. We will classify it based on its nearest neighbors.
- We calculate the **Euclidean distance** between the test flower and all training samples.
- Select **k = 3** (3 nearest neighbors).

**Distance Calculations**:
- Distance from Setosa (1.4, 0.2):  
  \[
  \sqrt{(4.8 - 1.4)^2 + (1.6 - 0.2)^2} = \sqrt{11.56 + 1.96} = \sqrt{13.52} = 3.68
  \]
- Distance from Versicolor (4.7, 1.4):  
  \[
  \sqrt{(4.8 - 4.7)^2 + (1.6 - 1.4)^2} = \sqrt{0.01 + 0.04} = \sqrt{0.05} = 0.22
  \]
- Distance from Virginica (5.1, 1.8):  
  \[
  \sqrt{(4.8 - 5.1)^2 + (1.6 - 1.8)^2} = \sqrt{0.09 + 0.04} = \sqrt{0.13} = 0.36
  \]

**Conclusion**:  
The three nearest neighbors are from **Versicolor** (distance 0.22), **Virginica** (distance 0.36), and **Virginica** (distance 0.50). Since two out of the three neighbors belong to Virginica, we classify the test flower as **Virginica**.

---

## KNN for Regression

### Steps for Regression
1. For each test data point, find the 'k' nearest neighbors.
2. Calculate the **average** (or median) of the target values of the 'k' nearest neighbors and assign this as the predicted value.

---

## Example: KNN for Regression

**Dataset**: Housing prices dataset, where we predict the house price based on the number of rooms.

| Number of Rooms | House Price ($)  |
|-----------------|------------------|
| 3               | 200,000          |
| 5               | 300,000          |
| 4               | 250,000          |
| 6               | 350,000          |
| 3               | 210,000          |

**Step-by-step Regression**:
- Suppose we are given a test house with **4.5 rooms**, and we want to predict the price.
- We calculate the **Euclidean distance** between the test house and all the training samples.
- We select **k = 3** (3 nearest neighbors).

**Distance Calculations**:
- Distance from 3 rooms:  
  \[
  |4.5 - 3| = 1.5
  \]
- Distance from 5 rooms:  
  \[
  |4.5 - 5| = 0.5
  \]
- Distance from 4 rooms:  
  \[
  |4.5 - 4| = 0.5
  \]

**Nearest Neighbors**:  
The three nearest neighbors have the following house prices: **250,000**, **300,000**, and **200,000**.

**Prediction**:
- The average of these house prices is:
  \[
  \frac{250,000 + 300,000 + 200,000}{3} = 250,000
  \]
- Therefore, the predicted price for the test house is **$250,000**.

---

## Time Complexity in KNN
- KNN has a high computational cost due to the need to calculate the distance between the test point and all points in the training dataset.

---

## KNN Variants for Optimization

### KD Tree
- The KD Tree organizes data into a binary tree structure, reducing the number of distance calculations by partitioning the space and eliminating large parts of the dataset during the search.

### Ball Tree
- The Ball Tree groups points into "balls" or clusters, further grouping these balls to eliminate parts of the dataset during the search.

---

## Advantages of KNN
1. **Simplicity**: Easy to understand and implement.
2. **No Training Phase**: As a lazy learner, KNN does not require training.
3. **Versatility**: Can be used for both classification and regression.
4. **Non-parametric**: Makes no assumptions about the data distribution.

---

## Disadvantages of KNN
1. **High Computational Cost**: Slow for large datasets.
2. **Sensitive to Noise**: Outliers can impact predictions.
3. **Memory Intensive**: Stores the entire dataset.
4. **Curse of Dimensionality**: The distance between points becomes less meaningful in high dimensions.

---

## Hyperparameter Tuning for KNN

### Choosing the Right k
- Use cross-validation to determine the optimal value of 'k'. Small 'k' values can cause overfitting, while large 'k' values can result in underfitting.

### Distance Metric
- Depending on the data, you can use other distance metrics such as **Minkowski** or **Cosine Similarity**.

---

## KNN with Feature Scaling
- KNN is based on distance calculations, so it is sensitive to the scale of the features. Always apply **standardization** or **normalization**.

---

## Handling Missing Values in KNN
KNN can be used to impute missing values by identifying the nearest neighbors and taking the **mean** or **mode** of the neighbors' values.

---

## KNN in Imbalanced Datasets
KNN can be adapted to handle imbalanced datasets by weighting the neighbors based on distance or applying techniques like **oversampling** or **undersampling**.

---

## Applications of KNN
1. **Recommendation Systems**: KNN can recommend products based on users with similar preferences.
2. **Image Classification**: KNN can classify images based on pixel similarities.
3. **Text Categorization**: KNN can classify documents into categories like spam vs. non-spam.
4. **Anomaly Detection**: KNN can detect outliers by identifying points far from their neighbors.

---

## Common Pitfalls and Best Practices in KNN

1. **Choosing the Right Distance Metric**: Select the appropriate distance metric based on your dataset.
2. **Handling High Dimensionality**: Use dimensionality reduction techniques like **PCA** before applying KNN on high-dimensional data.
3. **Memory Efficiency**: Use **Approximate Nearest Neighbor (ANN)** techniques to reduce computational time.
