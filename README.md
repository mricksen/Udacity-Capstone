# Udacity Data Science Capstone

## Starbucks Promotional Offers Demographic Analysis
The Starbucks promotional offers capstone project provides a dataset that allows us to track member behavior and interactions with offers. 

There are three types of offers: buy-one-get-one (BOGO), discount, and informational. In a BOGO offer, a user needs to spend a certain amount to get a reward equal to that threshold amount. In a discount, a user gains a reward equal to a fraction of the amount spent. In an informational offer, there is no reward, but neither is there a requisite amount that the user is expected to spend. Offers can be delivered via multiple channels.

## Problem Statement
The basic task is to use the data to identify which groups of people are most responsive to each type of offer, and how best to present each type of offer.

In the notebook, I first looked at the data I was working with and determined that I would need to create a dataframe to track for each user which offers did they complete and figure out a way to track completions for the information offers that didn't provide the offer completion event. Once created I can look at different facets of the demographic data to understand which offers are successes and which ones are failures with an understanding as to the effect that channel plays in offer completion rates. 

## Results
My results are written up in this blog post: 

## Data Munging
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
