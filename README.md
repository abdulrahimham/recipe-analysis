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

### Univariate Analysis

#### Distribution of Recipe Preparation Time

<iframe
  src="assets/preparation_time_distribution_filtered.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

This plot shows the distribution of preparation times for recipes. Most recipes have preparation times between 0 and 60 minutes, with a sharp decline in the number of recipes requiring more time.

#### Distribution of Average Ratings

<iframe
  src="assets/average_rating_distribution.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

This plot displays the distribution of average ratings for recipes. The majority of recipes have ratings between 3.5 and 5, indicating that users generally rate recipes positively. Notably, a significant number of recipes have a perfect rating of 5, suggesting that users are quite satisfied with many of the recipes.

### Bivariate Analysis

#### Preparation Time vs. Average Rating

<iframe
  src="assets/preparation_time_vs_average_rating.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

This scatter plot shows the relationship between preparation time (in minutes) and average recipe rating. The data points are widely scattered, indicating no clear trend that longer or shorter preparation times significantly affect ratings. High ratings are distributed across various preparation times, suggesting that preparation time alone does not influence user ratings.

### Interesting Aggregates

#### Grouped by Preparation Time

<iframe src="assets/time_rating.html" width="800" height="200" frameborder="0"></iframe>

This table shows the average rating of recipes grouped by preparation time. By examining the average ratings for different preparation times, we can see that shorter preparation times (0-10 minutes) tend to have the highest average rating. However, there is not a dramatic difference in average ratings across different preparation time ranges, suggesting that preparation time alone might not be a significant factor influencing recipe ratings. This analysis can provide insights into user preferences, helping recipe creators and food bloggers to tailor their content. For instance, if recipes with shorter preparation times consistently receive slightly higher ratings, this might indicate a preference for quick and easy recipes among users.


#### Grouped by Calories

<iframe src="assets/calorie_rating.html" width="800" height="200" frameborder="0"></iframe>

This table shows the average rating of recipes grouped by calorie content. By analyzing the average ratings for different calorie ranges, we observe that there is little variation in average ratings across different calorie ranges, indicating that calorie content may not significantly affect user ratings. However, the slightly higher average ratings for lower calorie recipes might suggest a preference for healthier recipes among some users. This analysis can help identify trends in user preferences regarding healthier versus more indulgent recipes, which can inform recipe development and content creation for health-conscious audiences. For example, if lower-calorie recipes tend to have slightly higher ratings, this might indicate a growing interest in healthy eating among users.

## Assessment of Missingness

### NMAR Analysis

In our dataset, we need to determine if there are any columns for which the missing data is likely Not Missing At Random (NMAR). After examining the data generating process, I believe the `average_rating` column may be NMAR. The reasoning behind this is that users might not rate a recipe if they found it extremely dissatisfactory or if they did not prepare it at all. To further investigate this, additional data such as user feedback or reasons for not rating could be collected. This would help explain the missingness and potentially reclassify it as Missing At Random (MAR).

To potentially reclassify this missingness as MAR (Missing At Random), we would need additional data to explain why some recipes have missing ratings. This additional data could include:
- **Recipe Visibility Data**: Information on how often a recipe is viewed by users.
- **Recipe Complexity Data**: Data on the number of steps or the complexity of ingredients.
- **User Interaction Data**: Data on user engagement, such as the number of users who bookmarked the recipe but did not rate it.
- **Marketing and Promotion Data**: Information on whether the recipe was featured or promoted on the platform.

By analyzing this additional data, we could better understand the reasons behind the missing ratings and potentially explain the missingness through observed data, thus making it MAR.

### Missing Dependency

To analyze the dependency of the missingness of `average_rating` on other columns, I performed permutation tests. Specifically, I looked at the dependency on `minutes` (preparation time) and `calories`.

### Permutation Test for Missingness Dependency

#### Preparation Time

<iframe src="assets/permutation_test_preparation_time.html" width="800" height="600" frameborder="0"></iframe>


**Column: minutes**
- Observed Difference: -70.0318
- P-value: 0.394

The permutation test for preparation time shows a high p-value (0.0394), indicating that there is no significant difference in preparation times between recipes with missing and non-missing ratings.


#### Calories

<iframe src="assets/permutation_test_calories.html" width="800" height="600" frameborder="0"></iframe>


**Column: calories**
- Observed Difference: 456.9785
- P-value: 0.079

The permutation test for calories shows a p-value (0.079), which is closer to the significance threshold. This suggests a potential association between calorie content and missing ratings, but it is not statistically significant at the conventional 0.05 level.

These results indicate that the missingness of `average_rating` might be influenced by factors other than `minutes` and `calories`. Further investigation into other potential factors or collecting additional data could provide more insights.

## Hypothesis Testing

### Hypothesis:
- **Null Hypothesis (H0):** The average rating of a recipe does not depend on the number of ingredients.
- **Alternative Hypothesis (H1):** The average rating of a recipe depends on the number of ingredients.

We want to investigate if the complexity or simplicity of a recipe (measured by the number of ingredients) affects how well it is rated by users. This information could be useful for recipe creators to understand if simpler or more complex recipes tend to be rated higher by users.

### Test Statistic and Significance Level:
- **Test Statistic:** The difference in means of average ratings between recipes with a low and high number of ingredients.
- **Significance Level:** 0.05

The difference in means is a straightforward and interpretable measure of the effect size, allowing us to see if there is a meaningful difference in ratings based on the number of ingredients. The significance level of 0.05 is a standard threshold in statistical hypothesis testing, balancing the risk of Type I and Type II errors.

### Method:
- A permutation test was conducted to determine if the average rating of a recipe depends on the number of ingredients.
- The dataset was split into two groups: recipes with a low number of ingredients and recipes with a high number of ingredients, using the median number of ingredients as the threshold.

<iframe
  src="assets/permutation_test_ingredients.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

### Results:
- **Observed Difference:** 0.0247
- **P-value:** 0.001

Given the p-value of 0.001, which is less than our chosen significance level of 0.05, we reject the null hypothesis. This indicates that there is a significant difference in the average ratings of recipes based on the number of ingredients. Recipes with different numbers of ingredients tend to receive different average ratings. Understanding this relationship can help recipe developers tailor their recipes to achieve higher ratings, either by simplifying or adding complexity to match user preferences.

## Framing a Prediction Problem

### Prediction Problem

The prediction problem we are addressing is predicting the average rating of a recipe based on its characteristics. This is a regression problem because we are predicting a continuous variable (average rating).

### Response Variable

The response variable is `average_rating`. We chose this variable because the rating of a recipe is a critical measure of its success and user satisfaction. Predicting the rating can help in understanding what factors contribute to higher-rated recipes.

### Evaluation Metric

We are using the Mean Absolute Error (MAE) to evaluate our model. The MAE measures the average magnitude of errors in a set of predictions, without considering their direction. It is a straightforward metric that provides a clear indication of the prediction accuracy of our model. We chose MAE over other metrics like RMSE because it is more interpretable and less sensitive to outliers.

### Justification

At the time of prediction, we would know the features of the recipes such as the number of ingredients, preparation time, and nutritional information. Using these features to predict the average rating is reasonable and ensures that we are not using any future information in our model.

### Features Used

- `minutes`: The preparation time of the recipe.
- `n_ingredients`: The number of ingredients used in the recipe.
- `calories`: The calorie content of the recipe.
- `total_fat`: The total fat content of the recipe.
- `sugar`: The sugar content of the recipe.
- `sodium`: The sodium content of the recipe.
- `protein`: The protein content of the recipe.
- `saturated_fat`: The saturated fat content of the recipe.
- `carbohydrates`: The carbohydrate content of the recipe.

These features are relevant because they provide a comprehensive view of the recipe's characteristics, which can influence user ratings.

### Model Training and Evaluation

We trained a RandomForestRegressor model using the features mentioned above. The model was evaluated using the Mean Absolute Error (MAE) on a test set. This evaluation helps us understand how well the model predicts the average rating of unseen recipes.

### Model Performance

Mean Absolute Error: 0.4781631198009695

<iframe
  src="assets/prediction_error_distribution.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

## Baseline Model

### Model Description

For the baseline model, I used a simple linear regression model with standard scaling for feature normalization. The features included in this model were:

1. **Preparation Time (`minutes`)**: This quantitative feature represents the time required to prepare a recipe.
2. **Number of Ingredients (`n_ingredients`)**: This quantitative feature represents the total number of ingredients used in a recipe.

These features were selected because they are directly related to the complexity and effort required to prepare a recipe, which are likely to influence user ratings.

### Feature Encoding

Both features in the baseline model are quantitative and did not require any special encoding. However, standard scaling was applied to normalize the feature values, ensuring that the model treats each feature equally regardless of its scale.

### Model Performance

The baseline model's performance was evaluated using the mean absolute error (MAE) on the test dataset:

- **Mean Absolute Error**: 0.757

This value indicates the average magnitude of errors in the model's predictions, with a lower value representing better performance. Although the baseline model provides a starting point for our predictions, it is relatively simple and may not capture more complex relationships in the data.

<iframe src="assets/baseline_model_errors.html" width="800" height="600" frameborder="0"></iframe>

The histogram above shows the distribution of prediction errors for the baseline model. The majority of errors are centered around zero, indicating that the model's predictions are reasonably accurate. However, there is a spread of errors, suggesting that there is room for improvement.

By starting with this baseline model, we have a benchmark to compare against as we explore more sophisticated modeling techniques and feature engineering in the next steps.


## Final Model

### Model Description
For the final model, I aimed to improve the baseline model by engineering new features and tuning hyperparameters. I used a RandomForestRegressor due to its ability to handle non-linear relationships and interactions between features.

### Features Added
1. **Log of Preparation Time (`log_minutes`)**: The logarithm of preparation time was used to handle the skewness in the distribution of preparation times and to capture non-linear relationships.
2. **Interaction between Preparation Time and Number of Ingredients (`interaction`)**: This feature captures the combined effect of preparation time and number of ingredients, which may impact the complexity and perceived quality of a recipe.

These features were added because they provide additional insights into the data. The log transformation helps normalize the distribution of preparation times, and the interaction term captures the combined effect of preparation time and the number of ingredients, which may influence user ratings.

### Feature Encoding
All features in the final model are quantitative. Standard scaling was applied to normalize the feature values, ensuring that the model treats each feature equally regardless of its scale.

### Hyperparameter Tuning
The following hyperparameters were tuned using GridSearchCV:
- **Number of Estimators (n_estimators)**: The number of trees in the forest. Options: [50, 100, 200]
- **Maximum Depth (max_depth)**: The maximum depth of the trees. Options: [None, 10, 20, 30]

The best hyperparameters found were:
- **max_depth**: 10
- **n_estimators**: 100

#### Model Performance Comparison

The performance of the final model was evaluated using the mean absolute error (MAE), which measures the average magnitude of the errors in predictions without considering their direction. The final model's performance was compared to the baseline model:

- **Baseline Model MAE**: 0.757
- **Final Model MAE**: 0.755

Although the improvement in MAE is marginal, the final model demonstrates a slightly better ability to generalize to unseen data compared to the baseline model. This improvement can be attributed to the additional engineered features that allowed the model to capture more intricate patterns in the data.


<iframe src="assets/final_model_errors.html" width="800" height="600" frameborder="0"></iframe>

This histogram shows the distribution of prediction errors for the final model. Most of the errors are concentrated around zero, indicating that the model's predictions are close to the actual ratings. The plot provides a visual representation of the model's accuracy and the spread of prediction errors.

By implementing these steps, the final model has shown an improvement over the baseline model, demonstrating the effectiveness of feature engineering and hyperparameter tuning in enhancing model performance.

## Fairness Analysis

### Group 1 and Group 2
For our fairness analysis, we chose to compare the model's performance between two groups:
- **Group 1**: Recipes with a low number of ingredients (below the median).
- **Group 2**: Recipes with a high number of ingredients (above the median).

### Evaluation Metric
We use the Mean Absolute Error (MAE) to evaluate our model's fairness. The MAE measures the average magnitude of errors in the model's predictions, providing a clear indication of prediction accuracy.

### Hypotheses
- **Null Hypothesis (H0)**: The model is fair. The MAE for recipes with a low number of ingredients and a high number of ingredients are roughly the same, and any differences are due to random chance.
- **Alternative Hypothesis (H1)**: The model is unfair. The MAE for recipes with a low number of ingredients is higher than the MAE for recipes with a high number of ingredients.

### Test Statistic and Significance Level
- **Test Statistic**: The difference in MAE between recipes with a low number of ingredients and a high number of ingredients.
- **Significance Level**: 0.05

### Results
- **Observed Difference**: 0.00385
- **P-value**: 0.39

Given the p-value of 0.39, which is greater than our chosen significance level of 0.05, we fail to reject the null hypothesis. This indicates that there is no significant difference in the MAE between recipes with a low number of ingredients and those with a high number of ingredients. Therefore, we conclude that our model performs fairly between these two groups.

<iframe src="assets/fairness_analysis.html" width="800" height="600" frameborder="0"></iframe>

The histogram above shows the distribution of the differences in MAE obtained from the permutation test. The red dashed line represents the observed difference. The majority of permutation differences are centered around zero, suggesting that any observed difference in MAE between the two groups is likely due to random chance.
