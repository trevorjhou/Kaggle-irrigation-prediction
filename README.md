# Kaggle Homework - Trevor Jhou - trevorjhou

## Competition: Predicting Irrigation Need 

## HW2-Baseline Models

1. URLs for the resources you upvoted on the competition site.  Discuss why you chose each--how will it help you improve your approach?

Answer:
Some useful Kaggle resources include:

- https://www.kaggle.com/competitions/playground-series-s6e4/discussion/687460  
  This discussion helped me understand the target structure and overall patterns in the dataset.

- https://www.kaggle.com/competitions/playground-series-s6e4/discussion/687104  
  This resource suggested strong baseline modeling approaches and common strategies used by others.

- https://www.kaggle.com/code/zaouiyassine/s6e4-baseline-submissions  
  This notebook showed a simple pipeline that I could use as a starting point and compare my results against.

These resources helped guide my modeling decisions and provided context for why relatively simple tree-based models performed well in this competition.

They also reinforced the importance of starting with a solid baseline before applying more advanced models. This guided my approach of using Random Forest and XGBoost for comparison.

Overall, these resources helped explain why both bagging and boosting methods achieved very similar performance in this project.

2. Links to your EDA notebook and bagging and boosting notebook(s).

Answer: 
https://www.kaggle.com/code/trevorjhou/ml-homework


3. What insights did you gain? Is there a feature you think is especially important? Any potential issues? Did you try anything new that you learned from Kaggle or other sources? Consider posting a public EDA notebook on Kaggle.

Answer: 
From the EDA, the dataset appears to be relatively clean and well-structured. There are no missing values, and the features include a mix of numerical and categorical variables.

One important observation is that the target variable `Irrigation_Need` is imbalanced, with the "Low" class appearing much more frequently than the "High" class. This influenced the decision to use macro F1 score as the evaluation metric instead of accuracy.

Several features, such as soil properties, rainfall, and temperature, are likely to be important predictors, as they are directly related to irrigation needs. Although a detailed feature importance analysis was not performed, these variables are intuitively relevant and are effectively handled by tree-based models.

A potential issue with the dataset is that it appears to be relatively simple or well-structured, which may limit the performance differences between models. This was observed in later modeling steps, where different models produced very similar results.

From Kaggle discussions, I learned that establishing a strong baseline model is important before applying more complex techniques. This guided the approach of starting with Random Forest and XGBoost, which already performed very well on this dataset.

4. Discuss your modeling approaches. What did you try? What worked well? What didn't work well? Were model improvements meaningful or small?
   Make sure to use performance metrics in your discussion. Also provide leaderboard scores for the models. A table might be useful for organizing the metrics and    leaderboard scores.

Answer: 
Two modeling approaches were explored in this project: Random Forest as the bagging model and XGBoost as the boosting model.

For both models, I preprocessed the data by removing the id column, encoding the target variable into numeric labels, and applying one-hot encoding to categorical features. During model development, I found that a target-derived column (target_encoded) had mistakenly remained in the dataset, which caused target leakage and unrealistically high validation scores. After removing that column, the evaluation results became more reliable.

To compare the two approaches fairly, I used 5-fold stratified cross-validation with balanced accuracy as the evaluation metric. Balanced accuracy was chosen because the target classes were somewhat imbalanced.

| Model         | Approach | CV Balanced Accuracy | Leaderboard Score |
| ------------- | -------- | -------------------: | ----------------: |
| Random Forest | Bagging  |               0.9553 |           0.95939 |
| XGBoost       | Boosting |               0.9617 |           0.95939 |


Both models performed strongly, but XGBoost slightly outperformed Random Forest in cross-validation. The improvement was meaningful but still relatively small (about 0.0064 in balanced accuracy), suggesting that boosting captured the data patterns somewhat better. However, both models achieved the same leaderboard score, which indicates that the practical difference in Kaggle performance was limited.

Overall, both approaches worked well. Random Forest provided a strong and stable baseline, while XGBoost produced the best validation result. The improvement from boosting was noticeable, but not dramatic.


5. How did boosting versus bagging compare for your work? 

Answer:

In this project, boosting performed slightly better than bagging.

Random Forest, representing bagging, achieved a cross-validated balanced accuracy of 0.9553, while XGBoost, representing boosting, achieved 0.9617. This shows that XGBoost provided a modest but consistent improvement over Random Forest during validation.

However, both models received the same Kaggle leaderboard score of 0.95939. This suggests that although boosting had the advantage in cross-validation, the difference did not translate into a noticeable leaderboard gain at this stage.

Overall, bagging and boosting were both effective, but boosting had a small edge in model performance.

6. What is your "phase 2" plan to improve your model performance? Note that although the leaderboard is fun to watch, you are not graded on it (and a shake up often occurs at the end!)

Answer:
To improve model performance in phase 2, I would focus on feature engineering, hyperparameter tuning, and testing additional boosting models.

First, I would explore interaction features among environmental and soil variables, such as combinations of temperature, rainfall, wind speed, and soil moisture. These may help the model capture more complex irrigation patterns.

Second, I would perform more systematic hyperparameter tuning, especially for XGBoost. Since XGBoost already performed slightly better, tuning parameters such as learning rate, tree depth, subsampling, and number of estimators may lead to additional gains.

Third, I would compare other strong boosting methods such as CatBoost or LightGBM under the same cross-validation framework.

Finally, I would review feature importance and remove redundant or weak variables to reduce noise and improve efficiency.

Overall, my phase 2 plan would focus on refining features and tuning the strongest model rather than simply increasing model complexity.


## HW3 - Additional Boosting Models

1. Links to your gradient boosting notebook(s).

LightGBM: https://www.kaggle.com/code/trevorjhou/homework-3-lightgbm

CatBoost: https://www.kaggle.com/code/trevorjhou/homework-3-catboost-set-3


3. Discuss your modeling approaches. What did you try? What worked well? What didn't work well? Were model improvements meaningful or small? Make sure to use performance metrics in your discussion. Also provide leaderboard scores for the models. A table might be useful for organizing the metrics and leaderboard scores.
How did the different models compare for your work?

Answer: 
Two boosting algorithms were explored in this project: LightGBM and CatBoost, each with multiple hyperparameter settings. All models were trained on one-hot encoded features, and performance was evaluated using 5-fold cross-validated balanced accuracy, which was chosen to account for class imbalance.

The following table summarizes the best results for each models:

| Model    | Hyperparameters         | CV Balanced Accuracy | Public Leaderboard Score | Private Leaderboard Score |
| -------- | ----------------------- | -------------------: | -----------------------: | ------------------------: |
| LightGBM | Set 3 - Simpler         |               0.9699 |                  0.96791 |                   0.97022 |
| CatBoost | Set 3 - Faster Learning |               0.9691 |                  0.96579 |                   0.96861 |

For LightGBM, the simpler configuration produced the best result, with a CV balanced accuracy of 0.9699, slightly outperforming both the baseline (0.9695) and the more complex version (0.9683). This suggests that increasing model complexity did not improve performance and may have slightly reduced generalization.

For CatBoost, the faster-learning configuration produced the best result, with a CV balanced accuracy of 0.9691. Compared with the baseline (0.9669) and the deeper-tree setting (0.9670), the improvement was still relatively small.

Overall, LightGBM performed better than CatBoost on this dataset. The improvements from hyperparameter tuning were modest rather than dramatic, suggesting that the dataset is already fairly structured and can be modeled effectively without extreme tuning.

3. How did the different models compare for your work?

Answer:

The two boosting models performed similarly overall, but LightGBM achieved the best validation result. Its best configuration reached a CV balanced accuracy of 0.9699, while the best CatBoost configuration reached 0.9691.

This indicates that LightGBM captured the patterns in the dataset slightly better, although the overall difference between the models was still small. Both boosting approaches were effective, and model choice had some impact on performance, but not a very large one.

The Kaggle leaderboard results showed the same pattern. LightGBM achieved a public score of 0.96791 and a private score of 0.97022, while CatBoost achieved a public score of 0.96579 and a private score of 0.96861. This suggests that LightGBM had a small but consistent advantage in both validation and competition performance.

Overall, the differences between the boosting models were limited, with LightGBM showing a small but consistent advantage.

## HW4: Feature Engineering, Selection, and Ensembling

### Notebook
- Kaggle Notebook: https://www.kaggle.com/code/trevorjhou/ml-homework

### Models Used
I experimented with several models that differ in meaningful ways:

- Random Forest (bagging)
- XGBoost (boosting)
- LightGBM (boosting)
- CatBoost (boosting)

These models represent different learning approaches and provide diversity for later ensembling.

### Feature Engineering
To improve feature representation, I created several interaction features:

- `moisture_x_temp` (Soil Moisture × Temperature)
- `rain_x_humidity` (Rainfall × Humidity)
- `sun_per_temp` (Sunlight / Temperature)
- `water_per_area` (Previous Irrigation / Field Area)

These features were designed to capture relationships between environmental variables that may influence irrigation needs.

### Feature Importance
Using tree-based models (XGBoost), I examined feature importance:

- Key original features include:
  - Crop growth stage
  - Soil moisture
  - Temperature
- Some engineered features also contributed, though their impact was smaller.

This suggests that the dataset is already informative, but interaction features can add minor improvements.

### Ensemble Method
I combined XGBoost, CatBoost, and LightGBM using probability averaging:

- Each model outputs class probabilities
- Final prediction is based on the average probabilities

The ensemble slightly improved macro F1 score compared to individual models.

### Results
- XGBoost (with engineered features): ~0.9690 (macro F1)
- Ensemble model: ~0.9691 (macro F1)

The improvement is small but consistent.

### Reflection
The improvements from feature engineering and ensembling were modest, indicating that the dataset is already well-structured and strong boosting models perform well.

However, this process helped refine my workflow:
- exploring feature interactions
- comparing multiple model types
- combining models to improve robustness

Overall, the assignment demonstrates how feature engineering and ensembling can be used to improve model performance and understanding.
