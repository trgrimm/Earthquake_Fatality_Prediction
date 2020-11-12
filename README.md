# Earthquake Fatality Prediction

Earthquakes impact thousands of people across the world each year, often causing many fatalities. There are many sources across the internet that contain data for what are considered "significant" earthquakes. The data used for this analysis was webscraped from three separate Wikipedia pages documenting earthquakes that satisfy the following criteria:
  Magnitude 6 or above (1900-2000), "unless they are notable for some other reason".
  Magnitude 7 or above (2001-2020) or which caused fatalities.
 
 
This analysis focuses on predicting whether or not an earthquake that can be classified as "significant" will cause fatalities based on the following factors: month of year, hour of day, magnitude, Latitude, and Longitude.

Various machine learning classification models were fit to train and test sets and then the predictive performance of each analyzed. Between Naïve Bayes, Gradient Boosting, and Random Forest, the Random Forest model performed the best.
