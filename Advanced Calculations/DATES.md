# Advanced Pandas - Advanced Calculations

## Working with Dates
```python
# Import the pandas library and assign it the alias 'pd'
import pandas as pd

## Generate series of dates with period_range

# Create a pandas PeriodIndex 'daterange_df' with a frequency of 30 days, 
# starting from May 1, 2024, and consisting of 4 periods
daterange_df = pd.period_range('5/1/2024', freq='30d', periods=4)

# Create a pandas DataFrame 'date_df' with a single column 'sample date' 
# containing the values from 'daterange_df'
date_df = pd.DataFrame(data=daterange_df, columns=['sample date'])

# The resulting DataFrame 'date_df' will have a single column named 'sample date', 
# with each row containing a value from the 'daterange_df' PeriodIndex.

# Display the DataFrame 'date_df'
date_df

## Date difference from prior date using diff

# Import the 'warnings' module to manage warnings in Python
import warnings

# Suppress RuntimeWarning warnings
# Filter out RuntimeWarning warnings and ignore them
warnings.filterwarnings('ignore', category=RuntimeWarning)
warnings.simplefilter(action='ignore', category=pd.errors.PerformanceWarning)


# Calculate the difference between consecutive values 
# in the 'sample date' column and add it as a new column 'date difference'
date_df['date difference'] = date_df['sample date'].diff(periods=1)

# The resulting DataFrame 'date_df' will have an additional column named 
# 'date difference', which represents the difference between consecutive 
# dates in the 'sample date' column.

# Display the updated DataFrame 'date_df'
date_df

## Find the first day of the month

# Create a new column 'first of month' containing the first day of 
# the month corresponding to each date in the 'sample date' column
date_df['first of month'] = date_df['sample date'].values.astype('datetime64[M]')

# This code will populate the 'first of month' column with the first day of the 
# month for each date in the 'sample date' column.

# Display the updated DataFrame 'date_df'
date_df

## Date types

date_df.dtypes

# Convert the 'sample date' column to datetime format
date_df['sample date'] = date_df['sample date'].astype('datetime64[ns]')

# Display the data types of columns in the DataFrame 'date_df'
date_df.dtypes

## Date Subtraction

# Calculate the difference between each date in the 'sample date'
# column and the corresponding first day of the month

# The output will be a Series representing the difference in days between each date in the
# 'sample date' column and the corresponding first day of the month in the 'first of month' column.
date_df['sample date'] - date_df['first of month']

# Calculate the difference between each date in the 'sample date' column 
# and the corresponding value in the 'date difference' column

# The output will be a Series representing the result of subtracting the values in the 
# 'date difference' column from the corresponding values in the 'sample date' column.
date_df['sample date'] - date_df['date difference']


# Subtract a timedelta of 30 days from each value in the 'sample date' column

# The output will be a Series containing the result of subtracting 
# 30 days from each value in the 'sample date' column.
date_df['sample date'] - pd.Timedelta('30 d')

## More datetime properties with dt

# Extract the name of the day of the week for each date in the 'sample date' column

# The output will be a Series containing the name of the day of the week
#  (e.g., 'Monday', 'Tuesday', etc.) for each date in the 'sample date' column.
date_df['sample date'].dt.day_name()

```