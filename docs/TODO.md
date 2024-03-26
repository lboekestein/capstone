# Project planning

## Overview of Deadlines

| Date  | What | Completed |
|---|---|---|
| March 13  | Research Proposal | Yes |
| April 10(?) | Writing Update  |   |
| May 8 | Draft of Thesis  |   |
| May 29 | Final Thesis |   |

## Timeline of project

### Week 5 (March 4 - March 10)

- [X] Make a list of all countries and the ways they can be referred to
        - [X] Crosslist with GDELT naming conventions
        - [X] Look at Mueller & Rauh's criteria for article selection
- [X] Make a list of all relevant themes we want to track
    - [X] Look at GDELT documentation
    - [X] Check most frequently used themes
- [X] Test scraping operation
    - [X] Scrape % for all themes
    - [X] Write code to estimate time left of scraping 
    - [X] Make code to retrieve data in chunks
    - [X] Test with first chunk
    - [X] Compress chunk
    - [X] Make code to uncompress and combine chunks
- [X] Scrape country to country coverage

### Week 6 (March 11 - March 17)
#### DEADLINE: Research Proposal

- [X] Write Research Proposal (deadline March 13)
    - [X] Narrow down RQ based on data availability
    - [X] Extract relevant overlapping literature from ARW research
    - [X] Narrow down methods and write methods section
- [X] Explore GDELT country to country coverage
    - [X] Evaluate which countries receive the most world-wide coverage
    - [X] Evaluate which countries talk about what countries the most
        - [ ] Compute closeness score on the basis of this?
        - [X] BONUS: make graph with geopandas

### Week 7 (March 18 - March 24)

- [X] Retrieve data from ACLED
    - [X] Evaluate cases of violence
    - [X] Evaluate presence of hard-cases
- [X] Smooth on monthly basis
- [X] Make predictor of log monthly change in violence
    - [X] See prediction metric given by Hegre e.a. 2022
- [X] Classify hard cases
- [X] Scrape data from ACLED as features
- [ ] Combine country naming of ACLED and GDELT
    - [ ] Find relation between conflict intensity and news coverage

### Week 8 (March 25 - March 31)
- [ ] Meeting Jelke on RP feedback
- [ ] Decide on country/countries to case study
    - [ ] Evaluate world-wide coverage
    - [ ] Evaluate relevant literature
- [ ] Scrape all data for selected country/countries from GDELT API
- [ ] Compute ACLED features
    - [ ] History of conflict, amount of cases per month
- [ ] Preprocess GDELT data
    - [ ] Classify coverage into local, regional and global
        - [ ] Look into literature for measures of closeness to classify regional news
        - [ ] See Schafer paper? Van Atteveldt?

### Week 9 & 10 (April 1 - April 14)
#### SOFT DEADLINE APRIL 10: Writing Update

- [ ] Make prediction model
    - [ ] Apply Random forest
    - [ ] If needed, evaluate other methods
- [ ] Evaluate model(s)
    - [ ] Compute prediction accuracy
    - [ ] Compute prediction difference for local, regional and global
    - [ ] See is there is a statistically significant difference in prediction accuracy (Answer RQ)
    - [ ] Compare with baseline models (ViEWS, Mueller & Rauh)
- [ ] OPTIONAL:
    - [ ] Generalize pipeline
    - [ ] Test for different countries

### Week 11 (April 15 - April 21)

- [ ] Make vizualizations
- [ ] Start writing process
    - [ ] Results
    - [ ] Discussion

### Weeks 12 & 13 (April 22 - May 5)
#### DEADLINE MAY 8: Draft of thesis

- [ ] Write draft of thesis

### Weeks 14-16 (May 6 - May 26)
#### DEADLINE MAY 29: Final thesis

- [ ] Write final thesis

