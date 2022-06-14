## Subreddit API and NLP

### **Problem Statement**

Taco Bell holds the largest share of the Mexican-style restaurant market in the US. A main driver of Taco Bell’s success is their product innovation (think Doritos Tacos Locos). Taco Bell has successfully incorporated popular elements of Mexican cuisine to craft an exciting menu that attracts over 40 million customers on a weekly basis.

**_The product innovation team has task the data science team to search for other popular elements of Mexican cuisine that are currently missing from their menu._**

### **Approach**

In order to tackle this problem, I will analyze posts from the r/tacobell and the r/mexicanfood subreddits to extract items that are popular in mexican cuisine but missing in the Taco Bell menu.

Benefits of using subreddit posts:
- Content rich (posts are allowed over 40,000 characters)
- Observe directly how consumers from each group write about food items they like
- The r/mexicanfood subreddit highlights popular and favorite foods

**EDA**
- Explore sentiment analysis with VADER
    -  What differences are there in sentiment between each subreddit
- Explore commong words after vectorizing
    -  What are common words in each subreddit

**Modeling**

Although our problem statement is not concerned with predictions, I will explore different classification models to learn more about the differences between each subreddit. These models use the vocabulary from each posts to predict from which subreddit the post originated. Therefore, looking at the words the models has identified as most important to differentiate both groups can help us identify food-related words from the r/mexicanfood subreddit that are not in the r/tacobell subreddit and highlight opportunities for Taco Bell to expand its menu.

### **The Data**

The data used for this analysis was extracted from the r/tacobell and the r/mexicanfood subreddits using Reddit's API. To see code for extracting and filtering the data, please refer to the get_data.ipynb notebook in this repository.

#### Data Dictionary

|Feature|Type|Datase|Description|
|---|---|---|---|
|author|object|subreddits|Reddit username of the author|
|selftext|object|subreddits|Text in the post|
|title|object|subreddits|Title of the post|
|subreddit|object|subreddits|The subreddit where the post originates (target variable)|
|selftext_lenth|int|subreddits|The length of the post|
|selftext_words|int|subreddits|Count of the total words in the post|
|sentiment_score|float|subreddits|Compound sentiment score from VADER|
|sentiment|object|subreddits|Sentiment classification based on the compound sentiment score|

### Analysis

In the above analysis, I sought to identify popular food items from Mexican cuisine that may be missing from the Taco Bell menu. While Taco Bell is not known for its authenticity, it has done a great job of taking key ideas from mexican food to recreate an exciting menu that attracts a loyal consumer base. To identify popular items from Mexican food, I explored about 1200 posts from r/mexicanfood subreddit. I also explored about 1200 post from the r/tacobell subreddit to understand favorite food items from the franchise, and overall customer preferences and sentiments that can inform my final recommendations.

**Sentiment Analysis**

In the EDA process above we identified that posts from both subreddits had a high proportion of unique authors, and shared a similar distribution of post length. Insights began to emerged when we used VADER's sentiments analysis to assign each post a sentiment score. We then used the sentiment scores to segregate very positive posts and very negatives posts. Exploring posts that scored as very positive I noticed that in the users of r/mexicanfood had the following favorite foods:
- *salsas (sauces) and meat (carne)*

Exploring positive posts from the r/tacobell subreddit highlighted priorities for this customer base:
- *affordability and convenience*

**Most Frequent Words Analysis**

The top 40 words in r/mexicanfood included the following food-related words:
- *sauce, chicken, tacos, beef, (corn) tortillas, salsa, meats, beans, and rice*

And these are all ingredients (corn tortillas to a lesser extend) that are part of Taco Bell's menu, highlighting that Taco Bell does a good job of incorporating popular Mexican ingredients into their Menu.

Other frequent words in the r/tacobell subreddit stresses that Taco Bell customers are not only interested in their food experience, but care just as much about the ease of the transaction.
The word *app* and *drive* are also among the most frequent words, meaning customers often write about their purchasing experience.

**Most Frequent Words Pairs Analysis**

I also used CountVectorizer to explore bigrams (pairs of words) that were most popular in each subreddit, which identified specific items from Mexican food are very popular, including:
- Corn tortilla, carne asada, salsa verde, al pastor

These items are not currently present in the Taco Bell menu, so they do present an opportunity for the product development team to explore.

**Modeling**

Lastly, I explored classification models to confirm the insights we gained from the EDA, and explore other patterns in the data. I used an AdaBoost model that performed very well with few cases of misclassification and accuracy score of 0.90. I, therefore, feel confident that we can use the feature importances identified by this model to better understand the data. Food-related words identified by the model as meaningful in distinguishing between both subreddits include tortillas, salsa, and meat. Words that our EDA had already identified as being prominent in the r/mexicanfood subreddit, but less prominent in r/tacobell.

I also used a logistic regression model with an accuracy score of 0.95. Examining the model's coefficients we saw that the model identified many of the same words as our EDA and AdaBoost \. However, this model identified tamales and birria as significant words in classifying posts from r/mexicanfood. And in fact, these are two items that are not currently part of the Taco Bell menu.

### Recommendations

Our analysis of r/mexicanfood and r/tacobell subreddits helped identify important ingredients and foods that are popular and prominent in Mexican cuisine. Taco Bell has done a really great job of incorporating most of the popular components. However, I want to highlight opportunities to enhance the Taco Bell menu with popular Mexican cuisine items.

**Identified Opportunities**

- The data shows that corn tortillas are very popular in Mexican cuisine, perhaps Taco Bell should explore whether they should offer corn tortilla soft tacos
- Salsas (sauces) are another prominent component of Mexican cuisine, and while Taco Bells does a great job of developing many different sauces, our analysis suggests that Taco Bell should explore the development of more authentic sauces - and consider branding them as salsas.
-  Meats are another important food component in Mexican cuisine, of note is the emphasis in different types of meat preparations. In particular carne asada and al pastor where identified in our EDA as favorites. Again, our data suggest that Taco Bell should explore its meat offerings.
- Lastly, the logistic model identified two Mexican food items that were not revealed during our EDA. Tamales and Birria (tacos) are very popular items not yet incorporated by Taco Bell. While tamales does not fit the profile of the typical Taco Bell item, birria tacos - which are currently surging in popularity - may be a good fit. Birria tacos are essentially very saucy tacos with cheese and meat filling (ingredients already developed).

**Additional Considerations**

The opportunities above are suggestions for the product development team who seek new ideas to expand it's menu. However, these are merely suggestions that should be further explored in conjunction with the business and marketing team to determine whether adding corn tortillas, developing salsa, or adding birria tacos is appropriate.

Our analysis also identified that customers priorities includes costs and convenience, which are additional factors to consider when expanding the menu. 
