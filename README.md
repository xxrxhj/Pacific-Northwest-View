# data-cleaning

Situated in the Pacific Northwest, Vancouver BC is known for its Mediterranean climate, which sees rainy winter/spring and temperate summer.
As a wine-enthusiast, I was fascinated by the degree of weather fluctation attributable to quality grapes.

The following database is a climate report that features extreme highs and lows. Let's find out the duplicates and outliers.

1. import libraries

import pandas as pd
import seaborn as sns
import numpy as np
import matplotlib.pyplot as plt

2. upload database

weather = pd.read_csv('weatherstats_vancouver_daily.csv')
weather.sample(5)

