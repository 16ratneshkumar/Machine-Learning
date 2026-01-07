# Model Development and Assessment

Complete guide to building, training, and evaluating machine learning models.

---

## The ML Development Process

### 1. Data Collection
Gather relevant data for your problem.
- **Sources:** Databases, APIs, web scraping, sensors, surveys
- **Quality matters:** More quality data = better models

### 2. Data Preprocessing
Clean and transform the data into a suitable format.
- Remove duplicates and handle missing values
- Convert data into mathematical format

### 3. Model Selection
Choosing the appropriate algorithm for the task (Regression, Classification, etc.).

### 4. Training
Feeding the data into the <abbr title="A mathematical representation of a real-world process">model</abbr> to learn patterns.

### 5. Evaluation
Assessing the model's performance using metrics like Accuracy or MSE.

### 6. Deployment
Implementing the model in a real-world scenario (e.g., as part of an app).

### 7. Monitoring
Continuously evaluating performance and updating with new data.

---

### 🔄 The Workflow Diagram

```text
Data Collection -> Data Preprocessing -> Model Selection -> Training -> Evaluation -> Deployment -> Monitoring
```

---

## Key Terminology

- **Algorithm**: A procedure or formula for solving a problem (used to train models).
- **Features**: The input variables used to make predictions (e.g., square footage of a house).
- **Labels**: The output variable that the model is trying to predict (e.g., the price of the house).
- **Training Data**: The dataset used to teach the model patterns.
- **Test Data**: The dataset used to evaluate how well the model works on unseen information.

---

## Data Splitting Strategy

### Why Split Data?

We need to evaluate how well our model performs on **new, unseen data** (not the data it was trained on).

### Common Split Ratios:

#### **75:25 Split**
- **75%** → <abbr title="Data used to teach the model patterns and relationships">Training Data</abbr>
- **25%** → <abbr title="Data used to evaluate how well the model performs on unseen data">Test Data</abbr>

#### **80:20 Split** (Most Common)
- **80%** → Training Data
- **20%** → Test Data

#### **70:15:15 Split** (Advanced)
- **70%** → Training Data
- **15%** → <abbr title="Data used to tune model parameters during training">Validation Data</abbr>
- **15%** → Test Data

### Example:

If you have **1000 data samples**:
- **800 samples** for training (teaching the model)
- **200 samples** for testing (evaluating the model)

### Code Example:

```python
from sklearn.model_selection import train_test_split

# Split data 80:20
X_train, X_test, y_train, y_test = train_test_split(
    X, y, test_size=0.2, random_state=42
)
```

---

## Model Training

### What is Training?

<abbr title="The process of teaching a model to recognize patterns in data">Training</abbr> is the process where the model learns patterns from the training data.

### Training Process:

1. **Feed training data** to the model
2. **Model makes predictions** on training data
3. **Calculate error** (difference between prediction and actual value)
4. **Adjust model parameters** to reduce error
5. **Repeat** until error is minimized

### Key Concepts:

**<abbr title="When a model learns training data too well, including noise, and performs poorly on new data">Overfitting</abbr>**
- Model memorizes training data instead of learning patterns
- Performs well on training data but poorly on test data
- **Solution:** Use more data, simplify model, use regularization

**<abbr title="When a model is too simple to capture patterns in the data">Underfitting</abbr>**
- Model is too simple to capture patterns
- Performs poorly on both training and test data
- **Solution:** Use more complex model, add more features

---

## Model Evaluation

### Performance Metrics

Different metrics for different tasks:

#### For Prediction (Regression):

**1. <abbr title="Average of squared differences between predicted and actual values">Mean Squared Error (MSE)</abbr>**
- Lower is better
- Penalizes large errors more

**2. <abbr title="Square root of MSE, in same units as the target variable">Root Mean Squared Error (RMSE)</abbr>**
- Lower is better
- Easier to interpret (same units as target)

**3. <abbr title="Average absolute difference between predicted and actual values">Mean Absolute Error (MAE)</abbr>**
- Lower is better
- Less sensitive to outliers

**4. R² Score (R-squared)**
- Ranges from 0 to 1
- Higher is better (1 = perfect predictions)

#### For Classification:

**1. <abbr title="Percentage of correct predictions out of total predictions">Accuracy</abbr>**
- Percentage of correct predictions
- Formula: (Correct Predictions / Total Predictions) × 100

**2. <abbr title="Of all predicted positives, how many were actually positive">Precision</abbr>**
- How many predicted positives are actually positive
- Important when false positives are costly

**3. <abbr title="Of all actual positives, how many were correctly predicted">Recall</abbr>**
- How many actual positives were correctly identified
- Important when false negatives are costly

**4. <abbr title="Harmonic mean of precision and recall, balances both metrics">F1-Score</abbr>**
- Balance between precision and recall
- Useful when classes are imbalanced

---

## Model Quality Assessment

### Error Rate Threshold

**General Rule:**

If the model's <abbr title="Percentage of incorrect predictions">error rate</abbr> is **less than 5%**, the model quality is considered **good**.

- **Error Rate < 5%** → ✅ Good model
- **Error Rate > 5%** → ⚠️ Consider improving or changing the model

### What to Do if Model Quality is Poor:

1. **Collect more data** - More examples help the model learn better
2. **Try different algorithms** - Some models work better for certain problems
3. **Feature engineering** - Create better input features
4. **Tune hyperparameters** - Adjust model settings
5. **Remove noise** - Clean the data better
6. **Try ensemble methods** - Combine multiple models

---

## Model Improvement Techniques

### 1. Cross-Validation
- Split data into multiple folds
- Train and test on different combinations
- Get more reliable performance estimates

### 2. Hyperparameter Tuning
- Adjust model settings (learning rate, depth, etc.)
- Use Grid Search or Random Search
- Find optimal configuration

### 3. Feature Engineering
- Create new features from existing ones
- Remove irrelevant features
- Transform features for better representation

### 4. Ensemble Methods
- Combine multiple models
- Examples: Random Forest, Gradient Boosting
- Often performs better than single models

---

## Complete ML Workflow Example

```python
# 1. Import libraries
import pandas as pd
from sklearn.model_selection import train_test_split
from sklearn.linear_model import LinearRegression
from sklearn.metrics import mean_squared_error, r2_score

# 2. Load data
data = pd.read_csv('data.csv')

# 3. Prepare features and target
X = data[['feature1', 'feature2', 'feature3']]
y = data['target']

# 4. Split data (80:20)
X_train, X_test, y_train, y_test = train_test_split(
    X, y, test_size=0.2, random_state=42
)

# 5. Create and train model
model = LinearRegression()
model.fit(X_train, y_train)

# 6. Make predictions
y_pred = model.predict(X_test)

# 7. Evaluate model
mse = mean_squared_error(y_test, y_pred)
r2 = r2_score(y_test, y_pred)

print(f"MSE: {mse}")
print(f"R² Score: {r2}")

# 8. Use model for new predictions
new_data = [[value1, value2, value3]]
prediction = model.predict(new_data)
```

---

## Key Takeaways

✅ **Always split your data** - Never test on training data

✅ **Use appropriate metrics** - Different tasks need different metrics

✅ **Aim for < 5% error rate** - General benchmark for good models

✅ **Watch for overfitting** - Model should generalize to new data

✅ **Iterate and improve** - ML is an iterative process

---

**Previous Topic:** [← Libraries & Tools](3_Libraries_and_Tools.md)
