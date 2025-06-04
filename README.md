# A Data-Driven Approach to Estimating Calories in Recipes

## Introduction

The first dataset **RAW_recipes** contains 83,782 rows, indicating 83,782 recipes and 12 columns providing the following information:

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

The second dataset **RAW_interactions** contains 731,927 rows, indicating 731,927 reviews from users on recipes and 5 columns providing the following information:

| Column     | Description            |
|------------|------------------------|
| user_id    | User ID                |
| recipe_id  | Recipe ID              |
| date       | Date of interaction    |
| rating     | Rating given           |
| review     | Review text            |

**Question**: _What is the relationship between the cooking time and average rating of recipes?_

## Data Cleaning and Exploratory Data Analysis


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

## Hypothesis Testing

## Framing a Prediction Problem

## Baseline Model

## Final Model

## Fairness Analysis
