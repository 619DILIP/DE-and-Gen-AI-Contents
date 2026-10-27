# Cumulative for matplotlib

<details><summary>Learning Objectives</summary>

# Learning Objectives
After completing this module, associates should be able to:

- Describe what matplotlib is and when to use it
- Create basic plots using `matplotlib.pyplot` (line, bar, scatter, histogram)
- Customize plots with titles, axis labels, legends, and figure size
- Save plots to image files for reports or presentations
- Understand how matplotlib works together with NumPy and pandas

</details>

<details><summary>Description</summary>

# What is matplotlib?

**matplotlib** is a widely used Python library for creating static, animated, and interactive visualizations.

Most of the time, beginners interact with it through the **`matplotlib.pyplot`** module, usually imported as `plt`. It provides functions that feel similar to plotting tools in other environments (like MATLAB or Excel charts).

Key points:

- Works very well with **NumPy** arrays and **pandas** data structures.
- Can create many types of plots: line charts, bar charts, scatter plots, histograms, pie charts, and more.
- Allows detailed customization of almost every visual aspect (colors, markers, line styles, axes, annotations, etc.).
- Can display plots in a window or export them as images (PNG, JPG, PDF, etc.).

matplotlib is often the **foundational plotting library** in the Python data stack; many higher-level libraries (like `seaborn` and `pandas.plot`) are built on top of it.

</details>

<details><summary>Real World Application</summary>

# Real World Application for matplotlib

matplotlib is used whenever we need to **visualize data** to understand patterns, communicate findings, or debug computations. Examples:

- **Data analysis and reporting**  
  Plotting trends, distributions, and comparisons (e.g., monthly sales, website traffic, system metrics).

- **Scientific and engineering work**  
  Visualizing experimental results, simulation outputs, and mathematical functions.

- **Machine learning workflows**  
  Inspecting training curves, feature distributions, confusion matrices, or model predictions.

- **Business dashboards or presentations**  
  Generating figures that are included in PowerPoint slides, PDFs, or web apps.

In practice, you will often:

1. Load or compute data (using Python, NumPy, or pandas).
2. Use matplotlib to turn that data into charts.
3. Share those charts with others or embed them into documentation.

</details>

<details><summary>Implementation</summary>

# Implementation

## Installing and Importing matplotlib

If matplotlib is not already available in your environment, it can be installed with:

```bash
pip install matplotlib
```

The most common import pattern uses `pyplot` as `plt`:

```python
import matplotlib.pyplot as plt
import numpy as np
```

NumPy is often used to generate or transform numerical data for plotting.

---

## Creating a Simple Line Plot

A basic example: plotting a function `y = x ** 2`:

```python
import matplotlib.pyplot as plt
import numpy as np

# Create some data
x = np.array([0, 1, 2, 3, 4])
y = x ** 2

# Create a line plot
plt.plot(x, y)

# Add labels and title
plt.xlabel("x")
plt.ylabel("y = x^2")
plt.title("Simple Line Plot")

# Display the plot
plt.show()
```

Here, `plt.show()` opens a window (or inline view in some environments) to display the figure.

---

## Bar, Scatter, and Histogram Examples

### Bar Chart

```python
import matplotlib.pyplot as plt

categories = ["A", "B", "C"]
values = [10, 15, 7]

plt.bar(categories, values)
plt.xlabel("Category")
plt.ylabel("Value")
plt.title("Example Bar Chart")

plt.show()
```

### Scatter Plot

```python
import matplotlib.pyplot as plt
import numpy as np

x = np.array([1, 2, 3, 4, 5])
y = np.array([5, 4, 3, 4, 5])

plt.scatter(x, y)
plt.xlabel("X")
plt.ylabel("Y")
plt.title("Example Scatter Plot")

plt.show()
```

### Histogram

```python
import matplotlib.pyplot as plt
import numpy as np

data = np.random.normal(loc=0, scale=1, size=1000)

plt.hist(data, bins=30)
plt.xlabel("Value")
plt.ylabel("Frequency")
plt.title("Histogram of Normally Distributed Data")

plt.show()
```

---

## Figures and Axes

For more control, use the **Figure / Axes** API:

```python
import matplotlib.pyplot as plt
import numpy as np

x = np.linspace(0, 2 * np.pi, 100)
y_sin = np.sin(x)
y_cos = np.cos(x)

fig, ax = plt.subplots()  # Create a Figure and an Axes

ax.plot(x, y_sin, label="sin(x)")
ax.plot(x, y_cos, label="cos(x)")

ax.set_xlabel("x")
ax.set_ylabel("Value")
ax.set_title("Sine and Cosine")
ax.legend()

plt.show()
```

This pattern is especially common in more complex figures (multiple subplots, custom layout, etc.).

---

## Saving a Figure

Instead of (or in addition to) displaying a plot, you can save it to a file:

```python
import matplotlib.pyplot as plt
import numpy as np

x = np.linspace(0, 10, 50)
y = 2 * x + 1

plt.plot(x, y)
plt.xlabel("x")
plt.ylabel("y")
plt.title("Line Plot to Save")

# Save before or after plt.show()
plt.savefig("line_plot.png")   # Saves to current working directory

plt.show()
```

This is useful for reports, documentation, or web pages that need static images.

</details>

<details><summary>Summary</summary>

# Summary

* **matplotlib** is a core Python library for creating visualizations.
* It is most commonly used through the `matplotlib.pyplot` interface, imported as `plt`.
* matplotlib integrates tightly with **NumPy** and **pandas** and is the foundation for many higher-level plotting tools.
* You can create many plot types (line, bar, scatter, histogram, etc.) with just a few lines of code.
* Customization options include titles, axis labels, legends, figure size, and more.
* Plots can be displayed interactively with `plt.show()` or saved to image files with `plt.savefig()`.

</details>

<details><summary>Practice Questions</summary>

[Practice Questions](./Quiz.gift)

</details>