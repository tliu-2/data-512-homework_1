# DATA 512 Homework 1
This notebook constructs and analyzes a dataset from monthly article traffic data for a subset of pages on 
rare diseases from English Wikipedia through the Wikimedia API. 

There are three goals for this project:
1. Create a repository, code, and analysis which focuses on implementing the best practices described in
   ["Assessing Reproducibility"](http://www.practicereproducibleresearch.org/core-chapters/2-assessment.html)
   and ["The Basic Reproducible Workflow Template"](http://www.practicereproducibleresearch.org/core-chapters/3-basic.html).
2. Construct 3 separate datasets corresponding to:
   1. Monthly mobile page views
   2. Monthly desktop page views
   3. Monthly cumulative views
3. Conduct a basic visual analysis on the timeseries data examining:
   1. Article pages with the highest and lowest page requests for desktop and mobile access.
   2. Top 10 article pages with the largest peak page views over the entire time series by access type.
   3. Article pages that have the fewest months of data by access type.


## Dependencies
For replication and reproduction of this data set construction and analysis, the Python version and packages are
listed here:

- Python 3.10.11
- Jupyter 1.1.1
- Polars 1.9.0
- Pandas 2.2.3
- Pyarrow 17.0.0
- Numpy 2.1.1
- Matplotlib 3.9.2

## Folder Structure:
The repository is divided into two folders:
```bash
data-512-homework_1
├── data
│   ├── rare-disease_cleaned.AUG.2024.csv
│   ├── rare-disease_monthly_cumulative_2015010100-2024093000.json
│   ├── rare-disease_monthly_desktop_2015010100-2024093000.json
│   └── rare-disease_monthly_mobile_2015010100-2024093000.json
├── figures
│   ├── fewest_months_articles.png
│   ├── max_min_avg_views_articles.png
│   └── top10_articles_peak_views.png
├── LICENSE
├── README.md
└── construct_and_analyze_rare_diseases_view_data.ipynb
```

## Data Source Information and Disclosures

Wikimedia's data is provided under the [CC0 1.0 License](https://creativecommons.org/publicdomain/zero/1.0/).
Abiding by Wikimedia Foundations' [terms of use](https://foundation.wikimedia.org/wiki/Policy:Terms_of_Use),
this project does its best to provide a dataset and accompany basic analysis that is accurate to the data and
not intentionally misleading or false. The authors of the project receive no contribution from any other party that
is a conflict of interest.

Wikimedia Foundations' API can be found here: https://doc.wikimedia.org/generated-data-platform/aqs/analytics-api/.

## Data Source
This project uses the file `rare-diseased_cleaned.AUG.2024.csv` as the source for articles to pull from the
Wikimedia API. This file was provided by Dr. David W. McDonald from 
University of Washington's Department of Human Centered Design & Engineering and was collected by using a database
of rare diseases provided by the [National Organization for Rare Diseases (NORD)](https://rarediseases.org/) and
matching them to the Wikipedia articles.

The project uses the `disease` column as the article title in the API pull. In the event that the `disease` is
invalid or the API does not return the anticipated data, the disease is skipped and no page view data is collected
on that disease/page.


The notebook generates three data files which are stored in the data folder.
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

## Outputs
This project generates a total of six files.
Three of which are json datasets of article page view data which are described above.

The other remaining three being time series figures corresponding to the third goal of basic visual analysis.
- Article pages with the highest and lowest page requests for desktop and mobile access -> `max_min_avg_views_articles.png`
- Top 10 article pages with the largest peak page views over the entire time series by access type -> `top10_articles_peak_views.png`
- Article pages that have the fewest months of data by access type -> `fewest_months_articles.png`
