# Chicago Crime Prevention
## Adrien Talbot & Nacho Martínez Jacobson
### Data Analytics Bootcamp --- 25/02/2019 - 26/04/2019

## Overview
-------------
Our beleif prior to starting this analysis is that Chicago is high crime rate city comparing to the rest of the US, so we're conducting this analysis to check if we're correct.

The main questions we will be trying to answer are the following:

- Evolution of the arrest rate in Chicago compared to the rest of the US.
- Severity of crimes commited in Chicago vs the rest of the US.
- How has the arrest rate per neighbourhood evolved over the years?
- Are crimes more severe now than in the past?
- Has the proportion of crimes in school changed from 2001 to 2018?
- Has the nature, severity and proportion of crimes commited in schools changed over the years?

To complete our analysis we will implement a Machine Learning algorithm (Logistic Regression) that depending on specific features will determine if a crime will end up in arrest or not.


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
