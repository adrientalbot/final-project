# Chicago Crime Prevention
## Adrien Talbot & Nacho Martínez Jacobson
### Data Analytics Bootcamp --- 25/02/2019 - 26/04/2019

## Overview
-------------
By reading an article, we found out that the number of homicides in Chicago tremendously increased between 2015 and 2016 with an approximate growth of 58% in that period. 
Therefore, we got interested in the evolution of the total crimes in Chicago over time in order to see if the number of total crimes experienced a similar increase post 2015 as did the number of homicides.  

Our hypothesis prior to starting the analysis is that the number of crimes increased post 2015. But we  want to look at the seasonality trends from 2001 until nowadays as well. We are also interested in the evolution of the monthly arrest rate for the same period and the repartition of total crimes per district. 
We will check if that assumption is true in the following analysis. 

To complete our analysis we will implement a machine learning algorithm (using Random Forest Classifier) that will predict whether a specific crime (using features such as type of crime, location and arrest rate/district) leads to an arrest or not. We believe that it is important as this algorithm will allow the Chicago Police deparment to better allocate its resources (number of agents per district or neighborhood).

Finally, we will predict the number of crimes per month in the next five years by doing an SARIMA time series analysis (Samira.ipynb file).

## Repository structure
--------------------------------

- In the EDA folder, there is the data cleaning file (Data_Wrangling.ipynb) which contains all the cleaning we performed prior to starting the analysis. Additional cleaning is also present in the onehotencoding_analysis.ipynb file (from the analysis folder) to create the one hot encoded table to perform the machine learning algorithm. 

- In the main analysis folder, you will find the SARIMA times series analysis along with the Random Forest Classifier ML algorithm which gives predictions on arrests (classification_ml_prediction.ipynb) as well as the statistics file (stats_analysis.ipynb).


## Data preparation
---------------------
We will be working with the [Chicago Crime rates](https://data.cityofchicago.org/Public-Safety/Crimes-2001-to-present/ijzp-q8t2), which has reported incidents of crime from 2001 to the present date in the area of Chicago, US.

- For more information on the dataset, we have created a table containing detailed information about it.

## Data ingestion & Database
-------------------------------
- The downloaded database comes formatted as a .csv. Below we will provide code to load the database using python:

```python
# make sure to install pandas before running:
# pip3 install pandas

import pandas as pd
chicago_cmr = pd.read_csv('Crimes_-_2001_to_present.csv')
```

- Use of an API is also possible, we provide the code below and [API Doc link](https://dev.socrata.com/foundry/data.cityofchicago.org/ijzp-q8t2) for those who prefer working with it instead of the .csv file:

```python
# make sure to install these packages before running:
# pip3 install pandas
# pip3 install sodapy

import pandas as pd
from sodapy import Socrata

# Unauthenticated client only works with public data sets. Note 'None'
# in place of application token, and no username or password:
client = Socrata("data.cityofchicago.org", None)

# Example authenticated client (needed for non-public datasets):
# client = Socrata(data.cityofchicago.org,
#                  MyAppToken,
#                  userame="user@example.com",
#                  password="AFakePassword")

# First 2000 results, returned as JSON from API / converted to Python list of
# dictionaries by sodapy.
results = client.get("ijzp-q8t2", limit=2000)

# Convert to pandas DataFrame
results_df = pd.DataFrame.from_records(results)

```
## Data Wrangling and Cleaning
--------------------------------
