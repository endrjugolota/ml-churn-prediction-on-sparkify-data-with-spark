
# Churn prediction on sparkify dataset with PySpark

## Table of contents
* [General info](#general-info)
* [Technologies](#technologies)
* [Files](#files)
* [Summary of the results](#summary-of-the-results)

## General info

This repository contains code and data to create a churn prediction model with PySpark.

Data used in this project is the Sparkify dataset containing different users interactions with the music streaming service (like Spotify or Pandora). 
Interactions could be playing the song, logging out, giving the thumbs up etc. Source of this dataset is one of the [Udacity](https://www.udacity.com) courses on [Spark](https://learn.udacity.com/courses/ud2002).

Project consists of three parts:
1. Data Exploration and cleaning
2. Feature engineering
3. Modeling

The final result of the project is machine learning model for churn prediction.
Modeling part of the project contains code for building and training three different ml prediction models fromm which the one with the best performance is chosen and tuned.

## Technologies
* pyspark 3.5.0
* pandas 2.1.4
* datetime 4.3.0

## Files
* Data_Exploration_and_Cleaning.ipynb - jupyter notebook with code for exploration and cleaning of mini_sparkify_event_data.json dataset (input file: mini_sparkify_event_data.json, output file: mini_sparkify_event_data_cleaned.json)
* Feature Engineering.ipynb - jupyter notebook with code for feature engineering (input file: mini_sparkify_event_data_cleaned.json, output file: mini_sparkify_data_features.json)
* Modeling.ipynb - jupyter notebook with code for modeling including building models, evaluation and model tuning (input file: mini_sparkify_data_features.json)
* mini_sparkify_event_data.json - sparkify dataset containing users interactions with service
* mini_sparkify_event_data_cleaned.json - cleaned sparkify dataset containing users interactions with service
* mini_sparkify_data_features.json - sparkify users dataset with features and labels for training ml model
* README.md

## Summary of the results 

In the first part an exploratory analysis of the data was performed. The key results of this analysis were:
* Dataset consists of 286500 rows for 226 different users
* Dataset contains 18 fields, few of them identifying the user (userId, firstName, lastName, gender, location), other fields are connected to the activities of users (artist, auth, page etc.)
* Information about the type of activity is kept in "page" field
* One of the possible activities stored in "page" field is "Cancellation Confirmation", which can be used to identify users who cancelled their subscription
* There is one emptyt value for "userId"

After exploration of the dataset, cleaning was performed which included:
* Dropping empty values for "userId" and "sessionId" fields
* Changing format of timestamp column kept in "ts" field from epoch time to timestamp string

In the next part of the project cleaned dataset was aggregated to user level and features were calculated. 
Based on data exploration fallowing features were chosen:

* total time on a paid version
* time on a paid or free version
* number of songs played
* number of Thumbs Down
* number of Roll Advert
* number of Add to Playlist
* number of Add Friend
* number of Thumbs Up
* number of Errors

Aggregated dat with features was saved to mini_sparkify_data_features.json file.

After data preparation models 3 different models were created and validated. 

Fallowing models were trained:

### Random Forest Classifier:

Accuracy:  0.85,    Precision:  0.55,    Recall:  0.6,    F1 score:  0.57

### Logistic Regression:

Accuracy:  0.87,    Precision:  0.6,    Recall:  0.6,    F1 score:  0.6

### Stochastic Gradient Boosting:

Accuracy:  0.82,    Precision:  0.47,    Recall:  0.7,    F1 score:  0.56



Based on F1 score metrics Logistic Regression was chosed to be the winning model 
