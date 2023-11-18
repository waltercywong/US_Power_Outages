# US_Power_Outages
Data Analysis of US Power Outages for UCSD DSC80 Project

Nathan Ko, Walter Wong

# Introduction and Question Identification

This dataset has major power outage data in the continental U.S. from January 2000 to July 2016, provided by Laboratory for Advancing Sustainable Critical Infrastructure (LASCI)

Question: Are power outages worse during the summer? 

Null hypothesis: The summer months (7, 8, 9) have the same average number of customers affected as the rest of the year.

Alternate hypothesis: The summer months have greater power outages than rest of the year.

TODO\
We use mean to do permutation test
Accounting for outliers of both sets, but outliers are often urban centers which are important

1534 rows, 54 columns

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



<iframe src="assets/plot_univar_1.html" width=800 height=600 frameBorder=0></iframe>



did this shit work