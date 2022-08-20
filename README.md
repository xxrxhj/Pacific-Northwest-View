# Pacific-Northwest-View

Vancouver BC is known for its Mediterranean climate with rainy winter/spring and temperate summer.

As a wine-enthusiast, I was fascinated by the degree of weather fluctation attributable to quality grapes.

The following database features extreme highs and lows in climate. Let's discover the duplicates and outliers.


1. The Libraries

```bash

import pandas as pd

import seaborn as sns

import numpy as np

import matplotlib.pyplot as plt

```

2. Upload Database

```bash

# load in the database as Weather
weather = pd.read_csv('weatherstats_vancouver_daily.csv')

# take a look at the first few dates
weather.sample(5)

|No.|    date    | max_temperature | avg_hourly_temperature | avg_temperature | min_temperature | max_humidex | min_windchill | max_relative_humidity | avg_hourly_relative_humidity | avg_relative_humidity | ... | avg_cloud_cover_4 | min_cloud_cover_4 | max_cloud_cover_8 | avg_hourly_cloud_cover_8 | avg_cloud_cover_8 | min_cloud_cover_8 | max_cloud_cover_10 | avg_hourly_cloud_cover_10 | avg_cloud_cover_10 | min_cloud_cover_10 |
|---|-----------:|----------------:|-----------------------:|----------------:|----------------:|------------:|--------------:|----------------------:|-----------------------------:|----------------------:|----:|------------------:|------------------:|------------------:|-------------------------:|------------------:|------------------:|-------------------:|--------------------------:|-------------------:|-------------------:|
| 0 | 2022-08-01 |            24.4 |                  20.59 |           20.60 |            16.8 |        31.0 |           NaN |                   100 |                         85.9 |                  85.0 | ... |               NaN |               NaN |                 8 |                      3.2 |               4.0 |                 0 |                NaN |                       NaN |                NaN |                NaN |
| 1 | 2022-07-31 |            27.8 |                  23.07 |           23.20 |            18.6 |        35.0 |           NaN |                   100 |                         85.6 |                  78.0 | ... |               NaN |               NaN |                 2 |                      0.5 |               1.0 |                 0 |                NaN |                       NaN |                NaN |                NaN |
| 2 | 2022-07-30 |            28.8 |                  23.20 |           23.45 |            18.1 |        36.0 |           NaN |                    99 |                         80.8 |                  76.5 | ... |               NaN |               NaN |                 0 |                      0.0 |               0.0 |                 0 |                NaN |                       NaN |                NaN |                NaN |
| 3 | 2022-07-29 |            28.6 |                  23.23 |           23.40 |            18.2 |        37.0 |           NaN |                    97 |                         82.0 |                  80.0 | ... |               NaN |               NaN |                 1 |                      0.1 |               0.5 |                 0 |                NaN |                       NaN |                NaN |                NaN |
| 4 | 2022-07-28 |            27.9 |                  22.83 |           22.90 |            17.9 |        34.0 |           NaN |                    96 |                         79.8 |                  78.5 | ... |               NaN |               NaN |                 2 |                      0.6 |               1.0 |                 0 |                NaN |                       NaN |                NaN |                NaN |
| 5 | 2022-07-27 |            30.4 |                  24.36 |           24.45 |            18.5 |        37.0 |           NaN |                    95 |                         71.9 |                  71.0 | ... |               NaN |               NaN |                 4 |                      1.6 |               2.0 |                 0 |                NaN |                       NaN |                NaN |                NaN |

```

3. Remove the duplicates
```bash
weather.drop_duplicates(keep=False, inplace=True)
```

4. Filter for null value

It seems like many fields have 'NaN' as value. Let's have a look at 'min_windchill' column:
```
weather['min_windchill'].fillna('NaN')
```
| No. | min_windchill |
|-----|---------------|
| 0   | NaN           |
| 1   | NaN           |
| 2   | NaN           |
| 3   | NaN           |
| 4   | NaN           |
| ... | ...           |
| 95  | NaN           |
| 96  | NaN           |
| 97  | NaN           |
| 98  | NaN           |
| 99  | NaN           |

Name: min_windchill, Length: 100, dtype: object

The null values could be errors in the database

4. Prepare for data analysis
```
# replace null with number 0
weather = weather.fillna(0)

# display a few rows randomly
print(weather.sample(6))
```

|    | date       | max_temperature | avg_hourly_temperature | avg_temperature | min_temperature | max_humidex | min_windchill | max_relative_humidity | 
|----|------------|-----------------|------------------------|-----------------|-----------------|-------------|---------------|-----------------------|
| 57 | 2022-06-05 | 19.8            | 15.21                  | 16.05           | 57              | 12.3        | 0.0           | 0.0                   | 
| 11 | 2022-07-21 | 23.2            | 19.31                  | 19.25           | 11              | 15.3        | 29.0          | 0.0                   | 
| 45 | 2022-06-17 | 18.3            | 14.52                  | 14.20           | 45              | 10.1        | 0.0           | 0.0                   | 
| 39 | 2022-06-23 | 18.1            | 14.00                  | 14.55           | 39              | 11.0        | 0.0           | 0.0                   | 
| 64 | 2022-05-29 | 15.8            | 13.30                  | 13.35           | 64              | 10.9        | 0.0           | 0.0                   | 
| 19 | 2022-07-13 | 20.9            | 18.13                  | 18.25           | 19              | 15.6        | 0.0           | 0.0                   | 

Now, notice the 'min_windchill' column has numbers only.


5. Data visualization

I learn in Geography that grapes grow in extreme condition. So, I created a scatterplot for column 'max_temperature.'

```
plt.figure(figsize=(20,10))

plt.subplot(1,2,1)

plt.xlim(0,35)

plt.ylim(0,0.1)

sns.distplot(weather['max_temperature'])

plt.show()
```

![Screen Shot 2022-08-16 at 10 10 32 PM](https://user-images.githubusercontent.com/108639250/185019277-4fddbf5f-ad59-45d6-ba58-22e98d0cf34a.png)


6. Determine 90% confidence interval

In order to assess the extent to which weather changes, let's calculate the interquartile range. IQR is where the majority of data lie in.
```
Q1 = weather.quantile(0.25)

Q3 = weather.quantile(0.75)

IQR = Q3 - Q1
```

7. Detect outliers

Based on the criterion, I filtered for outliers in selected columns

```
print(weather < (Q1 - 1.5 * IQR)) |(weather > (Q3 + 1.5 * IQR))
```
|    | avg_cloud_cover_10 | avg_cloud_cover_4 | avg_cloud_cover_8 | avg_dew_point | avg_health_index |
|----|--------------------|-------------------|-------------------|---------------|------------------|
| 0  | False              | False             | False             | False         | False            |
| 1  | False              | False             | False             | False         | False            |
| 2  | False              | False             | TRUE              | False         | False            |
| 3  | False              | False             | False             | False         | False            |
| 4  | False              | False             | False             | False         | False            |
| .. | ...                | ...               | ...               | ...           |                  |
| 95 | False              | False             | False             | False         | False            |
| 96 | False              | False             | False             | False         | False            |
| 97 | False              | False             | False             | False         | False            |
| 98 | False              | False             | False             | False         | False            |
| 99 | False              | False             | False             | False         | False            |

The second row in column 'avg_cloud_cover_8' seems to be an outlier.


8. Skewness test

print(weather['avg_cloud_cover_8'].skew())
weather['avg_cloud_cover_8'].describe()

skewness: -0.5

count    100.000000

mean       4.895000

std        1.942734

min        0.000000

25%        4.000000

50%        5.000000

75%        6.500000

max        8.000000

Name: avg_cloud_cover_8, dtype: float64

The skewness of -0.5 implies a left-skewed distribution. That explains the presence of extreme lower outliers.

9. Let's visualize the outliers in a histogram

weather.avg_cloud_cover_8.hist()

![Screen Shot 2022-08-16 at 10 12 38 PM](https://user-images.githubusercontent.com/108639250/185019552-6f8200db-83fd-4a99-8e33-650c4063dc6f.png)

The chart comfirms a left-skewed distribution, indicating outliers on the left


10. determine 90% confidence interval

print(weather['avg_cloud_cover_8'].quantile(0.05))

print(weather['avg_cloud_cover_8'].quantile(0.95))

1.0

7.5

11. finally we remove the outliers and return the skewness value

weather['avg_cloud_cover_8'] = np.where(weather['avg_cloud_cover_8']<1.0, 1.0, weather['avg_cloud_cover_8'])

weather['avg_cloud_cover_8'] = np.where(weather['avg_cloud_cover_8']>7.5, 7.5, weather['avg_cloud_cover_8'])

print(weather['avg_cloud_cover_8'].skew())

-0.4, which is closer to 0 than -0.5

12. Return the database

weather


## The database is now free of outliers and duplicates.
