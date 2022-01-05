# NLP & Classification Project on Reddit posts

This project leverages on natural language processing to classify text, specifically, developing an algorithm to classify reddit posts into the rightful subject matter.

## Problem Statement

As a new investment firm with 2 main trading desks (one for traditional securities and one for crytocurrency), we aim to develop a tool to analyze the top trending topics in equities and crytocurrencies. In doing so, we could explore if there may be any correlation between any specific trending topics and a stock ticker or cryptocurrency, to support the firm in taking up data-informed trading positions.

The idea is to develop a classification model that leverages on natural language programming (NLP) to identify and classify content into the categories of 'investing' vs. 'crytocurrency'.\
This is no mean feat, as it is expected that there are likely parallels between r/investing and r/cryptocurrency since they revolves around trading. Their uniqueness is exactly what we are keen to find out, and part of the deliverables of this undertaking.

Performance metrics that will be part of the success criteria are:\
(We have specified in the binary classification, 1 or positive refers to r/investing category while 0 or negative refers to r/cryptocurrency category)
- accuracy or how well the model is able to make correct classification
- sensitivity (true positive rate) or how well the model is able to make correct classification as an r/investing topic
- specificity (true negative rate) or how well the model is able to make correct classification as a r/cryptocurrency topic

## Data Sources

Web scraping (5000 posts for each category) is carried out to gather the data, namely from the following sources:
* [r/investing posts](https://www.reddit.com/r/investing/)
* [r/CryptoCurrency posts](https://www.reddit.com/r/CryptoCurrency/)

## Data dictionary

|  Feature  |  Type  |  Dataset  |  Description  |
|:----------|:------:|:---------:|:--------------|
| title     | object | invest    | The title of the subreddit post|
| create    | int    | invest    | The time that the reddit post was created in epoch unix units|
| subreddit | object | invest    | The subreddit that the post belongs to |
| body      | object | invest    | The body contents of the reddit post |
| author    | object | invest    | The author of the reddit post |
| permalink | object | invest    | The url link of the reddit post |
| num_comments | object | invest | The number of comments for the reddit post |
| title     | object | crypto    | The title of the subreddit post|
| create    | int    | crypto    | The time that the reddit post was created in epoch unix units|
| subreddit | object | crypto    | The subreddit that the post belongs to |
| body      | object | crypto    | The body contents of the reddit post |
| author    | object | crypto    | The author of the reddit post |
| permalink | object | crypto    | The url link of the reddit post |
| num_comments | object | crypto | The number of comments for the reddit post |

## Executive Summary

In this day and age, the ease of setting up trading accounts with the many platforms available has resulted in high accessibility in stocks and crytocurrencies trading by the average retail investor.

As a trading firm, we need to keep abreast of developments and discussions in platforms like Reddit to understand the prevailing trading sentiments in the current volatile environment. We aim to sieve out trading trends, sentiments through analyzing Reddit posts to support two of our most important trading desks - equities and crytocurrencies.

By leveraging on techniques such as web API scraping, natural language processing, classification modelling and evaluation, we were able to develop a respectable model that provides an accuracy rate of 95%. In other words, only 5 out of 100 posts were misclassified.

Having said that, the misclassification may be a misnomer as we have also found out that the model had actually 'correctly' classified some of the 'misclassified posts'.
What we mean by this is that, the model was able to pick up post contents on cryptocurrency that were posted in the r/investing subreddit instead of the r/cryptocurrency subreddit.

This is impressive, as it signals some of the authors could have posted their discussion in a more appropriate subreddit. This suggests that the model performed better than expected, and beyond what the plain metrics suggest.

## Conclusions

This is the final model selected with the following results:

| Model| Vectorizer| Best Cross Val| Train Accuracy| Test Accuracy| Sensitivity| Specificity| Precision| F1-Score|
|:-----|:---------:|:-------------:|:-------------:|:------------:|:----------:|:----------:|:--------:|:-------:|
|Logistic Regression   | TVEC | 94.1% |      95.9% |        94.9% |      94.2% |      95.5% |     94.8%|    94.5%|

Note: positive refers to r/investing subreddit while negative refers r/cryptocurrency subreddit.\
Therefore, sensitivity (true positive rate) refers to hit rate for predicting r/investing subreddit.\
In the same token, specificity (true negative rate) refers to the hit rate for predicting r/cryptocurrency subreddit.

This model has 95% accuracy, 94% sensitivity and 96% specificity.\
It is slightly able to predict a post in r/cryptocurrency (96%) better than a post in r/investing (94%). The slight betterment could be due to the consistently higher counts of oft-used lingo or words in the cryptocurrency space where the range of vocabulary is more specific.
This is also reflected in the predictor words probabilty with 9 words having >95% likelihood to be belonging to the r/cryptocurrency as opposed to 4 words having >95% likelihood for r/investing subreddit.

The data cleaning is done at the basic level, with the removal of non-words and basic stopwords. Lemmatizer preferred over Stemming so as to preserve the integrity of dictionary words, given the focus on understanding and interpretability of the model. Likewise, a conscious decision has been made not to scale the data prior to model fitting, again in the spirit of interpretability or ease of model understanding. The use of hyperparameters such as max_df and max_features through Vectorizer acts as a pseudo-cleaning step. The use of min_df was also considered but ultimately not adopted as the removal of low frequency words is addressed by limiting the max_features hyperparameter. High word counts (if any) that occurs across both categories and thus has low predictive value will be disregarded through max_df hyperparameter. Distinct words such as misspelt or non-standard English vocabulary words will be naturally omitted as max_feature caps the highest occurring words to a limit.

Logistic Regression has been found superior to the Naive Bayes model, and across all key metrics of accuracy, specificity and sensitivity as illustrated above. Misclassification rate at 5% is not too much of a concern at the given time, based on the analysis of the misclassified text as those appeared to have some elements of ambiguity that even human judgement may not be able to accurately classify it in spite of the added element of contextual knowledge.

In conclusion, it can be said with 95% confidence that the developed model will be able to address the problem our trading firm has set out to achieve. Beyond being able to provide classification into r/investing or r/cryptocurrency subreddit, we were able to identify word predictors and its associated probability of making a correct classification. The understanding of this knowledge could then open further doors on classifying between investing or cryptocurrency on different platforms and fora. This could provide early detection for nascent topics before they go viral and have some impact on the equities or crytocurrency market.

In essence, we managed to achieve what we had sought to do. In fact, we surpassed our own expectations with a model that is 95% accurate, and virtually equally adept at identifying r/investing and r/cryptocurrency posts. Future improvements and work can focus on expanding beyond Reddit to broaden the scope of internet chatter, as well as evaluating other model algorithms that could be superior to Logistic Regression.
