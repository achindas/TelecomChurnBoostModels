# Telecom Churn Case Study - Decision Tree Based Boosting Models

## Table of Contents
* [Boosting Models Overview](#boosting-models-overview)
* [Problem Statement](#problem-statement)
* [Technologies Used](#technologies-used)
* [Approach for Modeling](#approach-for-modeling)
* [Classification Outcome](#classification-outcome)
* [Conclusion](#conclusion)
* [Acknowledgements](#acknowledgements)

## Boosting Models Overview

Boosting is an ensemble learning technique that aims to combine the predictions of several weak learners (typically decision trees) to create a strong learner. The central idea is to sequentially train models, with each subsequent model focusing on correcting the errors made by the previous ones. Boosting algorithms assign higher weights to misclassified instances to ensure that subsequent models pay more attention to them.

### AdaBoost

Adaptive Boosting (AdaBoost) is one of the most popular boosting algorithms. It works by training weak classifiers iteratively, with each classifier improving upon the mistakes of the previous ones. The key steps in AdaBoost are as follows:

1. Assign equal weights to all training samples initially.
2. Train a weak learner on the weighted data and calculate the weighted error.
3. Update the weights of the samples: increase the weights of misclassified samples and decrease the weights of correctly classified ones.
4. Combine the weak learners to form the final strong model, with each weak learner’s contribution weighted by its accuracy.

AdaBoost is widely used for binary classification problems and is known for its simplicity and effectiveness.

### Gradient Boosting

Gradient Boosting is a more generalized and powerful form of boosting that minimizes the loss function of the model by adding weak learners sequentially. Unlike AdaBoost, which focuses on reweighting samples, Gradient Boosting builds models by optimizing the residual errors (gradients) of the loss function. The key steps in Gradient Boosting are:

1. Fit a weak learner to the data and calculate the residual errors (the difference between the actual and predicted values).
2. Train subsequent weak learners to predict the residuals and iteratively improve the model's performance.
3. Combine the weak learners to form a strong model, minimizing the overall loss function.

Gradient Boosting is highly flexible and can handle both regression and classification problems. Popular implementations, such as XGBoost, LightGBM, and CatBoost, incorporate advanced features like regularization, parallelism, and efficient handling of missing data, making Gradient Boosting a preferred choice for many machine learning tasks.

Boosting models, including AdaBoost and Gradient Boosting, are highly effective in handling complex datasets and achieving state-of-the-art results in both classification and regression tasks.

 The approach described here represent the practical process utilised in industry to predict categorical or numeric target parameters for business.


## Problem Statement

In the telecom industry, customers are able to choose from multiple service providers and actively switch from one operator to another. In this highly competitive market, the telecommunications industry experiences **an average of 15-25% annual churn rate**. Given the fact that it costs 5-10 times more to acquire a new customer than to retain an existing one, customer retention has now become even more important than customer acquisition.

For many incumbent operators, **retaining high profitable customers is the number one business goal**. To reduce customer churn, telecom companies need to predict which customers are at high risk of churn. In this project, we will analyze customer-level data of a leading telecom firm, build predictive models to identify customers at high risk of churn, and identify the main indicators of churn.

In this case study, our goal is to build a machine learning model, using primarily `decision tree based Boosting models`, that is able to predict churning customers based on the features provided for their usage.

## Technologies Used

Python Jypyter Notebook in local PC environment has been used for the exercise. Apart from ususal Python libraries like  Numpy and Pandas, there are machine Learning specific libraries used to prepare, analyse, build model and visualise data. The following model specific libraries have been used in the case study:

- sklearn
- imblearn


## Approach for Modeling

The following steps are followed to build the various models for Telecom Churn analysis:

1. Import & Understand Data
2. Clean & Transform Data
3. Perform Exploratory Data Analysis
4. Perform Feature Engineering
5. Preprare Data for Modeling
6. Build and Evaluate Models
7. Select Model and Make Predictions
8. Conclusion

Some distinguishing processes in this approach include,

- Trimming of the input parameters by analysing the dependencies among the parameters and drop those parameters which are covered in aggregated parameters

- Resetting the `outlier values` in numeric parameters to $\pm 3\sigma$ of the parameter values

- Filling the missing values with zeros using `SimpleImputer` function for numeric parameters and with `modes` for categorical parameters

- Performing `feature engineering` by combining different parameters to identify useful derived features that can be used for modeling

- Addressing data imbalance of churned customers by using `SMOTE` function to augment observations for churning customers

- Tuning of model hyper-parameters using `GridSearchCV` method by feeding the hyper-parameters through params grid.

- Determination of most important feature variables through feature importance parameter of ensemble models


## Classification Outcome

As part of this exercise, we have created following Classifier models to arrive at a suitable model to predict churn among telecom customers:
- Random Forest
- Bagging Classifier
- Adaptive Boost
- Gradient Boost
- Logistic Regression

Target metric used for model selection was primarily **Recall** score. For telecom industry, customer retention is very important and hence the model should accurately predict all potentially churning customers even if that means some non-churning customers are also tagged as churning customer. Hence the focus of the model was to reduce false negatives (miss classification of the churn customers) as much as possible. **A high Recall score indicates less false negative** and hence the most appropriate metric for the problem at hand. 

Among the above models, the one that gives better consistent result is **Gradient Boosting** ensemble model. We achieved a high model `accuracy of greater than 90%` with a precision of over 75% and `recall score of close to 65%`. This model is more consistent with training and test dataset. Even though the Logistic regression model, after addressing the imbalance in the dataset, improved the Recall score, but there was significant disparity between the precision and recall values. Hence, we selected the Gradient Boost model over Logistic Regression keeping the long-term stability of the model in mind.


## Conclusion

Gradient Boosting is an effective machine learning algorithm that works well in **classification** tasks by iteratively improving model performance. It combines the strengths of multiple weak learners, typically decision trees, to create a strong predictive model. Its ability to handle **imbalanced datasets, incorporate feature importance** for interpretability, and achieve high accuracy makes it particularly useful for classification problems, such as predicting customer churn, disease diagnosis, or fraud detection.


## Acknowledgements

This case study has been developed as part of Post Graduate Diploma Program on Machine Learning and AI, offered jointly by Indian Institute of Information Technology, Bangalore (IIIT-B) and upGrad.