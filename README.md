# ![](https://ga-dash.s3.amazonaws.com/production/assets/logo-9f88ae6c9c3871690e33280fcf557f33.png) Predicting Reddit Categories: Cinematography vs. Photography

Reddit is a forum-based website curated to users' interests. The site is made up of specialized sub-forums, or 'subreddits,' for users with similar interests to gather, ask questions, and share information. Each post is scored, as users can up-vote or down-vote posts, and I gathered my data based on posts with the highest score in each category.

Photography is a really broad world, which encompasses enthusiasts, professionals, and anyone that picks up a camera or a phone. Cinematography is more niche, with a focus specifically on the shooting and lighting of a film. This difference can be seen through the amount of members in each subreddit. r/Cinematography has 171k members, while photography has over 3.5m. Despite their differences in still and motion shooting, and lot of the terminology, brands, and gear are similar. Because of this, it leads to an interesting challenge of separating these subreddits on a higher level.


### Problem Statement

Given the format of Reddit, can we use Natural Language Processing(NLP) and Classification Modeling to accurately predict what subreddit it belongs to based on the contents of a post?

Through this project, I will be digging into the similarities and differences of the r/Cinematography subreddit, and the r/Photography subreddit. After cleaning and visualizing the data, I will run the data through three different models to find the highest results. I will be focusing on Random Forest Classifier, Bagging Classifier, and Support Vector Machines as the models to measure success. The overall success of these models will be based on the percentage of testing accuracy, and the proximity that testing data can get to the training data success.


### Data:

The data was scraped using a Python Reddit API Wrapper(PRAW), and I gathered 1000 of the highest scored posts from each subreddit. This left me with a (2000, 9) data frame, which I narrowed down to 2000 cells, and 5 columns. 

526 posts had no text in the body, so the header and body features were combined into one feature to avoid NaN values. The final features were:
    -score
    -number of comments
    -subreddit category
    -text
  

### EDA:

The Dataframe was split into smaller dataframes of their respecting subreddits, for a comparison analysis. I then count vectorized with a stop words hyperparameter of english, to see the most common words in each Dataframe. From this I was able to get a closer look at the content similarities between Photography and Cinematography.
In the top 10 most used words for each subreddit, four of them were found in both. 
    -Camera
    -Just
    -Like
    -Want


### Data Preprocessing

For preprocessing, I used train-test-split on the larger 2000 row dataset, and added lemmatizer to count vectorizer, to fit the model. From here I used stop_words to isolate the words that would have the largest impact on the meaning of the posts, before I started running models.
   
   
### Modeling:

Three models were used to find the fit for the data.

    1. Random Forest Classifier 
    {'max_features': 475, 'min_samples_leaf': 2, 'n_estimators': 50}
        -Training score: 92.7%
        -Testing score: 92.25%
        
    2. Bagging Classifier
        -Training score: 98.98%
        -Testing score: 90.2%
        
    3. Support Vector Machines
        -Training score: 87%
        -Testing score: 82.5%
        
After initially running all three models and seeing that Random Forest had the highest score, I went in with GridSearchCV to see if I could fine tune the parameters for a more successful model. The parameters above are the resuls.
  

### Conclusions:
Given the similarities in the subreddits, and the lack of posts that had text in the body, I am pleased with a final score of 92.25% testing accuracy. 

I creates a dataframe specifically of misclassified posts to see where the model could imporve, and posts tended to have little contextual references:

    "Fall Foliage Map amp Nationwide Peak Leaf Forecast"

Or the text relied on key words that were strong in both subreddits:
   
    “Why few cameras provide Geotagging just wondering why not built into any higher grade cameras… would be awesome for travelling”

  
### Next Steps:

The next step is to pull a much larger dataset. This should allow the model to have more information for both categories, and can hopefully distinguish between the two better. 

Because one of the concerns was not enough text in a post, I would also filter to posts with a minimum word count.
   

---

