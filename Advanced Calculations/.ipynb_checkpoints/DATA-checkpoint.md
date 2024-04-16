# Advanced Pandas - Advanced Calculations

## Working with missing data
```python
# Import the pandas library and assign it the alias 'pd'
import pandas as pd

import warnings
# Suppress FutureWarning messages
warnings.simplefilter(action='ignore', category=FutureWarning)

# Create a pandas DataFrame 'temps_df' containing temperature measurements

# The DataFrame consists of three columns:
    # 'sequence': Sequence numbers for the measurements.
    # 'measurement_type': Type of measurement ('actual' or 'estimated').
    # 'temperature_f': Temperature values in Fahrenheit.
temps_df = pd.DataFrame({
    "sequence": [1, 2, 3, 4, 5],  # Sequence numbers
    "measurement_type": ['actual', 'actual', 'actual', None, 'estimated'],  # Type of measurement
    "temperature_f": [67024, 84.56, 91.61, None, 49.64]  # Temperature values in Fahrenheit
})

# Display the DataFrame 'temps_df'
temps_df

## Using isna() to identify null values in a dataframe

# Check for missing values (NaNs) in the DataFrame 'temps_df'

# The output will be a DataFrame of the same shape as 'temps_df',
# where each cell contains True if the corresponding value in 'temps_df' is NaN, 
# and False otherwise.
temps_df.isna()

## How is missing data handled?

# Calculate the cumulative sum of the 'temperature_f' 
# column in the DataFrame 'temps_df'

# The output will be a Series containing the cumulative sum of the 
#'temperature_f' column. Each value represents the sum of all previous 
# temperature values along the column.
temps_df['temperature_f'].cumsum()

# Calculate the cumulative sum of the 'temperature_f' column 
# in the DataFrame 'temps_df', including NaN values

# The output will be a Series containing the cumulative sum of the 
# 'temperature_f' column, where NaN values are treated as NaNs in the calculation.
temps_df['temperature_f'].cumsum(skipna=False)

# Group the DataFrame 'temps_df' by the 'measurement_type' 
# column and calculate the maximum value for each group

# The output will be a DataFrame with 'measurement_type' as the index and the 
# maximum value of 'sequence' and 'temperature_f' columns for each group. Since 
# 'sequence' is a numerical column, the maximum value is the largest sequence 
# number in each group. For 'temperature_f', the maximum value will be the largest # temperature value in each group.
temps_df.groupby(by=['measurement_type']).max()

# Retain NA dimensions in grouping
temps_df.groupby(by=['measurement_type'], dropna=False).max()

### Dealing with missing data: The blunt approach using dropna()

# Remove rows with missing values (NaNs) from the DataFrame 'temps_df'
# using axis=0 (default)
temps_df.dropna()

# Remove columns with missing values (NaNs) from the DataFrame 'temps_df'

# The axis=1 parameter specifies that columns should be checked for missing 
# values and dropped if any are found.
temps_df.dropna(axis=1)

### Replace null values using fillna()

# Replace missing values (NaNs) in the DataFrame 'temps_df' with zeros
temps_df.fillna(0)

# Replace missing values (NaNs) in the DataFrame 'temps_df' 
# with the preceding non-null value along each column

# The fillna(method='pad') method, also known as forward fill, fills missing values 
# in 'temps_df' with the value from the previous row along each column. If the 
# first row contains NaNs, they will remain unchanged.
temps_df.fillna(method='pad')

### Interpolate

temps_df.interpolate()

# Perform linear interpolation to fill in missing values 
# (NaNs) in the DataFrame 'temps_df'

# The interpolate() method fills missing values in 'temps_df' by linear
# interpolation along each column. It computes intermediate values based on the 
# neighboring data points, providing a smooth transition between them.
temps_df.interpolate()
```