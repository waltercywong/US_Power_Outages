# US_Power_Outages
Data Analysis of US Power Outages for UCSD DSC80 Project

Nathan Ko, Walter Wong

# Introduction and Question Identification

Power outages are a large concern to functioning societies, with massive implications for daily life, commerce, and infrastructure. This report focuses on a comprehensive data cleaning and analysis of a major power outage dataset covering the continental U.S. from January 2000 to July 2016. The dataset, provided by the Laboratory for Advancing Sustainable Critical Infrastructure (LASCI), offers a unique opportunity to explore the patterns and potential causes of power outages. We can examine the distribution of outages and their correlation with demographic and geographical variables to come up with a more targeted approach to maintenance and develeopment of infrastructure in the future. Analyzing this data, there can be responsive changes taken in order to minimize the devastating effects of power outages. 

**Question:** Are power outages worse during the summer? 

**Null hypothesis:** The summer months (7, 8, 9) have the same average number of customers affected as the rest of the year.

**Alternate hypothesis:** The summer months have greater power outages than rest of the year.

The cleaned dataframe has 54 features and 1534 observations.

**Relevant columns:**
- `U.S._STATE`: Represents all the states in the continental U.S.
- `YEAR`: Indicates the year when the outage event occurred
- `MONTH`: Indicates the month when the outage event occurred
- `CUSTOMERS.AFFECTED`: Number of customers affected by the power outage event
- `CLIMATE.REGION`: U.S. Climate regions as specified by National Centers for Environmental Information (nine climatically consistent regions in continental U.S.A.)
- `DEMAND.LOSS.MW`: Amount of peak demand lost during an outage event (in Megawatt) [but in many cases, total demand is reported]
- `TOTAL.PRICE`: Average monthly electricity price in the U.S. state (cents/kilowatt-hour)
- `TOTAL.CUSTOMERS`: Annual number of total customers served in the U.S. state
- `POPULATION`: Population in the U.S. state in a year

# Data Cleaning

In the original data in the excel file, the 5 rows are unwanted as they are just the title and some notes about the data. The dataframe and its columns "start" from the 6th row downward. Additionally, below the columns, there is a row to specify the units of the column if necessary. We also removed this columns when cleaning the data as there are no actual observations.

At this point, the data being loaded has all the columns and observations in the excel file data. However, the columns ``OUTAGE.START.DATE`` and ``OUTAGE.START.TIME`` can be combined as the first always has a time of "00:00:00". The same is true for the restoration date and time. We combined these columns into ``OUTAGE.START`` and ``OUTAGE.RESTORATION``, dropping the original 4.


|   OBS |   YEAR |   MONTH | U.S._STATE   | POSTAL.CODE   | NERC.REGION   | CLIMATE.REGION     |   ANOMALY.LEVEL | CLIMATE.CATEGORY   | CAUSE.CATEGORY     | CAUSE.CATEGORY.DETAIL   |   HURRICANE.NAMES |   OUTAGE.DURATION |   DEMAND.LOSS.MW |   CUSTOMERS.AFFECTED |   RES.PRICE |   COM.PRICE |   IND.PRICE |   TOTAL.PRICE |   RES.SALES |   COM.SALES |   IND.SALES |   TOTAL.SALES |   RES.PERCEN |   COM.PERCEN |   IND.PERCEN |   RES.CUSTOMERS |   COM.CUSTOMERS |   IND.CUSTOMERS |   TOTAL.CUSTOMERS |   RES.CUST.PCT |   COM.CUST.PCT |   IND.CUST.PCT |   PC.REALGSP.STATE |   PC.REALGSP.USA |   PC.REALGSP.REL |   PC.REALGSP.CHANGE |   UTIL.REALGSP |   TOTAL.REALGSP |   UTIL.CONTRI |   PI.UTIL.OFUSA |   POPULATION |   POPPCT_URBAN |   POPPCT_UC |   POPDEN_URBAN |   POPDEN_UC |   POPDEN_RURAL |   AREAPCT_URBAN |   AREAPCT_UC |   PCT_LAND |   PCT_WATER_TOT |   PCT_WATER_INLAND | OUTAGE.START        | OUTAGE.RESTORATION   |
|------:|-------:|--------:|:-------------|:--------------|:--------------|:-------------------|----------------:|:-------------------|:-------------------|:------------------------|------------------:|------------------:|-----------------:|---------------------:|------------:|------------:|------------:|--------------:|------------:|------------:|------------:|--------------:|-------------:|-------------:|-------------:|----------------:|----------------:|----------------:|------------------:|---------------:|---------------:|---------------:|-------------------:|-----------------:|-----------------:|--------------------:|---------------:|----------------:|--------------:|----------------:|-------------:|---------------:|------------:|---------------:|------------:|---------------:|----------------:|-------------:|-----------:|----------------:|-------------------:|:--------------------|:---------------------|
|     1 |   2011 |       7 | Minnesota    | MN            | MRO           | East North Central |            -0.3 | normal             | severe weather     | nan                     |               nan |              3060 |              nan |                70000 |       11.6  |        9.18 |        6.81 |          9.28 |     2332915 |     2114774 |     2113291 |       6562520 |      35.5491 |      32.225  |      32.2024 |         2308736 |          276286 |           10673 |           2595696 |        88.9448 |        10.644  |       0.411181 |              51268 |            47586 |          1.07738 |                 1.6 |           4802 |          274182 |       1.75139 |             2.2 |      5348119 |          73.27 |       15.28 |           2279 |      1700.5 |           18.2 |            2.14 |          0.6 |    91.5927 |         8.40733 |            5.47874 | 2011-07-01 17:00:00 | 2011-07-03 20:00:00  |
|     2 |   2014 |       5 | Minnesota    | MN            | MRO           | East North Central |            -0.1 | normal             | intentional attack | vandalism               |               nan |                 1 |              nan |                  nan |       12.12 |        9.71 |        6.49 |          9.28 |     1586986 |     1807756 |     1887927 |       5284231 |      30.0325 |      34.2104 |      35.7276 |         2345860 |          284978 |            9898 |           2640737 |        88.8335 |        10.7916 |       0.37482  |              53499 |            49091 |          1.08979 |                 1.9 |           5226 |          291955 |       1.79    |             2.2 |      5457125 |          73.27 |       15.28 |           2279 |      1700.5 |           18.2 |            2.14 |          0.6 |    91.5927 |         8.40733 |            5.47874 | 2014-05-11 18:38:00 | 2014-05-11 18:39:00  |
|     3 |   2010 |      10 | Minnesota    | MN            | MRO           | East North Central |            -1.5 | cold               | severe weather     | heavy wind              |               nan |              3000 |              nan |                70000 |       10.87 |        8.19 |        6.07 |          8.15 |     1467293 |     1801683 |     1951295 |       5222116 |      28.0977 |      34.501  |      37.366  |         2300291 |          276463 |           10150 |           2586905 |        88.9206 |        10.687  |       0.392361 |              50447 |            47287 |          1.06683 |                 2.7 |           4571 |          267895 |       1.70627 |             2.1 |      5310903 |          73.27 |       15.28 |           2279 |      1700.5 |           18.2 |            2.14 |          0.6 |    91.5927 |         8.40733 |            5.47874 | 2010-10-26 20:00:00 | 2010-10-28 22:00:00  |
|     4 |   2012 |       6 | Minnesota    | MN            | MRO           | East North Central |            -0.1 | normal             | severe weather     | thunderstorm            |               nan |              2550 |              nan |                68200 |       11.79 |        9.25 |        6.71 |          9.19 |     1851519 |     1941174 |     1993026 |       5787064 |      31.9941 |      33.5433 |      34.4393 |         2317336 |          278466 |           11010 |           2606813 |        88.8954 |        10.6822 |       0.422355 |              51598 |            48156 |          1.07148 |                 0.6 |           5364 |          277627 |       1.93209 |             2.2 |      5380443 |          73.27 |       15.28 |           2279 |      1700.5 |           18.2 |            2.14 |          0.6 |    91.5927 |         8.40733 |            5.47874 | 2012-06-19 04:30:00 | 2012-06-20 23:00:00  |
|     5 |   2015 |       7 | Minnesota    | MN            | MRO           | East North Central |             1.2 | warm               | severe weather     | nan                     |               nan |              1740 |              250 |               250000 |       13.07 |       10.16 |        7.74 |         10.43 |     2028875 |     2161612 |     1777937 |       5970339 |      33.9826 |      36.2059 |      29.7795 |         2374674 |          289044 |            9812 |           2673531 |        88.8216 |        10.8113 |       0.367005 |              54431 |            49844 |          1.09203 |                 1.7 |           4873 |          292023 |       1.6687  |             2.2 |      5489594 |          73.27 |       15.28 |           2279 |      1700.5 |           18.2 |            2.14 |          0.6 |    91.5927 |         8.40733 |            5.47874 | 2015-07-18 02:00:00 | 2015-07-19 07:00:00  |

# Univariate Analysis

## Power Outages by Region

<iframe src="assets/plot_univar_1.html" width=800 height=600 frameBorder=0></iframe>

### Explanation of Graph: 'Power Outages by Region'
This is a graph displaying the distributions of power outages within climate regions in the U.S. 

It is evident that the Northeast region has the highest number of power outages, totaling 350, while the West North Central region has the least, with fewer than 20 outages. For the most part, the other regions fall between 100 to 250 outages.

## Power Outages by Month

<iframe src="assets/plot_univar_2.html" width=800 height=600 frameBorder=0></iframe>

# Bivariate Analysis

## State Proportions of Customers

<iframe src="assets/plot_bivar_1.html" width=800 height=600 frameBorder=0></iframe>

### Explanation of Graph: 'State Proportions of Customers'
This graph displays the proportion of customers to the population mean over the years of each state.

There isn't particularly any state that is a significant outlier. Hawaii and Maine have a small customer base while Maine has a surprising amount. 

# Interesting Aggregates

## Mean Price vs Mean Customers per State

<iframe src="assets/plot_agg_1.html" width=800 height=600 frameBorder=0></iframe>

### Explanation of Graph: 'Mean Price vs Mean Customers per State'
'Mean Price vs Mean Customers per State' reveals the outliers of data set. Hawaii is outlandishly expensive despite have a small number of customers. California has a massively large customer base. 

# Assessment of Missingness

## NMAR Analysis
Column that we think is NMAR: ``CAUSE.CATEGORY.DETAIL``

``CAUSE.CATEGORY.DETAIL`` is a detailed description of the event categories causing the major power outages. It is NMAR because the cause doesnt fit in one of the limited categories due to being a multitude of causes. To possibly collect more data to make it MAR, we can have someone present at the site of the power outage and provide detailed observations of everything going on there. From this text, we can parse it for observations previously present in CAUSE.CATEGORY.DETAIL and count the number of unique observations we see. If the missing is correlated to higher counts of these occurrences, we can say that ``CAUSE.CATEGORY.DETAIL`` is MAR due to not being able to put a certain outage in a single category.


 



