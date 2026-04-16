# Kaggle Homework - Trevor Jhou - trevorjhou

1. URLs for the resources you upvoted on the competition site.  Discuss why you chose each--how will it help you improve your approach?

Answer:
Some useful Kaggle resources include:

- https://www.kaggle.com/competitions/playground-series-s6e4/discussion/687460  
- https://www.kaggle.com/competitions/playground-series-s6e4/discussion/687104  
- https://www.kaggle.com/code/zaouiyassine/s6e4-baseline-submissions  

These resources provided valuable insights into the dataset and modeling strategies. In particular, they highlighted that the dataset may contain strong underlying patterns, 
which helps explain why tree-based models perform very well.

They also emphasized the importance of starting with a solid baseline before applying more advanced models. This guided the approach of using Random Forest and XGBoost for comparison.

Overall, these resources helped explain why both bagging and boosting methods achieved very similar performance in this project.


2. Links to your EDA notebook and bagging and boosting notebook(s).

Answer: https://www.kaggle.com/code/trevorjhou/notebook126e22d6c5?scriptVersionId=311967971


3. Discuss your modeling approaches. What did you try? What worked well? What didn't work well? Were model improvements meaningful or small?
   Make sure to use performance metrics in your discussion. Also provide leaderboard scores for the models. A table might be useful for organizing the metrics and leaderboard scores.

Answer: 
Two modeling approaches were explored in this project: Random Forest (bagging) and XGBoost (boosting).

For the bagging approach, a Random Forest model was used, while XGBoost was used for the boosting approach. Both models were trained on the dataset after preprocessing, 
including one-hot encoding of categorical variables.

The performance of the models was evaluated using macro F1 score due to class imbalance in the target variable.

| Model        | Approach | CV F1 Score | Leaderboard Score |
|--------------|----------|-------------|-------------------|
| RandomForest | Bagging  | 0.966       | 0.95939           |
| XGBoost      | Boosting | 0.969       | 0.95939           |

Both models were trained on the dataset after preprocessing, including one-hot encoding of categorical variables. Default model settings were used, with minimal tuning applied.
The results suggest that both bagging and boosting methods are effective for this dataset. The lack of significant improvement from boosting indicates that the dataset may already be well-structured, 
allowing Random Forest to capture most of the underlying patterns.

Overall, model improvements were small, and no substantial performance gain was observed between the two approaches.


4. How did boosting versus bagging compare for your work? 

Answer:

In this project, both bagging (Random Forest) and boosting (XGBoost) performed very similarly. 

XGBoost achieved a slightly higher F1 score during cross-validation, but on the Kaggle leaderboard both models obtained the same score of 0.95939. 
This suggests that the performance difference between the two approaches was minimal.

While boosting is generally expected to outperform bagging by sequentially correcting errors, in this case the dataset appears to be relatively well-structured, 
allowing Random Forest to already capture most of the important patterns.

Overall, boosting did not provide a significant improvement over bagging for this task, and both approaches were equally effective.
