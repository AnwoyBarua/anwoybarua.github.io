---
title: '𝐈𝐦𝐩𝐨𝐫𝐭𝐚𝐧𝐭 𝐅𝐞𝐚𝐭𝐮𝐫𝐞 𝐒𝐞𝐥𝐞𝐜𝐭𝐢𝐨𝐧 𝐓𝐞𝐜𝐡𝐧𝐢𝐪𝐮𝐞𝐬'
date: 2024-06-25
permalink: /posts/2024/06/feature_selection/
excerpt: "This post dives into the filter based feature selection methods in Machine Learning."
tags:
  - ML
  - Feature Selection
---

In a Machine Learning problem, not all features may contribute to the final prediction. Sometimes, reducing the number of features can improve a model's performance or interpretability. Regardless of the reason, it's often beneficial to remove irrelevant or unwanted features.

Generally, 𝐭𝐡𝐫𝐞𝐞 methods are widely used for feature selection:
   - 𝐅𝐢𝐥𝐭𝐞𝐫 𝐛𝐚𝐬𝐞𝐝 𝐦𝐞𝐭𝐡𝐨𝐝𝐬
   - 𝐖𝐫𝐚𝐩𝐩𝐞𝐫 𝐦𝐞𝐭𝐡𝐨𝐝𝐬
   - 𝐄𝐦𝐛𝐞𝐝𝐝𝐞𝐝 𝐦𝐞𝐭𝐡𝐨𝐝𝐬
In today's post we will be going through the first one - 𝐅𝐢𝐥𝐭𝐞𝐫 𝐛𝐚𝐬𝐞𝐝 𝐦𝐞𝐭𝐡𝐨𝐝𝐬.
For python implementation of these methods visit my [kaggle notebook](https://www.kaggle.com/code/anwoybarua/all-feature-selection-techniques).

𝐅𝐢𝐥𝐭𝐞𝐫 𝐛𝐚𝐬𝐞𝐝 𝐦𝐞𝐭𝐡𝐨𝐝:
	It’s usually best to begin your feature selection using a univariate method, as these are easy to implement and time-efficient.

   1. 𝐃𝐞𝐥𝐞𝐭𝐢𝐧𝐠 𝐝𝐮𝐩𝐥𝐢𝐜𝐚𝐭𝐞 𝐜𝐨𝐥𝐮𝐦𝐧𝐬: Your dataset may contain duplicate columns, possibly with different column names. It’s always a good idea to identify and remove these duplicates.

   2. 𝐕𝐚𝐫𝐢𝐚𝐧𝐜𝐞 𝐓𝐡𝐫𝐞𝐬𝐡𝐨𝐥𝐝: Columns with zero or low variability usually contribute little to changes in the target variable (y). Thus, you may want to remove them. You can do this manually, or use the dedicated function in scikit-learn for this task. One major challenge with this method is selecting the right threshold. It often requires personal experience and trial and error to determine the optimal threshold for your data.

   3. 𝐂𝐨𝐫𝐫𝐞𝐥𝐚𝐭𝐢𝐨𝐧: The Pearson correlation coefficient is utilized to filter out features. Features with high correlation are considered to contribute equally to the final prediction, so it doesn’t hurt to remove one of them. 

   4. 𝐀𝐍𝐎𝐕𝐀: This method examines the relationship between each individual feature and the target variable (categorical). It determines the strength of the relationship using the p-value (from the F-statistic) for each feature, and retains the k best features. Scikit-learn provides a dedicated function called SelectKBest that can be used with f_classif or f_regression to select the k most important features. Finding the optimal value for k may require some trial and error or hyperparameter tuning.

   5. 𝐂𝐡𝐢-𝐬𝐪𝐮𝐚𝐫𝐞: The chi-square test can be used to study the dependency between categorical features and a categorical target variable, retaining those that show significant dependency.

While these filter-based methods are a good starting point for feature selection, they have some major flaws:
    - Being a univariate method, they don't consider the interaction between features and target variables.
    - There is a chance that we may delete features bearing low importance individually, but having significant impact when combined with other features.

On my next post I will be going through the wrapper method in details. 



