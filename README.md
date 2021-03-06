# Project 3: Web APIs & NLP

# Problem Statement

Perform exploratory analysis and classification of chess, poker subreddits to identify words and phrases that could be used in targeted advertisement. Use results of the analysis in targeted ads by online chess servers, chess classes, poker cardrooms (e.g. chess.com, pokerstars).

# Executive Summary

I used requests library to collect around 5,000 titles for each of chess and poker subreddits. Latest datapoint of collected data is January 13, 2021 and earliest is September 27, 2020. (please see notebook_1 for details) After cleaning the data, I looked closer at each subreddit title and their composition. I decomposed title length and discovered that majority of chess subreddit titles are longer compared to poker titles. Mean number of characters in the chess subreddit is 62, while titles in the poker subreddit are 40 characters long on average. I also wanted to look at distribution of words in both subreddits and, again, most chess titles contained more words ~1-11 compared to ~1-6 words in the poker subreddit. 

Digging one layer deeper, I wanted to see what were the most commonly used words in chess and poker subreddits. Not very surprising that the most common words use in the chess subreddit is 'chess'. Among some other words: 'white', 'black', 'mate', 'checkmate', 'queen', 'opponent', 'moves'.Learned that among most repeated words in the chess subreddit, there were quite a few commonly used in the poker subreddit as well. They are: 'game', 'play', 'best', 'playing'. In the poker subreddit, most used word is 'poker'. As well as, words:'live', 'players', 'games', 'cash', 'tournament', 'pokerstars'. (please see notebook_2 for details)

I also wanted to compare polarity sentiment of chess and of poker subreddits. I removed titles with 0 polarity for a more clear representation. And it looks like, on average, chess subreddit titles scored 0.16, while poker scored 0.12. (please see notebook_2 for details). 

After performing exploratory analysis, I engineered two features - ‘title_length’ and ‘title_word_count’ related to the length and number of words in each title. Saved the data as a clean csv file that I used for my models. I dummified my target. 
My baseline null model scored 0.52 accuracy. 

I’ve built 6 models in total using 'title' as the only predictor (please see detailed comparison below). My best performing model was Naive Bayes with lemmatizer based on accuracy, f1, and recall scores. Random Forest and Logistic Regression performed worst based on recall. Random forest was very overfit - on the train data, the scores ranged from 0.96 to 0.98 compared to 0.55 to 0.77 on the test data.

### Model Comparison and Summary

| Model | Accuracy | F1 Score | Recall|
|-------|----------|----------|-------|
| Lemmatizer / Naive Bayes | 0.93 | 0.92 | 0.94 |
| CountVectorizer / StandardScaler / SVC | 0.9 | 0.89 | 0.87 |
| CountVectorizer / Naive Bayes | 0.83 | 0.79 | 0.69 |
| CountVectorizer / StandardScaler / Logistic Regression | 0.82 | 0.78 | 0.66 |
| CountVectorizer / StandardScaler / KNeighbors Classifier | 0.78 | 0.77 | 0.73 |
| CountVectorizer / Random Forest | 0.77 | 0.70 | 0.55 |

### Naive Bayes vs SVC Comparison

| Model | Best Parameters | Mean Fit Time | Scaling | Coefficients |
|-------|-----------------|---------------|---------|--------------|
| Lemmatizer / Naive Bayes | max features: 10,000, ngram range: (1, 1), stop words: None, alpha: 1 | 3.53 | No | chess, move, game, white, mate|
CountVectorizer / SVC | max features: 1,000, ngram range: (1, 1), stop words: None, C: 1, gamma: scale | 7.56 | Yes | Does not provide coefficient details

# File Directory

This Repo contains 4 folders: 

1. Data Folder: 

    - combined_df.csv - raw data collected from subreddit api
    - clean_combined.csv - cleaned csv file including engineered features

2. Notebooks: 

    - notebook_1_api_data_collection
    - notebook_2_cleaning_eda
    - notebook_3_model
    
3. Presentation:

    - project presentation pdf file 

4. Drafts

# Data Dictionary

| title | subreddit | selftext | created_utc | title_length | title_word_count |
|-------|-----------|----------|-------------|--------------|------------------|
| subreddit page title | subreddit name | subreddit selftext | date and time title was posted | number of characters in title | number of words in title |

# Conclusion and Recommendation

### Chess

Based on the findings of the exploratory data analysis, I would recommend online chess platforms bidding on the following keywords for in the search engine advertisements:
- chess
- mate 
- checkmate
- lichess
- moves

Phrases:
- chess set
- new chess
- blitz game
- playing chess

Avoid words: 
- game
- best
- playing
- play

### Poker

I would recommend online poker platforms bidding on the following keywords:
- poker
- tournament
- pokerstars
- stakes
- hands

Phrases: 
- online poker
- live poker
- cash game
- bad bet

Avoid words: 
- game
- best
- playing
- play

# Future Research

If I had more resources, I would expand the current project to include:

- Build a neural network
- Include posts and comments as features
- Collect and add data from chess and poker blogs

# Sources:
https://www.earthdatascience.org/courses/use-data-open-source-python/intro-to-apis/analyze-tweet-sentiment-in-python/
https://www.reddit.com/r/chess/
https://www.reddit.com/r/poker/