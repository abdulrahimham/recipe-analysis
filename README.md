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

## Bivariate Analysis

### Preparation Time vs. Average Rating

<iframe
  src="assets/preparation_time_vs_average_rating.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

This scatter plot shows the relationship between preparation time (in minutes) and average recipe rating. The data points are widely scattered, indicating no clear trend that longer or shorter preparation times significantly affect ratings. High ratings are distributed across various preparation times, suggesting that preparation time alone does not influence user ratings.

## Interesting Aggregates

### Grouped by Preparation Time

<iframe src="assets/grouped_by_time.html" width="800" height="200" frameborder="0"></iframe>

This table shows the average rating of recipes grouped by preparation time. By examining the average ratings for different preparation times, we can see that shorter preparation times (0-10 minutes) tend to have the highest average rating. However, there is not a dramatic difference in average ratings across different preparation time ranges, suggesting that preparation time alone might not be a significant factor influencing recipe ratings. This analysis can provide insights into user preferences, helping recipe creators and food bloggers to tailor their content. For instance, if recipes with shorter preparation times consistently receive slightly higher ratings, this might indicate a preference for quick and easy recipes among users.


### Grouped by Calories

<iframe src="assets/grouped_by_calories.html" width="800" height="200" frameborder="0"></iframe>

This table shows the average rating of recipes grouped by calorie content. By analyzing the average ratings for different calorie ranges, we observe that there is little variation in average ratings across different calorie ranges, indicating that calorie content may not significantly affect user ratings. However, the slightly higher average ratings for lower calorie recipes might suggest a preference for healthier recipes among some users. This analysis can help identify trends in user preferences regarding healthier versus more indulgent recipes, which can inform recipe development and content creation for health-conscious audiences. For example, if lower-calorie recipes tend to have slightly higher ratings, this might indicate a growing interest in healthy eating among users.

## Assessment of Missingness

### Permutation Test for Missingness Dependency

#### Preparation Time

<iframe
  src="assets/permutation_test_minutes.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

**Column: minutes**
- Observed Difference: 117.34
- P-value: 0.039

The permutation test for preparation time shows an observed difference of 117.34 minutes, with a p-value of 0.039. This suggests a statistically significant relationship between missing ratings and longer preparation times.

#### Calories

<iframe
  src="assets/permutation_test_calories.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

**Column: calories**
- Observed Difference: 87.86
- P-value: 0.0

The permutation test for calories shows an observed difference of 87.86, with a p-value of 0.0. This indicates a highly significant relationship between missing ratings and higher calorie content.



