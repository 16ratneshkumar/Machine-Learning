# Common Libraries and Tools

Essential Python libraries used in Machine Learning projects:

---

## Data Processing Libraries

### 1. NumPy

**Full Name:** Numerical Python

**Purpose:** <abbr title="Working with numbers, arrays, and mathematical operations">Numerical computing</abbr> and array operations

**What it Does:**
- Creates and manipulates multi-dimensional arrays
- Performs fast mathematical operations
- Provides linear algebra functions
- Generates random numbers

**Common Uses:**
```python
import numpy as np
# Create arrays, perform calculations
data = np.array([1, 2, 3, 4, 5])
mean = np.mean(data)
```

**Why Important:** Foundation for most ML libraries, extremely fast for numerical operations

---

### 2. Pandas

**Full Name:** Panel Data

**Purpose:** <abbr title="Organizing, cleaning, and analyzing data in tables">Data manipulation and analysis</abbr>

**What it Does:**
- Works with tabular data (like Excel spreadsheets)
- Cleans and prepares data
- Handles missing values
- Filters, sorts, and groups data

**Common Uses:**
```python
import pandas as pd
# Load and analyze data
df = pd.read_csv('data.csv')
df.describe()  # Get statistics
```

**Why Important:** Makes data cleaning and exploration easy and intuitive

---

## Data Visualization Libraries

### 3. Matplotlib

**Purpose:** <abbr title="Creating charts and graphs to visualize data">Data visualization</abbr>

**What it Does:**
- Creates line plots, bar charts, scatter plots
- Customizes colors, labels, legends
- Saves plots as images

**Common Uses:**
```python
import matplotlib.pyplot as plt
# Create visualizations
plt.plot(x, y)
plt.show()
```

**Why Important:** Helps understand data patterns visually

---

### 4. Seaborn

**Purpose:** <abbr title="Creating beautiful statistical charts and graphs">Statistical data visualization</abbr>

**What it Does:**
- Creates beautiful, professional-looking plots
- Built on top of Matplotlib
- Specializes in statistical visualizations
- Easier syntax than Matplotlib

**Common Uses:**
```python
import seaborn as sns
# Create statistical plots
sns.heatmap(data)
sns.boxplot(x='category', y='value', data=df)
```

**Why Important:** Makes complex statistical visualizations simple and attractive

---

## Machine Learning Libraries

### 5. Scikit-learn

**Full Name:** SCI-entific KIT for machine LEARN-ing

**Purpose:** <abbr title="Ready-to-use algorithms for prediction, classification, and clustering">Machine learning algorithms</abbr>

**What it Does:**
- Provides pre-built ML algorithms (regression, classification, clustering)
- Splits data into train/test sets
- Evaluates model performance
- Preprocesses data (scaling, encoding)

**Common Algorithms:**
- Linear Regression, Logistic Regression
- Decision Trees, Random Forest
- SVM, K-Means, KNN

**Common Uses:**
```python
from sklearn.model_selection import train_test_split
from sklearn.linear_model import LinearRegression

# Train a model
model = LinearRegression()
model.fit(X_train, y_train)
```

**Why Important:** Most popular library for traditional ML, easy to use

---

## Deep Learning Libraries

### 6. TensorFlow

**Purpose:** <abbr title="Framework for building and training neural networks and deep learning models">Deep learning framework</abbr>

**What it Does:**
- Builds and trains neural networks
- Handles large-scale ML projects
- Supports GPUs for faster training
- Created by Google

**Common Uses:**
```python
import tensorflow as tf
# Build neural networks
model = tf.keras.Sequential([...])
model.compile(...)
model.fit(X_train, y_train)
```

**Why Important:** Industry standard for deep learning, very powerful

---

### 7. Keras

**Purpose:** High-level neural network API (now part of TensorFlow)

**What it Does:**
- Simplifies building neural networks
- User-friendly interface
- Runs on top of TensorFlow

**Why Important:** Makes deep learning accessible to beginners

---

### 8. PyTorch

**Purpose:** Deep learning framework (alternative to TensorFlow)

**What it Does:**
- Builds and trains neural networks
- More intuitive for research
- Created by Facebook

**Why Important:** Popular in research, easier to debug

---

## Typical ML Project Workflow

```
1. Load Data          → Pandas
2. Explore Data       → Pandas, Matplotlib, Seaborn
3. Clean Data         → Pandas, NumPy
4. Prepare Features   → NumPy, Scikit-learn
5. Split Data         → Scikit-learn
6. Train Model        → Scikit-learn / TensorFlow / PyTorch
7. Evaluate Model     → Scikit-learn, Matplotlib
8. Make Predictions   → Trained Model
```

---

## Quick Reference

| Library | Primary Use | Import As |
|---------|-------------|-----------|
| NumPy | Numerical computing | `import numpy as np` |
| Pandas | Data manipulation | `import pandas as pd` |
| Matplotlib | Basic plotting | `import matplotlib.pyplot as plt` |
| Seaborn | Statistical plots | `import seaborn as sns` |
| Scikit-learn | ML algorithms | `from sklearn import ...` |
| TensorFlow | Deep learning | `import tensorflow as tf` |

---

## 📚 Detailed Library References

Complete function references with syntax and examples for each library:

**[📖 NumPy Reference](NumPy_Reference.md)** - Array operations, math functions, linear algebra

**[📖 Pandas Reference](Pandas_Reference.md)** - DataFrames, data manipulation, grouping, merging

**[📖 Matplotlib Reference](Matplotlib_Reference.md)** - Plotting, customization, subplots, saving figures

**[📖 Seaborn Reference](Seaborn_Reference.md)** - Statistical plots, heatmaps, distribution plots

**[📖 Scikit-learn Reference](Scikit-learn_Reference.md)** - ML models, preprocessing, evaluation, tuning

**[📖 TensorFlow/Keras Reference](TensorFlow_Reference.md)** - Neural networks, layers, training, callbacks

---

**Previous Topic:** [← 2. Three Main Tasks](2_Three_Main_Tasks.md) | **Next Topic:** [4. Model Development →](4_Model_Development.md)
