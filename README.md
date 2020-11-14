# Earthquake Fatality Prediction

Earthquakes impact thousands of people across the world each year, often causing many fatalities. There are many sources across the internet that contain data for what are considered "significant" earthquakes. The data used for this analysis was webscraped from three separate Wikipedia pages documenting earthquakes that satisfy the following criteria:

  - (1900-2000): Magnitude 6 or above, "unless they are notable for some other reason".
  - (2001-2020): Magnitude 7 or above, or which caused fatalities.
 
 
This analysis focuses on predicting whether or not an earthquake that can be classified as "significant" will cause fatalities based on the following factors: month of year, hour of day, magnitude, Latitude, and Longitude.

Data included in the analysis is a subset of the datasets from the Wikipedia pages described above, including only the past 40 years of data (1981 - 2020).

## Best Model and Model Performance
Various machine learning classification models were fit to train and test sets and then the predictive performance of each analyzed. Metrics used for performance evaluation were accuracy, f1 score, precision score, recall score, and AUC. In order to ensure optimal performance, optimal tuning parameters for the Gradient Boosting and Random Forest models were determined through sci-kit learn's GridSearchCV function. These optimal tuning parameters were applied when fitting the models, and the models were analyzed after being fit and used for prediction on the testing dataset. Between Naïve Bayes, Gradient Boosting, and Random Forest, the Random Forest model had the best overall predictive performance, with an AUC score of 0.968.

One useful piece of information we can obtain from the model is which feature is the most important in predicting whether or not a "significant" earthquake will result in any fatalities. From this Random Forest, we learn that the most important feature is (probably unsurprisingly) Magnitude.
