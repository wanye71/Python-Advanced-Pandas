# Advanced Pandas - Beyond pandas

# Table of Contents

1. [Accelerate EDA with pandas-Profiling](#accelerate-eda-with-pandas-profiling)
2. [Explore Geographic data with Geopandas](#explore-geographic-data-with-geopandas)
3. [Beyond pandas with Dask and Koalas (Spark)](#beyond-pandas-with-dask-and-koalas-spark)

### Accelerate EDA with pandas-Profiling
```python
# Get ready to dive into data profiling with pandas-profiling!
# We're importing the pandas library as pd for some data manipulation magic.
# We're also importing the ProfileReport class from the pandas_profiling library to generate data profiling reports.

import pandas as pd
from pandas_profiling import ProfileReport

# Time to load up some data and get profiling!
# We're reading in the Iris dataset from a CSV file located one directory up.

iris = pd.read_csv('../iris.csv')

# Now, let's get into some serious data profiling!
# We're creating a profile report for the Iris dataset using pandas_profiling.

profile = ProfileReport(iris, title="Ires Data Profile")

# Let's display the profile report as an interactive notebook iframe.

profile.to_notebook_iframe()
```

### Explore Geographic data with Geopandas
```python

```

### Beyond pandas with Dask and Koalas (Spark)
```python

```