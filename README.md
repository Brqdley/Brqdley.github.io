**DSC80 Project - Outages** 
Climate and Cause

**Introduction:**

The dataset I chose was outages. The question I plan to investigate further is, is there a relationship between climate, the cause category, and the number of outages? I feel as though a relationship between those columns is prevalent based off of looking at the dataset. If a cause category is more prevalent in a certain type of climate, these companies can implement more preventative measures against specific causes in certain locations. 

1534 rows in the dataset, and relevant columns are YEAR, CLIMATE.CATEGORY, CAUSE.CATEGORY, CLIMATE.REGION. Year is the year the outage occured. Climate category(normal,cold,warm) is the type of climate the outage occurred in. Cause category(severe weather, etc) is the type of cause the outage occurred in. Climate region(south,central,etc) is the climate region the outage occurred in.


**Cleaning and EDA:**

I first cleaned the column names as they were in the fifth row of the dataset. I set this as the column names and then dropped the first 5 rows. Then I reset the index. I converted ANOMALY.LEVEL and OUTAGE.DURATION to floats, so I could compute means/sums with them in the future.

I converted the OUTAGE.START.TIMES and the OUTAGE.START.DATES to one column of datetime to simplify the dataframe. I also converted the RESTORATION.START.TIMES and RESTORATION.START.DATES to one column of datetime. Although converting the times to pd.datetime made it much easier to groupby date and time, as I could now use functions on this data, grouping both times into one datetime column did not affect my analysis, it only made it easier for me to understand the data.

|   OBS |   YEAR |   MONTH | U.S._STATE   | POSTAL.CODE   | NERC.REGION   | CLIMATE.REGION     |   ANOMALY.LEVEL | CLIMATE.CATEGORY   | CAUSE.CATEGORY     | CAUSE.CATEGORY.DETAIL   |   HURRICANE.NAMES |   OUTAGE.DURATION |   DEMAND.LOSS.MW |   CUSTOMERS.AFFECTED |   RES.PRICE |   COM.PRICE |   IND.PRICE |   TOTAL.PRICE |   RES.SALES |   COM.SALES |   IND.SALES |   TOTAL.SALES |   RES.PERCEN |   COM.PERCEN |   IND.PERCEN |   RES.CUSTOMERS |   COM.CUSTOMERS |   IND.CUSTOMERS |   TOTAL.CUSTOMERS |   RES.CUST.PCT |   COM.CUST.PCT |   IND.CUST.PCT |   PC.REALGSP.STATE |   PC.REALGSP.USA |   PC.REALGSP.REL |   PC.REALGSP.CHANGE |   UTIL.REALGSP |   TOTAL.REALGSP |   UTIL.CONTRI |   PI.UTIL.OFUSA |   POPULATION |   POPPCT_URBAN |   POPPCT_UC |   POPDEN_URBAN |   POPDEN_UC |   POPDEN_RURAL |   AREAPCT_URBAN |   AREAPCT_UC |   PCT_LAND |   PCT_WATER_TOT |   PCT_WATER_INLAND | OUTAGE.START.DATETIME   | OUTAGE.RESTORATION.DATETIME   |
|------:|-------:|--------:|:-------------|:--------------|:--------------|:-------------------|----------------:|:-------------------|:-------------------|:------------------------|------------------:|------------------:|-----------------:|---------------------:|------------:|------------:|------------:|--------------:|------------:|------------:|------------:|--------------:|-------------:|-------------:|-------------:|----------------:|----------------:|----------------:|------------------:|---------------:|---------------:|---------------:|-------------------:|-----------------:|-----------------:|--------------------:|---------------:|----------------:|--------------:|----------------:|-------------:|---------------:|------------:|---------------:|------------:|---------------:|----------------:|-------------:|-----------:|----------------:|-------------------:|:------------------------|:------------------------------|
|     1 |   2011 |       7 | Minnesota    | MN            | MRO           | East North Central |            -0.3 | normal             | severe weather     | nan                     |               nan |              3060 |              nan |                70000 |       11.6  |        9.18 |        6.81 |          9.28 |     2332915 |     2114774 |     2113291 |       6562520 |      35.5491 |      32.225  |      32.2024 |         2308736 |          276286 |           10673 |           2595696 |        88.9448 |        10.644  |         0.4112 |              51268 |            47586 |          1.07738 |                 1.6 |           4802 |          274182 |       1.75139 |             2.2 |      5348119 |          73.27 |       15.28 |           2279 |      1700.5 |           18.2 |            2.14 |          0.6 |    91.5927 |         8.40733 |            5.47874 | 2011-07-01 17:00:00     | 2011-07-03 20:00:00           |
|     2 |   2014 |       5 | Minnesota    | MN            | MRO           | East North Central |            -0.1 | normal             | intentional attack | vandalism               |               nan |                 1 |              nan |                  nan |       12.12 |        9.71 |        6.49 |          9.28 |     1586986 |     1807756 |     1887927 |       5284231 |      30.0325 |      34.2104 |      35.7276 |         2345860 |          284978 |            9898 |           2640737 |        88.8335 |        10.7916 |         0.3748 |              53499 |            49091 |          1.08979 |                 1.9 |           5226 |          291955 |       1.79    |             2.2 |      5457125 |          73.27 |       15.28 |           2279 |      1700.5 |           18.2 |            2.14 |          0.6 |    91.5927 |         8.40733 |            5.47874 | 2014-05-11 18:38:00     | 2014-05-11 18:39:00           |
|     3 |   2010 |      10 | Minnesota    | MN            | MRO           | East North Central |            -1.5 | cold               | severe weather     | heavy wind              |               nan |              3000 |              nan |                70000 |       10.87 |        8.19 |        6.07 |          8.15 |     1467293 |     1801683 |     1951295 |       5222116 |      28.0977 |      34.501  |      37.366  |         2300291 |          276463 |           10150 |           2586905 |        88.9206 |        10.687  |         0.3924 |              50447 |            47287 |          1.06683 |                 2.7 |           4571 |          267895 |       1.70627 |             2.1 |      5310903 |          73.27 |       15.28 |           2279 |      1700.5 |           18.2 |            2.14 |          0.6 |    91.5927 |         8.40733 |            5.47874 | 2010-10-26 20:00:00     | 2010-10-28 22:00:00           |
 |     4 |   2012 |       6 | Minnesota    | MN            | MRO           | East North Central |            -0.1 | normal             | severe weather     | thunderstorm            |               nan |              2550 |              nan |                68200 |       11.79 |        9.25 |        6.71 |          9.19 |     1851519 |     1941174 |     1993026 |       5787064 |      31.9941 |      33.5433 |      34.4393 |         2317336 |          278466 |           11010 |           2606813 |        88.8954 |        10.6822 |         0.4224 |              51598 |            48156 |          1.07148 |                 0.6 |           5364 |          277627 |       1.93209 |             2.2 |      5380443 |          73.27 |       15.28 |           2279 |      1700.5 |           18.2 |            2.14 |          0.6 |    91.5927 |         8.40733 |            5.47874 | 2012-06-19 04:30:00     | 2012-06-20 23:00:00           |
 |     5 |   2015 |       7 | Minnesota    | MN            | MRO           | East North Central |             1.2 | warm               | severe weather     | nan                     |               nan |              1740 |              250 |               250000 |       13.07 |       10.16 |        7.74 |         10.43 |     2028875 |     2161612 |     1777937 |       5970339 |      33.9826 |      36.2059 |      29.7795 |         2374674 |          289044 |            9812 |           2673531 |        88.8216 |        10.8113 |         0.367  |              54431 |            49844 |          1.09203 |                 1.7 |           4873 |          292023 |       1.6687  |             2.2 |      5489594 |          73.27 |       15.28 |           2279 |      1700.5 |           18.2 |            2.14 |          0.6 |    91.5927 |         8.40733 |            5.47874 | 2015-07-18 02:00:00     | 2015-07-19 07:00:00           |


    Univariate Analysis:
<iframe src="assets/uni.html" width=800 height=600 frameBorder=0></iframe>

This plot shows the amount of outages per year from 2000 to 2016. As you can see, outages per year steadily increases from 2000 to 2011, then decreases from 2011 to 2016. There is a peak at 2011. This could be due to the 2011 Southwest blackout which effected more than 2.7m customers.

    Bivariate Analysis:
<iframe src="assets/bi.html" width=800 height=600 frameBorder=0></iframe>

This plot shows the amount of outages with warm/normal/cold climates in different cause categories. One interesting trend is that for fuel supply emergenices, it is rarely in warm weather. One could infer that fuel supply is harder to recieve in colder climates, due to pipe issues or transporting issues, which is why the chart displays this.



    Interesting Aggregates:
<iframe src="assets/pivot.html" width=600 height=300 frameBorder=0></iframe>

This table shows that fuel supply emergencies have the longest outage duration, while islanding has the shortest outage duration.

**Assessment of Missingness:**

CAUSE.DETAIL could be NMAR. Value could be NA if detail is too specific, would not fit into a "category" of detail.
Adding column that asks if detail is too specific or not could be one way to test if the cause is dependent on this variable.If these columns overlap with significance then the CAUSE.DETAIL column is MAR.



<iframe src="assets/tvd_hurricane.html" width=600 height=600 frameBorder=0></iframe>

This graph shows the empirical distribution of the test statistic and where the observed test statistic lands. The p-value of 0.0 indicates that the observed data is unlikely to have occurred if the null hypothesis were true, and suggests that we should reject the null hypothesis in favor of the alternative hypothesis that there is an association between HURRICANE.NAMES and the missingness of CAUSE.CATEGORY.DETAIL.


**Hypothesis Testing:**

Is there a significant difference in the number of severe weather outages in cold versus warm climates?

Null hypothesis: there is not a signifcant difference between the number of severe weather outages in cold versus warm climates. i.e. cold=warm

Alternate hypothesis: there is a signifcant difference between the number of severe weather outages in cold versus warm climates. i.e. cold!=warm

Significance level: .05

Test-statistic is absolute value of difference between means. This is a good test-statistic because we care about difference in general, not if one is specifically greater or less than the other.

p-value: 0.839
The p-value of .839 means that there is a high probability of observing the test statistic or a more extreme result under the null hypothesis. It indicates that the observed result is not statistically significant at the significance level of 0.05. We fail to reject the null hypothesis that there is not a significant difference between the number of severe weather outages in cold versus warm climates.






