# A Data-Driven Approach to Estimating Calories in Recipes

**Author:** Keanu Ventura

## Introduction

> “Every second counts”  
> — *The Bear*

In the stressfull and exacting world of cooking, time, ingredients, preparation, and other factors all play a crucial role in determining the outcome of a dish. In one of my favorite TV series, *The Bear*, special emphasis is placed on the importance of time, not just in the kitchen, but in life. Inspired by this, my data science project dives into two large datasets consisting of recipes and ratings posted since 2008 on Food.com to answer one central question:  

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

Understanding what makes a recipe have a high rating allows home cooks, foodies, and recipe developers to make informed decisions when choosing or creating meals. By investigating the relationship between time and ratings, we can discover if there are patterns that illustrate what people value in a recipe. This project will check if people think spending more time actually leads to better quality recipes or if they just want quick and easy meals.

## Data Cleaning and Exploratory Data Analysis

> “I need you to understand that you’re not just cleaning, you’re resetting the systems”  
> — Sydney, *The Bear*

The following data cleaning steps I took were:

1. Left merged the RAW_recipes and RAW_interactions datasets together
    - This matched the unique recipes with their respective reviews
2. In the merged dataset, filled all ratings of 0 with np.nan
    - This was necessary because ratings only go from 1-5 and therefore a rating of 0 indicates the reviewer did not leave a rating
3. Calculated the average rating per recipe, added it as a column
    - This provides an understanding of how each recipe was rated overall 
4. Filtered out recipes with a cooking time greater than 500 minutes
    - The extreme values removed were either outliers, data entry errors, or data that would skew the analysis. Removing them made a dataset more representative of typical cooking times
5. Binned the minutes column into time intervals and added it as a column
    - Grouping the recipes by these time ranges makes it easier to analyze metrics across different durations
6. Extracted the calories value from nutrition per recipe, converted it to a float, and added it as a column
    - The nutrition column stored the different nutrition info values and so this step isolated the calories value and made it a type that can be used for analysis
7. Filtered out recipes with more than 1000 calories
    - This removed outliers, data entry errors, or recipes with exceptionally large calorie counts. Removing them helps the analysis focus on more typical calorie ranges

The final cleaned dataset **cleaned** contains 218885 rows, indicating the recipe with their respective review(s) retained after cleaning, and 19 columns providing the following information:

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

Here are a few rows of the cleaned dataset showing columns relevant to the future analysis:

| name                                 |   minutes |   n_steps |   n_ingredients |   rating |   avg_rating | time_bins   |   calories |
|:-------------------------------------|----------:|----------:|----------------:|---------:|-------------:|:------------|-----------:|
| 1 brownies in the world    best ever |        40 |        10 |               9 |        4 |            4 | 40-50       |      138.4 |
| 1 in canada chocolate chip cookies   |        45 |        12 |              11 |        5 |            5 | 40-50       |      595.1 |
| 412 broccoli casserole               |        40 |         6 |               9 |        5 |            5 | 40-50       |      194.8 |



### Univariate Analysis              

For this analysis, I analyzed the **distribution of cooking time (minutes) for the recipes**. The histogram below depicts how frequently different cooking times appeared in the dataset. The distribution is skewed to the right with a long right tail. There is also a decreasing trend, indicating that as cooking time gets longer, there are less of those recipes on Food.com. 

<iframe 
  src="assets/cooking-time-distribution.html" 
  width="800" 
  height="600" 
  frameborder="0">
</iframe>

### Bivariate Analysis

For this analysis, I analyzed the **average recipe ratings across different durations**. The line graph below illustrates the average rating for each cooking time interval. The distribution shows a clear downward trend, revealing that was cooking time increases, the average ratings tends to slightly decrease. This suggests that recipes that take longer to make may not be rated as highly as those with shorter times.

<iframe 
  src="assets/average_recipe_rating.html" 
  width="800" 
  height="600" 
  frameborder="0">
</iframe>

### Interesting Aggregates

To further understand the relationship between cooking time and average rating, I computed summary statistics for each time bin. Looking at the mean and median average ratings, the values remain consistently high across the bins, however, there is a noticeable **decline** once it reaches the 240-300 minute range. This suggests that once recipes exceed 240 minutes, their reviews have lower ratings. Additionally, the 0-20 minutes bins present the highest mean and median average ratings, suggesting that **people may favor quick recipes**. While every time interval contains recips rated from 1-5, it is evident that recipes with shorter cooking durations are more frequent in the dataset, indicating that fast meals are not only more loved on Food.com, but more common.

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

I believe that the rating column in my data set is **Not Missing At Random** (NMAR) because the missingness of a rating may depend on the **user_id** column. This is because certain users who leave reviews on Food.com may have a habit of consistently choosing not to leave a rating after leaving a review. Users individual behavior may be linked to the missingness and is not captured by any of the other observed variables. Thus to explore this, I performed the following permutation test:

**Null Hypothesis (H₀):** The missingness of ratings does not depend on the user_id  
**Alternative Hypothesis (H₁):** The missingness of ratings does depend on the user_id  
**Test Statistic:** The variance of the proportions of missing ratings across different user_id's  
**Significance Level:** 5% (α = 0.05)  

The bar chart below displays the top 20 user_id's that have the most missing ratings, highlighting how some users consistently leave reviews on recipes without leaving a rating. The distribution supports the notion that the missingness is user-dependent.

<iframe 
  src="assets/top20_userid_by_rating_missingness.html" 
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

**Results:** The observed variance of the proportions of missing ratings across different user_id's was 0.128, and the resulting p-value was 0.0  
**Conclusion:** Since the p-value of 0.0 is less than the significance level of 0.05, we **reject the null hypothesis**. This suggests there is strong evidence that the missingness of ratings does depend on the user_id, supporting the idea that the data is NMAR  

Building on the previous test that proved missingness depends on user_id, I also tested whether the missingess of the ratings columns depends on the **minutes** column. I did this to prove that missingness is not related to cooking time and to reinforce that the missingness pattern is specifically tied to user behavior and not random with respect to other variables. Thus, to explore this, I performed the following permutation test:

**Null Hypothesis (H₀):** The missingness of ratings does not depend on the cooking time of the recipe in minutes  
**Alternative Hypothesis (H₁):** he missingness of ratings does depend on the cooking time of the recipe in minutes  
**Test Statistic:** The variance of the proportions of missing ratings across different cooking times  
**Significance Level:** 5% (α = 0.05)  

The histogram below portrays the distribution of cooking time by rating missingness, highlighting that missing and non-missing rating values are similarly distributed across cooking times. This suggests that the missingness does not depend the minutes column.

<iframe 
  src="assets/minutes_by_rating_missingness.html" 
  width="800" 
  height="600" 
  frameborder="0">
</iframe>

<div style="width: 800px; height: 600px; overflow-x: auto; overflow-y: hidden; white-space: nowrap;">
  <iframe 
    src="assets/missingness_test_minutes_histogram.html" 
    width="900" 
    height="600" 
    frameborder="0" 
    style="display: inline-block; border:none; transform-origin: 0 0; transform: scale(0.68);">
  </iframe>
</div>

**Results:** The observed variance of the proportions of missing ratings across different cooking times was 0.0131, and the resulting p-value was 0.297  
**Conclusion:** Since the p-value of 0.297 is greater than the significance level of 0.05, we **fail to reject the null hypothesis**. This suggests there is strong evidence that the missingness of ratings does not depend on the cooking time (minutes)

## Hypothesis Testing

> “I just thought it’d be nice… something simple, something good”  
> — Carmy, *The Bear*

To investigate the relationship between cooking time and recipe ratings, I performed a hypothesis test comparing recipes with short cooking times (20–30 minutes) to those with long cooking times (300–400 minutes)  

**Null Hypothesis (H₀):** There is no difference in average recipe ratings between recipes with short cooking times and those with long cooking times  
**Alternative Hypothesis (H₁):** There is a difference in average recipe ratings between the two cooking time bins  
**Test Statistic:** The difference in means of average ratings between the two cooking time bins  
**Significance Level:** 5% (α = 0.05)  

<iframe 
  src="assets/hypothesis_test_permutation_distribution.html" 
  width="800" 
  height="600" 
  frameborder="0">
</iframe>

**Results:** The observed difference in average ratings was approximately 0.124, and the resulting p-value was 0.0.  
**Conclusion:** Since the p-value of 0.0 is less than the significance level of 0.05, we **reject the null hypothesis**. This suggests there is strong evidence that recipes with short and long cooking times tend to receive different average ratings.

## Framing a Prediction Problem

> “What grows together, goes together”  
> — Tina, *The Bear*

For my project, I plan to **predict the number of calories in a recipe**.  

**Type of problem:** Regression  
**Response variable:** Calories (continous)  
**Evaluation Metrics:**  Root Mean Squared Error (RMSE) and R²  
**Time of prediction information:** For the features I would know at the time of prediction, I decided to stray away from features like the full nutrition breakdown (e.g., fat, sugar) as they would only be known after calories are already calculated. Thus, I selected features known before the nutritional information is calculated such as **n_ingredients** and **minutes**  

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

**Group X:** Simple recipes (n_steps ≤ 9)  
**Group Y:** Complex recipes (n_steps > 9)  
**Evaluation metric:** Root mean squared error (RMSE)  
**Null Hypothesis (H₀):** My model is fair. Its RMSE for simple and complex recipes is roughly the same, and any differences are due to random chance  
**Alternative Hypothesis (H₁):** My model is unfair. Its RMSE for simple recipes is lower than that for complex recipes  

<iframe 
  src="assets/fairness_permutation_test.html" 
  width="800" 
  height="600" 
  frameborder="0">
</iframe>

**Results:** The RMSE for simple recipes was 198.40, while the RMSE for complex recipes was 210.37, resulting in an observed difference of 11.97. The resulting p-value was 0.0.  
**Conclusion:** Since the p-value of 0.0 is less than the significance level of 0.05, we **reject the null hypothesis**. This provides strong evidence that my model is unfair, as it performs significantly worse on complex recipes than on simple ones. In other words, the model is less accurate when predicting calorie content for recipes with larger n_steps.
