# Useing survival analysis to predict primary election results 
---
Author
- Nick Read 

### Table of Contents 

* [Problem Statement](#Problem-Statement)
* [Executive Summary](#Executive-Summary)
* [Datasets](#Datasets)
* [Data Dictionary](#Data-Dictionary) 
* [Conclusion](#Conclusion)
* [Next Steps](#Next-Steps)

## Problem Statement
When predicting outcomes of elections there are many factors that go into the success of an individual candidates campaign. Having cash on hand for expenses is vital for a campaign to survive and we believe that it can be an important factor in predicting wether the campaign will be successful or unsuccessful however it is not the only factor. In this project we believe that we can predict the outcomes of elections based on the financial contribution rates and the expenditures of primary campaigns. We seek to find if there is a "critical mass" of money spent on a variety of factors including paid media, staffing and transportation etc. that a candidate must spend or take in to survive the primaries.

Using Survival Analysis we believe that we can create a model to predict if a candidates campaign will be successful or if their campaign will fall short before the primary winners are announced.I believe that this will be a useful tool for presidential candidates looking to improve their odds of success in the primary stages of the election.    

## Executive Summary 

In [Data Collection](./code/data_cleaning.ipynb) we were tasked with dealing with a large amount of data gathered from the Federal Election Committee (FEC) website: fec.gov. This website has a vast quantity of data but the data can be messy and has to be cleaned. The original data set is 27.8 GB and needed to be withheld down quit a bit to be handled by the machine available to me. The necessary files we collected were Individual Donations to Campaigns, Campaigns Expenditures, and Political Action Committees (pac's) allowing us too create a necessary frame work for the Primary campaigns intake and disbursements. 

The next step was [Data Cleaning](./code/data_cleaning.ipynb).The first step is too bulk download the data needed form the FEC website. We pulled in the necessary data for the 2008 up to the current date for the 2020 primaries. After reading in the data in chunks form an external hard drive I was able to drop un-needed columns like "Name of individual", "alternate id", "Recipe type" and other columns of this nature. After this process we achieved a workable size of 10.4 GB. We further condensed our data to be within the appropriate time frames for the campaigns as some data was recorded incorrectly by the FEC. After this step we Created data frames of each candidate by their unique ID issued by the FEC to gather just the candidates that met the threshold of being relevant in the process. After this process we checked our data for common errors like missing values changing nans to 0 where appropriate and changing the types of our data from strings to integers and date time objects where appropriate. After this process we were able to aggregate all of the candidates donations, expenditures and contributions form PACs into CSV files and neatly store them for use later in the project. 

The final step was [Modeling](./code/modeling.ipynb), I used the Lifelines package to predict the probability of candidates dropping out of the race. For this we took the quarter by quarter donations as well as the quarter by quarter expenditures of the campaigns as well as a dummied columns for what the expenditures were for. Our model was then trained on the data and created a prediction curve based on the amount of days left in the race to likely hood of a candidate dropping out.

## Datasets

The data sets used for this project were sourced from the fec.gov website. This data set was roughly 27.8GB uncompressed, so it was not included in this repo. The data set consisted of Campaign donations and Campaign expenditures.  

## Data Dictionary 

|File name| Description|
|---|---|
|Don| This folder contains CSV file includes all data obtained dealing with donations|
|Exp| This folder contains CSV file includes all data obtained dealing with Expenditures|
Modeling| This folder contains CSV file includes all cleaned data organized by row |


## Conclusion

Our model meets our goals however could still use more features to improve its predictive capabilities. I am able to create accurate predictions of when candidates will drop out as the presidential primaries continue. From the Life lines package I am also able to predict the number of days a candidate is likely to survive until they reach their half life (%50 chance of drop out) The model beats our base line accuracy score for the elections tested. With our baseline accuracy being 1/n  where n is the number of candidates in the election cycle we see the model accurately predicting the candidates who will make it through the primaries for each election cycle. This model takes the features of Quarter by Quarter total donations up to the 3rd quarter of the year, the observed "death" of a candidate if ti is available and the number of days survived from announcement to drop out or form announcement to loss of election. 


## Next Steps

For this project we would like to further refine the model to be more useful as the election moves froward. We realize that the electoral land scape is ever changing and this means constant tweaking of features and parameters to account for a wide range of changing factors.

In further iterations of this project we would like to add more features including expenditures as well as a page rank for each candidate. There is also room for a  net work analysis of when one candidate drops out and then throws their support behind another. We saw this affect our models predictive abilities and believe it could be a strong feature for our model.