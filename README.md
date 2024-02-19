# Evaluation the Value of Local News for Violence Prediction
#### Capstone Project - Luuk Boekestein

# Data

## 1. Newspaper data

#### 1.1 Professional News aggregation services

Many large-scale news aggregating projects exist, though most of them are paid or only offer servics to large-scale research projects, companies or governments. A few examples are:
- [Lexisnexis](https://www.lexisnexis.com/en-us/gateway.page)
    - Offers large scale news aggregation and data insights, but is paid for large applications. There is a [student version](https://www.lexisnexis.com/nl-nl/producten/nexis-uni), but seems to contain mainly western news sources, and unclear if API is offered
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

TODO
- [ ] GDELT
- [ ] Different levels of aggregation
- [ ] Google BigQuery issues
- [ ] Mueller & Rauh (2022) raw data
 
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

See their [API documentation](https://conflictforecast.org/downloads) for more information on filtering methods and variables.