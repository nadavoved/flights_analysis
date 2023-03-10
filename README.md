# Overview
___
# Dataset - Data Expo 2009: Airline on time data (Udacity Given)
> [Download Manually](https://dataverse.harvard.edu/dataset.xhtml?persistentId=doi:10.7910/DVN/HG7NV7)
,or simply follow the setup bellow...
## Introduction
> This is a flights analysis based 
on a dataset containing various 
flight metrics. I chose to focus 
on the various carriers and their 
performance 
(e.g, delay - wise, popularity - wise, 
etc...), therefore I included features 
that are relevant to this direction. The entire dataset is very memory consuming, even when heavily optimized, so I had to use a sample in my analysis in order to create visualizations. The sample I used contains 9000 from years 2000-2008, 1000 records for each year.

## Setup
```
cd <project root>
python3.11 -m venv venv
./venv/Scripts/activate
pip install -r requirements.txt
```
- To get the data, either run `gather.py` located in root folder, 
or add the data manually to the `data` folder. <mark> NOTE - `gather.py` will download and extract the data automatically.</mark>

- ***REQUIRED:*** After getting the data, 
run `load.py` for loading time and memory optimizations. 
___
### About Optimization:
**Initially, all yearly dataset consume a lot of memory:**
**for example, 1987 alone weighs 484 MB.**
Steps taken:
1. Convert yearly csv files to feather files for faster loading time.

2. Use only relevant column for the analysis.

3. Convert numerical columns to lower float type (to 32, so numpy calculations won't be limited by float16 smaller size.)

4. Convert relevant columns to categorical (done by `get_years` function in `load.py` module). Also assists with loading time from feather.
___
<mark> NOTE - initially planned to just use unsampled datasets, but
visualization operations are taking way too long. yearly sample size is 1000 by default, 
`get_years` function allows for custom size as well.</mark> 

___

# Exploratory Analysis Findings
1. Distribution of departure delays in for each carrier in 2000-2008 (95% of data)
   > Findings: looking at all carriers, 
there are mostly right - skewed distributions. 
They are uni-modal, 
and most samples are very close to zero, 
which is a positive finding about delays.
2. Distribution of departure delay combined with arrival delay (%90 of data)
   > Findings: Most common delay combination is (0,0),
followed by values that are close to zero, 
which is a good thing for delays.
Please note that this plot is not meant 
to provide any information about relationship 
between arrival and departure delays, 
but rather provide info about overall 
distribution of the two variables.
3. Most common routes
   > Findings: By looking at the graph, 
we can clearly see the top 10 flight routes.
4. yearly flight counts faceted by carrier
   > Findings: Overall, Carrier `WN` was the most popular 
across all years, with many carriers have very 
low yearly flight counts across all years. 
Others, like `DL`, reduced dramatically over the years.
In contrast, there's `XE`, that mostly managed 
to increase over the years.
5. Monthly activity for each UniqueCarrier (by flight counts)
   > Findings: The most popular carrier overall is 
`WN`, as seen by its extremely blue - shaded 
cells across all months. For example, 
its most popular month is March, 
followed by April.
6. Average air times for each UniqueCarrier
   > Findings: It is noticeable that the avg. 
airtime per flight for most carriers is bellow 80. 
On the other hand, `B6` and `TZ` top the 
chart with above 150 minutes.
7. DepDelay vs ArrDelay (95% of data)
   > Findings: Coming back to the heatmap describing 
these two variables, the correlation between 
them wasn't noticeable. In contrast, 
here there's a very noticeable relatively strong 
correlation between them. Most values are 
concentrated around  (0,0), as better 
described within the heatmap before.
8. Distribution of total delay time for each day of the week (95% of data).</mark>
   > Findings: In all weekdays, 
there's a right - skewed distribution of total 
delay time, where the mode is around 0 total delay 
time - another positive finding 
about flight delays.
9. total delay time by year
    > Findings: 2002 - 2003 were the most 
"on - time" years for the flights within the dataset. 
In contrast, there's 2006 - 2008, 
which had the most delay.
10. Airtime vs Distance (95% of data)
    > Findings: There's a strong correlation between 
airtime and flight distance. 
Most values are shorter flights in terms of 
time and distance, and have very low spread, 
while the larger values are more spread - out 
and are scarcer.
11. Mean Ground Time prop for each UniqueCarrier
    > Findings: `EV` spend the largest portion of its 
flight process on the ground compared to the other carriers. 
This finding could be a measure for 
each carrier's efficiency in executing 
flights, but more data is required to 
properly determine their efficiency, 
such as the airports they use, 
or any other limiting factors that a carrier could encounter.
12. Distribution  of flight distance
    > Findings: It is observed that the most 
probable distances are up to 1000, 
when larger distances are much less probable, 
even more so as the distance goes above 3000.
13. Cancelled flights prop for each UniqueCarrier
    > Findings: `MQ` has the highest cancellation rate, 
while `HA` and `F9` has no cancellations over the 
sampled dataset. 
This is implies that it is probable that their rate 
would be the lowest, 
if not zero, even if the whole dataset would be included, 
not just 9,000 records.

14. Distribution of elapsed time
    > Findings: Most flights have elapsed time 
between 50 and 150. After that,
the proportion is only decreasing.
15. Mean flight speed by Distance
    > Findings: The avg. speed significantly increases 
between the three first bins of width 1000km. then, 
it's barely increasing above 8 km / minute.

### Base visualizations for presentation:
I would include in my explanatory analysis the following:
- plot 1
  - vis #15 - mean flight speed, as this metric is an essential piece of infomation about flights that was not originally included in the dataset.
  - vis #12 - Distribution of flight distance. This vis combined with the speed visualization could comprehensively describe flight air time metric.
- plot 2
  - vis #11 - mean ground time, beacause it is a useful metirc in observing how much time of a given flight is actually spent within airports. This data is as well not given in the dataset, but I find it interesting to present, as it can offer a different perpective to look on each carrier's performance.
  - vis #6 - avg. air times by unique carrier, should present on the same dashboard with avg. ground time, in order to show two sides of the flight process.
- plot 3
  - vis #4 - yearly flight counts by carrier.