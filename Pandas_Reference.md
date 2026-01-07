# Pandas Reference Guide

Complete reference for Pandas - powerful data manipulation and analysis library.

---

## Installation and Import

### Installation
```bash
pip install pandas
```

### Import
```python
import pandas as pd
```

**Convention:** Always import Pandas as `pd`.

---

## Creating DataFrames

### `pd.DataFrame()`
**Description:** Create a DataFrame from various data structures  
**Syntax:** `pd.DataFrame(data, index=None, columns=None)`

```python
# From dictionary
df = pd.DataFrame({
    'Name': ['Alice', 'Bob', 'Charlie'],
    'Age': [25, 30, 35],
    'City': ['NYC', 'LA', 'Chicago']
})

# From list of lists
df = pd.DataFrame([[1, 2, 3], [4, 5, 6]], columns=['A', 'B', 'C'])

# From NumPy array
import numpy as np
df = pd.DataFrame(np.random.rand(3, 3), columns=['A', 'B', 'C'])
```

---

## Reading Data

### `pd.read_csv()`
**Description:** Read CSV file into DataFrame  
**Syntax:** `pd.read_csv(filepath, sep=',', header='infer')`

```python
df = pd.read_csv('data.csv')
df = pd.read_csv('data.csv', sep=';')  # Different separator
df = pd.read_csv('data.csv', index_col=0)  # Use first column as index
```

### `pd.read_excel()`
**Description:** Read Excel file into DataFrame  
**Syntax:** `pd.read_excel(filepath, sheet_name=0)`

```python
df = pd.read_excel('data.xlsx')
df = pd.read_excel('data.xlsx', sheet_name='Sheet2')
```

### `pd.read_json()`
**Description:** Read JSON file into DataFrame  
**Syntax:** `pd.read_json(filepath)`

```python
df = pd.read_json('data.json')
```

---

## Viewing Data

### `df.head()`
**Description:** View first N rows  
**Syntax:** `df.head(n=5)`

```python
df.head()        # First 5 rows
df.head(10)      # First 10 rows
```

### `df.tail()`
**Description:** View last N rows  
**Syntax:** `df.tail(n=5)`

```python
df.tail()        # Last 5 rows
df.tail(10)      # Last 10 rows
```

### `df.info()`
**Description:** Display DataFrame information  
**Syntax:** `df.info()`

```python
df.info()        # Column names, data types, non-null counts
```

### `df.describe()`
**Description:** Statistical summary of numerical columns  
**Syntax:** `df.describe()`

```python
df.describe()    # Count, mean, std, min, max, quartiles
```

### `df.shape`
**Description:** Dimensions of DataFrame  
**Returns:** Tuple (rows, columns)

```python
df.shape         # (100, 5) means 100 rows, 5 columns
```

### `df.columns`
**Description:** Column names  
**Returns:** Index object

```python
df.columns       # Index(['Name', 'Age', 'City'])
```

### `df.dtypes`
**Description:** Data type of each column  
**Returns:** Series

```python
df.dtypes        # Name: object, Age: int64, City: object
```

### `df.index`
**Description:** Row index  
**Returns:** Index object

```python
df.index         # RangeIndex(start=0, stop=100, step=1)
```

---

## Selecting Data

### Column Selection

```python
# Single column (returns Series)
df['Name']
df.Name          # Alternative (not recommended if column name has spaces)

# Multiple columns (returns DataFrame)
df[['Name', 'Age']]
```

### Row Selection

#### `df.iloc[]`
**Description:** Select by integer position  
**Syntax:** `df.iloc[row_indexer, column_indexer]`

```python
df.iloc[0]           # First row
df.iloc[0:5]         # First 5 rows
df.iloc[:, 0]        # First column
df.iloc[0:5, 0:3]    # First 5 rows, first 3 columns
df.iloc[[0, 2, 4]]   # Rows 0, 2, 4
```

#### `df.loc[]`
**Description:** Select by label  
**Syntax:** `df.loc[row_labels, column_labels]`

```python
df.loc[0]            # Row with index label 0
df.loc[0:5]          # Rows 0 to 5 (inclusive)
df.loc[:, 'Name']    # Column 'Name'
df.loc[0:5, ['Name', 'Age']]  # Specific rows and columns
```

### Conditional Selection

```python
# Single condition
df[df['Age'] > 25]

# Multiple conditions (use & for AND, | for OR)
df[(df['Age'] > 25) & (df['City'] == 'NYC')]
df[(df['Age'] < 25) | (df['Age'] > 35)]

# Using isin()
df[df['City'].isin(['NYC', 'LA'])]
```

---

## Data Manipulation

### Adding Columns

```python
# New column with single value
df['Country'] = 'USA'

# New column from calculation
df['Age_Plus_10'] = df['Age'] + 10

# New column from function
df['Name_Length'] = df['Name'].apply(len)
```

### Dropping Columns

#### `df.drop()`
**Description:** Remove columns or rows  
**Syntax:** `df.drop(labels, axis=0, inplace=False)`

```python
# Drop column
df.drop('City', axis=1)          # Returns new DataFrame
df.drop('City', axis=1, inplace=True)  # Modifies original

# Drop multiple columns
df.drop(['City', 'Country'], axis=1)

# Drop rows
df.drop(0, axis=0)               # Drop row with index 0
df.drop([0, 1, 2], axis=0)       # Drop multiple rows
```

### Renaming Columns

#### `df.rename()`
**Description:** Rename columns or index  
**Syntax:** `df.rename(columns=dict, inplace=False)`

```python
df.rename(columns={'Name': 'Full_Name', 'Age': 'Years'})
df.rename(columns={'Name': 'Full_Name'}, inplace=True)
```

---

## Sorting

### `df.sort_values()`
**Description:** Sort by column values  
**Syntax:** `df.sort_values(by, ascending=True, inplace=False)`

```python
# Sort by single column
df.sort_values('Age')                    # Ascending
df.sort_values('Age', ascending=False)   # Descending

# Sort by multiple columns
df.sort_values(['City', 'Age'])
```

### `df.sort_index()`
**Description:** Sort by index  
**Syntax:** `df.sort_index(ascending=True)`

```python
df.sort_index()
```

---

## Handling Missing Data

### Detecting Missing Values

#### `df.isnull()` / `df.isna()`
**Description:** Detect missing values  
**Returns:** Boolean DataFrame

```python
df.isnull()          # True where values are missing
df.isnull().sum()    # Count missing values per column
df.isnull().any()    # True if column has any missing values
```

#### `df.notnull()` / `df.notna()`
**Description:** Detect non-missing values  
**Returns:** Boolean DataFrame

```python
df.notnull()         # True where values are present
```

### Removing Missing Values

#### `df.dropna()`
**Description:** Remove rows/columns with missing values  
**Syntax:** `df.dropna(axis=0, how='any', inplace=False)`

```python
df.dropna()          # Drop rows with any missing values
df.dropna(axis=1)    # Drop columns with any missing values
df.dropna(how='all') # Drop only if all values are missing
df.dropna(subset=['Age'])  # Drop rows where 'Age' is missing
```

### Filling Missing Values

#### `df.fillna()`
**Description:** Fill missing values  
**Syntax:** `df.fillna(value, method=None, inplace=False)`

```python
df.fillna(0)         # Fill with 0
df.fillna(df.mean()) # Fill with column mean
df.fillna({'Age': 30, 'City': 'Unknown'})  # Different values per column
df.fillna(method='ffill')  # Forward fill
df.fillna(method='bfill')  # Backward fill
```

---

## Grouping and Aggregation

### `df.groupby()`
**Description:** Group data by column values  
**Syntax:** `df.groupby(by, as_index=True)`

```python
# Group and aggregate
df.groupby('City')['Age'].mean()
df.groupby('City')['Age'].sum()
df.groupby('City')['Age'].count()

# Multiple aggregations
df.groupby('City')['Age'].agg(['mean', 'min', 'max'])

# Group by multiple columns
df.groupby(['City', 'Country'])['Age'].mean()
```

### `df.pivot_table()`
**Description:** Create pivot table  
**Syntax:** `df.pivot_table(values, index, columns, aggfunc='mean')`

```python
df.pivot_table(values='Age', index='City', aggfunc='mean')
```

---

## Applying Functions

### `df.apply()`
**Description:** Apply function along axis  
**Syntax:** `df.apply(func, axis=0)`

```python
# Apply to column
df['Age'].apply(lambda x: x * 2)

# Apply to entire DataFrame
df.apply(np.sqrt)

# Apply custom function
def categorize_age(age):
    return 'Young' if age < 30 else 'Old'

df['Age_Category'] = df['Age'].apply(categorize_age)
```

### `df.map()`
**Description:** Map values (for Series)  
**Syntax:** `series.map(dict_or_function)`

```python
df['City'].map({'NYC': 'New York', 'LA': 'Los Angeles'})
```

### `df.applymap()`
**Description:** Apply function element-wise to DataFrame  
**Syntax:** `df.applymap(func)`

```python
df.applymap(lambda x: x * 2)
```

---

## Merging and Joining

### `pd.concat()`
**Description:** Concatenate DataFrames  
**Syntax:** `pd.concat([df1, df2], axis=0, ignore_index=False)`

```python
# Vertical concatenation (stack rows)
pd.concat([df1, df2])
pd.concat([df1, df2], ignore_index=True)

# Horizontal concatenation (stack columns)
pd.concat([df1, df2], axis=1)
```

### `pd.merge()`
**Description:** Merge DataFrames (SQL-like join)  
**Syntax:** `pd.merge(left, right, on=None, how='inner')`

```python
# Inner join
pd.merge(df1, df2, on='ID')

# Left join
pd.merge(df1, df2, on='ID', how='left')

# Right join
pd.merge(df1, df2, on='ID', how='right')

# Outer join
pd.merge(df1, df2, on='ID', how='outer')

# Join on multiple columns
pd.merge(df1, df2, on=['ID', 'Name'])
```

---

## String Operations

### `df['column'].str` Methods

```python
# Convert to lowercase/uppercase
df['Name'].str.lower()
df['Name'].str.upper()

# Check if contains substring
df['Name'].str.contains('Alice')

# Replace substring
df['Name'].str.replace('Alice', 'Alicia')

# Split string
df['Name'].str.split(' ')

# Strip whitespace
df['Name'].str.strip()

# Get string length
df['Name'].str.len()
```

---

## Exporting Data

### `df.to_csv()`
**Description:** Write DataFrame to CSV  
**Syntax:** `df.to_csv(filepath, index=True, sep=',')`

```python
df.to_csv('output.csv')
df.to_csv('output.csv', index=False)  # Don't write index
df.to_csv('output.csv', sep=';')      # Different separator
```

### `df.to_excel()`
**Description:** Write DataFrame to Excel  
**Syntax:** `df.to_excel(filepath, sheet_name='Sheet1', index=True)`

```python
df.to_excel('output.xlsx')
df.to_excel('output.xlsx', index=False)
df.to_excel('output.xlsx', sheet_name='MyData')
```

### `df.to_json()`
**Description:** Write DataFrame to JSON  
**Syntax:** `df.to_json(filepath)`

```python
df.to_json('output.json')
```

---

## Useful Methods

### `df.value_counts()`
**Description:** Count unique values (for Series)  
**Syntax:** `series.value_counts()`

```python
df['City'].value_counts()
```

### `df.unique()`
**Description:** Get unique values (for Series)  
**Syntax:** `series.unique()`

```python
df['City'].unique()
```

### `df.nunique()`
**Description:** Count number of unique values  
**Syntax:** `df.nunique()`

```python
df['City'].nunique()
```

### `df.duplicated()`
**Description:** Identify duplicate rows  
**Syntax:** `df.duplicated(subset=None, keep='first')`

```python
df.duplicated()
df[df.duplicated()]  # Show duplicate rows
```

### `df.drop_duplicates()`
**Description:** Remove duplicate rows  
**Syntax:** `df.drop_duplicates(subset=None, keep='first', inplace=False)`

```python
df.drop_duplicates()
df.drop_duplicates(subset=['Name'])  # Based on specific column
```

---

**Back to the Topic:** [Libraries & Tools](3_Libraries_and_Tools.md)
