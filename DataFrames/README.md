# Advanced Pandas - Options

## Configuring options using pandas
```python
# Import the pandas library and assign it the alias 'pd'
import pandas as pd

# Create a new DataFrame 'emissions' containing information about 
# CO2 emissions for different countries and years
emissions = pd.DataFrame({
    "country": ['China', 'United States', 'India'],
    "year": ['2018', '2018', '2018'],
    "co2_emissions": [10060000000.0, 5410000000.0, 2650000000.0]
})

# Display the DataFrame 'emissions'
emissions

# Set the maximum number of rows to display to 2
pd.set_option('display.max_rows', 2)

# Display the DataFrame 'emissions'
emissions

# Set the maximum number of columns to display to 2
pd.set_option('display.max_columns', 2)

# Display the DataFrame 'emissions'
emissions

# Set the floating-point formatting for displaying DataFrame floats to two decimal places
# This ensures that floating-point numbers in the DataFrame are displayed with exactly two decimal places

# '{:,.2f}': This part is a format string specifying how the floating-point number should be formatted. Here's what each part means:
# {}: This indicates a placeholder for the value to be formatted.
# ,: This part adds a comma as a thousands separator.
# .2f: This specifies that the value should be formatted as a floating-point number with two decimal places.
pd.options.display.float_format = '{:,.2f}'.format

# Display the DataFrame 'emissions'
# This will show the 'emissions' DataFrame with floating-point numbers formatted to two decimal places
emissions
```