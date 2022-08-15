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

| date       | max\_temperature | avg\_hourly\_temperature | avg\_temperature | min\_temperature | max\_humidex | min\_windchill | max\_relative\_humidity | avg\_hourly\_relative\_humidity | avg\_relative\_humidity

| country             | child_mort | exports | health | imports | income | inflation | life_expec | total_fer | gdpp  |
|---------------------|------------|---------|--------|---------|--------|-----------|------------|-----------|-------|
| Afghanistan         | 90.2       | 10      | 7.58   | 44.9    | 1610   | 9.44      | 56.2       | 5.82      | 553   |
| Albania             | 16.6       | 28      | 6.55   | 48.6    | 9930   | 4.49      | 76.3       | 1.65      | 4090  |
| Algeria             | 27.3       | 38.4    | 4.17   | 31.4    | 12900  | 16.1      | 76.5       | 2.89      | 4460  |
| Angola              | 119        | 62.3    | 2.85   | 42.9    | 5900   | 22.4      | 60.1       | 6.16      | 3530  |
| Antigua and Barbuda | 10.3       | 45.5    | 6.03   | 58.9    | 19100  | 1.44      | 76.8       | 2.13      | 12200 |
| Argentina           | 14.5       | 18.9    | 8.1    | 16      | 18700  | 20.9      | 75.8       | 2.37      | 10300 |
| Armenia             | 18.1       | 20.8    | 4.4    | 45.3    | 6700   | 7.77      | 73.3       | 1.69      | 3220  |
| Australia           | 4.8        | 19.8    | 8.73   | 20.9    | 41400  | 1.16      | 82         | 1.93      | 51900 |
| Austria             | 4.3        | 51.3    | 11     | 47.8    | 43200  | 0.873     | 80.5       | 1.44      | 46900 |
| Azerbaijan          | 39.2       | 54.3    | 5.88   | 20.7    | 16000  | 13.8      | 69.1       | 1.92      | 5840  |
| Bahamas             | 13.8       | 35      | 7.89   | 43.7    | 22900  | -0.393    | 73.8       | 1.86      | 28000 |
| Bahrain             | 8.6        | 69.5    | 4.97   | 50.9    | 41100  | 7.44      | 76         | 2.16      | 20700 |
| Bangladesh          | 49.4       | 16      | 3.52   | 21.8    | 2440   | 7.14      | 70.4       | 2.33      | 758   |
