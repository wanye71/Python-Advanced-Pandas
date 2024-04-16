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
```python
# Import the pandas library and assign it the alias 'pd'
import pandas as pd

# Constructing a DataFrame 'df' to represent financial data pertaining to various regions, teams, and squads within a political organization
# This DataFrame serves as a structured repository for financial information, enabling systematic analysis and evaluation

df = pd.DataFrame({
    "Region": ['North', 'West', 'East', 'South', 'North', 'West', 'East', 'South'],  
    # Enumeration of geographical regions where financial transactions occur, encompassing a comprehensive geographic scope
    "Team": ['Republicans', 'Republicans', 'Republicans', 'Republicans', 'Democrats', 'Democrats', 'Democrats', 'Democrats'],  
    # Categorization of teams within each region, delineated by their respective political affiliations
    "Squad": ['A', 'B', 'C', 'D', 'E', 'F', 'G', 'H'],  
    # Identification of squads within each team, designated by alphabetical labels for distinctiveness
    "Revenue": [7500, 5500, 2750, 6400, 2300, 3750, 1900, 575],  
    # Quantification of revenue generated by each squad, denominated in monetary units for financial clarity
    "Cost": [5200, 5100, 4400, 5300, 1250, 1300, 2100, 50]  
    # Computation of costs incurred by each squad, expressed in monetary terms to elucidate financial expenditures
})

# Displaying the DataFrame 'df' encapsulating the financial dataset, thereby enabling comprehensive examination and scrutiny of financial metrics
df

# Performing a pivot operation on DataFrame 'df' to reshape the financial data
# This operation reorganizes the data by pivoting the values in the 'Revenue' column, with 'Region' as index and 'Team' as columns
# The pivot creates a new DataFrame that presents revenue data categorized by regions and teams

df.pivot(index='Region', columns='Team', values='Revenue')

<center><h1>Stack</h1></center>

# Picture this, my dear! We're setting the stage for a captivating journey through our financial data.
# By setting the index to a delightful combination of 'Region' and 'Team', we're creating a roadmap for our adventure.
# This magical transformation brings clarity and intimacy to our exploration, allowing us to dive deep into the heart of each region-team duo.
# Now, every row becomes a unique tale, where the 'Region' sets the scene and the 'Team' adds its own colorful twist.
# It's a harmonious union, my love, where we can unravel the intricate stories behind each revenue figure, guided by the enchanting duo of 'Region' and 'Team'.

df2 = df.set_index(['Region', 'Team'])

# Ok, y'all, let's add a twist to our tale! We're about to uncover the hidden depths of our financial data.
# By stacking the DataFrame 'df2', we're orchestrating a mesmerizing transformation.
# The `stack` function reshapes the DataFrame from wide to long format, combining the 'Revenue' and 'Cost' columns into a single column and adding a new hierarchical index with 'Region' and 'Team'.
# Each row will now reveal a captivating glimpse into the interwoven layers of our financial narrative.
# It's like weaving a tapestry of information, where every thread holds its own story, waiting to be unraveled.
# The resulting DataFrame 'stacked' will display the combined revenue and cost data for each region-team combination, providing a detailed view of the financial performance across different teams and regions.

stacked = pd.DataFrame(df2.stack())
stacked

<center><h1>Unstack</h1></center>

# Darling, let's dive right in! After stacking up our DataFrame and delving into the treasure trove of financial insights, it's time for a delightful twist.
# We've uncovered all these fascinating stories about revenue and cost for each region and team, and now we're simply spreading them out again.
# Picture it like unstacking a deck of cards, revealing each card's unique story with effortless grace.
# This clever maneuver effortlessly reverses the stacking we did earlier, restoring our DataFrame to its original wide format.
# Each row will now effortlessly display the 'Revenue' and 'Cost' for a specific team within each region, just as it did before.

unstacked = stacked.unstack()
unstacked

# Ok, darling, let's continue our exploration! Now, after stacking up our DataFrame and uncovering those enchanting financial insights, it's time for another captivating move.
# We're unstacking once more, but this time we're focusing on the 'Region' dimension, adding a touch of finesse to our storytelling.
# Imagine it like rearranging a puzzle, effortlessly slotting each piece into its rightful place to reveal the bigger picture.
# This operation gracefully reverses the stacking we did earlier, providing a fresh perspective on our financial narrative.
# Each column will now effortlessly display the 'Revenue' and 'Cost' for a specific team within each region, allowing us to explore the data with even greater clarity.

unstacked = stacked.unstack(['Region'])
unstacked

<center><h1>Melt</h1></center>

# Ok, darling, let's take a peek at the beginning of our adventure! Here, we're diving into the first few rows of our DataFrame to get a taste of what lies ahead.
# Each row represents a unique combination of 'Region', 'Team', and 'Squad', offering a glimpse into the intricate tapestry of our financial data.
# It's like peeking through a window into a world of financial insights, where each row tells its own captivating story.
# With this quick glance, we can start to piece together the bigger picture and uncover the patterns hidden within our data.

df.head(3)

# Ah, darling, let me tell you a story! Our DataFrame is like a treasure map, holding secrets and riches within its wide expanse.
# But to uncover its true treasures, we must embark on a journey of transformation.

# Our trusty guide in this adventure is the melt function, known for its magical powers to reshape DataFrames.
# With each invocation, it opens new pathways, turning the wide expanse of our DataFrame into a winding path of possibilities.

# We choose to preserve our anchors, 'Region' and 'Team', like steadfast companions on our quest.
# These columns remain untouched, serving as beacons of familiarity in a sea of change.

# And as we traverse this newly forged path, we name our discoveries with care. 'value type' becomes the moniker for the melted values,
# each one a piece of the puzzle waiting to be deciphered.

# With each step forward, our DataFrame reveals new dimensions, new stories to unravel. It's a journey of discovery, a quest for insight into the heart of our data.

# The melt function reshapes our DataFrame, converting it from wide to long format.
# The id_vars parameter specifies the columns to be preserved during reshaping, ensuring they remain unchanged in the melted DataFrame.
# Here, 'Region' and 'Team' serve as our steadfast anchors, guiding us through the transformation.
# The value_name parameter sets the name for the new column that will store the melted values.
# We've chosen 'value type' to represent the type of data contained in each melted value.

melted_df = df.melt(id_vars=['Region', 'Team'], value_name='value type')
melted_df

## Supporting aggregation with pivot_table

# Alright, let's explore another facet of our data journey! Here, we're creating a pivot table called 'pivot_df' from our DataFrame.

# Think of it as reshaping our data to gain new perspectives. We're focusing on the 'Team' column as the index,
# which will serve as the row labels in our pivot table.

# The pivot_table() function is like a magic wand that transforms our data into a more structured format,
# making it easier to analyze and extract meaningful insights.

# By specifying the 'Revenue' column as the values, we're interested in understanding revenue trends across different teams.
# This will allow us to uncover patterns and identify which teams are generating the most revenue.

# With each pivot, we unlock new layers of understanding, like peeling back the petals of a flower to reveal its beauty.

# The pivot_table() function reshapes our DataFrame into a pivot table, providing a structured view of our data.
# The (index) parameter specifies the column to be used as the index (or row labels) in the pivot table.
# The (values) parameter specifies the column to be used as the values in the pivot table.

pivot_df = df.pivot_table(index='Team', values='Revenue')
pivot_df

# Ok, darling, let's dive into the next chapter of our adventure! This time, we're creating a pivot table from our DataFrame.
# Picture it like rearranging pieces on a chessboard, where each row represents a 'Team' and each column represents a 'Region'.

# The pivot_table() function helps us organize our data in a more structured format, making it easier to analyze and interpret.

# Here, we're using 'Team' as the index, 'Region' as the columns, and 'Revenue' as the values.
# This arrangement allows us to see how revenue is distributed across different teams and regions, painting a clearer picture of our financial landscape.

# With each pivot, our DataFrame takes on new dimensions, revealing insights and patterns that were previously hidden.
# It's like assembling a puzzle, where each piece adds to the larger picture of our data story.

# The pivot_table() function reshapes our DataFrame into a pivot table, providing a structured view of our data.
# The (index) parameter specifies the column to be used as the index in the pivot table:
# The (columns) parameter specifies the column to be used as the columns in the pivot table:
# The (values) parameter specifies the column to be used as the values in the pivot table:

pivot_df = df.pivot_table(index='Team', columns='Region', values='Revenue')
pivot_df
```

### Merging (merge, join) dataframes
```python

```

### Concatenating (concat) dataframes
```python

```

### Mapping variables into groups
```python

```