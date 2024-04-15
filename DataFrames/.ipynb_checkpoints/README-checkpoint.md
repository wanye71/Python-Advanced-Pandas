# Advanced Pandas - DataFrames

## Intro to DataFrames using Pandas
```python
# Import the pandas library and assign it the alias 'pd'
import pandas as pd

# Define a dictionary containing information about scores
scores = {
    # List of names
    "name": ['Ray', 'Japhy', 'Zosa'],
    # List of cities
    "city": ['San Francisco', 'Charlotte', 'Denver'],
    # List of scores
    "score": [75, 92, 94]
}


# Create a DataFrame from the 'scores' dictionary
df = pd.DataFrame(scores)

# This will output the DataFrame 'df', showing the data in a tabular format 
# with columns for 'name', 'city', and 'score'.
# Output: A pandas Series with scores data: 75, 92, 94.
df

# Access the 'score' column of the DataFrame 'df'
df['score']

# Create a new column in the DataFrame by concatenating 'name' and 'city' columns, 
# separated by an underscore
df['name_city'] = df['name'] + '_' + df['city']

# Filter the DataFrame to select rows where the 'score' column is greater than 90
# Result: A DataFrame containing rows where the score is greater than 90.
df[df['score'] > 90]
```