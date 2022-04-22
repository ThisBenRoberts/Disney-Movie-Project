#  Predicting Performance of Disney Movies

---

Using a history of film data, as well as performance data from associated directors and writers, can we estimate how well a Disney movie will perform at the box or the film's rating on IMDB?

### Author: 

Ben Roberts


## Table of Contents
1. Executive Summary
2. Sources & Data Dictionary
3. Analysis
4. Conclusions
5. Recommendations


## Executive Summary
---
According to Disney.com, as of April 2022, 657 Disney movies have been release since the first Disney feature film, Snow White and The Seven Dwarfs, premiered in 1937.  Since that time, the Walt Disney Company has expanded in many different directions. From theme parks, to TV, music, merchandise, cruise ships, venture capital, and streaming services, today The Walt Disney Company is truly a global conglomerate.  But it all started with the movies and in 2021, Disney and it's subsidiaries generated a box office revenue of $ 1.17 Billion dollars. Understanding just a small piece of the Disney magic that affects that revenue could have enormous implications.  This project seeks to understand if the previous performance of the Walt Disney Company, the Directors, and Writers of Disney movies can be used to estimate the success of future films.  This is just the first phase of a larger project that will hopefully lead to the creation of a tool for future film-makers could leverage to help create successful movie projects in the future.


### Definitions and Scope

This project focuses on full-length, feature releases from The Walt Disney Company. We are exluding Disney produced shorts, TV Shows, Direct to Video releases, and Direct to Streaming releases.  In some cases, the films considered were produced by the Walt Disney Company or its subsidiaries, in other cases, they were distributed by The Walt Disney Company or its subsidiaries.  We did not the limit the scope to a specific genre or type of film.  This project considered live-action, animation, and hybrid films.  We also considered musicals, dramas, comedies, documentaries and more so long as they were full-length feature film releases.


## Sources & Data Dictionary
---

With the expectation that this projects represents just the first phase, a wide net was originally cast for this project.  Ultimately this first phase used film lists from Disney.com, D23 (the official Disney fan club), and Wikipedia, as well as film data given to us by IMDB.com and additional film data scraped from IMDB.com. Additionally, 33 scripts from different Disney films were found, as well as lyrics to more than 790 Disney songs. Ultimately, the scripts and lyrics data will be used as part of future project phases. Data from 10 similar projects by other authors was also gathered and considered but not used in this phase.

#### Sources
This model relied on the following data sources:

| Source                                                | Data                                     | Reference                                                    | Description                               |
| ----------------------------------------------------- | ---------------------------------------- | ------------------------------------------------------------ | ----------------------------------------- |
| Disney.com                                            | Disney Films List | [Link](https://movies.disney.com/a-z) | List of 657 Disney Films |
| IMDB (datasets) | Ratings, Principals, Title Basic Infromation, Crew Members             | [Link](https://datasets.imdbws.com/)                      |                                         Film data made available from IMDB.com  |
|IMDB (web scrape) | MPAA Rating, Votes, runtime, release date, budget, and revenue.             | [Link](https://www.imdb.com/)                      |Film data scraped from various pages|

#### Data Dictionary

| Feature                                                      | Type                        | Description                                                  |
| --------------------------------------------------------- | --------- | ------------------------------------------------------ |
| Start Year            | Int        | Year of subject film's release |
| Run time (minutes)    | Int        | Length of subject film         |
| Director Count | Float          |Number of people credited by IMDB for having directed the film.        |
| Director Age   | Float     |Average age at the time of release for those people credited with having directed the subject film.       |
| Director Rating| Float         |Average IMDB Rating for each film previously directed by those credited with directing the subject film.        |
| Director Film Count| Float    |Average number of films previously directed by those credited with directing the subject film.        |
| Writer Count     | Float      |Number of people credited by IMDB for having written the film.        |
| Writer Age     | Float      |Average age at the time of release for those people credited with having written the subject film.        |
| Writer Film Count     | Float     |Average number of films previously directed by those credited with writing the subject film.        |
| Genre     | Object      |IMDB Film Genre(s) associated with the subject film.        |
| MPAA Rating   | Object     |MPAA Suitability Rating for each subject film.       |
| Release Date     | Datetime         |Data of release for each subject film.        |



### Files

This project and its accompanying data are stored in the following [git repository](https://git.generalassemb.ly/thisbenroberts/Disney_Capstone), and has the following structure:

- README file


- Bens_Code
  - 01_Curate_Disney_Films_List
  - 02_Combine_IMDB_Disney
  - 03_Gather_IMDB_Ratings_Votes
  - 04_Disney_IMDB_Scrape
  - 05_Get_Principals_Data
  - 06_Explore_Principals_Data
  - 07_EDA_Clean_Principal_Data
  - 08_Update_Directors_Writers_List
  - 09_Summarize_Track_Records
  - 10_EDA_Visualizations
  - 11_Modeling_for_IMDB_Rating
  - 12_Modeling_for_Worldwide_Rev
  - 13_Modeling_for_ROI
  - 14_Predictions



- Bens_Data
  - Disney_IMDB_Combined_483
  - imdb_ereors
  - Combined_IMDB_Disney_455
  - Updated_IMDB_Disney_444
  - imdb_errors_2
  - Combined_IMDB_Disney_453
  - Updated_IMDB_Disney_442
  - imdb_errors_1
  - imdb_errors_rnd2
  - Disney_imdb_scrape_final
  - imdb_scrape_director_writer_hist
  - directors_writers_combined_history_updated
  - principals_history_updated
  - directors_demo_history
  - writers_demo_history
  - directors_history
  - writers_history
  - directors_writers_combined_history
  - Disney_Films_For_Modeling
  - Disney_Films_For_EDA
  - Disney_Films_For_Visual
  - Upcoming_Releases
  - imdb_scrapefor_preds
  - imdb_scrapefor_preds - Copy


- Images
  - Film Ratings by Year
  - Films Released By Year
  - Rating by Dir Age
  - Rating by Dir Film Count_1
  - Rating by Dir Film Count_2
  - Rev By Season
  - RevByMpAA
  - ROI by Season


- Other Projects for Reference
  - DD_001
  - DD_002
  - DD_004
  - DD_005
  - DD_006
  - DD_007
  - DD_008
  - DD_009
  - DD_010
  - DD_011


- Other Source Data 
  - DD_Animated_List_WK
  - DD_Films_List_D23
  - DD_Films_List_Disney_Com
  - DD_Films_LIst_WK
  - IMDB (not included**) 
  - movie_meta_data
  - scripts
  - songs 

- Additional_data (not included***) 
  - imdb_scrape_complete
  - imdb_disney_soup
  - imdb_scrape_rnd2
  - imdb_scrape_director_writer_hist_SOUP
  - imdb_scrape
  - imdb_scrape_2
  - imdb_scrape_1 

** These files are too large to upload to git-hub but are available directly from [IMDB](https://datasets.imdbws.com/) 

*** These files are created by the code but too large to upload to git-hub

## Process Outline
---

After gathering a few different lists of Disney movies from different sources, there was a lot of variation discovered.  Ultimately the decision was made to work from the list of movies gathered from Disney.com.  Data provided by IMDB was then combined with the movie list. Working with more than 8 million titles, trying to narrow down the IMDB data involved comparing a lot of text and manually checking duplicate titles. 

Once the list back down to a reasonable number of suspected Disney films, a number of titles including TV Shows, similarly titled films, Disney Shorts and Compliations, and Direct to Video Releases among others were removed. Then a scrape of IMDB was performed to gathered more data that was not originally provided.

Next, a list of Directors and Writers was created and their performance histories were gathered, then combined with the films list. After some EDA and Visualizations, models were created and predictions generated.

## Analysis
---

After data cleaning and exploratory data analysis the following regression models were used to predict the IMDB User Rating for each title:

1. Linear Regression
2. Decision Tree Regressor
3. Bagged Tree Regressor
4. Random Forest Regressor
5. Adaboost regressor
6. KNN Regressor
7. Lasso
8. Ridge

The baseline model, the mean IMDB User Rating, produced a Root Mean Squared Error of 0.947%.  The root mean squared error indiactes that the errors are about 0.947% off from the actual IMDB Rating.  

Additionally, the same types of models were used to predict the Worldwide Revenue of each title. The baseline model for revenue produced an RMSE of 359,926,713%. The root mean squared error indiactes that the errors are about 359% off from the actual Revenue.  Given the vast difference between the min and max reveunes, this odd result isn't too surprising. 


## Conclusions
---
After comparing and tuning the models, Lasso was deemed the best fit as it produced the best Cross Val scores and a reasonably small Root Mean Squared error for the test data.

We were able to predict the IMDB User Rating and Worldwide Revenue for two upcoming releases, Doctor Strange in the Multiverse of Madness and The Bob's Burgers Movie, both due to be released in May of 2022. Doctor Strange is predicted to have an IMDB rating of 6.63 with Worldwide Revenue of \\$294 294,513,986. The Bob's Burgers Movie is predicated to have an IMDB rating of 6.37 with Worldwide Revenue of \\$45,963,783. It remains to be seen how accurate these predications will be. 


## Recommendations
---

Data availability was uneven amongst films and features of interest, forcing us to drop a few observations, consider different features, and different targets. With more time there are a number of things that could be done to improve the model and the results. 

- Budget and Revenue numbers were not readily available from IMDB for each Disney film. Nor were they available for each film in the Director's and Wirter's history, meaning our previous performance indicators may not be complete or 100% accurate.  With more time, the missing budget and revenue numbers may be sourced elsewhere.

- Additional features could be valuable in analyzing IMDB User Ratings as well as Revenue numbers. Currently, the model does not take in to account source material, or source authors.  It also does not account for Disney having produced versus distributed the film. 

- While there is some accounting for live-action vs animation, movie plot elements are not considered. With more time, I'd like to attempt to categorize leading characters/supporting roles (human vs animal vs other, male/female, young/old, etc), the presence of a villain or villains, continuous story line vs series of adventures, presence of absence of a love interest, main character family traits and how prominently family members are featured, atc.

- This model does account for the track record of the directors and writers of the film, it does not account for the track records of the principal actors. Also, there are some gaps in the data provided by IMDB. With more time, those gaps could be researched and filled in making the model more complete.

- For those films featuring songs, the writers and composers track records and demographics could be considered. 

- For those films featuring action sequences and/or special effects, the track records of those producing the effects could also be considered. As well as the amount of runtime dedicated to those sequences.

- Marketing and Promotional efforts are not accounted for in this analysis either. Marketing campaign, or marketing spend as percent of total budget. If toys or merchandise were produced, in what quantities, in which price ranges, how widely available, etc.  Additionally, partnerships and collaborations with companies such as McDonald's (i.e. Happy Meals) are not considered.

- Script elements such as the number of words or sentiment of the film is also not considered and may be interesting to look at as well.

- While the code currently exists to create predicitions for future releases, it's not very user friendly.  A tool should be created allowing the user to enter specific parameters (budget, writers, directors, estimated release date, and additional feature data), and receive an estimated IMDB User Rating, Revenue Numbers, and ROI predictions. 


 
