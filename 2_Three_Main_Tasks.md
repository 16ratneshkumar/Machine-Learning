# Three Main Tasks in Machine Learning

Machine learning performs three primary tasks, each serving different purposes:

---

## 1. Prediction (Regression)

### What is Prediction?

<abbr title="Predicting continuous numerical values like prices, temperatures, or quantities">Prediction</abbr> involves training a model on <abbr title="Data with known correct answers">labeled data</abbr> to forecast future continuous values.

### How it Works:

1. **Collect historical data** with known outcomes
2. **Train the model** to find patterns and relationships
3. **Use the model** to predict future values

### Common Models:

- **<abbr title="Finding a straight line that best fits the data points">Linear Regression</abbr>** - Predicts values using a straight line relationship
- **<abbr title="Finding a curved line that best fits the data points">Polynomial Regression</abbr>** - Predicts values using curved relationships
- **Ridge Regression** - Linear regression with penalty to prevent overfitting
- **Lasso Regression** - Linear regression that can eliminate less important features

### 💻 Code Example: Linear Regression
```python
import numpy as np
from sklearn.linear_model import LinearRegression

# Sample data (X: input, y: target)
X = np.array([[1], [2], [3], [4], [5]])
y = np.array([2, 4, 6, 8, 10])

# Create and train the model
model = LinearRegression()
model.fit(X, y)

# Make a prediction for input 6
prediction = model.predict(np.array([[6]]))
print(f"Prediction for input 6: {prediction[0]}") # Output: 12.0
```

### Real-World Examples:

- **House Price Prediction** - Predicting property prices based on size, location, age
- **Stock Market Forecasting** - Predicting future stock prices
- **Weather Prediction** - Forecasting temperature, rainfall
- **Sales Forecasting** - Predicting future product sales
- **Energy Consumption** - Predicting electricity usage

### Key Characteristics:

- Works with **continuous numerical outputs** (prices, temperatures, quantities)
- Requires <abbr title="Data used to teach the model patterns">training data</abbr> with known values
- Output is a **number** (not a category)

---

## 2. Classification

### What is Classification?

<abbr title="Categorizing data into predefined groups or classes">Classification</abbr> involves training a model to categorize data into predefined groups or classes.

### How it Works:

1. **Collect labeled examples** from each category
2. **Train the model** to recognize patterns for each class
3. **Use the model** to classify new, unseen data

### Common Models:

- **<abbr title="Tree-like model that makes decisions based on asking questions">Decision Trees (DT)</abbr>** - Makes decisions by asking yes/no questions
- **<abbr title="Finds the best boundary line to separate different classes">Support Vector Machines (SVM)</abbr>** - Finds optimal boundaries between classes
- **<abbr title="Computer systems inspired by the human brain with connected nodes">Artificial Neural Networks (ANN)</abbr>** - Mimics human brain structure for complex patterns
- **Random Forest** - Combines multiple decision trees for better accuracy
- **Naive Bayes** - Uses probability to classify data
- **K-Nearest Neighbors (KNN)** - Classifies based on similarity to nearby examples

### Real-World Examples:

- **Email Spam Detection** - Spam or Not Spam
- **Disease Diagnosis** - Healthy or Diseased
- **Image Recognition** - Cat, Dog, Bird, etc.
- **Sentiment Analysis** - Positive, Negative, Neutral reviews
- **Credit Approval** - Approve or Reject loan applications
- **Handwriting Recognition** - Identifying written digits/letters

### Key Characteristics:

- Works with **categorical outputs** (labels, classes)
- Requires labeled training data
- Output is a **category or class** (not a number)

---

## 3. Clustering

### What is Clustering?

<abbr title="Grouping similar data together without predefined categories">Clustering</abbr> involves grouping similar data points together without predefined categories, discovering natural patterns in <abbr title="Data without predefined categories or answers">unlabeled data</abbr>.

### How it Works:

1. **Collect unlabeled data** (no predefined categories)
2. **Apply clustering algorithm** to find natural groupings
3. **Analyze clusters** to understand patterns and similarities

### Common Models:

- **K-Means** - Divides data into K groups based on similarity
- **Hierarchical Clustering** - Creates a tree of clusters
- **DBSCAN** - Finds clusters of varying shapes and sizes
- **Gaussian Mixture Models** - Uses probability distributions to cluster

### 💻 Code Example: K-Means Clustering
```python
import numpy as np
from sklearn.cluster import KMeans

# Sample data (unlabeled)
X = np.array([[1, 2], [1, 4], [1, 0],
              [4, 2], [4, 4], [4, 0]])

# Create and fit the model (into 2 clusters)
kmeans = KMeans(n_clusters=2, random_state=0).fit(X)

# Predict the cluster for a new sample [0, 0]
cluster = kmeans.predict([[0, 0]])
print(f"Cluster for input [0, 0]: {cluster[0]}")
```

### Real-World Examples:

- **Customer Segmentation** - Grouping customers by shopping behavior
- **Document Organization** - Grouping similar articles or documents
- **Image Segmentation** - Separating different parts of an image
- **Anomaly Detection** - Finding unusual patterns (fraud, defects)
- **Social Network Analysis** - Finding communities in networks
- **Gene Sequence Analysis** - Grouping similar genetic patterns

### Key Characteristics:

- Works with **unlabeled data** (no predefined answers)
- Discovers **hidden patterns** automatically
- Number of groups may or may not be known in advance

---

## Comparison Table

| Aspect | Prediction | Classification | Clustering |
|--------|------------|----------------|------------|
| **Data Type** | Labeled | Labeled | Unlabeled |
| **Output** | Continuous number | Category/Class | Groups/Clusters |
| **Goal** | Forecast values | Categorize data | Find patterns |
| **Example** | Predict price: $250,000 | Spam: Yes/No | Group 1, 2, 3 |
| **Learning Type** | Supervised | Supervised | Unsupervised |

---

**Previous Topic:** [← 1. Introduction](1_Introduction.md) | **Next Topic:** [3. Libraries & Tools →](3_Libraries_and_Tools.md)
