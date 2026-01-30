# Netflix Movie Rating Prediction

## Overview
This project uses a regression-based approach to predict movie ratings using a subset of the Netflix Prize dataset. The objective is to estimate one missing rating per movie based on historical user–movie interactions. Multiple regression models were trained and evaluated to compare performance using Root Mean Squared Error (RMSE).

## Problem 
Recommender systems often rely on sparse user–item data, making accurate prediction challenging. This project explores whether simple, well-engineered features can effectively predict movie ratings and how different regression models perform under large-scale, sparse data constraints.

## Data
The original Netflix dataset was provided in a raw text format where each movie ID was followed by multiple user ratings. To enable analysis and modeling, the data was transformed into a structured DataFrame with the following columns:
- `movie_id`
- `user_id`
- `rating`
- `date`

After preprocessing, the dataset contained:
- 27,010,225 ratings  
- 5,000 unique movies  
- 462,542 unique users  

Exploratory analysis included visualizing rating distributions and the number of ratings per user.

## Train–Test Split
To construct the test set, one rating was randomly selected for each movie by grouping the data by `movie_id` and sampling a single rating per group. All remaining ratings were used for training. This ensured that every movie appeared in both the training and test sets while maintaining realistic sparsity.

## Feature Engineering
Due to the sparsity of the dataset, aggregate features were created to summarize historical behavior:
- Average rating given by each user
- Average rating received by each movie
- Count of ratings per user
- Count of ratings per movie

For users or movies appearing only in the test set, missing values were imputed using the global average rating. A `years_since_release` feature was created using movie metadata but was removed after analysis showed it had no variation.

## Modeling Approach
Three regression models were trained and evaluated using RMSE:

- **Linear Regression** served as a baseline model.
- **Ridge Regression** applied L2 regularization to reduce potential overfitting. Features were standardized prior to training.
- **Random Forest Regression** was used to capture potential non-linear relationships. To maintain feasible runtime on the large dataset, the model was constrained with a limited number of trees and shallow depth.

## Results

| Model               | RMSE  |
|--------------------|-------|
| Linear Regression  | 0.9910 |
| Ridge Regression   | 0.9910 |
| Random Forest      | 0.9971 |

Linear and ridge regression performed equally well and outperformed the Random Forest model. This suggests that the engineered aggregate features captured most of the predictive signal and that additional model complexity did not improve performance under the given constraints.

## Feature Importance Analysis
Feature importance scores from the Random Forest model showed that:
- `user_avg` and `movie_avg` were the most influential features
- Count-based features contributed relatively little to predictions

This indicates that a user’s typical rating behavior and a movie’s overall reception are the strongest predictors of individual ratings.

## Takeaways
- Simple aggregate features can be highly effective for rating prediction in sparse datasets.
- Linear models performed competitively and more efficiently than complex non-linear models.
- Model complexity does not guarantee improved performance, especially under scalability constraints.

## Tools
Python, Pandas, NumPy, scikit-learn, Matplotlib

