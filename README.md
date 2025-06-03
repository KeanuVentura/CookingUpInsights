# A Data-Driven Approach to Estimating Calories in Recipes

## Introduction

The first dataset **RAW_recipes** contains 83,782 rows, indicating 83,782 recipes and 12 columns providing the following information:

| Column         | Description                                                                                                       |
|----------------|-------------------------------------------------------------------------------------------------------------------|
| name           | Recipe name                                                                                                       |
| id             | Recipe ID                                                                                                         |
| minutes        | Minutes to prepare recipe                                                                                         |
| contributor_id | User ID who submitted this recipe                                                                                 |
| submitted      | Date recipe was submitted                                                                                         |
| tags           | Food.com tags for recipe                                                                                          |
| nutrition      | Nutrition info: calories, fat, sugar, sodium, protein, sat. fat, carbs (% daily value)                           |
| n_steps        | Number of steps in recipe                                                                                         |
| steps          | Text for recipe steps, in order                                                                                   |
| description    | User-provided description                                                                                         |
| ingredients    | Text for recipe ingredients                                                                                       |
| n_ingredients  | Number of ingredients in recipe                                                                                    |



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

<iframe 
  src="assets/cooking-time-distribution.html" 
  width="800" 
  height="600" 
  frameborder="0">
</iframe>

<iframe 
  src="assets/average_recipe_rating.html" 
  width="800" 
  height="600" 
  frameborder="0">
</iframe>



## Assessment of Missingness

## Hypothesis Testing

## Framing a Prediction Problem

## Baseline Model

## Final Model

## Fairness Analysis
