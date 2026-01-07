# Scikit-learn Reference Guide

Complete reference for Scikit-learn - the most popular machine learning library in Python.

---

## Installation and Import

### Installation
```bash
pip install scikit-learn
```

### Import
```python
from sklearn import <module>
# Examples:
from sklearn.model_selection import train_test_split
from sklearn.preprocessing import StandardScaler
from sklearn.linear_model import LinearRegression
```

---

## Data Splitting

### `train_test_split()`
**Description:** Split arrays into train and test subsets  
**Syntax:** `train_test_split(*arrays, test_size=0.25, random_state=None)`

```python
from sklearn.model_selection import train_test_split

X_train, X_test, y_train, y_test = train_test_split(
    X, y, test_size=0.2, random_state=42
)

# Stratified split (maintains class distribution)
X_train, X_test, y_train, y_test = train_test_split(
    X, y, test_size=0.2, stratify=y, random_state=42
)
```

---

## Preprocessing

### `StandardScaler`
**Description:** Standardize features (mean=0, std=1)  
**Methods:** `fit()`, `transform()`, `fit_transform()`

```python
from sklearn.preprocessing import StandardScaler

scaler = StandardScaler()
X_train_scaled = scaler.fit_transform(X_train)
X_test_scaled = scaler.transform(X_test)
```

### `MinMaxScaler`
**Description:** Scale features to [0, 1] range  
**Methods:** `fit()`, `transform()`, `fit_transform()`

```python
from sklearn.preprocessing import MinMaxScaler

scaler = MinMaxScaler()
X_scaled = scaler.fit_transform(X)
```

### `LabelEncoder`
**Description:** Encode categorical labels as integers  
**Methods:** `fit()`, `transform()`, `fit_transform()`

```python
from sklearn.preprocessing import LabelEncoder

encoder = LabelEncoder()
y_encoded = encoder.fit_transform(y)
y_decoded = encoder.inverse_transform(y_encoded)
```

### `OneHotEncoder`
**Description:** Encode categorical features as one-hot vectors  
**Methods:** `fit()`, `transform()`, `fit_transform()`

```python
from sklearn.preprocessing import OneHotEncoder

encoder = OneHotEncoder(sparse=False)
X_encoded = encoder.fit_transform(X)
```

---

## Regression Models

### `LinearRegression`
**Description:** Ordinary least squares linear regression  
**Methods:** `fit()`, `predict()`, `score()`

```python
from sklearn.linear_model import LinearRegression

model = LinearRegression()
model.fit(X_train, y_train)
predictions = model.predict(X_test)
score = model.score(X_test, y_test)  # R² score

# Get coefficients
print(model.coef_)
print(model.intercept_)
```

### `Ridge`
**Description:** Linear regression with L2 regularization  
**Parameters:** `alpha` (regularization strength)

```python
from sklearn.linear_model import Ridge

model = Ridge(alpha=1.0)
model.fit(X_train, y_train)
predictions = model.predict(X_test)
```

### `Lasso`
**Description:** Linear regression with L1 regularization  
**Parameters:** `alpha` (regularization strength)

```python
from sklearn.linear_model import Lasso

model = Lasso(alpha=0.1)
model.fit(X_train, y_train)
predictions = model.predict(X_test)
```

---

## Classification Models

### `LogisticRegression`
**Description:** Logistic regression classifier  
**Parameters:** `C` (inverse regularization strength)

```python
from sklearn.linear_model import LogisticRegression

model = LogisticRegression()
model.fit(X_train, y_train)
predictions = model.predict(X_test)
probabilities = model.predict_proba(X_test)
```

### `DecisionTreeClassifier`
**Description:** Decision tree classifier  
**Parameters:** `max_depth`, `min_samples_split`

```python
from sklearn.tree import DecisionTreeClassifier

model = DecisionTreeClassifier(max_depth=5, random_state=42)
model.fit(X_train, y_train)
predictions = model.predict(X_test)

# Feature importance
print(model.feature_importances_)
```

### `RandomForestClassifier`
**Description:** Random forest ensemble classifier  
**Parameters:** `n_estimators`, `max_depth`

```python
from sklearn.ensemble import RandomForestClassifier

model = RandomForestClassifier(n_estimators=100, max_depth=10, random_state=42)
model.fit(X_train, y_train)
predictions = model.predict(X_test)
```

### `SVC` (Support Vector Classifier)
**Description:** Support Vector Machine classifier  
**Parameters:** `kernel`, `C`, `gamma`

```python
from sklearn.svm import SVC

model = SVC(kernel='rbf', C=1.0, gamma='scale')
model.fit(X_train, y_train)
predictions = model.predict(X_test)
```

### `KNeighborsClassifier`
**Description:** K-Nearest Neighbors classifier  
**Parameters:** `n_neighbors`

```python
from sklearn.neighbors import KNeighborsClassifier

model = KNeighborsClassifier(n_neighbors=5)
model.fit(X_train, y_train)
predictions = model.predict(X_test)
```

### `GradientBoostingClassifier`
**Description:** Gradient boosting classifier  
**Parameters:** `n_estimators`, `learning_rate`

```python
from sklearn.ensemble import GradientBoostingClassifier

model = GradientBoostingClassifier(n_estimators=100, learning_rate=0.1)
model.fit(X_train, y_train)
predictions = model.predict(X_test)
```

---

## Clustering

### `KMeans`
**Description:** K-Means clustering  
**Parameters:** `n_clusters`

```python
from sklearn.cluster import KMeans

kmeans = KMeans(n_clusters=3, random_state=42)
clusters = kmeans.fit_predict(X)
centers = kmeans.cluster_centers_
```

### `DBSCAN`
**Description:** Density-based clustering  
**Parameters:** `eps`, `min_samples`

```python
from sklearn.cluster import DBSCAN

dbscan = DBSCAN(eps=0.5, min_samples=5)
clusters = dbscan.fit_predict(X)
```

---

## Model Evaluation

### Regression Metrics

```python
from sklearn.metrics import mean_squared_error, mean_absolute_error, r2_score
import numpy as np

# Mean Squared Error
mse = mean_squared_error(y_test, predictions)

# Root Mean Squared Error
rmse = np.sqrt(mse)

# Mean Absolute Error
mae = mean_absolute_error(y_test, predictions)

# R² Score
r2 = r2_score(y_test, predictions)
```

### Classification Metrics

```python
from sklearn.metrics import (
    accuracy_score, precision_score, recall_score, f1_score,
    confusion_matrix, classification_report
)

# Accuracy
accuracy = accuracy_score(y_test, predictions)

# Precision
precision = precision_score(y_test, predictions, average='binary')

# Recall
recall = recall_score(y_test, predictions, average='binary')

# F1 Score
f1 = f1_score(y_test, predictions, average='binary')

# Confusion Matrix
cm = confusion_matrix(y_test, predictions)

# Classification Report
print(classification_report(y_test, predictions))
```

---

## Cross-Validation

### `cross_val_score()`
**Description:** Evaluate model using cross-validation  
**Syntax:** `cross_val_score(estimator, X, y, cv=5)`

```python
from sklearn.model_selection import cross_val_score

scores = cross_val_score(model, X, y, cv=5)
print(f"Mean score: {scores.mean()}")
print(f"Std: {scores.std()}")
```

### `cross_validate()`
**Description:** Cross-validation with multiple metrics  
**Syntax:** `cross_validate(estimator, X, y, cv=5, scoring=None)`

```python
from sklearn.model_selection import cross_validate

scoring = ['accuracy', 'precision', 'recall']
scores = cross_validate(model, X, y, cv=5, scoring=scoring)
```

---

## Hyperparameter Tuning

### `GridSearchCV`
**Description:** Exhaustive search over parameter grid  
**Syntax:** `GridSearchCV(estimator, param_grid, cv=5)`

```python
from sklearn.model_selection import GridSearchCV

param_grid = {
    'n_estimators': [50, 100, 200],
    'max_depth': [5, 10, 15, None]
}

grid_search = GridSearchCV(
    RandomForestClassifier(),
    param_grid,
    cv=5,
    scoring='accuracy'
)

grid_search.fit(X_train, y_train)
best_model = grid_search.best_estimator_
best_params = grid_search.best_params_
best_score = grid_search.best_score_
```

### `RandomizedSearchCV`
**Description:** Random search over parameter distributions  
**Syntax:** `RandomizedSearchCV(estimator, param_distributions, n_iter=10, cv=5)`

```python
from sklearn.model_selection import RandomizedSearchCV
from scipy.stats import randint

param_dist = {
    'n_estimators': randint(50, 200),
    'max_depth': randint(5, 20)
}

random_search = RandomizedSearchCV(
    RandomForestClassifier(),
    param_dist,
    n_iter=20,
    cv=5,
    random_state=42
)

random_search.fit(X_train, y_train)
best_model = random_search.best_estimator_
```

---

## Pipelines

### `Pipeline`
**Description:** Chain transformers and estimator  
**Syntax:** `Pipeline(steps)`

```python
from sklearn.pipeline import Pipeline
from sklearn.preprocessing import StandardScaler
from sklearn.linear_model import LogisticRegression

pipeline = Pipeline([
    ('scaler', StandardScaler()),
    ('classifier', LogisticRegression())
])

pipeline.fit(X_train, y_train)
predictions = pipeline.predict(X_test)
```

---

## Model Persistence

### Save Model

```python
import joblib

# Save
joblib.dump(model, 'model.pkl')

# Load
loaded_model = joblib.load('model.pkl')
```

---

**Back to the Topic:** [Libraries & Tools](3_Libraries_and_Tools.md)
