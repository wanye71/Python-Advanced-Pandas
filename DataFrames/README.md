# Advanced Pandas - Functions

## Top functions using Pandas 
```python
# Import the pandas library and assign it the alias 'pd'
import pandas as pd

## Import CSV with pd.read_csv()

# Read the CSV file 'iris.csv' located in the parent directory and create 
# a DataFrame named 'iris_df'
iris_df = pd.read_csv('../iris.csv')

## Explore the data

# Output: The dimensions (number of rows, number of columns)
# of the DataFrame 'iris_df'
iris_df.shape

# Display the first 3 rows of the DataFrame 'iris_df'
iris_df.head(3)

# Display the last 3 rows of the DataFrame 'iris_df'
iris_df.tail(3)

## Datatypes

# Display the data types of each column in the DataFrame 'iris_df'
iris_df.dtypes

## Subsetting your data with loc & iloc

# Select rows with index labels from 3 to 5 (inclusive) from 
# the DataFrame 'iris_df'
iris_df.loc[3:5]

# Select the value in the 'sepal_length' column of the row with index
# label 3 in the DataFrame 'iris_df'
iris_df.loc[3, 'sepal_length']

iris_df.iloc[3,0]

# Select the value in the first column (index 0) of the 
# fourth row (index 3) in the DataFrame 'iris_df'
iris_df.iloc[3, 0]

## Exporting your data as csv using to_csv

# Export the DataFrame 'iris_df' to a CSV file named 'iris_output.csv' 
# without including the index
iris_df.to_csv('iris_output.csv', index=False)
```