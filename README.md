# Culinary Data Science Analysis

## Introduction

This project investigates the relationship between the preparation time of recipes and their user ratings. By analyzing data from Food.com, we aim to uncover whether quicker recipes tend to be rated as highly as those that take longer to prepare. This analysis is valuable for home cooks who want to optimize their time in the kitchen while still preparing highly rated dishes.

## Dataset Overview

The dataset contains information about recipes from Food.com, including details such as preparation time, nutritional information, and user ratings.

### Number of Rows
- Recipes dataset: 83,782
- Interactions dataset: 731,927

### Relevant Columns
- **id**: Unique identifier for each recipe.
- **minutes**: Preparation time for the recipe.
- **rating**: User ratings for the recipes (from interactions dataset).
- **name**: Name of the recipe.
- **nutrition**: Nutritional information for the recipe.

## Data Cleaning and Exploratory Data Analysis

### Data Cleaning

The data cleaning process involved several steps to ensure the data was in a usable format for analysis. The steps taken are detailed below:

1. **Replacing Zero Ratings with NaN**:
   - Ratings of 0 were replaced with NaN values to indicate missing data. This is because a rating of 0 does not provide any useful information and is likely a placeholder for missing ratings.

2. **Converting Nutrition Strings to Lists**:
   - The `nutrition` column in the recipes dataset contained nutritional information as strings. These strings were converted to lists to facilitate easier extraction and analysis of individual nutritional components.

3. **Creating New Columns from Nutrition Data**:
   - After converting the nutrition strings to lists, new columns were created for each nutritional component, including calories, total fat, sugar, sodium, protein, saturated fat, and carbohydrates. This allowed for more granular analysis of the nutritional content of recipes.

4. **Filtering Out Outliers in Preparation Time**:
   - Recipes with preparation times greater than 300 minutes were filtered out as outliers. These extreme values were likely data entry errors and could skew the analysis.

These data cleaning steps were crucial for ensuring the accuracy and reliability of subsequent analyses.

### Cleaned DataFrame Head

<iframe src="assets/cleaned_dataframe_head.html" width="100%" height="300" frameborder="0"></iframe>

## Univariate Analysis

### Distribution of Recipe Preparation Time

<iframe
  src="assets/preparation_time_distribution_filtered.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

This plot shows the distribution of preparation times for recipes. Most recipes have preparation times between 0 and 60 minutes, with a sharp decline in the number of recipes requiring more time.

### Distribution of Average Ratings

<iframe
  src="assets/average_rating_distribution.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

This plot displays the distribution of average ratings for recipes. The majority of recipes have ratings between 3.5 and 5, indicating that users generally rate recipes positively. Notably, a significant number of recipes have a perfect rating of 5, suggesting that users are quite satisfied with many of the recipes.

## Interesting Aggregates

### Grouped by Preparation Time

<iframe src="assets/grouped_by_time.html" width="800" height="200" frameborder="0"></iframe>

This table shows the average rating of recipes grouped by preparation time. By examining the average ratings for different preparation times, we can identify if there is a preference for quicker or longer recipes among users. This analysis is significant because it can provide insights into user preferences, helping recipe creators and food bloggers to tailor their content. For instance, if recipes with shorter preparation times consistently receive higher ratings, this might indicate that users prefer quick and easy recipes, which can guide future recipe development and marketing strategies.

### Grouped by Calories

<iframe src="assets/grouped_by_calories.html" width="800" height="200" frameborder="0"></iframe>

This table shows the average rating of recipes grouped by calorie content. By analyzing the average ratings for different calorie ranges, we can understand if there is a correlation between the healthiness of a recipe (as indicated by calorie content) and its popularity (as indicated by user ratings). This analysis is significant because it can help identify trends in user preferences regarding healthier versus more indulgent recipes. For example, if lower-calorie recipes tend to have higher ratings, this might suggest a growing interest in healthy eating among users, which can inform recipe development and content creation for health-conscious audiences.
