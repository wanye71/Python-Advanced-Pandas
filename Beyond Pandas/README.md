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
# Alright, folks, hold onto your hats because we're about to embark on a journey into the mysterious realm of geospatial data.
# Picture this: pandas and geopandas strutting onto the scene like the coolest cats in town, ready to rock and roll with data like never before!

# First things first, we're importing pandas and geopandas to get this party started.
# pandas is like the trusty sidekick, always there to lend a hand with data wrangling and analysis.
# And then there's geopandas, the suave and sophisticated cousin, bringing geospatial magic to the mix.

import geopandas  # geopandas: adding a touch of geospatial glamor to the party
import os

import pandas as pd  # pandas: the wingman of data analysis
# Welcome to the land of magical maps where Plotly Express is our genie!
import plotly.express as px

# Hold onto your hiking boots, folks, because we're about to summit some serious peaks with pandas!
# Imagine pandas as the fearless guide leading us to majestic mountain tops, while we explore the rugged beauty of nature's playground.

# We're kicking things off with a DataFrame called 'peaks', which will be our trusty map to the most breathtaking peaks in the region.
# Picture this: a list of epic peak names paired with their coordinates, ready to take us on an adventure of a lifetime.

peaks = pd.DataFrame(
    {'Peak Name': ['Green Mtn.', 'So. Boulder Peak', 'Bear Peak', 'Flagstaff Mtn.', 'Mt. Sanitas'],  
    # Names of the awe-inspiring peaks, each one a testament to the majesty of nature
     'Latitude': [39.9821, 39.9539, 39.9603, 40.0017, 40.0360968],  
    # The latitude coordinates, guiding us to the peaks' lofty summits
     'Longitude': [-105.3016, -105.2992, -105.2952, -105.3075, -105.3061024]})  
    # The longitude coordinates, leading us to the peaks' hidden treasures


# Brace yourselves, intrepid explorers, because we're about to elevate our adventure to new heights with GeoPandas!
# Think of GeoPandas as our magic carpet, whisking us away to the most enchanting landscapes on Earth.

# Here's where the magic happens: we're transforming our DataFrame of peaks into a GeoDataFrame called 'gdf'.
# With GeoPandas, we're not just plotting points; we're unlocking the power of spatial analysis and visualization.

gdf = geopandas.GeoDataFrame(
    peaks, geometry=geopandas.points_from_xy(peaks.Longitude, peaks.Latitude))  
    # Harnessing the magic of GeoPandas, we're creating a GeoDataFrame with our peaks' coordinates as geometry
gdf



token = os.getenv("MAPBOX_ACCESS_TOKEN")
# Setting up your access token for Plotly's Mapbox, because every explorer needs a secret key to unlock hidden treasures!
px.set_mapbox_access_token(token)

# Time to make our dataframe feel special by giving it a 'size' column. It's like giving your pet rock a top hat!
gdf['size'] = 65

# Hold onto your compasses as we embark on a journey through the enchanted lands of Plotly Express to create an interactive map!
fig = px.scatter_mapbox(gdf,
                        lat=gdf.geometry.y,  # Latitude coordinates: where the magic happens
                        lon=gdf.geometry.x,  # Longitude coordinates: leading us on the path to adventure
                        color="Peak Name",   # Colorful markers representing the mystical peak names
                        hover_name="Peak Name",  # Hover over the markers to reveal their secret identities
                        mapbox_style='outdoors',  # Choose the Mapbox style: because every map needs its own fashion statement
                        size='size',  # Size matters: setting the size of our markers to impress the cartographers
                        zoom=10)  # Zooming in to uncover hidden wonders with the click of a button

# Behold! The moment you've been waiting for: the unveiling of our magical map!
fig.show()
```

### Beyond pandas with Dask and Koalas (Spark)
```python

```