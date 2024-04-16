# Advanced Pandas - Transforming Dataframes

## Table of Contents
1. [Groupby and aggregations using pandas](#groupby-and-aggregations-using-pandas)
2. [Reshaping dataframes (pivot, stack)](#reshaping-dataframes-pivot-stack)
3. [Merging (merge, join) dataframes](#merging-merge-join-dataframes)
4. [Concatenating (concat) dataframes](#concatenating-concat-dataframes)
5. [Mapping variables into groups](#mapping-variables-into-groups)

### Groupby and aggregations using pandas
```python
# Import the pandas library and assign it the alias 'pd'
import pandas as pd

# Import the 'warnings' module
# This module provides facilities for issuing warnings from Python code
# Warnings are typically used to alert users about potential issues or unexpected behavior

import warnings
warnings.simplefilter(action='ignore', category=FutureWarning)

# Load the Iris dataset from the specified CSV file into the DataFrame 'iris_df'.
# This step involves importing data from an external source, which is a fundamental task in data analysis.
# The dataset contains measurements of iris flowers, a classic dataset frequently used in data science education.

iris_df = pd.read_csv('../iris.csv')

# Display the first 5 rows of the DataFrame 'iris_df' to inspect the data.
# Inspection of the initial rows provides an introductory overview of the dataset's structure and contents.
# This allows for a preliminary assessment of data quality, identifying potential issues or anomalies.
# Understanding the dataset's layout is crucial for formulating analysis strategies and interpreting results.

iris_df.head(5)

#### A simple groupby on one dimension with one aggregation for all variables

# Group the DataFrame 'iris_df' by the 'species' column 
# This groups the data by the different species of iris flowers, allowing for species-wise analysis
# The `.groupby()` method is used to group the DataFrame based on unique values in the 'species' column

# Calculate the maximum value for each group within each column
# This calculates the maximum value for each numerical column within each species group
# The `.max()` method is applied to each group to find the maximum value

# The result is a DataFrame containing the maximum values for each numerical column within each species group
# This summary provides insights into the maximum measurements for each feature across different species of iris flowers
iris_df.groupby(['species']).max()

#### Multiple aggregation methods to different variables

# Group the DataFrame 'iris_df' by the 'species' column and aggregate the data
# This groups the data by the different species of iris flowers for further analysis
# The `.groupby()` method is used to group the DataFrame based on unique values in the 'species' column

# Aggregate the data by calculating the mean, minimum, and maximum values of 'sepal_length' for each species
# Additionally, count the number of occurrences of 'sepal_width' for each species
# The `.agg()` method is applied to perform aggregation on specific columns using a dictionary

# The resulting DataFrame 'df' contains:
# - Mean, minimum, and maximum values of 'sepal_length' for each species
# - Number of occurrences of 'sepal_width' for each species
# This summary provides insights into the average sepal length, range of sepal length, and sepal width count for each species
df = iris_df.groupby(['species']).agg({'sepal_length':['mean', 'min', 'max'], 'sepal_width':'count'})

# Display the aggregated DataFrame 'df'
df

# Select the 'sepal_length' column from the DataFrame 'df'
# This extracts the 'sepal_length' column from the aggregated DataFrame 'df'
# The column can be accessed using bracket notation with the column name as the key

# The result is a Series containing the 'sepal_length' values for each species
# This allows for further analysis or visualization specifically focusing on sepal length across different species
df['sepal_length']

#### Flattening hierarchical indexes

# Concatenate multi-level column names into a single string with '_' separator and strip any leading/trailing whitespace
# This operation simplifies the column names, making them easier to work with and reference in subsequent analysis
# The list comprehension iterates over each column name and applies the '_'.join(col).strip() function to concatenate the names

# Reset the DataFrame index to default integer index
# This operation resets the index, removing any existing index labels and reverting to the default integer index
# The index reset ensures consistency and facilitates further data manipulation or analysis

# Note: The DataFrame 'df' is not reassigned with the result of the reset_index() operation
# As a result, the DataFrame remains unchanged, and the index reset is not reflected in subsequent operations
df.columns = ['_'.join(col).strip() for col in df.columns.values]
df.reset_index()

# The DataFrame 'df' is not reassigned with the result of the reset_index() operation, 
# so the DataFrame remains unchanged after executing this code snippet
df

#### Specify groupings prior to any aggregation

# Group the DataFrame 'iris_df' by the 'species' column
# This step divides the data into separate groups based on the unique values in the 'species' column
# Grouping facilitates analysis and comparison of data within each species category

groupings = iris_df.groupby(['species'])

# Retrieve the group corresponding to the 'setosa' species from the grouped DataFrame 'groupings'
# This operation extracts the subset of data specific to the 'setosa' species for further examination
# The `.get_group()` method is used to access the data associated with a particular group

groupings.get_group('setosa').head()

# Calculate the maximum value for each numerical column within each group in the grouped DataFrame 'groupings'
# This operation computes the maximum value for each numerical column (e.g., sepal_length, sepal_width, petal_length, petal_width)
# within each group defined by the 'species' column

groupings.max()

# Apply a function to each group in the grouped DataFrame 'groupings' to calculate the maximum value for each column
# This operation applies a custom function to each group, which computes the maximum value for each column within the group
# The `include_groups=False` parameter specifies that the function should not include the group keys in the result

groupings.apply(lambda x: x.max(), include_groups=False)


# Filter the groups in the grouped DataFrame 'groupings' based on a condition
# This operation applies a custom function to each group, which checks if the maximum value of 'petal_length' within the group is less than 5
# Groups for which the condition is True are retained, while others are filtered out

groupings.filter(lambda x: x['petal_length'].max() < 5)
```

### Reshaping dataframes (pivot, stack)

### Merging (merge, join) dataframes

### Concatenating (concat) dataframes

### Mapping variables into groups