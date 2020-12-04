# Earthquake Fatality Prediction

## Introduction
Earthquakes impact thousands of people across the world each year, often causing many fatalities. As such, it is useful to explore some questions that may be answered through various machine learning models to help us better understand and predict the effects of earthquakes. Therefore, this analysis focuses on the following prediction question: 
Can we predict whether or not an earthquake that can be classified as "significant" will cause fatalities based on the factors of month of year, hour of day, magnitude, latitude, and longitude?

There are many sources across the internet that contain data for what are considered "significant" earthquakes. The data used for this analysis was webscraped from three separate Wikipedia pages documenting earthquakes that satisfy the following criteria:

  - (1900-2000): Magnitude 6 or above, "unless they are notable for some other reason".
  - (2001-2020): Magnitude 7 or above, or which caused fatalities.

Data included in the analysis is a subset of the datasets from the Wikipedia pages described above, including only the past 40 years of data (1981 - 2020).

## Data Collection

Basic webscraping using the the `pandas.read_html` function was employed to retrieve data from three Wikipedia webpages listed in the `Earthquake Models.ipynb` file. The data obtained from each of these webpages came in the form of various tables, so I went through and selected the tables that contained the data I wanted. I then combined all of the tables I wanted into a single dataframe and performed further data cleaning and feature engineering to create a dataset that I could use in exploratory data analysis and prediction. This dataset can be found in the `earthquake_data.csv` file in the repository. The first few rows of the table are below:

| index	| DateTime | Lat.	| Long. 	| Fatalities |	Magnitude |	Month |	Hour |	Fatalities_bool |
| ----- | -------- | ---- | -------  | ---------- | ---------- | ----- | ---- | ---------------- |
|0	|1981-01-19 15:11:00	| -4.576 | 139.232|	305 |	6.7	| 1 |	15 |	True |
|1	|1981-01-23 21:13:00	| 30.93 |	101.1	| 150 |	6.8	| 1 |	21 |	True |
|2	|1981-10-25 03:22:00	| 18.05 |	-102.08 |	3 |	7.3 |	10 |	3 |	True |
|3	|1982-12-13 09:12:00	| 14.7 | 44.38|	2800 |	6.2 |	12 |	9	| True |
|4	|1983-10-28 14:06:00	| 44.09 |	-113.8|	2	| 7.0 |	10 |	14 |	True |


## Exploratory Data Analysis (EDA)

Below is a map that I created which shows a single point for each earthquake included in the `earthquake_data.csv` dataset. The points on the map below show which earthquakes caused fatalities and which earthquakes did not.

<img src="https://github.com/tgrimm14/Project_Stat426/blob/main/earthquakes_map.png" width="600" height="300">

The `earthquake_data.csv` dataset contains 575 earthquakes that caused fatalities and 196 earthquakes that did not cause fatalities. To get a better understanding of the data, below is a histogram that shows the distribution of magnitude across the earthquakes in the dataset. The average magnitude across the earthquakes in the datasaet is right around 6.5.

<img src="https://github.com/tgrimm14/Project_Stat426/blob/main/earthquakes_by_magnitude.png" width="450" height="300">

Further EDA with various maps, plots, and other summarized data can be found in the `Earthquake Models.ipynb` file, along with the step-by-step data collection, data cleaning, and feature engineering involved in the creation of the `earthquake_data.csv` dataset.

## Methods and Results
Due to the nature of the dataset and the prediction question of interest, various Machine Learning classification methods were used. These models include Naïve Bayes, Gradient Boosting, and Random Forest. These models were chosen for their popularity and general predictive performance and so that I could compare multiple models in this situation. The Naïve Bayes is generally considered a strong baseline classification model to use and runs quite quickly, but often performs relatively poorly due to a failure to meet assumptions required by the model. Gradient Boosting and Random Forests are very similar in they way they function, and they both give insight as to which factors are the most important predictors in the model. However, they are known to sometimes overfit the data, causing poor predictions.

The machine learning models listed above were fit to train and test subsets of the data and then the predictive performance of each model was analyzed. Metrics that were used for performance evaluation are accuracy, f1 score, precision score, recall score, and AUC. In order to ensure optimal performance, optimal tuning parameters for the Gradient Boosting and Random Forest models were determined through the usage of scikit-learn's `GridSearchCV` function. The performance of these models was analyzed after fitting the models with the optimal tuning parameters and then using the models for prediction on the test dataset.

Between Naïve Bayes, Gradient Boosting, and the Random Forest model, the Random Forest Classifier model had the best overall predictive performance. Due to the similarity in how Gradient Boosting and Random Forests function, and due to the predictive performance of each model in this situation, either one could arguably be selected as the best model. The Random Forest Classifier had an AUC score of 0.968 and an f1 score of 0.937, while the Gradient Boosting Classifier had an AUC score of 0.965 and an f1 score of 0.932. The f1 score is a metric that is computed as the harmonic mean of precision and recall, where recall measures the "true positive" rate and precision measures, of those that are predicted to be "positive", the percent that are actually "positive". In this case, "positive" means that an earthquake caused at least one fatality. The AUC score is a performance metric that tells us how well the model can predict (correctly classify) the thing we are interested in. An AUC score of 0.968 tells us that there is a 96.8% chance that the Random Forest model will be able to successfully distinguish between earthquakes that do cause fatalities and earthquakes that don't cause fatalities. For both the f1 and AUC scores, having a value closer to 1 indicates better predictive performance.

The Random Forest and Gradient Boosting models had quite similar performance, but they were both far superior to the Naïve Bayes model. For the Random Forest model, out of 120 earthquakes that caused fatalities in the testing set, only 8 were misclassified as not causing fatalities. Out of the 35 earthquakes that didn't cause fatalities, only 7 were misclassified as causing fatalities. This is slightly more impressive than Gradient Boosting's 10 and 6 respective missclassifications, and also more impressive than Naïve Bayes' 15 and 8.

One useful piece of information we can obtain from the model is which features are the most important in predicting whether or not a "significant" earthquake will result in any fatalities. From the Random Forest Classifier model, we learn that the most important factor in this case is, perhapys unsurprisingly, Magnitude. The next most important factors in order are Longitude, Latitude, Hour, and Month.

## Conclusion
Many machine learning classification models can successfully be used to predict whether or not a significant earthquake will cause fatalities, even when only a few pieces of data are known: magnitude, location (latitude/longitude), hour of day, and month of year. From this analysis, it was discovered that magnitude and location are the most important factors in predicting if an earthquake will cause fatalities. Additionally, a Random Forest Classifier was able to correctly classify 140 out of 155 earthquakes, achieving an AUC score of 0.968 and an f1 score of 0.937. Considering the limited number of features used in prediction, the model performed quite well.

In the future, it would be interesting to apply machine learning models to predict fatalities resulting from other types of natural disasters such as floods, tornadoes, hurricanes, etc. Additionally, machine learning models could be used to predict other variables of interest such as damages (measured in dollars or some other local currency) caused by a natural disaster. In order to further improve earthquake fatality prediction in the context of this analysis, more data could be obtained or included. This data could come from earthquakes not included in the Wikipedia pages or from years before 1981.

