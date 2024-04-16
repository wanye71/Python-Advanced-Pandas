# Advanced Pandas - Exploratory Data Analysis and Visualization

## Table of Contents
1. [Plotting with pandas](#plotting-with-pandas)
2. [Correlations and statistical functions](#correlations-and-statistical-functions)




### Plotting with pandas
```python
# Time to dive into the world of pandas and numpy as we prepare for some inline plotting magic!
# With pandas by our side, and numpy powering our calculations, we're ready to visualize our data inline.

# Get ready to plot like a pro as we unleash the power of inline plotting:
# - We're importing pandas as 'pd' and numpy as 'np' to harness their formidable data manipulation and numerical computing capabilities.
# - By including '%matplotlib inline', we're activating inline plotting in Jupyter Notebook, allowing us to see our plots right below our code cells.

# Hold onto your fishing rods as we cast our line into the data stream and explore the underwater world of inline plotting!
import pandas as pd
import numpy as np

%matplotlib inline

# Time to embark on a journey through time with pandas as we create a date range and generate some random data!
# With pandas as our time-traveling companion and numpy as our random number generator, we're ready to explore the temporal landscape.

# Get ready to step into the past as we craft a period range and fill it with random data:
# - We're using 'pd.period_range' to create a range of dates starting from December 11, 1971, with a daily frequency and a total of 50 periods.
# - This range of dates will serve as the temporal backbone of our DataFrame, allowing us to travel through time.
# - We're then creating a DataFrame 'date_df' with the date range as the 'day' column and two additional columns, 'value1' and 'value2', filled with random integers.

# Hold onto your time machines as we take our first leap into the past and glimpse at the early days of our DataFrame!
daterange = pd.period_range('12/11/1971', freq='1d', periods=50)
date_df = pd.DataFrame(data=daterange, columns=['day'])
date_df['value1'] = np.random.randint(45, 65, size=(len(date_df)))
date_df['value2'] = np.random.randint(25, 35, size=(len(date_df)))
date_df.head(3)

# It's showtime! We're about to let our data take center stage with a stunning plot.
# Brace yourselves for a visual spectacle as we summon the power of pandas to create a captivating display.

# Drumroll, please! With a flick of our coding wand, behold the magnificent plot!
ax = date_df.plot();

# Behold the majestic area plot born from the depths of 'date_df'!
# This plot emerges like a phoenix, with each area representing a dimension of data glory.
# By setting 'stacked' to False, we ensure that each area stands tall and proud, 
# unfettered by the weight of its data brethren.
date_df.plot.area(stacked=False)

# Prepare yourself for the grand entrance of our floral dataset, straight from the mystical realms of '../iris.csv'!
# As pandas takes the stage, it gracefully loads the CSV file into the variable 'iris', 
# ready to dazzle us with its botanical wonders.
iris = pd.read_csv('../iris.csv')

# Hold onto your gardening gloves as we summon the magic of pandas to conjure up a magnificent histogram!
# With a flick of its wand, pandas transforms the 'iris' DataFrame into a visual masterpiece,
# showcasing the distribution of its numerical columns in all their floral glory.
iris.hist();

# Ah, the beguiling dimensions of sepal width and length! These two attributes are fundamental measurements captured from the sepals of iris flowers, 
# serving as crucial descriptors in the realm of botanical classification.

# - Sepal Width: This dimension refers to the breadth or width of the sepal, typically measured in millimeters. It provides insight into the overall 
# girth of the sepal structure and plays a role in determining the flower's robustness.

# - Sepal Length: As the name suggests, sepal length measures the longitudinal extent of the sepal, also usually expressed in millimeters. It offers 
# a glimpse into the elongation or size of the sepal relative to other floral parts, aiding in the differentiation of iris species.

# Together, these two dimensions provide valuable botanical data, helping botanists and researchers distinguish between different species of iris 
# based on their sepal characteristics.

# Now, let's dive into the histogram plot to visualize the distribution of these dimensions!
iris[['sepal_width', 'sepal_length']].plot.hist(alpha=0.5);

# Alright, let's add some color to our scatter plot! Who said data visualization can't be stylish?

# First up, we define a dictionary 'colors' mapping each species to a specific color.
# Each color is represented as a hexadecimal code, ensuring our plot will be vibrant and eye-catching!
colors = {"versicolor":"#ff1500", "setosa":"#008000", "virginica":"#0000ff"}

# Now, we're going to create a new column in our DataFrame called 'colors'.
# We'll use the 'map' function to map each species in the 'species' column to its corresponding color from the 'colors' dictionary.
iris['colors'] = iris['species'].map(colors)

# It's time to plot! We're using the 'plot.scatter' function to create a scatter plot of sepal width versus sepal length.
# We're specifying the 'x' and 'y' parameters to set the variables for the x-axis and y-axis, respectively.
# To add some flair, we're using the 'color' parameter to specify the color of each point in the scatter plot.
# We're passing in the 'colors' column we created earlier, ensuring each species is represented by its designated color.
# The 'plot.scatter' function automatically uses the colors from the 'colors' column to color each point.
iris.plot.scatter(x='sepal_width', y='sepal_length', color=iris['colors']);


# Alright, time to up the ante with some serious plotting action! We're importing the scatter_matrix function from pandas.plotting module,
# ready to unleash a visual whirlwind of scatter plots and correlations.

# Buckle up as we prepare to dive deep into the data, exploring the relationships between different features of the Iris dataset.

from pandas.plotting import scatter_matrix


# Alright, let's dive into some data exploration with a scatter matrix plot!
# Scatter matrix plots are a powerful tool for visualizing relationships between multiple variables in a dataset.

# Now, we're going to create a scatter matrix plot for the Iris dataset.
# This dataset contains information about different species of iris flowers and their characteristics.

# To create the scatter matrix plot, we'll use the scatter_matrix function from the pandas.plotting module.
# This function takes the DataFrame 'iris' as input and generates a matrix of scatter plots for each pair of variables.

# We're also specifying the 'figsize' parameter to control the size of the plot.
# The 'figsize' parameter is a tuple specifying the width and height of the plot in inches.
# In this case, we're setting it to (15, 9), which means the plot will be 15 inches wide and 9 inches tall.

# Get ready for some visually stunning data exploration as we unveil the scatter matrix plot!
scatter_matrix(iris, figsize=(15, 9));
```

### Correlations and statistical functions
```python

```