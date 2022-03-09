
<img src="../images/download.png" style="float: center; margin: 0px; height: 150px; width: 100px">  

# Subreddit Classifier
#### By Afolabi Cardoso

---
## Problem Statement
There has been talk on the similarities between starwars and startrek universe. Some people say that writers use the same kind of keywords in both films. By using Natural Language Processing, this project seeks to clarify the conversation.

---
## DATA
---
#### **Data Library**

|Feature|Type|Dataset|Description|
|---|---|---|---|
|**title**|object|Reddit|String containing the title of the subreddit post|
|**selftext**|object|Reddit|String containing selftext of the subreddit|
|**created_utc**|int64|Reddit|The time the subreddit post was pulled|
|**subreddit**|object|Reddit|Name ot the subreddit i.e starwars or startrek|

#### **Data Gathering**

By using the [Pushshift's](https://github.com/pushshift/api) API, I was able to get 2000 posts from [Reddit](https://www.reddit.com/). 1000 posts from [starwars](https://www.reddit.com/r/StarWars/) and [startrek](https://www.reddit.com/r/startrek/) subreddit each. I used the json() method to convert the data to json format. Once in json format it was easy to extract the subreddit information into a dataframe.

---
## Methodology
---
#### **Data Cleaning**
- Checked for null values and replaced them with an empty string
- The string [removed] appeared a lot in the selftext, this was used to replace an empty post. I replaced [removed] with an empty string
- I set all the string column to lowercase


#### **EDA**
- I started exploring the dataset by looking at the top occuring words. I wasn't surprised that trek, star and wars were at the top of the list.
- I got curious and wanted to know the top characters poeple mention most. Obi-Wan and Picard had the most mentions. They both have new shows coming out, hence thier popularity.
- I continued the EDA by performing sentiment analysis on the data. Sentiment analysis is a method by which we try to determine the polarity of a statment. In this case, I used sentiment analysis to compare the two subreddits. I am curious to see which group of fans have more positive sentiments.
From the VADAR NLTK library, I used the SentimentIntensityAnalyzer() method. This method takes in a string and returns a dictionary containing, a positive, neutral, negative and compound value. I will be using the compound score to perform our analysis.
- The result of the sentiment analysis showed that they both have sentiments close to neutral. However, starwars has a slightly more negative sentiment score overall as compared to startrek. I believe this negative sentiment score can be attributed to certain negative words or phrases i.e wars and battle.



#### **Logistic Regression Model**
- Before starting the modeling process, I calculated the baseline accuracy to be 50.5%
- By using sklearn train_test_split method, I divided the dataset into the training and testing data.  
- I created a pipeline of CountVectorizer and LogisticRegression so I can pass them into a grid search
- I passed english as a stop_word into the CountVectorizer. This helps remove common english words that don't help the model
- I used a grid search to iterate through multiple hyper parameters.
- I got an accuracy score of 86.5%


#### **Random Forest Classifier**
- The accuracy for the random forest was 84%  

---
## Conclusion

The logistic regression had a slightly better accuracy score 87% than the random forest model 84%. It was able to correctly classify 239 posts from starwars and 191 posts from startrek. Total missclassified was 70. This in my opinion isn't a bad result.

I analysed the missclassified posts, most of the words from the misclassified post are words like series, episodes, seasons etc. These can easily be attributed to either subreddits

The results shows that both starwars and startrek have very distinct keywords.

---
## Reccomodations

For this experiment, I used only the subreddit titles, for my next experiment, I will be using both the titles and the subtext. I believe this will help increase the accuracy of the classifier.

