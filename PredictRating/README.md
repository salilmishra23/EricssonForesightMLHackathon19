## Problem 1 : [Predict ratings](https://www.hackerearth.com/challenges/hiring/ericsson-ml-challenge-2019/machine-learning/abc-test/)

### Problem Statement : 

Data have been extracted from a website that provides job reviews. The website wants to analyze texts and the corresponding rating that is provided by the user about startups. A research team wants to analyze the liability of the review. In other words, they want to verify whether texts correspond as the same as the score that is provided as the rating for a startup. 
This task helps the website to rank the user's reviews or ratings.   

Your tasking is to predict the overall rating of reviews.

### Data Description : 

    'ID': Indentificaition Number 
    'Place': Startup {1-6}
    'location': Location of startup 
    'date': Date of review 
    'status': Current status with the startup 
    'job_title': Position of work at the startup
    'summary': Overall summary
    'positives': Pros
    'negatives': Cons 
    'advice_to_mgmt': Comments given by the reviewer to the management
    'overall': Overall rating provided by the user {1-5}
    'score_1' to 'score_5': Intricate rating with reflects the condition of work at the startup {1-5}
    'score_6': Number of likes received by the reviewer for the review 

### Evaluation Metric :

F1-Score

### Approach :

The dataset was derived from the common employee review dataset available online but changed in such a way that modeling didn't show much result, and couldn't try a lot of methods due to lack of time (dataset was changed on the 3rd day of the 7 day hackathon). 

Most people were scoring in .3 to .35 zone. Seeing that I decided to focus majorly on the columns with score.

#### Features :
- Worked 
   - Columns score_1 to score_5 had missing values filled them with their respective modes.
   - Columns score_1 to score_5 had values like 1.5, 2.5, etc. I decided to floor them as they performed better on LB.
   - Made columns out of missing values from `advice_to_mgmt` & `location`. Like `avail_advice_to_mgmt` 0 where present and 1 where absent.
   - Removed all the text columns as features from them didn't perform well on LB.
   - Using CatBoost as majority of the columns were treated as categorical
   - Bagging CatBoost model 15 times.
   
- Not Worked 
  - Any sort of feature from text columns, Tfidf, CountVectorizer, etc. didn't try DL techniques due to time constraint.
  - Statistical features from text columns like length, average words, etc
  - Ceil on score_x columns

### Leaderboard Score : 
    0.39088 (3rd best solution, top solution being : 0.39486 & 0.39428)
