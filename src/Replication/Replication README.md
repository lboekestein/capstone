# Replication instructions for the project "The Value of Local News Sources for Conflict Forecasting: Predicting Changes in Violence Intensity in Afghanistan Using Themes in the Media"

This README file contains the instructions to replicate the results of the paper "The Value of Local News Sources for Conflict Forecasting: Predicting Changes in Violence Intensity in Afghanistan Using Themes in the Media". 

*TLDR*
>- The code for replicating the prediction results is given in the [prediction notebook](Predicting.ipynb). This contains the code for training the models and evaluating the results, and replicates Table 1, Table 2 and Appendix A of the paper.
> - The code for replicating the visualizations in the paper is in the [vizualization notebook](Vizualization.ipynb). This contains the code for the plots given in Figure 1-6 in the paper. The figures themselves are saved in the [Paper figures folder](/src/Replication/Paper%20figures/).
> - Both the prediction and vizualization notebook depend on datasets that were retrieved using code in this repository, but were too large to include in the repository itself. Thus, the rest of this README file will explain how to generate these datasets. Alternatively, the datasets are available upon request from the author (email luuk.boekestein@gmail.com).

## Instructions for generating the datasets

The analysis combines sources from the Global Database of Events, Language, and Tone (GDELT) with the Armed Conflict Location & Event Data Project (ACLED). The GDELT data is used to extract themes from news articles, and the ACLED data is used to extract conflict fatalities.

### ACLED data

The ACLED data can be downloaded from the [ACLED website](https://acleddata.com/data/#download), and should be saved in the `data/ACLED` folder. In the [ACLED notebook](../ACLED/ACLED.ipynb) the ACLED data is cleaned and preprocessed into a dataset with monthly conflict intensity changes, and saved as 'intensity_change_monthly_country.csv' in the `data/ACLED` folder.

### GDELT data

The GDELT data was scraped manually. In order to replicate this, see the [GDELT scraping notebook](../GDELT/scraping_gdelt.ipynb) and the [GDELT collect notebook](../GDELT/collect_all_data.ipynb). The scraping operation took about 80 hours to complete, and the resulting datasets are in in [this](../../data/GDELT/saved_data/) folder.

### Merging data

The GDELT and ACLED datasets are then merged in the [preprocessing notebook](../Predicting/Preprocess_data.ipynb), and this results in the pickled dataset that the prediction notebook depends on. This dataset will be saved as 'local_regional_global.pkl' and should then be found [here](../../data/Test_training/local_regional_global.pkl).

### Replication

If all datasets have been reconstructed as above, then the prediction and vizualization notebooks should be able to run without any issues. The prediction notebook will replicate the results in Table 1, Table 2 and Appendix A of the paper, and the vizualization notebook will replicate the figures in the paper.

For some of the notebooks above to run, the packages in the `requirements.txt` file may have to be installed. This can be done by running the following command in the terminal:

```bash
pip install -r requirements.txt
```