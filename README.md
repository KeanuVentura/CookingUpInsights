# A Data-Driven Approach to Estimating Calories in Recipes

## Introduction

> “Every second counts”  
> — *The Bear*

In the stressfull and exacting world of cooking, time, ingredients, preparation, and other factors all play a crucial role in determining the outcome of a dish. In the Apple TV series, *The Bear*, special emphasis is placed on the importance of time, not just in the kitchen, but in life. Thus, this data science project dives into two large datasets consisting of recipes and ratings posted since 2008 on Food.com to explore a central question: **What is the relationship between the cooking time and average rating of recipes?**

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




<iframe 
  src="assets/hypothesis_test_permutation_distribution.html" 
  width="800" 
  height="600" 
  frameborder="0">
</iframe>


> “What grows together, goes together”  
> — Tina, *The Bear*


## Framing a Prediction Problem

For my project, I plan to **predict the number of calories in a recipe** based on features known before the nutritional information is calculated. This is a **regression problem** because the response variable(calories) is continous. The metrics I'm choosing to evalute my model are **Root Mean Squared Error (RMSE)** and **R²**. For the features I would know at the time of prediction, I decided to stray away from features like the full nutrition breakdown (e.g., fat, sugar) as they would only be known after calories are already calculated. Thus, I selected features such as ***n_ingredients*** and **minutes**. 

## Baseline Model

## Final Model

## Fairness Analysis

<iframe 
  src="assets/fairness_permutation_test.html" 
  width="800" 
  height="600" 
  frameborder="0">
</iframe>


