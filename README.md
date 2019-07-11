# Udacity Data Science Capstone

## Starbucks Promotional Offers Demographic Analysis
The Starbucks promotional offers capstone project provides a dataset that allows us to track member behavior and interactions with offers. 

There are three types of offers: buy-one-get-one (BOGO), discount, and informational. In a BOGO offer, a user needs to spend a certain amount to get a reward equal to that threshold amount. In a discount, a user gains a reward equal to a fraction of the amount spent. In an informational offer, there is no reward, but neither is there a requisite amount that the user is expected to spend. Offers can be delivered via multiple channels.

## Problem Statement
The basic task is to use the data to identify which groups of people are most responsive to each type of offer, and how best to present each type of offer.

How I plan to solve this task is to create a labeled data set of users who have viewed an offer and did or did not complete it. I could have looked at other data sets of users like those that receive an offer, don't view it and complete it; as well as, users who receive an offer don't view it and don't complete it. 

I created a model per offer as there was variations amongst the offers I didn't want to lose by aggregating them together in offer groups (BOGO, discount, informational) such as the channels in which the offers were sent. 

The solution I was pursuing was creating a model that would predict what type of user would or would not complete the offer based on the demographic information available. The goal would be to send the offer to those likely to complete it and don't send the offer to those not likely to complete it. 

## Metrics
At first I was going to measure model performance using accuracy but I decided that F1 was a better measure to account for precision and recall. 

Accuracy measures the number of correct labels (True Positive and True Negatives) divided by the total number of predicted values (True Positives, False Positives, True Negatives, False Negatives). This can give you a sense for how well your model correctly labeled the data but it does not provide you with any information about the incorrect labels. 
In some instances, the incorrect labels are much more relevant than the correct labels. One example would be a rare disease that inflicts less than .001% of the population. Accuracy in this case is meaningless because we would have high accuracy by default since the disease is not well represented in the population. 

F1 score on the other hand does reflect incorrect labels as it utilizes both precision and recall in its calculation: 
F1 = 2 * (precision * recall / precision + recall)

As a quick reminder… precision is the correct number of True Positive labels divided by the total number of positive labels (True and False Positives). While recall is the correct number of True Positive labels divided by the total number of relevant elements (True Positive and False Negative). In other words, recall calculates how well we correctly identify the Positive labels as True. 

For my dataset there is a discrepancy in the number of viewed offers completed by users so I believe F1 is the better metric in this case.



## Data Cleaning
The greatest difficulty I encounted when manipulating the data was to figure out how to track a truly completed offer, offers that were viewed prior to completion. The most challenging aspect of this was how to track offer completions for informational offers, when transactions had occurred after informational offers were viewed but prior to the end of the offer availability. 

## Building a Prediction Model
I created a unique model per offer to make sure I accounted for the uniqueness of each model. I created three models a logistic regression, random forest classifier and an improved random forest classifier using GridSearchCV. I chose logistic regression as the first model as I create a binary classification dataset either a users completed an offer after viewing it or they did not. I then chose to use a random forest classifier as it would provide me with a clearer sense for which features were most relevant through the feature_importances_ attribute. GridSearchCV helped me find the best parameters to use for each offer model. 

While I did not reach my goal of an F1 score of .75 for each model I got fairly close to it. The only two offer models where I didn't succeed were the two informational offers. I would suggest to Starbucks that they figure out how to track offer completions than just transactions influenced by offers by tracking if the informational offer such as a pumpkin spiced latte was actually purchased by the use after viewing the offer. 

## Model Results
I printed out the accuracy, F1 score and feature importance for each model's prediction on the training data. Every model had days a member as the most important feature to predict offer completion. There were three offer models (0,1 and 7) where income was also a very important feature. Below you can see examples from the model results for offers 0 and 1.

![](Images/Image%202019-07-10%20at%206.57.30%20PM.png)

## Conclusion
The problem I was tyring to understand was what users would complete an offer after viewing it. 

My first approach was to try to build a set of heuristics about who completes which offers. 

I then decided I would try to build a set of models to try to predict which users would or would not complete an offer after viewing it. I created a model for each offer to retain the unique parameters for the offers. I started off with a simple logistic regression model and tried to improve upon those results using a random forest classifier using GridSearchCV. The feature_importances_ parameter made it quite clear and confirmed the importance of days a member of the starbucks rewards program that I saw when analyzing how the various demographics affected the offer completion rates.

My results are written up in this blog post: https://medium.com/@mricksen/starbucks-promotional-offers-demographic-analysis-7ff5d1839391

## Improvements
If I had more time I would explore how to build a recommendation engine that recommends an initial offer when a user first becomes a member based on demographic data, determine which offer to recommend when a user either does or does not complete an offer, as well as determines the best channel to send an offer for each demographic.

This was simulated data from starbucks but I hope that they include through which channel the offer was viewed as that information would be valuable to understanding how users interact with offers and how it may influence completion rates.

## Data Dictionary
### profile.json
Rewards program users (17000 users x 5 fields)
- gender: (categorical) M, F, O, or null
- age: (numeric) missing value encoded as 118
- id: (string/hash)
- became_member_on: (date) format YYYYMMDD
- income: (numeric)

### portfolio.json
Offers sent during 30-day test period (10 offers x 6 fields)
- reward: (numeric) money awarded for the amount spent
- channels: (list) web, email, mobile, social
- difficulty: (numeric) money required to be spent to receive reward
- duration: (numeric) time for offer to be open, in days
- offer_type: (string) bogo, discount, informational
- id: (string/hash)

### transcript.json
Event log (306648 events x 4 fields)
- person: (string/hash)
- event: (string) offer received, offer viewed, transaction, offer completed
- value: (dictionary) different values depending on event type
- offer id: (string/hash) not associated with any "transaction"
- amount: (numeric) money spent in "transaction"
- reward: (numeric) money gained from "offer completed"
- time: (numeric) hours after start of test


## Acknowledgements
I want to thank Starbucks for providing the simulated experiemental data for the capstone project.
