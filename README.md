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

- EDA:https://www.kaggle.com/code/trevorjhou/ml-homework2

- Random Forest:https://www.kaggle.com/code/trevorjhou/hw2-bagging

- XGboost:https://www.kaggle.com/code/trevorjhou/hw2-boosting


3. What insights did you gain? Is there a feature you think is especially important? Any potential issues? Did you try anything new that you learned from Kaggle or other sources? Consider posting a public EDA notebook on Kaggle.

Answer: 
From the EDA, the dataset appears to be relatively clean and well-structured. There are no missing values, and the features include a mix of numerical and categorical variables.

One important observation is that the target variable `Irrigation_Need` is imbalanced, with the "Low" class appearing much more frequently than the "High" class. This influenced the decision to use balanced accuracy as the evaluation metric instead of plain accuracy.

Several features, such as soil properties, rainfall, and temperature, are likely to be important predictors, as they are directly related to irrigation needs. Although a detailed feature importance analysis was not performed, these variables are intuitively relevant and are effectively handled by tree-based models.

Overall, these resources helped explain why tree-based methods performed strongly in this project and why boosting ultimately showed a small but consistent advantage over bagging.

From Kaggle discussions, I learned that establishing a strong baseline model is important before applying more complex techniques. This guided the approach of starting with Random Forest and XGBoost, which already performed very well on this dataset.

4. Discuss your modeling approaches. What did you try? What worked well? What didn't work well? Were model improvements meaningful or small?
   Make sure to use performance metrics in your discussion. Also provide leaderboard scores for the models. A table might be useful for organizing the metrics and    leaderboard scores.

Answer: 
In this project, I evaluated two gradient boosting models—LightGBM and CatBoost—under multiple hyperparameter settings. All models were trained on one-hot encoded features and evaluated using 5-fold cross-validated balanced accuracy to account for class imbalance.

| Model         | Approach | CV Balanced Accuracy | Public Leaderboard Score | Private Leaderboard Score |
| ------------- | -------- | -------------------: | -----------------------: | ------------------------: |
| Random Forest | Bagging  |               0.9553 |                  0.95274 |                   0.95640 |
| XGBoost       | Boosting |               0.9617 |                  0.95987 |                   0.96122 |

What worked / didn’t:
For LightGBM, the simpler configuration performed best (CV 0.9699), slightly outperforming both the baseline (0.9695) and the more complex setting (0.9683). This indicates that increasing complexity (deeper trees / more leaves) did not yield gains and likely introduced mild overfitting, as additional capacity did not capture new signal in this dataset.

For CatBoost, the faster learning configuration performed best (CV 0.9691), but the gains over baseline (0.9669) and deeper trees (0.9670) were small. A higher learning rate can accelerate convergence, but does not guarantee better generalization, while deeper trees increase capacity but can lead to diminishing returns or overfitting.

Were improvements meaningful?
Across both models, tuning improvements were modest (on the order of ~0.001–0.003 in CV). The close alignment between CV and leaderboard scores suggests stable generalization, and that the baseline models were already strong. Further gains are unlikely to come from simply increasing model complexity.

Model comparison:
LightGBM slightly outperformed CatBoost on both CV and leaderboard metrics. A plausible reason is LightGBM’s leaf-wise growth, which can capture useful splits efficiently; however, it also increases overfitting risk—consistent with the observation that simpler settings worked best. CatBoost’s symmetric trees are more constrained and stable, which may explain its slightly lower but consistent performance.

Takeaway:
Overall, both boosting models were effective and performed similarly. The small performance gap suggests that model choice had limited impact on this dataset. Future improvements are more likely to come from feature engineering or adding model diversity (e.g., non-tree models) rather than further increasing boosting complexity.


5. How did boosting versus bagging compare for your work? 

Answer:

In this project, boosting performed better than bagging.

Random Forest, representing bagging, achieved a cross-validated balanced accuracy of 0.9553, while XGBoost, representing boosting, achieved 0.9617. This shows that XGBoost provided a modest but consistent improvement over Random Forest during validation.

The leaderboard results also supported this comparison. XGBoost achieved a public score of 0.95987 and a private score of 0.96122, while Random Forest achieved a public score of 0.95274 and a private score of 0.95640. This indicates that boosting generalized better than bagging on this dataset.

Overall, both bagging and boosting were effective, but boosting had a clear edge in performance.

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

The two boosting models performed similarly overall, but LightGBM achieved slightly better performance. This may be due to its leaf-wise tree growth strategy, which can capture complex patterns more efficiently compared to CatBoost’s symmetric tree structure.

However, increasing model complexity (e.g., deeper trees or more leaves) did not significantly improve performance for either model. This suggests that the dataset is relatively structured and does not require highly complex models, and that additional complexity may introduce overfitting without improving generalization.

The improvements from hyperparameter tuning were modest, indicating that the baseline models were already strong. Overall, while model choice had some impact, the differences were small, and further improvements may require feature engineering or model diversity rather than additional tuning.

## HW4: Feature Engineering, Selection, and Ensembling

### Notebook
- https://www.kaggle.com/code/trevorjhou/ml-homework-4-feature-engineering-and-stacking

### Models Used
I experimented with several boosting models that differ in meaningful ways:

- XGBoost
- LightGBM
- CatBoost

These models use different boosting strategies and provide useful diversity for comparing individual performance and for building an ensemble model.

### Feature Engineering
I created several interaction features, including:
- moisture_x_temp
- rain_x_humidity
- sun_per_temp
- water_per_area
  
These features were designed to capture relationships between environmental factors that may influence irrigation needs.

Using XGBoost, the model with engineered features achieved a macro F1 score of about 0.9690, which suggests that the added interaction terms provided a small improvement in predictive performance.

### Feature Selection

To evaluate which features were most useful, I examined the feature importance rankings from the XGBoost model after feature engineering. The results showed that the strongest predictors were still the original variables, especially crop growth stage, soil moisture, temperature, wind speed, and rainfall. The engineered interaction features did not appear among the top-ranked variables, suggesting that their contribution was more limited.

Based on this analysis, I did not remove features aggressively, because the full engineered feature set still produced strong validation performance. Instead, I used feature importance mainly as a way to understand which variables mattered most and to assess whether the engineered features were adding meaningful information.

### Feature Importance
The feature importance results show that the most influential predictors were still the original variables rather than the engineered interaction terms.

| Rank | Feature                      | Importance |
| ---- | ---------------------------- | ---------: |
| 1    | Crop_Growth_Stage_Vegetative |   0.269943 |
| 2    | Crop_Growth_Stage_Flowering  |   0.202744 |
| 3    | Mulching_Used_No             |   0.115180 |
| 4    | Crop_Growth_Stage_Harvest    |   0.110424 |
| 5    | Soil_Moisture                |   0.083196 |
| 6    | Crop_Growth_Stage_Sowing     |   0.080900 |
| 7    | Temperature_C                |   0.049739 |
| 8    | Wind_Speed_kmh               |   0.043014 |
| 9    | Rainfall_mm                  |   0.015204 |
| 10   | Water_Source_Reservoir       |   0.001311 |



### Ensemble Method
I combined XGBoost, CatBoost, and LightGBM using probability averaging. The ensemble achieved a macro F1 score of about 0.9689.

This indicates that combining multiple boosting models can produce strong performance, although the improvement over the best individual model was relatively small.

### Results
- XGBoost (with engineered features): about 0.9690 (macro F1)
- Ensemble model: about 0.9689 (macro F1)
- Ensemble Kaggle leaderboard score: 0.96026 (public), 0.96223 (private)

Both approaches performed very well in validation, but the ensemble did not meaningfully outperform the single XGBoost model. The Kaggle leaderboard scores also suggest that the gains from ensembling were limited in practice.

### Reflection
Overall, the improvements from feature engineering and ensembling were modest rather than dramatic. This suggests that the dataset is already fairly well-structured and that strong boosting models can perform well even without extensive additional feature construction.

However, the process demonstrates how feature engineering and ensemble methods can still be used to refine model performance and strengthen a machine learning workflow.
