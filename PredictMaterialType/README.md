## Problem 2 : [Predict the material type](https://www.hackerearth.com/challenges/hiring/ericsson-ml-challenge-2019/machine-learning/predict-the-publishing-material-type-32/)

### Problem Statement : 

We are living in a digital world where people prefer to read articles online or watch videos rather than reading a book. Assume that you are a member of a marketing agency and you are given a dataset having the title, subjects, and other features based on which you have to predict what will be the material of to-be-published research so that you can tie-up with an ideal publisher and help them grow.

You have to predict the column “MaterialType” and submit in the format given in the “sample_submissions.csv” file.

### Data Description : 

    ID - Calculated unique ID for each research
    UsageClass - Denotes if an item is “physical” or “digital”
    CheckoutType - Denotes the vendor tool used to check out the item
    CheckoutYear - Year of checkout for this record(4-digit)
    CheckoutMonth - Month of checkout for this record
    Checkouts - A count of the number of times the title was checked out within the “Checkout Month”
    Title - Full title and subtitle of an individual item
    Creator - Author or entity that is responsible for authoring the item
    Subjects - The subject of the item as it appears in the catalog
    Publisher - Publisher of the title
    PublicationYear - Year from the catalog record in which the item was published, printed, or copyrighted
    MaterialType - Describes the type of item checked out 

### Evaluation Metric :

weighted F1-Score

#### Features :
- Worked 
   - Making columns out of `nan` values present in `Subject`, `Publisher` & `Creator` columns.
   - Removing stopwords, most frequent and least frequent words.
   - Adding statistical features like `word_count`, `char_count`, `average_word_length`
   - Tfidf & stemming on combined `Title` & `Subject` columns.
   - Using `Logistic Regression` with `l1 penalty` to experiment quickly with Text features. Local CV & LB were consistent with it
   - Removing redundant columns like `CheckoutYear`, `CheckoutMonth` &`UsageClass` having only 1 value.
   - Weighted average of LightGBM and XGBoost models on same features
   
- Not Worked 
  - Adding other columns like `Publisher`, `Creator` to the combined column for Tfidf.
  - Tfidf on individual text columns and SVD & PCA on them
  - Bagging performed poorly than weighted average

### Leaderboard Score : 
    0.89514 (3rd best solution without using leak, top solutions : 0.90969 & 0.89563)
  Some(3) people found leak in the dataset and scored 0.95x, 0.98x and 1.
