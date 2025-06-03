# A Data-Driven Approach to Estimating Calories in Recipes

## Introduction

The first dataset **RAW_recipes** contains 83,782 rows, indicating 83,782 recipes and 12 columns providing the following information:

| Column           | Description                                                                                                                                       |
|------------------|---------------------------------------------------------------------------------------------------------------------------------------------------|
| name             | Recipe name                                                                                                                                       |
| id               | Recipe ID                                                                                                                                        |
| minutes          | Minutes to prepare recipe                                                                                                                        |
| contributor_id   | User ID who submitted this recipe                                                                                                                |
| submitted        | Date recipe was submitted                                                                                                                        |
| tags             | Food.com tags for recipe                                                                                                                         |
| nutrition        | Nutrition information in the form [calories (#), total fat (PDV), sugar (PDV), sodium (PDV), protein (PDV), saturated fat (PDV), carbohydrates (PDV)]; PDV stands for “percentage of daily value” |
| n_steps          | Number of steps in recipe                                                                                                                        |
| steps            | Text for recipe steps, in order                                                                                                                  |
| description      | User-provided description                                                                                                                        |
| ingredients      | Text for recipe ingredients                                                                                                                      |
| n_ingredients    | Number of ingredients in recipe                                                                                                                  |

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

![Distribution of cooking time](images/distribution%20of%20cooking%20time.jpg)

![Distribution of average ratings](images/distribution%20of%20average%20ratings.jpg)

![Average rating vs cooking time](images/average%20rating%20vs%20cooking%20time.jpg)

![Average recipe rating by cooking time bins](images/average%20recipe%20rating%20by%20cooking%20time%20bins.jpg)

![Pivot table aggregate](images/pivot%20table%20aggregate.jpg)

## Assessment of Missingness

## Hypothesis Testing

## Framing a Prediction Problem

## Baseline Model

## Final Model

## Fairness Analysis
