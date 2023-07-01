# project-is-to-determine-which-regions-need-support-to-make-air-quality-improvements-
we will investigate data from the Air Quality Index (AQI) with respect to carbon monoxide.
Introduction
Due to the high rate of carbon monoxide a lot of cities are been polluted and with a dataset gotten of an analytics team for the United States Environmental Protection Agency (EPA).

This analysis is done using the statistical approach of python to derive insight for the team and yes this is my first python project so your feedback will be highly appreciated.

This dataset consist of the

the date local
the state name
the county name
the city name
the local site name
the parameter name
the unit of measure
the arithmetic mean
and the AQI which is the air quality index available.
The ability to determine which type of probability distribution best fits data, calculate z-score, and detect outliers are essential skills in data work. These capabilities enable data professionals to understand how their data is distributed and identify data points that need further examination

Okay we start our analysis by importing relevant libraries, packages, and modules. For this lab, you will need

numpy,

pandas,

matplotlib.pyplot,

statsmodels.api, and

scipy to import statistics libaries

Now we import our libraries needed with an alias to make it easy to understand in the further analysis.

import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import statsmodels.api as sm
from scipy import stats
Now we import our dataset needed using the pandas library

pd.read_csv("c4 epa air dataset.csv")

and that is our dataset and we can see that we have 260 rows and 10 columns as indicated at the lower left side of the dataset shown above.

Now we make an alias for naming the dataset to make it easy to just write using the ads which is also the an abbreviation for the Air dataset(ads)

ads = pd.read_csv("c4 epa air dataset.csv")
Now we get the first ten set of the dataset by using the head function and remember indices in python numbers starts from 0

ads.head(10)

the dataset above are the first 10 dataset numbering starting from zero(0)

Now To better understand the quantity of data you are working with, display the number of rows and the number of columns by using the shape function.

ads.shape

Now, you want to find out whether air quality index(AQI) fits a specific type of probability distribution. Create a histogram to visualize the distribution of AQI. Then, based on its shape, visually determine if it resembles a particular distribution

Now we Create a histogram to visualize distribution of the air quality index.

ads["aqi"].hist();

now what do we observe with the histogram

There is a slight right skew, . This shape suggests that the distribution of this data should be approximately normal.

Now Another way to visually check if the data is normally distributed is to create and inspect a QQ (quantile-quantile) plot.

so now we Create QQ plot for AQI data.

fig = sm.qqplot(ads["aqi"], line='s')
plt.show()

what do we observe on this QQ plot

In the QQ plot, most of the data points follow a straight line, which indicates that a normal distribution should fit the data. Only a few regions do not follow the line.

Interesting right .

for the statistician here we know about the empirical rule which states that, for every normal distribution:

68% of the data fall within 1 standard deviation of the mean 95% of the data fall within 2 standard deviations of the mean 99.7% of the data fall within 3 standard deviations of the mean First, define two variables to store the mean and standard deviation, respectively, for AQI. Creating these variables will help you easily access these measures as you continue with the calculations involved in applying the empirical rule.

now let us use the describe function to returns description of the data in the DataFrame for the air quality index.

ads.describe()

ads["state_name"].describe()

Now, check the first part of the empirical rule: whether 68% of the air quality index data falls within 1 standard deviation of the mean.

To compute the actual percentage of the data that satisfies this criteria, define the lower limit (for example, 1 standard deviation below the mean) and the upper limit (for example, 1 standard deviation above the mean). This will enable you to create a range and confirm whether each value falls within it.

now let us calculate for the lower limit and upper limit

lower_limit = mean_aqi_log - 1 * std_aqi_log
upper_limit = mean_aqi_log + 1 * std_aqi_log

print(lower_limit, upper_limit)

now let us calculate for percentage that falls within 1 standard deviation of mean

((ads["aqi"] >= lower_limit) & (ads["aqi"] <= upper_limit)).mean() * 100

Now, consider the second part of the empirical rule: whether 95% of the air quality index data falls within 2 standard deviations of the mean.

To compute the actual percentage of the data that satisfies this criteria, define the lower limit (for example, 2 standard deviations below the mean) and the upper limit (for example, 2 standard deviations above the mean). This will enable you to create a range and confirm whether each value falls within it.

percentage that falls within 2 standard deviation below the mean

lower_limit = mean_aqi_log - 2 * std_aqi_log
upper_limit = mean_aqi_log + 2 * std_aqi_log

percentage of data that falls within 2 standard deviations of the mean

((ads["aqi"] >= lower_limit) & (ads["aqi"] <= upper_limit)).mean() * 100

Now, consider the third part of the empirical rule:whether 99.7% of the air quality index data falls within 3 standard deviations of the mean.

To compute the actual percentage of the data that satisfies this criteria, define the lower limit (for example, 3 standard deviations below the mean) and the upper limit (for example, 3 standard deviations above the mean). This will enable you to create a range and confirm whether each value falls within it.

3 standard deviations below the mean

lower_limit = mean_aqi_log - 3 * std_aqi_log
upper_limit = mean_aqi_log + 3 * std_aqi_log

print(lower_limit, upper_limit)

percentage of data that falls within 3 standard deviations of the mean.

((ads["aqi"] >= lower_limit) & (ads["aqi"] <= upper_limit)).mean() * 100

Since z-score indicates the relative position of values (for instance, z-score measures how many standard deviations below or above the mean a data point is), it can be used to detect outliers.

Z-score could be used to identify values that lie more than 3 standard deviations below or above the mean. These values may be considered outliers

Compute the z-score for every air quality index value, and add a column named z_score in the data to store those results.

ads["z_score"] = stats.zscore(ads["aqi"])
Now let us Display the first 5 rows to ensure that the new column was added.

ads.head()

And yes we successfully added the z-score to our data

Identify the parts of the data where air quality index is above or below 3 standard deviations of the mean.

ads[(ads["z_score"] > 3) | (ads["z_score"] < -3)]

Question: Why is outlier detection an important part of this project?

Detecting outliers is important because they can reveal two important things, depending on the context: First, they can identify measurements that were taken incorrectly. Second, they can highlight parts of the data that can be focused on to make improvements.

For example, if the air quality index for West Phoenix is considered an outlier, then that site can be studied further to determine what practices or changes might improve the air quality.

Considerations
key takeaway

Plotting the data using a histogram and a QQ plot, then observing the shape, enables you to visually determine whether the data is normally distributed.

The empirical rule can be used to verify whether a distribution is normal.

The mean and standard deviation are important measures when applying the empirical rule to a distribution.

Z-score allows you to identify potential outliers in the data.

RECOMMENDATION TO STAKE HOLDERS
The distribution of the air quality index data is approximately normal.

Using statistical methods, it was determined that the site at West Phoenix has worse air quality than the other sites.

Consider allocating more resources toward further examining this site in order to improve its air quality.
