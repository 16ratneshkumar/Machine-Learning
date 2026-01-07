# Matplotlib Reference Guide

Complete reference for Matplotlib - the foundational plotting library in Python.

---

## Installation and Import

### Installation
```bash
pip install matplotlib
```

### Import
```python
import matplotlib.pyplot as plt
```

**Convention:** Import pyplot as `plt` - this is the standard convention.

---

## Basic Plotting

### `plt.plot()`
**Description:** Create a line plot  
**Syntax:** `plt.plot(x, y, format_string, **kwargs)`

```python
import matplotlib.pyplot as plt

# Simple line plot
x = [1, 2, 3, 4, 5]
y = [2, 4, 6, 8, 10]
plt.plot(x, y)
plt.show()

# With labels
plt.plot(x, y)
plt.xlabel('X Axis')
plt.ylabel('Y Axis')
plt.title('My Plot')
plt.show()

# Multiple lines
plt.plot(x, y, label='Line 1')
plt.plot(x, [1, 3, 5, 7, 9], label='Line 2')
plt.legend()
plt.show()
```

### `plt.scatter()`
**Description:** Create a scatter plot  
**Syntax:** `plt.scatter(x, y, s=None, c=None, **kwargs)`

```python
# Basic scatter
plt.scatter(x, y)
plt.show()

# With size and color
plt.scatter(x, y, s=100, c='red', alpha=0.5)
plt.show()

# Color by values
colors = [1, 2, 3, 4, 5]
plt.scatter(x, y, c=colors, cmap='viridis')
plt.colorbar()
plt.show()
```

### `plt.bar()`
**Description:** Create a bar chart  
**Syntax:** `plt.bar(x, height, width=0.8, **kwargs)`

```python
categories = ['A', 'B', 'C', 'D']
values = [25, 40, 30, 55]

plt.bar(categories, values)
plt.show()

# Horizontal bar
plt.barh(categories, values)
plt.show()

# With colors
plt.bar(categories, values, color=['red', 'blue', 'green', 'orange'])
plt.show()
```

### `plt.hist()`
**Description:** Create a histogram  
**Syntax:** `plt.hist(x, bins=10, **kwargs)`

```python
data = [1, 2, 2, 3, 3, 3, 4, 4, 5]

plt.hist(data, bins=5)
plt.show()

# With customization
plt.hist(data, bins=10, color='skyblue', edgecolor='black', alpha=0.7)
plt.xlabel('Value')
plt.ylabel('Frequency')
plt.show()
```

### `plt.pie()`
**Description:** Create a pie chart  
**Syntax:** `plt.pie(x, labels=None, autopct=None, **kwargs)`

```python
sizes = [30, 25, 20, 25]
labels = ['A', 'B', 'C', 'D']

plt.pie(sizes, labels=labels, autopct='%1.1f%%')
plt.show()

# Explode a slice
explode = (0.1, 0, 0, 0)
plt.pie(sizes, labels=labels, autopct='%1.1f%%', explode=explode)
plt.show()
```

---

## Customization

### Line Styles and Colors

```python
# Line styles
plt.plot(x, y, linestyle='-')   # Solid (default)
plt.plot(x, y, linestyle='--')  # Dashed
plt.plot(x, y, linestyle='-.')  # Dash-dot
plt.plot(x, y, linestyle=':')   # Dotted

# Short format
plt.plot(x, y, 'r--')  # Red dashed line
plt.plot(x, y, 'bo')   # Blue circles
plt.plot(x, y, 'g^')   # Green triangles

# Colors
plt.plot(x, y, color='red')
plt.plot(x, y, color='#FF5733')  # Hex color
plt.plot(x, y, color=(0.1, 0.2, 0.5))  # RGB tuple

# Line width
plt.plot(x, y, linewidth=3)

# Markers
plt.plot(x, y, marker='o', markersize=10, markerfacecolor='red')
```

### Labels and Titles

#### `plt.xlabel()` / `plt.ylabel()`
**Description:** Set axis labels  
**Syntax:** `plt.xlabel(label, fontsize=None)`

```python
plt.xlabel('Time (seconds)', fontsize=14)
plt.ylabel('Temperature (°C)', fontsize=14)
```

#### `plt.title()`
**Description:** Set plot title  
**Syntax:** `plt.title(label, fontsize=None)`

```python
plt.title('Temperature Over Time', fontsize=16, fontweight='bold')
```

#### `plt.legend()`
**Description:** Add a legend  
**Syntax:** `plt.legend(loc='best')`

```python
plt.plot(x, y, label='Data 1')
plt.plot(x, y2, label='Data 2')
plt.legend()  # Auto position
plt.legend(loc='upper right')
plt.legend(loc='lower left')
```

### Grid

#### `plt.grid()`
**Description:** Add grid lines  
**Syntax:** `plt.grid(visible=True, which='major', axis='both')`

```python
plt.grid(True)
plt.grid(True, linestyle='--', alpha=0.5)
plt.grid(True, axis='x')  # Only x-axis grid
```

### Axis Limits

#### `plt.xlim()` / `plt.ylim()`
**Description:** Set axis limits  
**Syntax:** `plt.xlim(left, right)`

```python
plt.xlim(0, 10)
plt.ylim(-5, 5)

# Get current limits
x_min, x_max = plt.xlim()
```

### Ticks

#### `plt.xticks()` / `plt.yticks()`
**Description:** Set tick locations and labels  
**Syntax:** `plt.xticks(ticks, labels=None)`

```python
plt.xticks([0, 2, 4, 6, 8, 10])
plt.xticks([0, 1, 2, 3], ['A', 'B', 'C', 'D'])
plt.xticks(rotation=45)  # Rotate labels
```

---

## Figure and Subplots

### `plt.figure()`
**Description:** Create a new figure  
**Syntax:** `plt.figure(figsize=(width, height), dpi=100)`

```python
plt.figure(figsize=(10, 6))  # Width=10, Height=6 inches
plt.figure(figsize=(8, 8), dpi=150)  # Higher resolution
```

### `plt.subplots()`
**Description:** Create figure and subplots  
**Syntax:** `plt.subplots(nrows=1, ncols=1, figsize=None)`

```python
# Create 2x2 grid of subplots
fig, axes = plt.subplots(2, 2, figsize=(10, 8))

# Access individual subplots
axes[0, 0].plot(x, y)
axes[0, 1].scatter(x, y)
axes[1, 0].bar(categories, values)
axes[1, 1].hist(data)

plt.tight_layout()  # Adjust spacing
plt.show()

# Single row
fig, (ax1, ax2, ax3) = plt.subplots(1, 3, figsize=(15, 5))
ax1.plot(x, y)
ax2.scatter(x, y)
ax3.bar(categories, values)
```

### `plt.subplot()`
**Description:** Add subplot to current figure  
**Syntax:** `plt.subplot(nrows, ncols, index)`

```python
plt.subplot(2, 2, 1)  # 2x2 grid, position 1
plt.plot(x, y)

plt.subplot(2, 2, 2)  # Position 2
plt.scatter(x, y)

plt.subplot(2, 2, 3)  # Position 3
plt.bar(categories, values)

plt.subplot(2, 2, 4)  # Position 4
plt.hist(data)

plt.show()
```

---

## Saving Figures

### `plt.savefig()`
**Description:** Save figure to file  
**Syntax:** `plt.savefig(filename, dpi=None, bbox_inches=None)`

```python
plt.plot(x, y)
plt.savefig('plot.png')
plt.savefig('plot.png', dpi=300)  # High resolution
plt.savefig('plot.png', bbox_inches='tight')  # Remove extra whitespace
plt.savefig('plot.pdf')  # Save as PDF
plt.savefig('plot.svg')  # Save as SVG
```

---

## Additional Plot Types

### `plt.fill_between()`
**Description:** Fill area between two curves  
**Syntax:** `plt.fill_between(x, y1, y2, alpha=0.5)`

```python
plt.plot(x, y)
plt.fill_between(x, y, alpha=0.3)
plt.show()
```

### `plt.errorbar()`
**Description:** Plot with error bars  
**Syntax:** `plt.errorbar(x, y, yerr=None, xerr=None)`

```python
errors = [0.5, 0.3, 0.4, 0.6, 0.2]
plt.errorbar(x, y, yerr=errors, fmt='o', capsize=5)
plt.show()
```

### `plt.boxplot()`
**Description:** Create box plot  
**Syntax:** `plt.boxplot(data, labels=None)`

```python
data = [[1, 2, 3, 4, 5], [2, 3, 4, 5, 6], [3, 4, 5, 6, 7]]
plt.boxplot(data, labels=['A', 'B', 'C'])
plt.show()
```

### `plt.imshow()`
**Description:** Display image or 2D array  
**Syntax:** `plt.imshow(X, cmap=None)`

```python
import numpy as np
data = np.random.rand(10, 10)
plt.imshow(data, cmap='viridis')
plt.colorbar()
plt.show()
```

---

## Style and Themes

### `plt.style.use()`
**Description:** Use predefined style  
**Syntax:** `plt.style.use(style_name)`

```python
plt.style.use('ggplot')
plt.style.use('seaborn')
plt.style.use('dark_background')
plt.style.use('bmh')

# See available styles
print(plt.style.available)
```

---

## Useful Functions

### `plt.show()`
**Description:** Display all figures  
**Syntax:** `plt.show()`

```python
plt.plot(x, y)
plt.show()  # Display the plot
```

### `plt.close()`
**Description:** Close figure  
**Syntax:** `plt.close(fig=None)`

```python
plt.close()  # Close current figure
plt.close('all')  # Close all figures
```

### `plt.clf()`
**Description:** Clear current figure  
**Syntax:** `plt.clf()`

```python
plt.clf()  # Clear the figure
```

### `plt.text()`
**Description:** Add text to plot  
**Syntax:** `plt.text(x, y, text, fontsize=None)`

```python
plt.plot(x, y)
plt.text(3, 6, 'Important Point', fontsize=12)
plt.show()
```

### `plt.annotate()`
**Description:** Add annotation with arrow  
**Syntax:** `plt.annotate(text, xy, xytext, arrowprops=None)`

```python
plt.plot(x, y)
plt.annotate('Peak', xy=(3, 6), xytext=(4, 8),
             arrowprops=dict(facecolor='black', shrink=0.05))
plt.show()
```

---

**Back to the Topic:** [Libraries & Tools](3_Libraries_and_Tools.md)
