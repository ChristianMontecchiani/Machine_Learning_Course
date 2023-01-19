# Machine_Learning_Course
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

<center>
  
  
|         **Features**         | **Nr. missing values** |
|:----------------------------:|:----------------------:|
|           tweet_id           |            0           |
|       airline_sentiment      |            0           |
| airline_sentiment_confidence |            0           |
|        negativereason        |          5462          |
|   negativereason_confidence  |          4118          |
|            airline           |            0           |
|    airline_sentiment_gold    |          14600         |
|             name             |            0           |
|      negativereason_gold     |          14608         |
|         retweet_count        |            0           |
|             text             |            0           |
|          tweet_coord         |          13621         |
|         tweet_created        |            0           |
|        tweet_location        |          4733          |
|         user_timezone        |          4820          |   
  
  
</center>

### Methodology
The preprocessing step is the core phase of the entire analysis. We performed the selection, transformation and creation of
the features:
#### A. Feature Selection
As it is anticipated in the previous section in our data set there are columns with some missing value, but fortunately the
absence of these values is not critical in order to perform our task. We drop these features and we also drop some features
that have a very low correlation with the label, because they are not useful for the analysis.
At the end of the feature selection process, the data set is composed by just 4 features, which are:
- **airline sentiment**: it represents the target and it is fundamental for the task.
- **airline**: it is correlated with the label.
- **text**: it is the main feature. In the next subsection will be described the way we extract information from it.
- **tweet created**: as it shown in article [2] there are temporal patterns of happiness in social network, so we decided to use
this feature.

#### B. Feature Transformation
In this subsection we will describe the ***feature transformation process***.
  1) As described in section II the label, airline sentiment is represented by a *string*. It is converted in an integer value.
  2) The airline feature is a categorical value that assumes 6 values and we use the one-hot-encoding [3] technique to use it.
  3) The date is encoded as a string with the format:
                                $$YYYY − MM − DD\ hour : min : sec$$
  So we convert them in timestamp with the help of datetime library.
  4) Finally, text cleaning is performed. Different elements characterize a Twitter post and for a correct analysis we need
  to know all. The text is encoded in UTF-8, but some symbols are in HTML entities. We clean up HTML entities, we
  lowered the case of each tweet and transform emoticon and slang-terms into clear words; we remove numbers and replace
  repeated characters. Fig. 1 shows a summary of the text clean that we did.
  
  ![alt text](https://github.com/ChristianMontecchiani/Machine_Learning_Course/blob/main/img/schema.png "image title")

  Fig. 2: Overall schema of text cleaning.
  
#### C. Feature Creation
So after giving homogeneity to each tweet we carry on the analysis of the text. We applied TF-IDF [4] to extract the words
of main relevance. TF-IDF is a technique very useful in text mining when we want to evaluate how much impact have a
word in a particular context. We mainly focused on all the words that could have such an impact towards one class of each
sentiment, in Fig. 3 are reported some of these words.
Moreover, we also created three different features given by a pre-trained neural network and we used them to train the models.

3
These features represent the logarithm of the odds of a text to be classified with a positive, negative or neutral sentiment.
We use two different pre-trained neural networks (FastText AI by Meta’s [5] and BERT by Google [6]) which are well known
in the Natural Language Processing (NLP) field and then we compare the results obtained by using them. In Fig 4 shows a
summary of our approach.
Fig. 3: Word Cloud generated by the results of the TF-IDF.
Fig. 4: Overall schema of the pre-processing.

#### D. Dataset Split
The training validation, and test set are split from the dataset with ratio training:validation:test = 3:1:1. The reason behind
this choice is that we need a sufficiently large amount of data to train the model, while leaving a good amount of data for
validation and test purpose. The standard ratio is usually 3:1:1 which is widely used in the Machine Learning community. We
decide not to apply a K–fold cross validation since the creation of the features explained in III-C is time consuming and we
are not able to repeat the process K times. Moreover, the size of the data set permits to obtain informative result with just a
single split.

#### E. Model Selection
The majority of the ML methods presented during lectures do not perform well with high dimensional data. Random Forest
is great with them, since it works with subsets of data. The Random Forest uses bagging to learn an ensemble of decision
trees. So, the final hypothesis of it is obtained by taking the most predicted label by the Decision Trees. The hypothesis of
one of them is represented by a map: h : X → Y, which is constant over regions of the feature space X , as stated in [7].
These non-overlapping decision regions partition X into subsets of features that are all mapped to the same predicted label.
The second model used to compare the results collected with Random Forest is Multilayer Perceptron. A Multilayer
Perceptron is a feedforward artificial Neural Network and is the most basic Deep Neural Network that consists of a series
of fully connected layers. MLPs are useful in research for their ability to solve problems stochastically, which often allows
approximate solutions for extremely complex problems.


### Results
A. Comparison between FastText and BERT
We trained a Random Forest to compare the importance of the features created by the two Neural Networks. FastText’s
logits are the top three features used by the decision trees of the forest to classify the sentiment of the text. So, we decided
to use them.
B. Training, Validation and Test Error
Once the optimal combination of features was identified we went through two phases to show the results:
- In the first phase, we have performed a simple grid search considering different combinations of parameters, shown in
Table II. The best combination for each model is highlighted in the same Table. The models were trained with training
set (60%) and tested with the validation set (20%). The results are shown in Table III.
- In the second phase we trained the fine tuned models with a data set obtained by merging the training and validation sets.
Then the algorithms were tested with the remaining 20% of the initial data (test set). The test error chosen is always
F1-score for the same reasons specified above. The results are shown in Table IV.

### Future Work
One possible future work could be to use BertForSequenceClassification, which is an improved version of the
classic BERT and it is specialized in Sentiment Analysis. We did not use due to the limited computational resources of our
personal computers.

## References
A list of any sources that were referenced or used in the project.
