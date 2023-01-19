# Machine_Learning_Course 🌱
This repository contains the code for the project of Machine Learning D, course that I have done in AALTO University.


## Twitter US Airline Sentiment Analysis 

### Project Description
In this project, I developed a model that is able to classify the sentiments of Twitter’s tweet about US airlines. This task is
well known as **sentiment analysis**. It consists determining whether a given text contains _negative_, _positive_, or _neutral_ emotions.

### Data
The data set used in this **supervised** task was downloaded from Kaggle [1]. It contains tweets on six major United States
airlines, scraped from Twitter on February 2015.
The data set contains 14640 instances and every sample is characterized by 15 features. That are:
- **tweet id**: the unique identifier of the tweet. It is represented by a progressive integer number and it is ordinal.
- **airline sentiment**: the target variable of the classification. It is categorical and it assumes three possible string values:
positive, negative or neutral.
- **airline sentiment confidence**: a numerical continuous feature representing the confidence level of classifying the tweet
to one of the 3 classes.
- **negativereason**: a categorical feature which represent the reason behind considering this tweet as negative.
- **negativereason confidence**: a numerical continuous feature that represents the level of confidence in determining the
negative reason behind the negative tweet.
- **airline**: a categorical feature that represents the name of the airline company.
- **airline sentiment gold**: a feature that has the same meaning of ”airline sentiment” but only about Gold members1 of
the airline.
- **negativereason gold**: a feature that has the same meaning of ”negative reason” but only about Gold members1 of the
airline.
- **retweet count**: numerical discrete feature. It is number of retweets of a tweet.
- **text**: original tweet posted by the user.
- **tweet coord**: the coordinates of the tweet.
- **tweet created**: the date and the time of tweet.
- **tweet location**: location from where the tweet was posted. It is a categorical feature.
- **user timezone**: categorical string that indicates the timezone of the user.


<div align="center">  
<table class="tg">
<thead>
  <tr>
    <th class="tg-c3ow"><span style="font-weight:bold">**Features**</span></th>
    <th class="tg-c3ow"><span style="font-weight:bold">**Nr. missing values**</span></th>
  </tr>
</thead>
<tbody>
  <tr>
    <td class="tg-c3ow">tweet_id</td>
    <td class="tg-c3ow">0</td>
  </tr>
  <tr>
    <td class="tg-c3ow">airline_sentiment</td>
    <td class="tg-c3ow">0</td>
  </tr>
  <tr>
    <td class="tg-c3ow">airline_sentiment_confidence</td>
    <td class="tg-c3ow">0</td>
  </tr>
  <tr>
    <td class="tg-c3ow">negativereason</td>
    <td class="tg-c3ow">5462</td>
  </tr>
  <tr>
    <td class="tg-c3ow">negativereason_confidence</td>
    <td class="tg-c3ow">4118</td>
  </tr>
  <tr>
    <td class="tg-c3ow">airline</td>
    <td class="tg-c3ow">0</td>
  </tr>
  <tr>
    <td class="tg-c3ow">airline_sentiment_gold</td>
    <td class="tg-c3ow">14600</td>
  </tr>
  <tr>
    <td class="tg-c3ow">name</td>
    <td class="tg-c3ow">0</td>
  </tr>
  <tr>
    <td class="tg-c3ow">negativereason_gold</td>
    <td class="tg-c3ow">14608</td>
  </tr>
  <tr>
    <td class="tg-c3ow">retweet_count</td>
    <td class="tg-c3ow">0</td>
  </tr>
  <tr>
    <td class="tg-c3ow">text</td>
    <td class="tg-c3ow">0</td>
  </tr>
  <tr>
    <td class="tg-c3ow">tweet_coord</td>
    <td class="tg-c3ow">13621</td>
  </tr>
  <tr>
    <td class="tg-c3ow">tweet_created</td>
    <td class="tg-c3ow">0</td>
  </tr>
  <tr>
    <td class="tg-c3ow">tweet_location</td>
    <td class="tg-c3ow">4733</td>
  </tr>
  <tr>
    <td class="tg-c3ow">user_timezone</td>
    <td class="tg-c3ow">4820</td>
  </tr>
</tbody>
</table>
 </div>



### Methodology
The preprocessing step is the core phase of the entire analysis. We performed the selection, transformation and creation of
the features:

<div align="center">
   <img width="500px" height="auto" src="https://github.com/ChristianMontecchiani/Machine_Learning_Course/blob/main/img/schema.png"> 
 </div>

#### A. Feature Selection
I dropped some features that have a very low correlation with the label, so they are not useful for the analysis.
At the end of the feature selection process, the data set is composed by just 4 features, which are:
- **airline sentiment**: it represents the target and it is fundamental for the task.
- **airline**: it is correlated with the label.
- **text**: it is the main feature. In the next subsection will be described the way we extract information from it.
- **tweet created**: as it shown in article [2] there are temporal patterns of happiness in social network, so we decided to use
this feature.

#### B. Feature Transformation
In this subsection we will describe the ***feature transformation process***.
  1) Airline sentiment is converted in an *integer* value.
  2) The airline feature is a *categorical* so I used the one-hot-encoding technique.
  3) The date is encoded as a string with the format:
                                $$YYYY − MM − DD\ hour : min : sec$$
  4) Finally, text cleaning is performed:

<div align="center">
   <img width="500px" height="auto" src="https://github.com/ChristianMontecchiani/Machine_Learning_Course/blob/main/img/FinalPipeline%20(1).png"> 
 </div>
  
  
#### C. Feature Creation
So after giving homogeneity to each tweet we carry on the analysis of the text. We applied TF-IDF to extract the words
of main relevance. In the followinh Fig. are reported some of these words.
<div align="center">
   <img width="500px" height="auto" src="https://github.com/ChristianMontecchiani/Machine_Learning_Course/blob/main/img/word_cloud%20(1).png"> 
 </div>
Moreover, we also created three different features given by a pre-trained neural network and we used them to train the models.



#### D. Dataset Split
The training validation, and test set are split from the dataset with ratio training:validation:test = 3:1:1. I decide not to apply a K–fold cross validation since the creation of the features is time consuming and I was not able to repeat the process K times. Moreover, the size of the data set permits to obtain informative result with just a single split.


### Results
#### A. Comparison between FastText and BERT
We trained a Random Forest to compare the importance of the features created by the two Neural Networks. FastText’s
logits are the top three features used by the decision trees of the forest to classify the sentiment of the text. So, we decided
to use them.

### B. Training, Validation and Test Error
The test error chosen is F1-score and the results are shown in Table below.

<div align="center">
<table class="tg">
<thead>
  <tr>
    <th class="tg-7btt">Classifiers</th>
    <th class="tg-amwm">Test Error</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td class="tg-baqh">Decision Tree</td>
    <td class="tg-baqh">0.79</td>
  </tr>
  <tr>
    <td class="tg-c3ow">Random Forest</td>
    <td class="tg-baqh">0.82</td>
  </tr>
</tbody>
</table>
   </div>

### Future Work
One possible future work could be to use BertForSequenceClassification, which is an improved version of the
classic BERT and it is specialized in Sentiment Analysis. We did not use due to the limited computational resources of our
personal computers.

### References
[1] https://www.kaggle.com/datasets/crowdflower/twitter-airline-sentiment
