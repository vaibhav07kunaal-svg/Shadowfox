# Python Visualization Libraries: Comprehensive Documentation Guide

> A practical guide covering **Matplotlib**, **Seaborn**, **Plotly**, **Bokeh**, and **Pandas** — their graph types, code examples, and a comparative analysis.

---

## Table of Contents

1. [Matplotlib](#1-matplotlib)
2. [Seaborn](#2-seaborn)
3. [Plotly](#3-plotly)
4. [Bokeh](#4-bokeh)
5. [Pandas Visualization](#5-pandas-visualization)
6. [Library Comparison](#6-library-comparison)

---

## 1. Matplotlib

### Overview

Matplotlib is the foundational Python plotting library, offering a MATLAB-like API for producing static, animated, and interactive visualizations. It is highly customizable and serves as the backbone for many other libraries (like Seaborn and Pandas). Best suited for publication-quality static figures.

**Typical Use Cases:** Academic research, scientific publishing, exploratory data analysis, custom low-level plots.

---

### Graph Types

#### 1.1 Line Plot

**Description:** Displays data points connected by lines; ideal for time-series or continuous data.

**Use Case:** Tracking stock prices, temperature trends, or model training loss over epochs.

```python
import matplotlib.pyplot as plt
import numpy as np

x = np.linspace(0, 10, 100)
y = np.sin(x)

plt.figure(figsize=(8, 4))
plt.plot(x, y, color='steelblue', linewidth=2, label='sin(x)')
plt.title('Line Plot: sin(x)')
plt.xlabel('x')
plt.ylabel('sin(x)')
plt.legend()
plt.grid(True)
plt.tight_layout()
plt.show()
```

---

#### 1.2 Scatter Plot

**Description:** Displays individual data points to reveal relationships or clusters between two variables.

**Use Case:** Correlation analysis, outlier detection, cluster visualization.

```python
import matplotlib.pyplot as plt
import numpy as np

np.random.seed(42)
x = np.random.randn(100)
y = 2 * x + np.random.randn(100)

plt.figure(figsize=(6, 5))
plt.scatter(x, y, c='coral', edgecolors='black', alpha=0.7, s=60)
plt.title('Scatter Plot')
plt.xlabel('X Values')
plt.ylabel('Y Values')
plt.tight_layout()
plt.show()
```

---

#### 1.3 Bar Chart

**Description:** Compares categorical data using rectangular bars.

**Use Case:** Sales by region, survey results, feature importance scores.

```python
import matplotlib.pyplot as plt

categories = ['Python', 'R', 'Julia', 'Scala', 'Java']
values = [75, 60, 45, 30, 50]

plt.figure(figsize=(7, 4))
plt.bar(categories, values, color='mediumseagreen', edgecolor='black')
plt.title('Programming Language Popularity')
plt.xlabel('Language')
plt.ylabel('Popularity Score')
plt.tight_layout()
plt.show()
```

---

#### 1.4 Histogram

**Description:** Shows the distribution of a single numerical variable by dividing data into bins.

**Use Case:** Examining data distributions, checking normality, detecting skewness.

```python
import matplotlib.pyplot as plt
import numpy as np

data = np.random.normal(loc=50, scale=10, size=1000)

plt.figure(figsize=(7, 4))
plt.hist(data, bins=30, color='slateblue', edgecolor='white', alpha=0.85)
plt.title('Histogram of Normal Distribution')
plt.xlabel('Value')
plt.ylabel('Frequency')
plt.tight_layout()
plt.show()
```

---

#### 1.5 Pie Chart

**Description:** Shows proportional data as slices of a circle.

**Use Case:** Market share, budget breakdowns, composition of categories.

```python
import matplotlib.pyplot as plt

labels = ['Data Collection', 'EDA', 'Modeling', 'Deployment']
sizes = [20, 35, 30, 15]
colors = ['#ff9999', '#66b3ff', '#99ff99', '#ffcc99']

plt.figure(figsize=(6, 6))
plt.pie(sizes, labels=labels, colors=colors, autopct='%1.1f%%', startangle=140)
plt.title('Data Science Project Time Allocation')
plt.tight_layout()
plt.show()
```

---

#### 1.6 Subplots

**Description:** Arrange multiple plots in a grid layout on a single figure.

**Use Case:** Comparing multiple metrics side-by-side, dashboard-style reporting.

```python
import matplotlib.pyplot as plt
import numpy as np

x = np.linspace(0, 10, 100)

fig, axes = plt.subplots(1, 2, figsize=(12, 4))
axes[0].plot(x, np.sin(x), color='blue')
axes[0].set_title('sin(x)')

axes[1].plot(x, np.cos(x), color='red')
axes[1].set_title('cos(x)')

plt.tight_layout()
plt.show()
```

---

## 2. Seaborn

### Overview

Seaborn is a high-level statistical data visualization library built on top of Matplotlib. It provides a more elegant default aesthetic and simplifies the creation of complex statistical plots. It integrates tightly with Pandas DataFrames.

**Typical Use Cases:** Statistical analysis, correlation heatmaps, distribution plots, categorical comparisons in data science workflows.

---

### Graph Types

#### 2.1 Distribution Plot (histplot / kdeplot)

**Description:** Visualizes the distribution of a dataset; can overlay a KDE (Kernel Density Estimate) curve.

**Use Case:** Exploring data distributions, comparing distributions across groups.

```python
import seaborn as sns
import matplotlib.pyplot as plt
import numpy as np

data = np.random.normal(50, 10, 500)

sns.histplot(data, kde=True, color='teal', bins=30)
plt.title('Distribution Plot with KDE')
plt.xlabel('Value')
plt.tight_layout()
plt.show()
```

---

#### 2.2 Box Plot

**Description:** Shows the median, quartiles, and outliers of a distribution.

**Use Case:** Comparing distributions across categories, identifying outliers.

```python
import seaborn as sns
import matplotlib.pyplot as plt

tips = sns.load_dataset('tips')
sns.boxplot(x='day', y='total_bill', data=tips, palette='pastel')
plt.title('Total Bill by Day of Week')
plt.tight_layout()
plt.show()
```

---

#### 2.3 Heatmap

**Description:** Represents matrix data as a color-encoded grid.

**Use Case:** Correlation matrices, confusion matrices, feature relationships.

```python
import seaborn as sns
import matplotlib.pyplot as plt

flights = sns.load_dataset('flights')
pivot = flights.pivot_table(index='month', columns='year', values='passengers')

sns.heatmap(pivot, annot=True, fmt='d', cmap='YlOrRd')
plt.title('Monthly Airline Passengers Heatmap')
plt.tight_layout()
plt.show()
```

---

#### 2.4 Pair Plot

**Description:** Plots pairwise relationships between all numerical variables in a dataset.

**Use Case:** Exploratory data analysis, multivariate feature inspection.

```python
import seaborn as sns
import matplotlib.pyplot as plt

iris = sns.load_dataset('iris')
sns.pairplot(iris, hue='species', palette='Set2')
plt.suptitle('Iris Dataset Pair Plot', y=1.02)
plt.show()
```

---

#### 2.5 Violin Plot

**Description:** Combines a box plot with a KDE; shows the full distribution shape.

**Use Case:** Comparing distributions where shape matters (bimodal, skewed).

```python
import seaborn as sns
import matplotlib.pyplot as plt

tips = sns.load_dataset('tips')
sns.violinplot(x='sex', y='tip', data=tips, palette='muted', inner='quartile')
plt.title('Tip Distribution by Gender')
plt.tight_layout()
plt.show()
```

---

#### 2.6 Bar Plot (Statistical)

**Description:** Shows mean (or other estimate) with confidence intervals for categorical data.

**Use Case:** Comparing average values across groups with uncertainty shown.

```python
import seaborn as sns
import matplotlib.pyplot as plt

tips = sns.load_dataset('tips')
sns.barplot(x='day', y='total_bill', data=tips, palette='Blues_d')
plt.title('Average Total Bill by Day')
plt.tight_layout()
plt.show()
```

---

## 3. Plotly

### Overview

Plotly is a powerful library for creating interactive, web-based visualizations. It supports a wide range of chart types including 3D plots, maps, and financial charts. Plotly Express provides a concise high-level API, while `plotly.graph_objects` gives fine-grained control.

**Typical Use Cases:** Dashboards, web apps (Dash), interactive data exploration, geospatial maps, financial analytics.

---

### Graph Types

#### 3.1 Interactive Line Chart

**Description:** A line chart with hover tooltips, zoom, and pan capabilities.

**Use Case:** Interactive time-series dashboards.

```python
import plotly.express as px
import pandas as pd
import numpy as np

dates = pd.date_range('2024-01-01', periods=90)
values = np.cumsum(np.random.randn(90))
df = pd.DataFrame({'Date': dates, 'Stock Price': values})

fig = px.line(df, x='Date', y='Stock Price', title='Interactive Stock Price')
fig.show()
```

---

#### 3.2 Interactive Scatter Plot

**Description:** Scatter plot with interactive hover, color-coding, and size encoding.

**Use Case:** Exploring relationships in multi-dimensional datasets.

```python
import plotly.express as px

df = px.data.iris()
fig = px.scatter(df, x='sepal_width', y='sepal_length',
                 color='species', size='petal_length',
                 title='Iris Dataset — Interactive Scatter')
fig.show()
```

---

#### 3.3 Bar Chart (Grouped)

**Description:** Grouped bars for comparing multiple categories side by side.

**Use Case:** Quarterly sales comparison across product lines.

```python
import plotly.express as px

df = px.data.tips()
fig = px.bar(df, x='day', y='total_bill', color='sex',
             barmode='group', title='Total Bill by Day and Gender')
fig.show()
```

---

#### 3.4 Distribution Plot (Histogram + KDE)

**Description:** Interactive histogram with optional KDE overlay.

**Use Case:** Inspecting distributions interactively.

```python
import plotly.express as px
import numpy as np

data = np.random.normal(50, 15, 1000)
fig = px.histogram(data, nbins=40, marginal='kde',
                   title='Interactive Distribution Plot')
fig.show()
```

---

#### 3.5 Pie / Donut Chart

**Description:** Interactive pie chart with hover labels.

**Use Case:** Showing proportions interactively in a dashboard.

```python
import plotly.express as px

labels = ['Rent', 'Food', 'Transport', 'Entertainment', 'Savings']
values = [35, 25, 15, 10, 15]

fig = px.pie(values=values, names=labels,
             title='Monthly Budget Allocation', hole=0.3)
fig.show()
```

---

#### 3.6 3D Scatter Plot

**Description:** A 3D scatter plot for visualizing three-dimensional data.

**Use Case:** Clustering in 3D feature space, scientific visualization.

```python
import plotly.express as px

df = px.data.iris()
fig = px.scatter_3d(df, x='sepal_length', y='sepal_width', z='petal_width',
                    color='species', title='3D Iris Scatter Plot')
fig.show()
```

---

## 4. Bokeh

### Overview

Bokeh is a Python library for creating interactive visualizations in web browsers. It targets large and streaming datasets and integrates with web frameworks. Unlike Plotly, Bokeh's output is pure HTML/JavaScript, making it ideal for embedding in custom web applications.

**Typical Use Cases:** Real-time dashboards, web application embedding, large dataset streaming, custom interactive tools.

---

### Graph Types

#### 4.1 Line Plot

**Description:** Interactive line chart with pan, zoom, and hover tools.

**Use Case:** Time-series dashboards, sensor data monitoring.

```python
from bokeh.plotting import figure, show
from bokeh.io import output_notebook
import numpy as np

output_notebook()  # Use output_file('plot.html') for saving

x = np.linspace(0, 4 * np.pi, 200)
y = np.sin(x)

p = figure(title='Bokeh Line Plot', x_axis_label='x', y_axis_label='sin(x)',
           width=700, height=350, tools='pan,zoom_in,zoom_out,reset,hover')
p.line(x, y, line_width=2, color='navy', legend_label='sin(x)')
p.legend.location = 'top_left'
show(p)
```

---

#### 4.2 Scatter Plot

**Description:** Interactive scatter plot with tooltip and selection tools.

**Use Case:** Exploratory analysis with browser-based interactivity.

```python
from bokeh.plotting import figure, show
from bokeh.io import output_notebook
import numpy as np

output_notebook()
np.random.seed(0)
x = np.random.randn(100)
y = x + np.random.randn(100) * 0.5

p = figure(title='Bokeh Scatter Plot', width=600, height=400,
           tools='pan,wheel_zoom,box_select,reset,hover')
p.circle(x, y, size=8, color='firebrick', alpha=0.6)
show(p)
```

---

#### 4.3 Bar Chart

**Description:** Categorical bar chart rendered as interactive HTML.

**Use Case:** Displaying survey results or ranked metrics.

```python
from bokeh.plotting import figure, show
from bokeh.io import output_notebook

output_notebook()
languages = ['Python', 'R', 'Julia', 'Scala']
scores = [85, 65, 50, 40]

p = figure(x_range=languages, title='Language Popularity',
           width=600, height=400, tools='hover')
p.vbar(x=languages, top=scores, width=0.5, color='#4C72B0')
p.xaxis.axis_label = 'Language'
p.yaxis.axis_label = 'Score'
show(p)
```

---

#### 4.4 Patch / Area Plot

**Description:** Shaded area between curves or above/below a baseline.

**Use Case:** Visualizing uncertainty bands, risk ranges.

```python
from bokeh.plotting import figure, show
from bokeh.io import output_notebook
import numpy as np

output_notebook()
x = np.linspace(0, 10, 100)
y_upper = np.sin(x) + 0.5
y_lower = np.sin(x) - 0.5

p = figure(title='Patch / Area Plot', width=700, height=350)
p.varea(x=x, y1=y_lower, y2=y_upper, fill_alpha=0.4, fill_color='green')
p.line(x, np.sin(x), line_width=2, color='darkgreen')
show(p)
```

---

#### 4.5 Multi-line Plot

**Description:** Displays multiple lines simultaneously on one chart.

**Use Case:** Comparing multiple time-series or model outputs.

```python
from bokeh.plotting import figure, show
from bokeh.io import output_notebook
import numpy as np

output_notebook()
x = np.linspace(0, 10, 100)

p = figure(title='Multi-line Plot', width=700, height=350, tools='hover,pan,reset')
p.line(x, np.sin(x), color='blue', legend_label='sin(x)', line_width=2)
p.line(x, np.cos(x), color='red', legend_label='cos(x)', line_width=2)
p.legend.click_policy = 'hide'  # Toggle lines by clicking legend
show(p)
```

---

## 5. Pandas Visualization

### Overview

Pandas includes built-in plotting functionality via the `.plot()` accessor, which wraps Matplotlib under the hood. It is the fastest way to visualize data stored in DataFrames and Series — no extra imports needed. Ideal for quick exploratory analysis directly from your data structures.

**Typical Use Cases:** Quick EDA, rapid prototyping of charts, inline notebook visualizations.

---

### Graph Types

#### 5.1 Line Plot

**Description:** Plots index vs. column values as a line.

**Use Case:** Time-series plotting directly from a DataFrame.

```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt

df = pd.DataFrame({
    'Month': range(1, 13),
    'Sales': np.random.randint(100, 500, 12)
}).set_index('Month')

df.plot(kind='line', title='Monthly Sales', ylabel='Sales', marker='o', figsize=(8, 4))
plt.tight_layout()
plt.show()
```

---

#### 5.2 Bar Chart

**Description:** Horizontal or vertical bar charts directly from a DataFrame column.

**Use Case:** Quick category comparisons.

```python
import pandas as pd
import matplotlib.pyplot as plt

data = pd.Series({'Python': 75, 'R': 60, 'Julia': 45, 'Java': 50}, name='Popularity')
data.plot(kind='bar', color='steelblue', edgecolor='black', figsize=(6, 4))
plt.title('Language Popularity')
plt.xticks(rotation=0)
plt.tight_layout()
plt.show()
```

---

#### 5.3 Histogram

**Description:** Plots distribution of all numeric columns.

**Use Case:** Quick data distribution check during EDA.

```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt

df = pd.DataFrame(np.random.randn(500, 3), columns=['A', 'B', 'C'])
df.plot(kind='hist', bins=25, alpha=0.6, figsize=(8, 4), title='Multi-column Histogram')
plt.tight_layout()
plt.show()
```

---

#### 5.4 Box Plot

**Description:** Box-and-whisker plots for all numeric columns.

**Use Case:** Comparing spread and outliers across features quickly.

```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt

df = pd.DataFrame(np.random.randn(100, 4), columns=['Q1', 'Q2', 'Q3', 'Q4'])
df.plot(kind='box', title='Quarterly Data Distribution', figsize=(7, 4))
plt.tight_layout()
plt.show()
```

---

#### 5.5 Scatter Matrix

**Description:** A matrix of scatter plots for each pair of numeric columns.

**Use Case:** Fast multivariate relationship exploration.

```python
import pandas as pd
from pandas.plotting import scatter_matrix
import numpy as np
import matplotlib.pyplot as plt

df = pd.DataFrame(np.random.randn(100, 4), columns=['W', 'X', 'Y', 'Z'])
scatter_matrix(df, alpha=0.6, figsize=(8, 8), diagonal='hist')
plt.suptitle('Scatter Matrix', y=1.01)
plt.tight_layout()
plt.show()
```

---

## 6. Library Comparison

| Feature | Matplotlib | Seaborn | Plotly | Bokeh | Pandas |
|---|---|---|---|---|---|
| **Ease of Use** | Medium | High | High | Medium | Very High |
| **Interactivity** | Low | Low | Very High | High | Low |
| **Statistical Plots** | Manual | Built-in | Moderate | Manual | Moderate |
| **Aesthetics (default)** | Basic | Polished | Polished | Clean | Basic |
| **Customization** | Very High | High | High | Very High | Limited |
| **Performance (large data)** | Good | Good | Good | Excellent | Good |
| **Web/Dashboard Use** | No | No | Yes (Dash) | Yes | No |
| **3D Support** | Limited (mpl_toolkits) | No | Yes | Limited | No |
| **Learning Curve** | Steep | Gentle | Gentle | Moderate | Minimal |
| **Dependency on Matplotlib** | Core | Yes | No | No | Yes |

---

### Strengths and Weaknesses

#### Matplotlib
- **Strengths:** Maximum control, publication-quality output, widely used in academia, vast documentation.
- **Weaknesses:** Verbose API for complex plots, limited interactivity, dated default aesthetics.

#### Seaborn
- **Strengths:** Beautiful defaults, built-in statistical summaries (CI bands, regression lines), tight Pandas integration.
- **Weaknesses:** Less flexible than Matplotlib for custom layouts, not interactive.

#### Plotly
- **Strengths:** Rich interactivity out-of-the-box, supports 3D/maps/animations, excellent for dashboards via Dash.
- **Weaknesses:** Heavier dependency, can be slower for very large datasets, HTML output may not suit all workflows.

#### Bokeh
- **Strengths:** Superior streaming/real-time support, native HTML/JS output, excellent for embedding in web apps, handles large datasets well.
- **Weaknesses:** Steeper API than Plotly for basic charts, less popular community vs. Plotly.

#### Pandas Visualization
- **Strengths:** Zero extra setup, fast for quick EDA, works directly on DataFrame/Series objects.
- **Weaknesses:** Limited chart types, minimal customization, not suitable for production-quality visuals.

---

### When to Use Which Library

| Scenario | Recommended Library |
|---|---|
| Academic/scientific paper figures | Matplotlib |
| Statistical analysis and EDA with aesthetics | Seaborn |
| Interactive dashboards or web apps | Plotly or Bokeh |
| Real-time / streaming data visualization | Bokeh |
| Quick data exploration in a notebook | Pandas |
| 3D or geospatial visualizations | Plotly |
| Full control over every visual element | Matplotlib |

---

*References:*
- *Matplotlib:* https://matplotlib.org/stable/users/explain/quick_start.html
- *Seaborn:* https://seaborn.pydata.org/tutorial/introduction.html
- *Plotly:* https://plotly.com/python/distplot/
- *Bokeh:* https://docs.bokeh.org/en/latest/docs/user_guide/basic.html
- *Pandas:* https://pandas.pydata.org/docs/user_guide/index.html
