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

- We will be using data from 2009-2024 to ensure variety from multiple sources and joining them together
- We will be only looking at the **Cornerback** position, the reason for this is that it is the most independent position in football, a Cornerbacks reliance on other team members to do their job is minimal and is the reason why the position is nicknamed *The Island*, they are alone, detached from all other players on the field.
- An average score will be attained when preparing the data, outliers calculated by IQR and nulls will be removed. We will then use a score > than the average for our test/train data.
- Metrics for success will be based around accolades; *all-pro selections*, *drafted*, *1st round draft pick*, *PFF coverage grade*
- The data will be prepared in Excel Power Query and modelled in Python 3, this ensures a clean familiar way to get the data ready and a platform to evidence statistical modelling, testing and visualisations.

## The Data

The data has been sourced from various host sites:

[RAS](https://ras.football/) - Provided the RAS score for all data points

![RAS](assets/RAS.PNG)

[PFR](https://www.pro-football-reference.com/) - Provided data for all pro selections, draft selection indicator & position & combine results (note: although combine results wont be used in the model, they are to reference metrics that could potentially detect successful traits in athletes.)

![All Pro](assets/All-Pro.PNG)

![Combine](assets/Combine.PNG)

[PFF](https://www.pff.com/nfl/grades/position/cb) - Provided data through its paid service (PFF+) on player grading 

![Grading](assets/Grades.PNG)
