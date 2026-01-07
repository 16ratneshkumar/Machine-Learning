# Seaborn Reference Guide

Complete reference for Seaborn - statistical data visualization library built on Matplotlib.

---

## Installation and Import

### Installation
```bash
pip install seaborn
```

### Import
```python
import seaborn as sns
import matplotlib.pyplot as plt
```

**Convention:** Import as `sns`. Seaborn works with Matplotlib, so import both.

---

## Setting Styles

### `sns.set_style()`
**Description:** Set the aesthetic style  
**Syntax:** `sns.set_style(style)`

```python
sns.set_style('darkgrid')   # Dark background with grid
sns.set_style('whitegrid')  # White background with grid
sns.set_style('dark')       # Dark background, no grid
sns.set_style('white')      # White background, no grid
sns.set_style('ticks')      # White with ticks
```

### `sns.set_palette()`
**Description:** Set color palette  
**Syntax:** `sns.set_palette(palette)`

```python
sns.set_palette('deep')
sns.set_palette('muted')
sns.set_palette('pastel')
sns.set_palette('bright')
sns.set_palette('dark')
sns.set_palette('colorblind')
```

---

## Distribution Plots

### `sns.histplot()`
**Description:** Plot histogram with optional KDE  
**Syntax:** `sns.histplot(data, x, kde=False, bins='auto')`

```python
import pandas as pd

# Basic histogram
sns.histplot(data=df, x='age')

# With KDE (Kernel Density Estimate)
sns.histplot(data=df, x='age', kde=True)

# With hue (color by category)
sns.histplot(data=df, x='age', hue='gender', kde=True)
plt.show()
```

### `sns.kdeplot()`
**Description:** Plot kernel density estimate  
**Syntax:** `sns.kdeplot(data, x, hue=None)`

```python
sns.kdeplot(data=df, x='age')
sns.kdeplot(data=df, x='age', hue='gender')
plt.show()
```

### `sns.displot()`
**Description:** Figure-level distribution plot  
**Syntax:** `sns.displot(data, x, kind='hist', hue=None)`

```python
sns.displot(data=df, x='age', kind='hist')
sns.displot(data=df, x='age', kind='kde')
sns.displot(data=df, x='age', kind='ecdf')  # Empirical CDF
plt.show()
```

---

## Categorical Plots

### `sns.barplot()`
**Description:** Show mean values with confidence intervals  
**Syntax:** `sns.barplot(data, x, y, hue=None)`

```python
sns.barplot(data=df, x='category', y='value')
sns.barplot(data=df, x='category', y='value', hue='gender')
plt.show()
```

### `sns.countplot()`
**Description:** Count occurrences of categories  
**Syntax:** `sns.countplot(data, x, hue=None)`

```python
sns.countplot(data=df, x='category')
sns.countplot(data=df, x='category', hue='gender')
plt.show()
```

### `sns.boxplot()`
**Description:** Box plot showing distribution  
**Syntax:** `sns.boxplot(data, x, y, hue=None)`

```python
sns.boxplot(data=df, x='category', y='value')
sns.boxplot(data=df, x='category', y='value', hue='gender')
plt.show()
```

### `sns.violinplot()`
**Description:** Violin plot (box plot + KDE)  
**Syntax:** `sns.violinplot(data, x, y, hue=None)`

```python
sns.violinplot(data=df, x='category', y='value')
sns.violinplot(data=df, x='category', y='value', hue='gender', split=True)
plt.show()
```

### `sns.stripplot()`
**Description:** Scatter plot for categorical data  
**Syntax:** `sns.stripplot(data, x, y, hue=None)`

```python
sns.stripplot(data=df, x='category', y='value')
sns.stripplot(data=df, x='category', y='value', jitter=True)
plt.show()
```

### `sns.swarmplot()`
**Description:** Categorical scatter with non-overlapping points  
**Syntax:** `sns.swarmplot(data, x, y, hue=None)`

```python
sns.swarmplot(data=df, x='category', y='value')
plt.show()
```

---

## Relational Plots

### `sns.scatterplot()`
**Description:** Scatter plot with optional hue/size  
**Syntax:** `sns.scatterplot(data, x, y, hue=None, size=None)`

```python
sns.scatterplot(data=df, x='x_col', y='y_col')
sns.scatterplot(data=df, x='x_col', y='y_col', hue='category')
sns.scatterplot(data=df, x='x_col', y='y_col', hue='category', size='value')
plt.show()
```

### `sns.lineplot()`
**Description:** Line plot with confidence intervals  
**Syntax:** `sns.lineplot(data, x, y, hue=None)`

```python
sns.lineplot(data=df, x='time', y='value')
sns.lineplot(data=df, x='time', y='value', hue='category')
plt.show()
```

---

## Matrix Plots

### `sns.heatmap()`
**Description:** Plot rectangular data as color-encoded matrix  
**Syntax:** `sns.heatmap(data, annot=False, cmap=None)`

```python
# Correlation matrix
correlation = df.corr()
sns.heatmap(correlation, annot=True, cmap='coolwarm')
plt.show()

# Custom colormap
sns.heatmap(correlation, annot=True, cmap='viridis', fmt='.2f')
plt.show()

# With square cells
sns.heatmap(correlation, annot=True, square=True, linewidths=0.5)
plt.show()
```

### `sns.clustermap()`
**Description:** Hierarchically-clustered heatmap  
**Syntax:** `sns.clustermap(data, method='average')`

```python
sns.clustermap(df.corr(), annot=True, cmap='coolwarm')
plt.show()
```

---

## Regression Plots

### `sns.regplot()`
**Description:** Plot with linear regression line  
**Syntax:** `sns.regplot(data, x, y, order=1)`

```python
sns.regplot(data=df, x='x_col', y='y_col')
plt.show()

# Polynomial regression
sns.regplot(data=df, x='x_col', y='y_col', order=2)
plt.show()
```

### `sns.lmplot()`
**Description:** Figure-level regression plot  
**Syntax:** `sns.lmplot(data, x, y, hue=None)`

```python
sns.lmplot(data=df, x='x_col', y='y_col')
sns.lmplot(data=df, x='x_col', y='y_col', hue='category')
plt.show()
```

### `sns.residplot()`
**Description:** Plot residuals of regression  
**Syntax:** `sns.residplot(data, x, y)`

```python
sns.residplot(data=df, x='x_col', y='y_col')
plt.show()
```

---

## Multi-Plot Grids

### `sns.pairplot()`
**Description:** Pairwise relationships in dataset  
**Syntax:** `sns.pairplot(data, hue=None)`

```python
sns.pairplot(df)
sns.pairplot(df, hue='category')
sns.pairplot(df, hue='category', diag_kind='kde')
plt.show()
```

### `sns.FacetGrid()`
**Description:** Multi-plot grid for plotting conditional relationships  
**Syntax:** `sns.FacetGrid(data, col=None, row=None, hue=None)`

```python
g = sns.FacetGrid(df, col='category')
g.map(sns.histplot, 'value')
plt.show()

# With hue
g = sns.FacetGrid(df, col='category', hue='gender')
g.map(sns.scatterplot, 'x_col', 'y_col')
g.add_legend()
plt.show()
```

---

## Color Palettes

### `sns.color_palette()`
**Description:** Return or set color palette  
**Syntax:** `sns.color_palette(palette=None, n_colors=None)`

```python
# View palette
sns.color_palette('deep')
sns.palplot(sns.color_palette('deep'))

# Sequential palettes
sns.color_palette('Blues')
sns.color_palette('Greens')

# Diverging palettes
sns.color_palette('coolwarm')
sns.color_palette('RdBu')

# Custom palette
custom = ['#FF5733', '#33FF57', '#3357FF']
sns.set_palette(custom)
```

---

## Useful Functions

### `sns.despine()`
**Description:** Remove top and right spines  
**Syntax:** `sns.despine(top=True, right=True, left=False, bottom=False)`

```python
sns.boxplot(data=df, x='category', y='value')
sns.despine()
plt.show()
```

### `sns.set_context()`
**Description:** Set plotting context (scale)  
**Syntax:** `sns.set_context(context)`

```python
sns.set_context('paper')    # Smallest
sns.set_context('notebook') # Default
sns.set_context('talk')     # Larger
sns.set_context('poster')   # Largest
```

### `sns.set()`
**Description:** Set multiple aesthetic parameters  
**Syntax:** `sns.set(style=None, palette=None, context=None)`

```python
sns.set(style='darkgrid', palette='muted', context='notebook')
```

---

**Back to the Topic:** [Libraries & Tools](3_Libraries_and_Tools.md)
