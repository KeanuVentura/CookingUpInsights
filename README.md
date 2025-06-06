# A Data-Driven Approach to Estimating Calories in Recipes


## Introduction

> “Every second counts”  
> — *The Bear*

In the stressfull and exacting world of cooking, time, ingredients, preparation, and other factors all play a crucial role in determining the outcome of a dish. In the Apple TV series, *The Bear*, special emphasis is placed on the importance of time, not just in the kitchen, but in life. Thus, this data science project dives into two large datasets consisting of recipes and ratings posted since 2008 on Food.com to answer one central question:<br>

 **What is the relationship between the cooking time and average rating of recipes?**

The first dataset **RAW_recipes.csv** contains 83,782 rows, indicating 83,782 recipes and 12 columns providing the following information:

| Column         |Description                                                                                         |
|----------------|----------------------------------------------------------------------------------------------------|
| name           | Recipe name                                                                                        |
| id             | Recipe ID                                                                                          |
| minutes        | Minutes to prepare recipe                                                                          |
| contributor_id | User ID who submitted this recipe                                                                  |
| submitted      | Date recipe was submitted                                                                          |
| tags           | Food.com tags for recipe                                                                           |
| nutrition      | Nutrition info: calories, fat, sugar, sodium, protein, saturated fat, carbs (% daily value)        |
| n_steps        | Number of steps in recipe                                                                          |
| steps          | Text for recipe steps, in order                                                                    |
| description    | User-provided description                                                                          |
| ingredients    | Text for recipe ingredients                                                                        |
| n_ingredients  | Number of ingredients in recipe                                                                    |

The second dataset **RAW_interactions.csv** contains 731,927 rows, indicating 731,927 reviews from users on recipes and 5 columns providing the following information:

| Column     | Description            |
|------------|------------------------|
| user_id    | User ID                |
| recipe_id  | Recipe ID              |
| date       | Date of interaction    |
| rating     | Rating given           |
| review     | Review text            |







## Data Cleaning and Exploratory Data Analysis

> “I need you to understand that you’re not just cleaning, you’re resetting the systems”
> — Sydney, *The Bear*

| Column         | Description     |
|----------------|-----------------|
| name           | object          |
| id             | int64           |
| minutes        | int64           |
| contributor_id | int64           |
| submitted      | datetime64[ns]  |
| tags           | object          |
| nutrition      | object          |
| n_steps        | int64           |
| steps          | object          |
| description    | object          |
| ingredients    | object          |
| n_ingredients  | int64           |
| user_id        | float64         |
| date           | datetime64[ns]  |
| rating         | float64         |
| review         | object          |
| avg_rating     | float64         |
| time_bins      | category        |
| calories       | float64         |


| name                                 |   minutes |   n_steps |   n_ingredients |   rating |   avg_rating | time_bins   |   calories |
|:-------------------------------------|----------:|----------:|----------------:|---------:|-------------:|:------------|-----------:|
| 1 brownies in the world    best ever |        40 |        10 |               9 |        4 |            4 | 40-50       |      138.4 |
| 1 in canada chocolate chip cookies   |        45 |        12 |              11 |        5 |            5 | 40-50       |      595.1 |
| 412 broccoli casserole               |        40 |         6 |               9 |        5 |            5 | 40-50       |      194.8 |



### Univariate Analysis

<iframe 
  src="assets/cooking-time-distribution.html" 
  width="800" 
  height="600" 
  frameborder="0">
</iframe>

### Bivariate Analysis

<iframe 
  src="assets/average_recipe_rating.html" 
  width="800" 
  height="600" 
  frameborder="0">
</iframe>

### Interesting Aggregates

| time_bins   | mean_avg_rating | median_avg_rating |
|:------------|----------------:|------------------:|
| 0-10        |         4.71089 |           4.9     |
| 10-20       |         4.71461 |           4.90909 |
| 20-30       |         4.67489 |           4.85714 |
| 30-40       |         4.67723 |           4.85714 |
| 40-50       |         4.66288 |           4.85    |
| 50-60       |         4.66885 |           4.85185 |
| 60-90       |         4.67527 |           4.88095 |
| 90-120      |         4.66838 |           4.9     |
| 120-180     |         4.66414 |           4.875   |
| 180-240     |         4.66297 |           4.83333 |
| 240-300     |         4.58725 |           4.69231 |
| 300-400     |         4.5509  |           4.67742 |
| 400-500     |         4.57296 |           4.73333 |

| time_bins   | min_avg_rating | max_avg_rating | count_avg_rating |
|:------------|---------------:|---------------:|-----------------:|
| 0-10        |              1 |              5 |            21011 |
| 10-20       |              1 |              5 |            30721 |
| 20-30       |              1 |              5 |            35736 |
| 30-40       |              1 |              5 |            35190 |
| 40-50       |              1 |              5 |            25941 |
| 50-60       |              1 |              5 |            17356 |
| 60-90       |              1 |              5 |            32605 |
| 90-120      |              1 |              5 |             7985 |
| 120-180     |              1 |              5 |             7770 |
| 180-240     |              1 |              5 |             4114 |
| 240-300     |              1 |              5 |             3372 |
| 300-400     |              1 |              5 |             3913 |
| 400-500     |              1 |              5 |             2310 |


## Assessment of Missingness

> “This is a system. It’s not just chaos. Every little thing matters”
> — Carmy, *The Bear*

<iframe 
  src="assets/top20_userid_by_rating_missingness.html" 
  width="800" 
  height="600" 
  frameborder="0">
</iframe>

<iframe 
  src="assets/minutes_by_rating_missingness.html" 
  width="800" 
  height="600" 
  frameborder="0">
</iframe>


<div style="width: 800px; height: 600px; overflow-x: auto; overflow-y: hidden; white-space: nowrap;">
  <iframe 
    src="assets/userid_permutation_distribution.html" 
    width="900" 
    height="600" 
    frameborder="0" 
    style="display: inline-block; border:none; transform-origin: 0 0; transform: scale(0.68);">
  </iframe>
</div>

<div style="width: 800px; height: 600px; overflow-x: auto; overflow-y: hidden; white-space: nowrap;">
  <iframe 
    src="assets/missingness_test_minutes_histogram.html" 
    width="900" 
    height="600" 
    frameborder="0" 
    style="display: inline-block; border:none; transform-origin: 0 0; transform: scale(0.68);">
  </iframe>
</div>



## Hypothesis Testing

> “I just thought it’d be nice… something simple, something good”
> — Carmy, *The Bear*

To investigate the relationship between cooking time and recipe ratings, I performed a hypothesis test comparing recipes with short cooking times (20–30 minutes) to those with long cooking times (300–400 minutes).<br>

**Null Hypothesis (H₀):** There is no difference in average recipe ratings between recipes with short cooking times and those with long cooking times.<br>

**Alternative Hypothesis (H₁):** There is a difference in average recipe ratings between the two cooking time bins.<br>

**Test Statistic:** The difference in means of average ratings between the two cooking time bins.<br>

**Significance Level:** 5% (α = 0.05)

<iframe 
  src="assets/hypothesis_test_permutation_distribution.html" 
  width="800" 
  height="600" 
  frameborder="0">
</iframe>

**Results:**
The observed difference in average ratings was approximately 0.124, and the resulting p-value was 0.0. 

**Conclusion**
Since the p-value of 0.0 is less than the significance level of 0.05, we reject the null hypothesis. This suggests there is strong evidence that recipes with short and long cooking times tend to receive different average ratings.



## Framing a Prediction Problem

> “What grows together, goes togethe”  
> — Tina, *The Bear*

For my project, I plan to **predict the number of calories in a recipe** based on features known before the nutritional information is calculated. This is a **regression problem** because the response variable (calories) is continous. The metrics I'm choosing to evalute my model are **Root Mean Squared Error** (RMSE) and **R²**. For the features I would know at the time of prediction, I decided to stray away from features like the full nutrition breakdown (e.g., fat, sugar) as they would only be known after calories are already calculated. Thus, I selected features such as ***n_ingredients*** and **minutes**. 

## Baseline Model

> “Start from scratch. Make it clean. Make it simple”
> — Marcus, *The Bear*


## Final Model

> “This is not a sprint. It’s a marathon, and we’re learning every single day”
> — Carmy, *The Bear*


## Fairness Analysis

> “You don't get to decide how people feel”
> — Sydney, *The Bear*

To assess fairness in my model, I compared its performance across two groups:

**Group X:** Simple recipes (n_steps ≤ 9)<br>

**Group Y:** Complex recipes (n_steps > 9)<br>

**Evaluation metric:** Root mean squared error (RMSE)<br>

**Null Hypothesis (H₀):** My model is fair. Its RMSE for simple and complex recipes is roughly the same, and any differences are due to random chance.<br>

**Alternative Hypothesis (H₁):** My model is unfair. Its RMSE for simple recipes is lower than that for complex recipes.<br>

<iframe 
  src="assets/fairness_permutation_test.html" 
  width="800" 
  height="600" 
  frameborder="0">
</iframe>