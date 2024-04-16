# Advanced Pandas - Working with strings using pandas

## Working with Strings
```python
# Import the pandas library and assign it the alias 'pd'
import pandas as pd

# Create a pandas Series 'names_df' containing strings representing names
names_df = pd.Series(['Pomeray, CODY ', ' Wagner; Jarry', 'smith, Ray'])

# Replace all occurrences of ';' with ',' in each string of the 'names_df' Series
names_df = names_df.str.replace(';', ',')

# Display the modified Series 'names_df'
names_df

# Compute the length of each string in the 'names_df' Series
names_df.str.len()

# Remove leading and trailing whitespace from each string in the 'names_df' Series
names_df = names_df.str.strip()

# Compute the length of each string in the 'names_df' Series after stripping whitespace
names_df.str.len()

# Convert all strings in the 'names_df' Series to lowercase
names_df = names_df.str.lower()

# Display the modified Series 'names_df'
names_df

# Convert all strings in the 'names_df' Series to uppercase
names_df = names_df.str.upper()

# Display the modified Series 'names_df'
names_df

# Split each string in the 'names_df' Series by the ', ' delimiter
names_df = names_df.str.split(', ')

# Display the modified Series 'names_df'
names_df

# The output will be a Series of lists, 
# where each list contains the parts of the original strings that were separated by ', 

# Reverse each string in the lists contained within the 'names_df' Series 
# and create a new Series
names_df = pd.Series([i[::-1] for i in names_df])

# Display the modified Series 'names_df'
names_df

# The output will be a new Series 
# where each string in the original lists of 'names_df' is reversed.

# Join the elements of each list within the 'names_df' Series into a single string separated by a space
names_df = [' '.join(i) for i in names_df]

# Display the modified Series 'names_df'
names_df

# The output will be a new Series where each list of strings 
# in the original 'names_df' Series is joined into a single string.
```