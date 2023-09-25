# ![](https://ga-dash.s3.amazonaws.com/production/assets/logo-9f88ae6c9c3871690e33280fcf557f33.png) Project 3: Web APIs & NLP

## Problem Statement

Chat GPT (Chat Generative Pre-trained Transformer) was released in November 2023. Chat GPT is being used for translation, conversational AI,  coding, and education ([source](https://research.aimultiple.com/chatgpt-use-cases/#textual-applications)). Chat GPT seems to be useful. As a data scientist, we wish to explore the difference between ChatGPT’s response and humans' response. To be able to do that we need a model that can recognize whether the text is AI response or human response. The purpose of this project is to build a classification model by collecting all of the text written by both human and AI on the responses to the same question using Logistic Regression, Naive Bayes, and KNeighborsClassifier model, so that we can train a model to learn how to figure out whether text is human written or ai written.

---
## Data Collection

Human answers and questions were collected from Reddit by using PRAW (The Python Reddit API Wrapper) ([read more about PRAW](https://praw.readthedocs.io/en/stable/)). List of six subreddit topics chosen were "NoStupidQuestions", "Questions", "Askreddit", "MorbidQuestions", "TooAfraidToAsk”, and "AskScienceFiction". Collected around 900 questions and top comments in each subreddit topic. The AI answers were collected from Openai API ([read more about OpenAI](https://openai.com/blog/openai-api)) by asking the same questions as were collected from Reddit to ChatGPT. Saved the data collected from each topic as a csv file. Combine those csv files together for a full dataset with questions, human response and AI response. 


### Dataset

* [`project3_answer.csv`]('../data/project3_answer.csv'): Human answer and AI answer

**Brief description of the contents for each dataset.**

There are two columns in the dataset:

* First column: List of human answer and AI answer

* Second column: List of 1 and 0, 1 stand for human answer and 0 stand for AI answer

### Data Dictionary

|Feature|Type|Dataset|Description|
|---|---|---|---|
|answer|object|project3_answer|List of human answer and AI answer| 
|result|int64|project3_answer|List of 1 and 0, 1 stand for human answer and 0 stand for AI answer| 

---

## Table of Result

|Type of Model|Accuracy score|Recall score|Precision score|F1 score|
|---|---|---|---|---|
|Model 1 (CountVectorizer & BernoulliNB)|0.888151|0.957903|0.840570|0.895409|
|Model 2 (CountVectorizer & LogisticRegression)|0.912145|0.928360|0.899142|0.913517|
|Model 3 (CountVectorizer & KNeighborsClassifier)|0.549649|0.919498|0.528438|0.671159|
|Model 4 (CountVectorizer & MultinomialNB)|0.886305|0.912851|0.866760|0.889209|
|Model 5: TfidfVectorizer & LogisticRegression|0.902547|0.916544|0.891523|0.903860|
|Model 6: CountVectorizer and LogisticRegression with Lasso|0.910299|0.926883|0.897069|0.911733|
|Model 7: AdaBoostClassifier and LogisticRegression|0.910299|0.932792|0.892580|0.912243|

## Conclusions and Recommendations

* LogisticRegression gave a higher accuracy score than KNeighborsClassifier, BernoulliNB and MultinomialNB. 
* KNeighborsClassifier has the lowest accuracy score. Model 3 cannot be used to identify whether the text is human written or ai written.
* Model 2 has the highest accuracy score and F1 score but model 2 has the difference between test score and train score highest. Model 2 is overfit. 
* Model 5, model 6 and model 7 were built to improve the overfit and accuracy score of model 2. The accuracy score of those models are lower than model 2 but the difference between train score and test score did improve.
* Model 1 and 4 also have a good accuracy score. The difference between train score and test score of model 1 and 4 are lower than the difference between train score and test score of model 2. 
* Model 2, model 6 and model 7 can be used to identify whether the text is human written or ai written.
* In the future, apply different classification and different params to find a higher accuracy score.  

