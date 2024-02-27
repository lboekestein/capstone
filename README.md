# Evaluation the Value of Local News for Violence Prediction
#### Capstone Project - Luuk Boekestein

## Table of Contents
- [TODO's](#todos)
    - [Current TODO's](#current-todos)
    - [Future TODO's](#future-todos)
- [Mission Data](#mission-data)
    - [1. Newspaper data](#1-newspaper-data)
        - [1.1 Professional News aggregation services](#11-professional-news-aggregation-services)
        - [1.2 Open-source News aggregation alternatives](#12-open-source-news-aggregation-alternatives)
        - [1.3 GDELT](#13-gdelt)
            - [1.3.1 Google BigQuery](#131-google-bigquery)
            - [1.3.2 Direct download of CSV files](#132-direct-download-of-csv-files)
            - [1.3.3 GDELT DOC API](#133-gdelt-doc-api)
            - [1.3.4 GDELT python package](#134-gdelt-python-package)
    - [2. Conflict data](#2-conflict-data)
        - [2.1 UCDP data](#21-ucdp-data)
    - [3. Baselines and standards to compare with](#3-baselines-and-standards-to-compare-with)
        - [3.1 VIEWS Forecast](#31-views-forecast)
        - [3.1 Mueller & Rauh's (2022) newspaper based prediction model](#31-mueller--rauhs-2022-newspaper-based-prediction-model)


# TODO's

### Current TODO's

- [ ] Collect data from GDELT Project
    - [X] Make a list of all countries and the ways they can be referred to
        - [X] Crosslist with GDELT naming conventions
        - [ ] Look at Mueller & Rauh's criteria for article selection
    - [X] Make a list of all relevant themes we want to track
        - [X] Look at GDELT documentation
        - [X] Check most frequently used themes
- [ ] Write Research Proposal (deadline March 13)
    - [ ] Narrow down RQ based on data availability
    - [ ] Extract relevant overlapping literature from ARW research
    - [ ] Narrow down methods and write methods section

### Future TODO's

- [ ] Collect data from UCDP to use as predictors
    - [ ] Make list of all relevant predictors
    - [ ] Narrow down timeframe
    - [ ] Scrape all data from UCDP API
- [ ] Distinguish between local, regional and global news?
    - [ ] Look into literature for measures of closeness to classify regional news
        - [ ] See Schafer paper? Van Atteveldt?
    - [ ] Aggregate data based on local regional and global news
- [ ] Narrow down and substantiate relevant themes as predictors
    - [ ] Look at GDELT documentation
    - [ ] Check most frequently used themes
    - [ ] Check literature for relevant features in other prediction models
    - [ ] See Mueller & Rauh's paper, and [Correlates of War](https://correlatesofwar.org/) projects?
    - [ ] Make sure predictions are of the same resolutions as Mueller & Rauh's and ViEWS standard
- [ ] Merge GDELT and UCDP dataset
- [ ] Make prediction model
    - [ ] See replication data from Mueller & Rauh's paper
    - [ ] Evaluate different machine learning models
    - [ ] Compute prediction accuracy
- [ ] Compare local, regional and global models, and in combination with each other
    - [ ] See is there is a statistically significant difference in prediction accuracy (Answer RQ)
    - [ ] Check correlation and differences between different models
- [ ] Compare with baseline models (ViEWS, Mueller & Rauh)
- [ ] Retrieve results, make vizualizations
- [ ] Start writing process

# Mission Data

## 1. Newspaper data

#### 1.1 Professional News aggregation services

Many large-scale news aggregating projects exist, though most of them are paid or only offer servics to large-scale research projects, companies or governments. A few examples are:
- [Lexisnexis](https://www.lexisnexis.com/en-us/gateway.page)
    - Offers large scale news aggregation and data insights, but is paid for large applications. There is a [student version](https://www.lexisnexis.com/nl-nl/producten/nexis-uni), and although an API is offered, it is explicitly not to be used for mass article scraping. As listed on their uni site [here](https://help.lexisnexis.com/Flare/nexisuni/US/nl_NL/Content/topic/gh_urlapisearch.htm)
        > Note: As a reminder, using the API to create an automated process or script to perform high-volume searches isn’t an appropriate use of this feature.
        >
        Nevertheless, I tried to script their API in the [experiments notebook](data/newsdata/experiments.ipynb#lexis-nexis), but as expected this did not work
- [BBC Monitoring](https://monitoring.bbc.co.uk/)
    - Offers news monitoring and analysis, but is paid and seems unaccessible for me as an undergraduate

#### 1.2 Open-source News aggregation alternatives

- [Newscatcher](https://github.com/kotartemiy/newscatcher)
    - Python package that programmatically collect normalized news from (almost) any website. This is a manual scraper, so could be useful, but seems to have mainly US-centric news sites, and is designed for live news scraping, not historical data.
- [Pygooglenews](https://github.com/kotartemiy/pygooglenews)
    - Python package that serves as an API for google news. This could be useful, but has to be checked for up-to-date-ness, as the last commit was 3 years ago
- [Commoncrawl news dataset](https://commoncrawl.org/blog/news-dataset-available)
    - Open source data archive for news published on the internet. Large scale and relatively accessible, but only contains data from 2016 onwards.

#### 1.3. GDELT

The [GDELT Project](https://www.gdeltproject.org/) is a large-scale event database that scrapes millions of news-articles per second and codes them into event-data. It's open source and contains multiple finegrained datasets that could be useful for this project. The two main ones are:

- [GDELT Event Dataset](http://data.gdeltproject.org/documentation/GDELT-Event_Codebook-V2.0.pdf)
    - Contains records of event-data, including links to articles that were at the source of a codified event
- [GDELT Global Knowledge Graph (GKG)](http://data.gdeltproject.org/documentation/GDELT-Global_Knowledge_Graph_Codebook-V2.1.pdf)
    - Connects news sources, themes, people, events and locations with each other in a massive dataset spanning back to 2017.
    - Includes translations of 65 languages, increasing the accessibility of local news.
    - Already contains preprocessing step of "Themes" extraction, which could serve as a base for a topic model-like approach.

The dataset is immensily largely (~100TiB), and even though it is open-sourced, there are only a few different ways of accessing this dataset. 

##### 1.3.1. Google BigQuery

Google BigQuery is the main way they suggest users work with the GDELT data as it can handle the large size, but it is a paid service. Since BigQuery estimates Query costs based on the total size of the data, any query will likely be very costly, no matter what limit I set. Nevertheless, I ran a so-called dry-run query to estimate the costs [here](data/newsdata/experiments.ipynb), and a simple query extracting just a few of the columns from the GKG dataset would process around `14935754508141` bytes. This is somewhere around €90 per query, which is not feasible.

##### 1.3.2. Direct download of CSV files

GDELT also offers a download feed where you can download the last 15min of data in the form of a csv file, but here we run into the same problem as before and the data is too large too handle. I tried out the way to retrieve that data [here](data/newsdata/experiments.ipynb).

##### 1.3.3. GDELT DOC API

The final option that could be of use to me is the DOC API, documented [here](https://blog.gdeltproject.org/gdelt-doc-2-0-api-debuts/). This API allows for the retrieval of specific subcollections of the data, which allows me to download only the data I want using specific search terms. This could very well work, and I've used it in a test-case [here](gdelt/gdelt_api.ipynb)

In short, this allows me to get a dataset that has rows containing information like:
- date
- percentage of articles from 
    - source country x 
    - concerning country y
    - with theme z

The GDELT Themes can be found [here](http://data.gdeltproject.org/api/v2/guides/LOOKUP-GKGTHEMES.TXT), and are based on a wide array of features. There are many, so this will require some selection process. 

The advantage of this methods is that the API allows you to filter on specific themes and things mentioned in articles in 65 languages at the same time, so when I search for "Netherlands" I will get all articles mentioning the Netherlands in any language. The themes could then be used in a topic model-like approach and serve as predictors for the model.

It does mean that much of the preprocessing will have been done by GDELT for me, which is a big advantage. On the other hand the documentation is a bit vague in some places so trusting the data might be tricky. 

##### 1.3.4 GDELT python package

There is also a python package that allows for an easier workflow with Gdelt data, see the [pypi page](https://pypi.org/project/gdelt/). This could be an alternative in case the DOC API approach doesn't work, but it would still require some server hiring or use of a cloud service. A tutorial for this approach is [here](https://www.youtube.com/watch?v=kzzQxlk9bBY)

## 2. Conflict data

#### 2.1. UCDP data

The [UCDP data](https://ucdp.uu.se/encyclopedia) contains many datasets on fatalities, conflict, battledeaths and many other predictors that could be useful as target variables. See for an overview the [downloads page](https://ucdp.uu.se/downloads/). A few especially useful examples are:

- [UCDP/PRIO Armed Conflict Dataset version 23.1](https://ucdp.uu.se/downloads/index.html#armedconflict)
    - Contains information on armed conflicts, including the number of fatalities, start and end dats, location, actors, supporting actors, conflict issue, intensity level, type of conflict and more. See the [codebook](https://ucdp.uu.se/downloads/ucdpprio/ucdp-prio-acd-231.pdf) for more information.
- [UCDP Georeferenced Event Dataset (GED) Global version 23.1](https://ucdp.uu.se/downloads/index.html#ged_global)
    - Fine-grained violence event dataset, with source articles, date, location, actors, fatalities, type of violence and more. Similar to GDELT dataset, but specifically violence related. See the [codebook](https://ucdp.uu.se/downloads/ged/ged231.pdf) for more information.

The UCDP site also offers an API, which allows for easier data handling, which can be called as follows:
```
https://ucdpapi.pcr.uu.se/api/<resource>/<version>?<pagesize=x>&<page=x>`
````
Both the Armed Conflict Dataset and the GED dataset are available, as `ucdpprioconflict` and `gedevents` respectively.

For possible filtering methods and specific calling methods, see the [API documentation](https://ucdp.uu.se/apidocs/)

## 3. Baselines and standards to compare with

#### 3.1 VIEWS Forecast

The ViEWS forecasting project, host of most of the state-of-the-art prediction models at the moment, as a [data page](https://viewsforecasting.org/data/#latest-data) where most prediction data of their main models if publicly available. This could be useful to compare my model with the state-of-the-art. They offer predictions for different models, listed [here](https://github.com/prio-data/views_api/wiki/Available-datasets). 

They also offer an API to retrieve predictions for specific regions and at specific times, which can be called as follows:

```
https://api.viewsforecasting.org/{run}/{loa}/[{type_of_violence}/[{variable}]]?filters
```

See their [API wiki](https://github.com/prio-data/views_api/wiki) for more information on filtering methods and variables.


#### 3.1 Mueller & Rauh's (2022) newspaper based prediction model

The paper by [Mueller & Rauh (2022)](https://doi.org/10.1093/jeea/jvac025) offers a prediction model that is hosted at [conflictforecast.org](https://conflictforecast.org/). This could be especially useful since they explicitly use newspaper data as a predictor.

Their predictions can be downloaded [here](https://conflictforecast.org/downloads). Furthermore, they offer an API to retrieve predictions for specific regions and at specific times, which can be called as follows:

```
https://api.backendless.com/C177D0DC-B3D5-818C-FF1E-1CC11BC69600/C5F2917E-C2F6-4F7D-9063-69555274134E/services/fileService/get-file-listing?date=01-2022
```

I've quickly experimented with this API [here](data/baselines/conflictforecast/conflictforecastpredictions.ipynb). 
See their [API documentation](https://conflictforecast.org/downloads) for more information on filtering methods and variables.