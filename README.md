# Machine_Learning_Course
This repository contains the code for the project of Machine Learning D, course that I have done in AALTO University.


## Project Title

### Project Description
In this project, I developed a model that is able to classify the sentiments of Twitter’s tweet about US airlines. This task is
well known as **sentiment analysis**. It consists determining whether a given text contains _negative_, _positive_, or _neutral_ emotions.
It is widespread that customers tweet about their satisfaction or disappointment after a flight. There can be multiple reasons
behind the emotion such as bad flight, booking problems or customer service issues.

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
|**Feature**| **Numb. missing values** |
|:--------:|---------:|
| tweet_id                      | 0 |
| airline_sentiment             | 0 |
| airline_sentiment_confidence  | 0  |                          
| negativereason                | 5462 |                        
| negativereason_confidence     | 4118 |                        
| airline                       | 0 |                           
| airline_sentiment_gold       | 14600 |                        
| name                           | 0 |                           
| negativereason_gold           | 14608 |                        
| retweet_count                 | 0 |                            
| text                           | 0 |                           
| tweet_coord                   | 13621 |                        
| tweet_created                 | 0 |                            
| tweet_location                | 4733 |                         
| user_timezone                 | 4820 |                         

  </center>

## Methodology
A description of the machine learning techniques used in the project, including any libraries or frameworks that were utilized.

## Results
A summary of the project's main findings, including any relevant visualizations or statistical analyses.

## Future Work
A discussion of potential future directions for the project, including any planned improvements or additional features.

## References
A list of any sources that were referenced or used in the project.
