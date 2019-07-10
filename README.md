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
I plan to use F1 score as my main measure after initially using accuracy. The reason why I think F1 is a better measure is that it accounts for precision and recall. This is relevant as we want to account for the prediction mistakes which accuracy does not provide as the model is doing a binary classification: "will the user completed the order or not after viewing it?"

## Results
My results are written up in this blog post: https://medium.com/@mricksen/starbucks-promotional-offers-demographic-analysis-7ff5d1839391

## Data Cleaning
The greatest difficulty I encounted when manipulating the data was to figure out how to track a truly completed offer, offers that were viewed prior to completion. The most challenging aspect of this was how to track offer completions for informational offers, when transactions had occurred after informational offers were viewed but prior to the end of the offer availability. 

## Follow Up Questions
If I had more time I would explore how to build a recommendation engine that recommends an initial offer when a user first becomes a member based on demographic data, determines which offer to recommend when a user either does or does not complete an offer, as well as determines the best channel to send an offer for each demographic.

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
