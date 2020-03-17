# reddit-project
Scraped ask men and ask women and created model to predict which subreddit a post would go into

# Subreddit Analysis: AskWomen vs AskMen

## Table of Contents
[1.0 Directory Structure](#1.0-Directory-Structure)<br>
[2.0 Executive Summary ](#2.0-Project-Outline-/-Problem-Statement)<br>
[3.0 Description of Data](#3.0-Description-of-Data)<br>
[4.0 Final Model](#4.0-Final-Model)<br>
[5.0 Data Visualization](#5.0-Data-Visualization)<br>
[6.0 Conclusion](#5.0-Conclusion)<br>


## 1.0 Directory Structure

├── project_2
    
    ├── Scrape and Clean
    
    ├── Models
    
    ├── Data
        
    ├── README.md
    
    ├── subreddit_analysis.pdf

# Executive Summary

### Problem
Given two subreddits, 'Ask Men' and 'Ask Women', create a model that can predict which subreddit a post belongs to based on the text. 

### Process
I scraped roughly 5000 posts from each of the two subreddits using the Pushshift API. I then loaded the data into a combined dataframe with each post in its own row, and the given subreddit in the 'target' column represented by ones and zeros. I then cleaned and lemmatized the words, basically removing non-English characters and reducing words to their stem. I then vectorized the data, which is essentially transforming the words into strings of numbers so they can be analyzed.

### Models
I split my data into training and testing sets and then fit a variety of models to see which one produced the best results on the test data. For each model, I used the gridsearch function to evaluate each to find the optimal hyperparameters for each model. The two best performing models were Random Forest with a Count Vectorizer and a Logistic Regression model with a TFID Vectorizer. The LDA model was interesting but did not yield good results.

### Conclusion
The accuracy for the two top models was about 70%. The random forest achieved the best results, with an accuracy rate of 71.1%. While significantly better than the random guessing baseline of 53%, the final model certainly still leaves much to be desired. Overall, the short length of the posts and the similarity in frequently used words between the two reddits made differentiating quite difficult for the models. Going forward, I think using the comments would be an easier way to differentiate between the two. 


# Description of Data

I scrapped 2500 submission from each subreddit, and transformed them into a dataframe, and then cleaned them in various ways. Ask Women is represented by a one and Ask Men is represented as a zero. The data was cleaned using the Regular Expressions module and lemmatization. I also experimented with using all posts, only posts that hadn't been removed by moderators, and only posts that hadn't been removed and contained text in addition to the title. The model performed best on all submissions that hadn't been removed by moderators.

In the dataframe, I combined the 'title' and 'selftext' columns to make a 'text' column that used all available text

The majority of posts were under 200 characters, which was a challenge since the model often didn't have much to go on.

# Final Model

The best performing model was a Random Forest with a count vectorizer. It achieved an accuracy percentage of 71.1 percent. The count vectorizer transforms each document into a series of numbers, with a column for each word. The Random Forest model used 200 estimators or 'trees'. The following parameters were used:

'cvec__max_df': 0.8, 'cvec__min_df': 3, 'cvec__ngram_range': (1, 1), 'cvec__stop_words': 'english', 'rf__n_estimators': 200

TFIDVectorizer with Logistic Regression also achieved a fairly high accuracy score, of 68.5 percent. 

## Conclusion

Base on posts alone, it is difficult to predict which of the two subreddit, Ask Men and Ask Women came from. Even after extensive modeling, the best accuracy score achieved was only 68.5%. Going forward, it would be helpful to scrape comments that go with posts. The comments tend to be longer, more specific, and are generally answered by only men or only women, rather than questions that appear to come from both genders.

The modeled appeared to especially struggle with posts about relatioships, perhaps because they contained so many gendered terms that related to the other subreddit. 
