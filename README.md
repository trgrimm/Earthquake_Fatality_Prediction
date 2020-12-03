# Earthquake Fatality Prediction

Earthquakes impact thousands of people across the world each year, often causing many fatalities. There are many sources across the internet that contain data for what are considered "significant" earthquakes. The data used for this analysis was webscraped from three separate Wikipedia pages documenting earthquakes that satisfy the following criteria:

  - (1900-2000): Magnitude 6 or above, "unless they are notable for some other reason".
  - (2001-2020): Magnitude 7 or above, or which caused fatalities.
 
 
This analysis focuses on the following prediction question: Can we predict whether or not an earthquake that can be classified as "significant" will cause fatalities based on the factors of month of year, hour of day, magnitude, Latitude, and Longitude?

Data included in the analysis is a subset of the datasets from the Wikipedia pages described above, including only the past 40 years of data (1981 - 2020). Due to the nature of the dataset and the prediction question of interest, various Machine Learning classification methods were used. These models include Naïve Bayes, Gradient Boosting, and Random Forest.

## Data Collection

Basic webscraping using the the `pandas.read_html` function was used to scrape the data from 3 Wikipedia webpages.

```python
url1 = "https://en.wikipedia.org/wiki/Lists_of_20th-century_earthquakes"
url2 = "https://en.wikipedia.org/wiki/List_of_earthquakes_2001%E2%80%932010"
url3 = "https://en.wikipedia.org/wiki/List_of_earthquakes_2011%E2%80%932020"

earthquakes_1 = pd.read_html(url1)
earthquakes_2 = pd.read_html(url2)
earthquakes_3 = pd.read_html(url3)
```
The data obtained from each of these webpages came in the form of various tables, so I went through and selected the tables that contained the data I wanted. I then combined all of the tables I wanted into a single dataframe and performed further data cleaning and feature  

## Best Model and Model Performance
Various machine learning classification models were fit to train and test sets and then the predictive performance of each model was analyzed. Metrics that were used for performance evaluation are accuracy, f1 score, precision score, recall score, and AUC. In order to ensure optimal performance, optimal tuning parameters for the Gradient Boosting and Random Forest models were determined through the usage of scikit-learn's GridSearchCV function. These optimal tuning parameters were applied when fitting the models, and the models were analyzed after being fit and used for prediction on the testing dataset.

Between Naïve Bayes, Gradient Boosting, and Random Forest, the Random Forest Classifier model had the best overall predictive performance, with an AUC score of 0.968 and an f1 score of 0.937. The second best performing model was the Gradient Boosting Classifier, which had an AUC score of 0.962 and an f1 score of 0.928. These models had quite similar performance, but they were both far superior to the Naïve Bayes model. For the Random Forest model, out of 120 earthquakes that caused fatalities in the testing set, only 8 were misclassified as not causing fatalities. Out of the 35 earthquakes that didn't cause fatalities, only 7 were misclassified as causing fatalities. This is more impressive than the Naïve Bayes' 15 and 8 respective missclassifications and Gradient Boosting's 11 and 6.

One useful piece of information we can obtain from the model is which features are the most important in predicting whether or not a "significant" earthquake will result in any fatalities. From the Random Forest Classifier model, we learn that the most important feature in this case is (unsurprisingly) Magnitude. The next most important features in order are Longitude, Latitude, Hour, and Month.

