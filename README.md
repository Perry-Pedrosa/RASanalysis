# Does The RAS Metric System Predict Success In The NFL?
In 2013, Kent Lee Platte, a self proclaimed Maths junkie created a model to convert a group of metrics into a scoring system for prospective NFL players. This would come to be known as [RAS](https://ras.football/) or Relative Athetic Score.
Kent tells the story of how he came up with the system which provides a lot of context [here](https://www.prideofdetroit.com/2016/5/16/11678686/relative-athletic-scores-what-they-are-and-why-they-work).

If nothing else, I hope that you can at least take away from this how a non NFL affiliated individual, driven by his passion for data and football created a model that made NFL scouting a lot easier and whether he knows it or not, changed the landscape for "pre draft" analysts for years to come.

## Executive Summary
This project objective is not to challenge the RAS model, it is to use the score as a coefficiant to both understand the correlation between a score and success. Additionally we will use that to calculate the probability that a high score will lead to a successful career using the basis of this hypothesis:

*H0* - **A RAS of *x* will lead to a successful NFL career**

*H1* - **RAS doesnt not affect the career success of an NFL Player**

It is to be noted Kent has never stipulated a high score will lead to a successful career. American Football has a lot of variables so isolating them to minimise the impact on the model(s) will be paramount. However, no one has ever asked that question either and furthermore, if there is a way to detect success based on a pre draft process.

## Scope

- We will be using data from 2009-2022 to ensure variety from multiple sources and joining them together. We are excluding 2023 due to this data being rookies and contextually tthey are at a disadvantage being in their first year in the league due to lack of playing time or "growing pains" adapting to a professional league.
- We will be only looking at the **Cornerback** position, the reason for this is that it is the most independent position in football, a Cornerbacks reliance on other team members to do their job is minimal and is the reason why the position is nicknamed *The Island*, they are alone, detached from all other players on the field.
- An average score will be attained when preparing the data, outliers calculated by IQR and nulls will be removed. We will then use a score > than the average for our test/train data.
- Metrics for success will be based around accolades; *all-pro selections* *, *drafted*, *1st round draft pick*, *PFF coverage grade*. * *All recognised all-pro voting [entities](https://en.wikipedia.org/wiki/All-Pro) will count, however even if all 3 entities vote that player for the year the count will be 1, not 3* as well as height, weight, speed, explosivness metrics that are all captured as part of Combine data.
- The data will be prepared in Excel Power Query and modelled in R, this ensures a clean familiar way to get the data ready and a platform to evidence statistical modelling, testing and visualisations.

## The Data

The data has been sourced from various host sites:

[RAS](https://ras.football/) - Provided the RAS score for all data points

![RAS](assets/RAS.PNG)

[PFR](https://www.pro-football-reference.com/) - Provided data for all pro selections, draft selection indicator & position & combine results from [Kaggle](https://www.kaggle.com/search?q=nfl+combine+data+in%3Adatasets) (note: although combine results wont be used in the model, they are to reference metrics that could potentially detect successful traits in athletes.)

![All Pro](assets/All-Pro.PNG)

![Combine](assets/Combine.PNG)

[PFF](https://www.pff.com/nfl/grades/position/cb) - Provided data through its paid service (PFF+) on player grading. This is from a premium service and will adhere with the [licensing agreement](https://www.pff.com/premiumstats#:~:text=All%20subscriptions%20will%20be%20subject%20to%20the%20terms,points%20from%20the%20Licensor%E2%80%99s%20website%20for%20publication%20elsewhere)

![Grading](assets/Grades.PNG)

### Preparation

Beow is a visualisation of the data 'cleaning' process. Some data needs to be appended as it is stored by year so need to be combined. Data will then be merged in Power Query using the player name after some validation takes place to identify potential duplicates:

![Data Preparation Steps](assets/Cleaning2.PNG)

1. As per the process analysis pipeline, the first stage is to complete all appending activities:

![Data Append](assets/Append-1.png)

2. Once appended, I had multiple entries for all players. This meant further cleansing however it did let me take my target variables and average or sum them over the whole post-appended dataset.. which is something I was going to have to perform at somepoint!

![grouping](assets/group_and_agg.png)

3. Converted all-pro text data to numerical so that it can be quantifiably used in the model.

![Convert](assets/allpro.png)

4. At this stage we are going to merge all of the data in Power query together using the name of the player, duplicates have already been addressed where needed. However, some names do not fully match across different datasets due to a number of reasons (initials i.e. AJ/A.J, affixes such as jr, sr, III or players that are referenced by nickname rather than forename) to combat this fuzzy matching is performed at a threshold of .75 (after some tinkering) to create the dataset for modelling.

Once the merge is completed, decisions around exclusions will be made to ensure the dataset has variety, validity and meets general data ethics standards.
After excluding data that was not relevent to the model the dataset was reduced from 421 to 279 rows. However, additional datapoints from 2023 and 2024 will be used as a true predictive model which will be revisited on the conclusion of the 2024 season.

5. Clean up data types to ensure compatability with R reader when loading the data in:

![Data Type](assets/type1.png)

6. Finally change the header format to ensure compatability with the modelling software and we are ready to load the data.

![model_data](assets/final.png)
