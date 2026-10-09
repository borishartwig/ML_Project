# Machine Learning Project – Personality Types

*Boris Hartwig*  

## Abstract  
   
This project takes a Kaggle dataset from the so called **Big Five Personality Test** 

## Prerequisites

The data file should be stored in a subdirectory called "data" in a file called data.csv
It can be retrieved from: https://drive.google.com/drive/folders/1KhwTPAG07EdaENW_XX9nVvKhC-DP1Ags

Python files are in the repository https://github.com/borishartwig/ML_Project 

The *.joblib and requirements.txt are also in the repository.
The machine learning part is compare_models.py
The streamlit app is app.py 

(both only tested on Linux)

The streamlit App can also be found at https://mlproject-g5tqokqikfuq6faeutdhkk.streamlit.app/

## Data Cleaning
   
The Dataset contains 19,719 rows and 22 columns. Very little data is missing:
  
In the column **gender** 24 entries are missing; therefore we shall discard these for their small number.

In the column **hand**, 100 entries are missing; therefore we shall discard these for their small number.

In the age column, there appear birth years and some seemingly random large numbers. 
From Kaggle  info, we know that the dataset was created in 2008. We substract the year from the age entry. This leaves us with exactly 10 ages over 110 (assumed maximum age of a person), which we also discard.
 
The answers to the questions shall always be between 1 and 5, but there are a few scattered zeroes.
We discard these records as well and keep the remaining 19,599 records.

By using the correlation matrix heatmap from the seaborn library, we could confirm that no two columns have a correlation of more than 0.77. It seems therefore reasonable to keep them all of them as they are.

Note that as this point, we don't need to impute the data any further.

## Models and training

We use the usual 80/20 split for training and test data.
The models we are comparing are KNN, RandomForest and Logistic Regression according to F1-score with random search in the hyperparameter space (20 data points each).

# Model comparison (F1-score)

- Rows: 19527 (train: 15621, test: 3906)
- Classes: 4 -> F1 average: `weighted`
- Random search: 20 parameter sets per model, 5-fold CV

| Model | CV F1 (train) | Test F1 |
|---|---|---|
| KNeighborsClassifier | 0.8190 | 0.8101 |
| RandomForestClassifier | 0.8187 | 0.8158 |
| LogisticRegression | 0.8419 | 0.8373 |

## KNeighborsClassifier

- CV F1: **0.8190**
- Test F1: **0.8101**

| Hyperparameter | Value |
|---|---|
| n_neighbors | 12 |
| p | 2 |
| weights | distance |

## RandomForestClassifier

- CV F1: **0.8187**
- Test F1: **0.8158**

| Hyperparameter | Value |
|---|---|
| max_depth | 30 |
| max_features | sqrt |
| min_samples_leaf | 2 |
| min_samples_split | 5 |
| n_estimators | 188 |

## LogisticRegression

- CV F1: **0.8419**
- Test F1: **0.8373**

| Hyperparameter | Value |
|---|---|
| C | 4.5706 |
| class_weight | None |
| solver | lbfgs |

## Best model: **LogisticRegression**

CV F1 = 0.8419, Test F1 = 0.8373


The best model after parameter tuning was with distance Logistic Regression (F1 ca. 84%), which I found somewhat surprising as it is a rather simple model.

This is possibly due to the relatively small number of hyperparameter setting. 

However: In another run I first used XGBoost, which performed better than the other two models, but also not as good as LogisticRegression.
I could not get it to run in Streamlit, that why I switched to LogisticRegression. 

## The streamlit App 