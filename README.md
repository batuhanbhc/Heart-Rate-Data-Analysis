# Heart-Rate-Data-Analysis

Dataset: https://drive.google.com/file/d/16ZidUL6JziXJoVNyjq6fFvOTmcoadTFu/view?usp=sharing

Project submission short video: https://drive.google.com/file/d/1JPZeCZAQelarCwJC6gsUWT9QkCg9ouWR/view?usp=drive_link

## Motivation
This aim of this project is to analyze the nature of my heart rate throughout different stages and different activities in a day.

## Data Source
The data was collected by using Apple Watch Series 9 in between 10.11.2023 and 12.01.2024 (dd.mm.yyyy). After the collection of data was complete, the data files were exported using
the Apple Health application. The exported files were then opened and parsed in Jupyter Notebook environment to extract all the meaningful data that could help during the data analysis. An additional file containing the exam dates was also used to analyze heart rate distributions during exams.

## Data Analysis
The extracted data mainly consisted of heart rate events, sleep qualities, step counts and other features. Considering the possible dependency issues between the sampled heart rate events, the heart rate events were binned. As for the binning method employed, heart rate values from intervals as short as five minutes were averaged, with an additional criterion of requiring a minimum of 50 counts per bin. The resulting averages were then associated with a time, representing the mean point of the times corresponding to the heart rate events used. The intention was to enhance the statistical significance of each bin, and to assume that the realized heart rate observations in each distribution were independent of each other.

After the binning process, many different distributions from the dataset were extracted for further analysis. Some of these distributions consisted of sleeping heart rate, heart rate while moving, sleep and movement filtered heart rate, heart rate during different stages of day (morning, afternoon, evening, night, late night), heart rate during weekends and week days, heart rate during exams, heart rate during different stages of sleep and so forth. 

Analysis of each distribution mainly consisted finding certain sample statistics, applying normality tests, and applying hypothesis tests to see whether the mean of each distribution is bigger than 100 (upper limit for a normal resting heart rate). For sample statistics; sample mean, sample standard deviation, median, minimum and maximum points, range, and 95% confidence intervals for the mean and the standard deviation were calculated. For testing whether the sample was normally distributed, three different normality tests were used: Kolmogorov-Smirnov test, Anderson-Darling test and chi-squared goodness of fit test. For chi-squared test, using the parameters estimated from the sample, method of creating ten bins where each bin represents an equal portion (%10) under the normal distribution was used. Two different hypothesis tests for testing the mean being larger than 100 was used: one assuming the population was normally distributed (t-statistics), the other assuming population was not normally distributed (z-statistics by CLT).

For comparing whether two different distributions were significantly different from each other, Levene's test for testing the difference between variances, and Mann-Whitney U test for testing the difference between means were used. To test correlation between two variables, Spearman's rank test and pearson's test were used.

For visualisation, histograms of each distribution were created. Boxplots were used for comparing the distributions of certain groups (different stages of sleep, weekend-week day distributions) to find possible correlations affecting the heart rate. Scatter plot for showing the correlation between average heart rate per day vs. total step count was used. Line graphs were used to illustrate time series graphs showing the changes in heart rate over time.

## Findings
* The boxplot of different sleep stages show that the heart rate is dependent on the sleep stage. Distributions throughout the stages show a decreasing trend for following the stages: awake -> REM sleep -> core sleep -> deep sleep. 
* My heart rate on average is higher during week days, both when I am sleeping and when I am active during the day.
* The boxplot of different day periods show that the heart rate is dependent on the time of the day. Starting from afternoon, the distribution of heart rate shows declining trend towards the night.
* Afternoon distribution is normally distributed, evening is not normally distributed. Night is normal according to chi-squared and Kolmogorov-Smirnov tests, but not according Anderson-Darling test; indicating non-normality on tails (outliers).
* Except the afternoon and night distributions, none of the other extracted distributions are normally distributed according to normality tests.
* The average heart rate during exams exhibits high variability, with means consistently exceeding 100 beats per minute (ranging from 108 to 129). These values surpass the range observed in any of the other extracted distributions. Notably, heart rates during exams reach concerning levels.
* The standard deviation of heart rates during exams also varies significantly (ranging from 3.1866 to 8.6983), suggesting potential fluctuations in stress levels throughout the exam period. Lower standard deviation values may indicate more stable stress levels during certain exams. Additional data showing stress levels might be needed to justify this conclusion.
* Difference tests between sleep & movement filtered and sleep filtered distributions indicate the means and variances are significantly different. Movement affects the heart rate distribution significantly during the day.
* Difference tests between sleep filtered distribution vs. movement distribution shows the impact of all other activities except movement during the day. All other activities do not affect the variance of heart rate significantly, but they do change the mean of the distribution (lowering it).
* Even though not a strong correlation, there is a statistically significant correlation between average heart rate per day and total step counts per day according to Sperman's rank test and Pearson's test (coefficient being approximately 0.5 on both tests).
* * The moving average graph reveals an increasing trend towards the end of the dataset, particularly starting from around December 15, 2023. This observed trend could potentially be associated with the approaching final exams; however, drawing any conclusive inference requires additional data and analysis.

## Limitations and Future Work
Certain features (oxygen saturation, respiratory rate, etc.) could not be analyzed properly due to different frequency of the sampling of heart rate events in contrast to other features, since matching each heart rate event with a feature when a feature is missing would require certain assumptions about the nature of those features. Thus, there could be some other correlations between my heart rate and other features that might be missed. In the future, if possible, collecting the data with similar frequency for all attributes would allow me to match each heart rate event with actual feature values, analyze the correlations between the features to a deeper extent, and create machine learning models for predicting heart rate given the features. Additionally, acquiring skills in time series analysis in the future will enable me to analyze trends and changes in my heart rate over time.
