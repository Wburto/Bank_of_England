# LSE Employer Project: Bank of England

# The Maginficent Seven
## Team members:
### Craig McCracken​
### Emily Coughlan​
### Emma Roberts​
### Ian Munro​
### Joel Baksh​
### Will Burton​


# Structure of this submission
This repository was not used as a working space and therefore there is no version history of changes that have been made - it exists simply for code submission. There are multiple workbooks in this repository, divided into Final analysis and Early Drafts folders. Each folder has a number of subfolders with individual workbooks including the dependencies required to run the code.
The file name, dependencies, purpose and output of each folder are described below (Please note that some data files are zipped due to size, indicated in the description)

# Testing
All code in the this repository was tested in Juypter Notebooks through a clean installation of Anaconda.  In several of the notebooks, additional libraries are loaded and files downloaded as required.  For reference these are listed below.

- langdetect
- PyMuPDF
- PyPDF2
- pysentiment2
- requests
- textblob
- torch
- torchvision
- torchaudio
- tqdm
- transformers
- wordcloud
- nltk.download('punkt')
- nltk.download('stopwords')
- nltk.download('vader_lexicon')

It should be noted that some of the notebooks download large files and some will take considerable time to execute, particularly the FinBERT processing of speech and MPR/FSR data.  Progress bars are included through tqdm.



# Final analysis

## Economic data collation

#### Filename

- Economic Data Collation.ipynb

#### Dependencies

- base_rate.csv
- brent_usd_1987_2024.csv
- cpi.csv
- euro_2003_2024.csv
- ftse_250.csv
- ftse100_gbp_1990_2024.csv
- gdp.csv
- gold.csv
- house_prices.csv
- one_mo_bond.csv
- ten_yr_bond.csv
- two_yr_bond.csv
- unemployment.csv
- usd_2003_2024.csv
- wage_growth.csv

#### Purpose

- This notebook pulls all the economic data which was pulled from the internet into a single DataFrame on a daily basis and exports it to .csv.
- All economic data was viewed in excel prior to wrangling in this python notebook (see commentary where applicable).

#### Output

- combined_eco_data_1999_2022.csv

<br><br>

## Combining NLP and Economic data

#### Filename

- Combining eco and nlp data.ipynb

#### Dependencies

- all_speeches_scores_daily.xlsx
- combined_eco_data_1999_2022.csv

#### Purpose

- This notebook combines all the economic data on a daily basis with all of the speech sentiment NLP data on a daily basis.
- Data was sense checked in excel first. Since it was a small dataset, a number of boolean columns were added to the speech data. These columns were to indicate if a day was a BOE or Fed speech day, FSR or MPR report day (as not all days have speeches). This was to make filtering data easier at a later date.

#### Output

- all_data.csv

<br><br>

## Economic indicators

#### Filename

- Final Economic Indicators.ipynb

#### Dependencies

- all_data.csv
- all_speeches_scores_daily.csv

#### Purpose

- The purpose of this notebook is to try and find any correlation or possibly causation between CPI, GDP, Unemployment, and Wage growth with the speeches made.

#### Output

- The output consists of multiple plots for economic indicators at different time frames, as well as for all the speeches, and also grouped into the Governor's speeches solely. It groups speeches into either positive or negative polarity and attempts to visualise any correlation between economic indicators and the speech sentiment at the time.

<br><br>

## Market indicators

#### Filename

- Final Market Indicators.ipynb

#### Dependencies

- all_data.csv
- all_speeches_scores_daily.csv

#### Purpose

- The purpose of this notebook is to try and find any correlation or possibly causation between all the market indicators above and the speeches made.

#### Output

- The output consists of multiple plots for the market indicators at different time frames, as well as for all the speeches, and also grouped into the Governor's speeches solely. It groups speeches into either positive or negative polarity and attempts to visualise any correlation between market indicators and the speech sentiment at the time. This has been done for the whole period, as well as times of significance and in more granular form into months, weeks, and days.

<br><br>

## FinBERT

Filename:

- finbert \_sentiment_analysis.ipynb

Dependencies:

- speech_bert_1.csv

Purpose:

- Here we aim to quantify the speech data into sentiment scores by running it through the FinBERT NLP model.
- FinBERT is a deep learning large language model and can negotiate context at a far superior level to the other models. As it was trained on a variety of sources, including financial articles, no normalisation has taken place.
- The output file 'finbert_scores_raw_v2' contains the 'speech_bert_1.csv' contents as before, but now includes the compound (finbert_polarity), pos, neg, and neutral polarity scores.

Output:

- finbert_scores_raw_v2

<br><br>

## PySentiment2

#### Filename

- pysentiment2_sentiment_analysis.ipynb

#### Dependencies

- _speech_blob_1.csv_

#### Purpose

- Here we aim to quantify the speech data into sentiment scores by running it through the PySentiment2 (Loughran McDonald) NLP model.
- We require the same level of normalisation as TextBlob did so we use the same speech file. The _'speech_blob_1.csv'_ file uses speech text that has been normalised in the following way:
  - Ensure text is clean (Remove noise): Remove noise such as URLs, HTML tags, hashtags, mentions (if we don't believe it would contribute to sentiment). From the above, we have decided to keep hashtags and mentioned, but removed URLs
  - Ensure text is clean (Handle missing values): Also ensure there are no missing values. We have completed this step above.
  - Language: TextBlob primarily supports English out of the box. We have identified which speeches are in English.
  - Text preprocessing (Lowercase): Processed below. - Text preprocessing (Remove Stopwords): Processed below
  - Text preprocessing (Lemmatization): Lemmatization was not done at this stage (it is also optional), as we have received a sentiment labelled wordlist from BoE where the reference text has not been lemmatized.
- The output file _'pysentiment2_scores.csv'_ contains the ‘_speech_blob_1’_ contents as before, but now includes the polarity and subjectivity columns.

Output:

- _pysentiment2_scores.csv_

<br><br>

## TextBlob

#### Filename

- textblob_sentiment_analysis

#### Dependencies

- speech_blob_1.csv

#### Purpose

- Here we aim to quantify the speech data into sentiment scores by running it through the TextBlob NLP model.
  - The 'speech_blob_1.csv' file uses speech text that has been normalised in the following way:
  - Ensure text is clean (Remove noise): Remove noise such as URLs, HTML tags, hashtags, mentions (if we don't believe it would contribute to sentiment). From the above, we have decided to keep hashtags and mentioned, but removed URLs
  - Ensure text is clean (Handle missing values): Also ensure there are no missing values. We have completed this step above.
  - Language: TextBlob primarily supports English out of the box. We have identified which speeches are in English.
  - Text preprocessing (Lowercase): Processed below. - Text preprocessing (Remove Stopwords): Processed below
  - Text preprocessing (Lemmatization): Lemmatization was not done at this stage (it is also optional), as we have received a sentiment labelled wordlist from BoE where the reference text has not been lemmatized.
- The output file 'textblob_scores.csv' contains the ‘speech_blob_1’ contents as before, but now includes the polarity and subjectivity columns.

#### Output

- textblob_scores.csv

<br><br>

## Vader

#### Filename

- vader_sentiment_analysis.ipnyb

#### Dependencies

- speech_vader_1.csv

#### Purpose

- Here we aim to quantify the speech data into sentiment scores by running it through the Vader NLP model.
- The ‘speech_vader_1’ file uses speech text that has been normalised in the following way:
  - Ensure text is in English : We have tagged each speech for their language.
  - Handle missing values: That has been completed in the previous cleaning steps.
  - Standardise text data : Vader works well if the text is standardised (i.e. ensure consistent use of quotation marks etc). We will take the assumption that the use of quotation marks etc has been applied consistently.
  - Remove unnecessary elements: It is good practice to remove URLs and other specific mark ups. However in the same vein, it is important not to over clean. As seen above, we have kept hashtags and mentions as they appeared to be important in providing context to the speeches, however URLs have been removed.
  - Ensure Data is in a Suitable Format: The data is contained in a dataframe column.
- The output file ‘vader_scores.csv’ contains the ‘speech_vader_1’ contents as before, but now includes the compound, pos, neg, and neutral polarity scores.

#### Output

- vader_scores.csv

<br><br>

## All speeches

#### Filename

- all_speeches_scores.ipynb

#### Dependencies

- vader_scores.csv
- textblob_scores.csv
- pysentiment2_scores.csv
- finbert_scores_raw_v2.csv

#### Purpose

- This file first aims to collate all of the NLP model’s scores into one singular dataframe.
  - This file is outputted as ‘all_speeches_scores’.- Then, in order to best align with the economic data, ‘all_speeches_scores’ is forward filled to create daily speech sentiment scores across all of the models.
- This file is outputted as 'all_speeches_scores_daily.csv'.
- Then some more general exploratory analysis is conducted using various visualisations. Which includes an interactive plot called ‘daily_speech_sentiment_plot’.

#### Output

- all_speeches_scores
- all_speeches_scores_daily.csv
- daily_speech_sentiment_plot

#### Filename

- all_speeches_scores_frequencies.ipynb

#### Dependencies

- _all_speeches_scores.csv_

#### Purpose

- This file seeks to explore polarity frequencies by:
  - Sorting by top 20 pos/neg speeches for three models (Vader, LM, FinBERT)
  - Then using a more detailed analysis and word clouds, we explore top 30 most positive/negative words according to the FinBERT model specifically.

#### Output

- n/a

<br><br>

## Heatmap - ELB & Hiking Cycle

#### Filename

- Heatmap - Period-specific sentiment.ipynb

#### Dependencies

- all_data.csv

#### Purpose

- Analyse correlation between FinBERT polarity scores and key economic indicators at specific time periods:
- Base rate nearing the Effective Lower Bound (Between 5th March 2009 - 4th May 2022) also referred to as 'ELB' in the markdown below.
- The BoE implementing a hiking cycle (Between 5th May 2022 - 31st December 2022 (end of our dataset))
- As a control, the team also created a heatmap of correlations for the entire dataset period of 1999 - 2022 also to be able to compare and contrast between the three date ranges.

#### Output

- Correlation heatmaps for 1999-2022, the Effective Lower Bound and Hiking Cycle periods

<br><br>

## Speech Sentiment vs Eco Indicators over time

#### Filename

- BaseRate_CPI_Sentiment_Timescale.ipynb

#### Dependencies

- all_data.csv

#### Purpose

- Analyse the movement of Base Rate, CPI, and FinBERT speech sentiment over time

#### Output

- Interactive HTML files of economic metrics and sentiment over time
- Plots of base rate, CPI and average sentiment over time

<br><br>

## Analysis of FinBERT Sentiment Overtime and Versus Base Rate

#### Filename

- Analysis of Finbert Sentiment Overtime and Versus Base Rate.ipynb

#### Dependencies

- all_data.csv

#### Purpose

- To answer the business question: Does sentiment significantly change alongside macroeconomic indicators such as bank base rate and CPI?
- Define and section the time period into more manageable periods to analyse / deep dive
- Changes in sentiment over time
- Does speech sentiment correlate to base rate changes?
- Predictive model attempt: can the sentiment of a speech predict the base rate change?

#### Output

- Line plot of base rate and cpi over time, with key events marked.
- Box plot of FInbert polarity distribution for defined time periods
- Line plot of Finbert monthly average polarity over time

<br><br>

## Report downloading and extraction

#### Filename

- report_extraction - final.ipynb

#### Dependencies

- report_dates.csv
- The notebook will also automatically download all Monetary Policy and Financial Stability Reports and which are used in the code

#### Purpose

- Automatically download all the MPC and FSR pdf report files for the period 1999-2022, accounting for variation in location and file naming conventions over time
- Extract full text using PyMUpdf
- Output cleaned files for passing to NLP

#### Output:

- financial_stability_reports.csv
- monetary_policy_reports.csv

<br><br>

## FSR and MPC

#### Filename

- fsr_mpc_sentiment_analysis_v3.ipynb

#### Dependencies

- financial_stability_reports.csv
- monetary_policy_reports.csv

#### Purpose

- This file aims to run both the FSR and MPC reports through FinBERT to find their respective polarity scores. Then the files are outputted separately to avoid the inevitable inclusion of any NaNs.
- During the pre-processing of the reports specific .csv’s were exported allowing the user to view which speeches were affected by the cleaning process. These are self-explanatory in the output below.
- Then, once both the FSR and MPC reports have been run through FinBERT they are exported as ‘fsr_finbert_scores.csv’ and ‘mpc_finbert_scores.csv’.
- However further cleaning was required before the final export, which mostly involved removing unnecessary columns from each dataframe. These were exported as ‘fsr_finbert_scores_final.csv’ and ‘mpc_finbert_scores_final.csv’ and are in bold below to highlight their significance as the main file output.
- Finally word frequency analysis was conducted on both the FSR and MPC reports to discover the top 30 positive/negative words by FinBERT polarity.

#### Output

fsr_data_with_hashtag.csv

fsr_data_with_mentions.csv

fsr_data_with_urls.csv

fsr_finbert_scores.csv

fsr_finbert_scores_final.csv

mpc_data_with_hashtag.csv

mpc_data_with_mentions.csv

mpc_data_with_urls.csv

mpc_finbert_scores.csv

mpc_finbert_scores_final.csv

<br><br>

## Report Heat Map

#### Filename

- Speech MPR and FSR correlation.ipynb

#### Dependencies

- all_data.csv
- fsr_finbert_scores_final.csv
- mpc_finbert_scores_final.csv

#### Purpose

- This notebook looks at the following:
  - Does the speech sentiment correlate to the bank report (FSR and MPR) sentiment.

#### Output

- Correlation heatmap (in workbook)

<br><br>

# Early drafts

## Initial data exploration

#### Filename

- Explore the data_v5.ipynb

#### Dependencies

- all_speeches.csv (this is provided as all_speeches.zip) due to file size

#### Purpose

- Initial data exploration:
- Initial exploration and cleaning
- Initial summarisation of data
- Visualisation of data
- Preparation of data for NLP
- Pre-processing data for Vader, FinBERT, Textblob
- Further final summarisation and exploration of dataset

#### Output

- Processed .csv files (1.56Gb).

<br><br>

## Exploratory data analysis of market indicators, base rate, FSR and MPR against FinBERT

#### Filename

- EDA of market indicators, base rate, FSR and MPR against Finbert.ipynb

#### Dependencies

- all_data.csv

#### Purpose

- This notebook takes an early look at the data. The contents of it were used in team discussions and decision-making processes on what avenues to pursue further. The contents were not used in the final presentations / reports but did form part of the data analysis journey.
- It looks at:
- Market indicators vs. speech sentiment at a high level,
- The base rate vs. speech sentiment at a high level,
- FSR and MPR vs. speech sentiment at a high level

#### Output

Variety of exploratory plots, saved as .png files

<br><br>

## Report downloading and extraction

#### Filename

- report_extraction_eda.ipynb

#### Dependencies

- report_dates.csv

#### Purpose

- Download all Monetary Policy and Financial Stability reports between 1999 and 2022.
- Extract the full text and the summary/overview from the files and export as clean .csv files for input to NLP

#### Output

- All MPR and FSR in .pdf format between 1999 and 2022
- monetary_policy_reports.csv
- financial_stability_reports.csv
- monetary_policy_summary.csv

<br><br>

## Speech frequency exploration

#### Filename

- speeches_reports.ipynb

#### Dependencies

- cpi.csv
- ftse_gbp_1990_2024.xlsx
- Sentiment.csv
- speech_dates.csv
- Unemployment.csv

#### Purpose

- Initial exploration of :
  - Monetary Policy and Financial Stability frequency vs. economic indicators
  - Bank of England and Federal Reserve speeches vs. economic indicators
  - Speech frequency vs speech sentiment

#### Output

- Various .png exploratory visualisations

<br><br>

## FinBERT – 512 limit

#### Filename

- FinBert - 512 limit.ipynb

#### Dependencies

- speech_bert_1.csv (provided zipped as speech_bert_1.zip)

#### Purpose

- This was the first attempt to quantify the speech data into sentiment scores by running it through the FinBERT NLP model.
- FinBERT is a deep learning large language model and can negotiate context at a far superior level to the other models. As it was trained on a variety of sources, including financial articles, no normalisation has taken place.
- However there is a token limit of 512 tokens for BERT models and we have an average number of token per speech at 2459. Which ultimately gives us a runtime error and an opportunity to find a work around. Which we do in the FinBERT working model provided.

#### Output

- n/a

<br><br>

## Economic Indicators

#### Filename

- Economic Indicators.ipynb

#### Dependencies

- all_data.csv
- all_speeches_scores_daily.csv
- Base rate.xlsx

#### Purpose

- The purpose of this notebook is to try and find any correlation or possibly causation between all the economic indicators above and the speeches made.

#### Output

- The output consists of multiple plots for economic indicators at different time frames, as well as for all the speeches, and also grouped into the Governor's speeches solely. It groups speeches into either positive or negative polarity and attempts to visualise any correlation between economic indicators and the speech sentiment at the time.

<br><br>

## Market Indicators

#### Filename

- Market Indicators.ipynb

#### Dependencies

- all_data.csv
- all_speeches_scores_daily.csv
- mpc_finbert_scores_final.csv
- fsr_finbert_scores_final.csv

#### Purpose

- Examine the speech sentiment vs daily market data to investigate correlation.
- The markets chosen for analysis were: Bonds (1m, 2y, 10y) FTSE100, FTSE250, Gold as well as Forex GBP/USD.

#### Output

- Multiple plots within the workbook.
