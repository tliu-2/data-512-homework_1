# DATA 512 Homework 1
 
This notebook constructs and analyzes a dataset from monthly article traffic data for a subset of pages on 
rare diseases from English Wikipedia through the Wikimedia API. 

There are two primary goals for this project:
1. Construct 3 separate datasets corresponding to:
   1. Monthly mobile page views
   2. Monthly desktop page views
   3. Monthly cumulative views
2. Conduct a basic visual analysis on the timeseries data examining:
   1. Article pages with the highest and lowest page requests for desktop and mobile access.
   2. Article pages with the largest peak page views over the entire time series by access type.
   3. Article pages that have the fewest months of data.

Wikimedia's data is provided under the [CC0 1.0 License](https://creativecommons.org/publicdomain/zero/1.0/).
Abiding by Wikimedia Foundations' [terms of use](https://foundation.wikimedia.org/wiki/Policy:Terms_of_Use),
this project does its best to provide a dataset and accompany basic analysis that is accurate to the data and
not intentionally misleading or false. The authors of the project receive no contribution from any other party that
is a conflict of interest.

Wikimedia Foundations' API can be found here: https://doc.wikimedia.org/generated-data-platform/aqs/analytics-api/.

This project uses the file rare-diseased_cleaned.AUG.2024.csv as the source for articles to pull from the
Wikimedia API.

__The notebook generates three files:__
1. rare-disease_monthly_cumulative
   1. Page view data containing view counts from both desktop and mobile devices.
2. rare-disease_monthly_desktop
   1. Page view data containing view counts from only desktop.
3. rare-disease_monthly_mobile
   1. Page view data containing view counts from only mobile devices.


All three files are stored in the form where articles are keys and the values is a list of dictionaries
containing the remaining data such as views.
The keys are strings which represent the page title. The list of dictionaries contain monthly data whose
keys are the different are different kinds of data (timestamp, page views, etc.)

An example of the three files' schema:
```
{
   "Gyrification": [
           {
               "project": "en.wikipedia",
               "article": "Gyrification",
               "granularity": "monthly",
               "timestamp": "2020100100",
               "agent": "user",
               "views": 2315
           },
           {
               "project": "en.wikipedia",
               "article": "Gyrification",
               "granularity": "monthly",
               "timestamp": "2022090100",
               "agent": "user",
               "views": 1738
           },
           ...
}
```

## Python Version and Packages
For replication and reproduction of this data set construction and analysis, the Python version and packages are
listed here:

- Python 3.10.11 
- Jupyter 1.1.1 
- Polars 1.9.0 
- Pandas 2.2.3 
- Numpy 2.1.1 
- Matplotlib 3.9.2