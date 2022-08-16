# data-cleaning

Situated in the Pacific Northwest, Vancouver BC is known for its Mediterranean climate with rainy winter/spring and temperate summer.

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

|   |       date | max_temperature | avg_hourly_temperature | avg_temperature | min_temperature | max_humidex | min_windchill | max_relative_humidity | avg_hourly_relative_humidity | avg_relative_humidity | ... | avg_cloud_cover_4 | min_cloud_cover_4 | max_cloud_cover_8 | avg_hourly_cloud_cover_8 | avg_cloud_cover_8 | min_cloud_cover_8 | max_cloud_cover_10 | avg_hourly_cloud_cover_10 | avg_cloud_cover_10 | min_cloud_cover_10 |
|---|-----------:|----------------:|-----------------------:|----------------:|----------------:|------------:|--------------:|----------------------:|-----------------------------:|----------------------:|----:|------------------:|------------------:|------------------:|-------------------------:|------------------:|------------------:|-------------------:|--------------------------:|-------------------:|-------------------:|
| 0 | 2022-08-01 |            24.4 |                  20.59 |           20.60 |            16.8 |        31.0 |           NaN |                   100 |                         85.9 |                  85.0 | ... |               NaN |               NaN |                 8 |                      3.2 |               4.0 |                 0 |                NaN |                       NaN |                NaN |                NaN |
| 1 | 2022-07-31 |            27.8 |                  23.07 |           23.20 |            18.6 |        35.0 |           NaN |                   100 |                         85.6 |                  78.0 | ... |               NaN |               NaN |                 2 |                      0.5 |               1.0 |                 0 |                NaN |                       NaN |                NaN |                NaN |
| 2 | 2022-07-30 |            28.8 |                  23.20 |           23.45 |            18.1 |        36.0 |           NaN |                    99 |                         80.8 |                  76.5 | ... |               NaN |               NaN |                 0 |                      0.0 |               0.0 |                 0 |                NaN |                       NaN |                NaN |                NaN |
| 3 | 2022-07-29 |            28.6 |                  23.23 |           23.40 |            18.2 |        37.0 |           NaN |                    97 |                         82.0 |                  80.0 | ... |               NaN |               NaN |                 1 |                      0.1 |               0.5 |                 0 |                NaN |                       NaN |                NaN |                NaN |
| 4 | 2022-07-28 |            27.9 |                  22.83 |           22.90 |            17.9 |        34.0 |           NaN |                    96 |                         79.8 |                  78.5 | ... |               NaN |               NaN |                 2 |                      0.6 |               1.0 |                 0 |                NaN |                       NaN |                NaN |                NaN |
| 5 | 2022-07-27 |            30.4 |                  24.36 |           24.45 |            18.5 |        37.0 |           NaN |                    95 |                         71.9 |                  71.0 | ... |               NaN |               NaN |                 4 |                      1.6 |               2.0 |                 0 |                NaN |                       NaN |                NaN |                NaN |

3. Select null values in column 'min_windchill'

weather['min_windchill'].fillna('NaN')

0     NaN

1     NaN

2     NaN

3     NaN

4     NaN

... 

95    NaN

96    NaN

97    NaN

98    NaN

99    NaN

Name: min_windchill, Length: 100, dtype: object

3. drop duplicates

weather.drop_duplicates()

4. replace null values with 0

weather = weather.fillna(0)

print(weather.sample(6))

|    | date       | max_temperature | avg_hourly_temperature | avg_temperature | min_temperature | max_humidex | min_windchill | max_relative_humidity | 
|----|------------|-----------------|------------------------|-----------------|-----------------|-------------|---------------|-----------------------|
| 57 | 2022-06-05 | 19.8            | 15.21                  | 16.05           | 57              | 12.3        | 0.0           | 0.0                   | 
| 11 | 2022-07-21 | 23.2            | 19.31                  | 19.25           | 11              | 15.3        | 29.0          | 0.0                   | 
| 45 | 2022-06-17 | 18.3            | 14.52                  | 14.20           | 45              | 10.1        | 0.0           | 0.0                   | 
| 39 | 2022-06-23 | 18.1            | 14.00                  | 14.55           | 39              | 11.0        | 0.0           | 0.0                   | 
| 64 | 2022-05-29 | 15.8            | 13.30                  | 13.35           | 64              | 10.9        | 0.0           | 0.0                   | 
| 19 | 2022-07-13 | 20.9            | 18.13                  | 18.25           | 19              | 15.6        | 0.0           | 0.0                   | 


3. Create a scatterplot to visualize the distribution of max temperature

plt.figure(figsize=(20,10))

plt.subplot(1,2,1)

plt.xlim(0,30)

plt.ylim(0,0.1)

sns.distplot(weather['max_temperature'])

plt.show()

![image](https://user-images.githubusercontent.com/108639250/184941735-b8dcbcca-722c-4699-8492-6f4ada3f6d94.png)


