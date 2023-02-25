DSC80 Project - Outages

Introduction:

The dataset I chose was outages. The question I plan to investigate further is, is there a relationship between climate, the cause category, and the number of outages? I feel as though a relationship between those columns is prevalent based off of looking at the dataset. If a cause category is more prevalent in a certain type of climate, these companies can impliment more preventative measures against specific causes in certain locations. 

1534 rows in the dataset, and relevant columns are YEAR, CLIMATE.CATEGORY, CAUSE.CATEGORY, CLIMATE.REGION. Year is the year the outage occured. Climate category(normal,cold,warm) is the type of climate the outage occured in. Cause category(severe weather, etc) is the type of cause the outage occured in. Climate region(south,central,etc) is the climate region the outage occured in.


Data Cleaning:
I first cleaned the column names as they were in the fifth row of the dataset. I set this as the column names and then dropped the first 5 rows. Then I reset the index. I convert ANOMALY.LEVEL and OUTAGE.DURATION to floats, so I could compute means/sums with them in the future.

I converted the OUTAGE.START.TIMES and the OUTAGE.START.DATES to one column of datetime to simplify the dataframe. I also converted the RESTORATION.START.TIMES and RESTORATION.START.DATES to one column of datetime. Although converting the times to pd.datetime made it much easier to groupby dates and times, as I could now use functions on this data, grouping both times into one datetime column did not effect my analysis, it only made it easier for me to understand the data.

<iframe src="assets/head.html" frameBorder=0></iframe>


Univariate Analysis:
<iframe src="assets/uni.html" width=800 height=600 frameBorder=0></iframe>

This plot shows the amount of outages per year from 2000 to 2016. As you can see, outages per year steadily increases from 2000 to 2011, then decreases from 2011 to 2016. There is a peak at 2011. This could be due to the 2011 Southwest blackout which effected more than 2.7m customers.

Bivariate Analysis:
<iframe src="assets/bi.html" width=800 height=600 frameBorder=0></iframe>

This plot shows the amount of outages with warm/normal/cold climates in different cause categories. One interesting trend is that for fuel supply emergenices, it is rarely in warm weather. One could infer that fuel supply is harder to recieve in colder climates, due to pipe issues or transporting issues, which is why the chart displays this.



Interesting Aggregates:
<iframe src="assets/pivot.html" width=600 height=300 frameBorder=0></iframe>

This table shows that fuel supply emergencies have the longest outage duration, while islanding has the shortest outage duration.

NMAR Analysis:
CAUSE.DETAIL could be NMAR. Value could be NA if detail is too specific, would not fit into a "category" of detail.
Adding column that asks if detail is too specific or not could be one way to test if the cause is dependent on this variable.If these columns overlap with significance then the CAUSE.DETAIL column is MAR.

Missingness Dependency:
<iframe src="assets/tvd_hurricane.html" width=600 height=600 frameBorder=0></iframe>

This graph shows the empirical distribution of the test statistic and where the observed test statistic lands. The p-value of 0.0 indicates that the observed data is unlikely to have occurred if the null hypothesis were true, and suggests that we should reject the null hypothesis in favor of the alternative hypothesis that there is an association between HURRICANE.NAMES and the missingness of CAUSE.CATEGORY.DETAIL.

Hypothesis Testing:

Is there a significant difference in the number of severe weather outages in cold versus warm climates?

Null hypothesis: there is not a signifcant difference between the number of severe weather outages in cold versus warm climates. i.e. cold=warm

Alternate hypothesis: there is a signifcant difference between the number of severe weather outages in cold versus warm climates. i.e. cold!=warm

Significance level: .05

Test-statistic is absolute value of difference between means. This is a good test-statistic because we care about difference in general, not if one is specifically greater or less than the other.

p-value: 0.839
The p-value of .839 means that there is a high probability of observing the test statistic or a more extreme result under the null hypothesis. It indicates that the observed result is not statistically significant at the significance level of 0.05. We fail to reject the null hypothesis that there is not a significant difference between the number of severe weather outages in cold versus warm climates.






