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
I printed out the accuracy, F1 score and confusion matrix for each model's prediction on the training data. You can see the results below:

offer_0 
 Logistic Regression 
  (0.6036602802402059, 0.72391505078485685) 
  Random Forest Classifier 
  (0.98198455819273667, 0.71753846153846157) 
  GridSearch Random Forest Classifier Best results 
  (0.75207320560480406, 0.78534290666006434,                
  importance
days_a_member    0.457730
income           0.323266
gender_M         0.084154
age              0.080143
gender_F         0.051251
gender_O         0.003455)

 offer_1 
 Logistic Regression 
  (0.57341907824222937, 0.70185449358059915) 
  Random Forest Classifier 
  (0.97775991425509112, 0.67600487210718641) 
  GridSearch Random Forest Classifier Best results 
  (0.74651661307609862, 0.75718685831622168,                
  importance
days_a_member    0.409733
income           0.329487
gender_F         0.112514
age              0.087740
gender_M         0.056794
gender_O         0.003732)

 offer_2 
 Logistic Regression 
  (0.62845109967243795, 0.69043151969981242) 
  Random Forest Classifier 
  (0.97941038839494621, 0.62650602409638556) 
  GridSearch Random Forest Classifier Best results 
  (0.66682264857276552, 0.73152337858220218,                
  importance
days_a_member    0.613325
age              0.168613
income           0.164632
gender_O         0.023249
gender_M         0.022625
gender_F         0.007555)

 offer_3 
 Logistic Regression 
  (0.78132223763291719, 0.86450030656039245) 
  Random Forest Classifier 
  (0.98520573277854828, 0.81824370319945539) 
  GridSearch Random Forest Classifier Best results 
  (0.78270920018492829, 0.87792207792207788,                
  importance
days_a_member    0.584607
income           0.192689
age              0.125787
gender_M         0.046598
gender_F         0.046337
gender_O         0.003982)

 offer_4 
 Logistic Regression 
  (0.7168330955777461, 0.85110470701248797) 
  Random Forest Classifier 
  (0.98858773181169757, 0.81298992161254202) 
  GridSearch Random Forest Classifier Best results 
  (0.74679029957203991, 0.84298982750995133,                
  importance
days_a_member    0.663540
income           0.177070
age              0.145867
gender_O         0.005489
gender_F         0.004314
gender_M         0.003720)

 offer_5 
 Logistic Regression 
  (0.76522672390662727, 0.86182336182336172) 
  Random Forest Classifier 
  (0.98604775959216528, 0.8352799033427305) 
  GridSearch Random Forest Classifier Best results 
  (0.78374027367856181, 0.87279040404040409,                
  importance
days_a_member    0.747206
age              0.076324
income           0.065983
gender_M         0.059577
gender_F         0.050599
gender_O         0.000312)

 offer_6 
 Logistic Regression 
  (0.76587828859952167, 0.88218988218988226) 
  Random Forest Classifier 
  (0.99229338293914426, 0.86179507545671175) 
  GridSearch Random Forest Classifier Best results 
  (0.79697050225883603, 0.8787686448746429,                
  importance
days_a_member    0.769514
income           0.114780
age              0.077306
gender_F         0.019447
gender_M         0.018133
gender_O         0.000821)

 offer_7 
 Logistic Regression 
  (0.61798396334478811, 0.68197088465845457) 
  Random Forest Classifier 
  (0.97852233676975942, 0.62102689486552565) 
  GridSearch Random Forest Classifier Best results 
  (0.66924398625429549, 0.73839184597961516,                
  importance
days_a_member    0.465403
income           0.350802
age              0.159496
gender_M         0.011716
gender_F         0.008277
gender_O         0.004306)

 offer_8 
 Logistic Regression 
  (0.66422764227642273, 0.79953739398612178) 
  Random Forest Classifier 
  (0.98346883468834689, 0.7506029908345393) 
  GridSearch Random Forest Classifier Best results 
  (0.75745257452574521, 0.82294757665677543,                
  importance
days_a_member    0.615998
income           0.187246
age              0.153678
gender_M         0.027444
gender_F         0.009739
gender_O         0.005894)

 offer_9 
 Logistic Regression 
  (0.76473339569691301, 0.8658008658008659) 
  Random Forest Classifier 
  (0.98690364826941068, 0.81926029309141657) 
  GridSearch Random Forest Classifier Best results 
  (0.77128157156220767, 0.86935613144536472,                
  importance
days_a_member    0.679530
income           0.185681
age              0.102530
gender_F         0.018273
gender_M         0.009938
gender_O         0.004049)

## Conclusion
The problem I was tyring to understand was what users would complete an offer after viewing it. My first approach was to try to build a set of heuristics about who completes which offers. I then decided I would try to build a set of models to try to predict which users would or would not complete an offer after viewing it. I created a model for each offer to retain the unique parameters for the offers. I started off with a simple logistic regression model and tried to improve upon those results using a random forest classifier using GridSearchCV. The feature_importances_ parameter made it quite clear and confirmed the importance of days a member of the starbucks rewards program that I saw when analyzing how the various demographhics affected the offer completion rates.

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
