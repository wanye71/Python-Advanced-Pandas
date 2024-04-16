# Advanced Pandas - Data type Conversions

## Data Types
```python
# Import the pandas library and assign it the alias 'pd'
import pandas as pd

# Read the CSV file 'planets.csv' located in the parent directory and create 
# a DataFrame named 'planets_df'
planets_df = pd.read_csv('../planets.csv')

# Display the first 3 rows of the DataFrame ''
planets_df.head(3)

# Display the data types of each column in the DataFrame
planets_df.dtypes

# Compute the mean values of numeric columns in the DataFrame 'planets_df'
planets_df.mean(numeric_only=True)

# Calculate the ratio of the value in the 'number' column at index 0 to 
# the value in the 'mass' column at index 0
planets_df['number'][0] / planets_df['mass'][0]

# Convert the value in the 'number' column at index 0 to a floating-point number
planets_df['number'][0].astype(float)

# Convert the value in the 'mass' column at index 0 to an integer
planets_df['mass'][0].astype(int)

# Convert the value in the 'year' column at index 0 to a string
planets_df['year'][0].astype(str)

# Create a new column 'year_td' in the DataFrame 'planets_df' with datetime objects containing only the year component
planets_df['year_td'] = pd.to_datetime(planets_df['year'], format='%Y')
# Retrieve the values stored in the 'year_td' column of the DataFrame 'planets_df'
planets_df['year_td']
```