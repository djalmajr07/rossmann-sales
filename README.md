# Rossmann Stores 
Sales Prediction with Machine Learning

![Sales](https://github.com/djalmajr07/rossmann-sales/blob/main/img/0_7tM5SbKstuED5_AX.jpg)

[![NPM](https://img.shields.io/npm/l/react)](https://github.com/djalmajr07/rossmann-sales/blob/main/LICENSE) 



# Rossmann Prediction Problem

The CFO requests the prediction of each store in a monthly meeting, whereas she was having difficulty to find out the best investment value for the renovations of each store, due the prediction provided by the directors was not assertive, there was a lot of divergence. Therefore to solve this problem, I used Machine Learning algorithms to forecast most precisely how would be the store prediction for the next six weeks (forty-two days).


# Business Assumption

- The days when stores were closed were ruled out.
- Only stores with sales values greater than 0 were considered.
- For stores that did not have Competition Distance information, it was assumed that the distance would be two times greater than the greatest distance from a nearest competitor.

# Attribute List

| Attributes                       | Descriptions                                                      |
| -------------------------------- | ------------------------------------------------------------ |
| Id                               | An id that represents a (store, date) duple within the test set|
| Store                            | A unique id for each store                                   |
| Sales                            | The turnover for any given day                          |
| Customers                        | The number of customers on a given day                       |
| Open                             | An indicator for whether the store was open: 0 = closed, 1 = open |
| Stateholiday                     | Indicates a state holiday. Normally all stores, with few exceptions, are closed on state holidays. Note that all schools are closed on public holidays and weekends. A = public holiday, b = easter holiday, c = christmas, 0 = none |
| Schoolholiday                    | Indicates if the (store, date) was affected by the closure of public schools |
| Storetype                        | Differentiates between 4 different store models: a, b, c, d  |
| Assortment                       | Describes an assortment level: a = basic, b = extra, c = extended |
| Competitiondistance              |Distance in meters to the nearest competitor store           |
| Competitionopensince[month/year] | Gives the approximate year and month of the time the nearest competitor was opened |
| Promo                            | Indicates whether a store is running a promo on that day        |
| Promo2                           | Promo2 is a continuing and consecutive promotion for some stores: 0 = store is not participating, 1 = store is participating |
| Promo2since[year/week]           | Describes the year and calendar week when the store started participating in promo2 |
| Promointerval                    | Describes the consecutive intervals promo2 is started, naming the months the promotion is started anew. E.G. "Feb,may,aug,nov" means each round starts in february, may, august, november of any given year for that store |


# Solution Strategy

The method applied was CRISP-DM:

**Step 01. Data Description:** The objective is to use statistical metrics to identify outliers in the business scope.

**Step 02. Feature Engineering:** Derive new attributes based on the original variables to better describe the phenomenon to be modeled.

**Step 03. Data Filtering:** Filter rows and select columns that do not contain information for modeling or do not correspond to the business scope.

**Step 04. Exploratory Data Analysis:** Explore the data to find insights and better understand the impact of variables on model learning.

**Step 05. Data Preparation:** Prepare data so machine learning models can learn specific behavior.

**Step 06. Selection of resources:** Selection of the most significant attributes to train the model.

**Step 07. Machine Learning Modeling:** machine learning model training

**Step 08. Hyperparameter Fine Tunning:** Choose the best values for each of the parameters of the model selected in the previous step.

**Step 09. Convert model performance to business values:** Convert model performance to a business result.

**Step 10. Deploy Model to Production:** Publish the model to a cloud environment so that other people or services can use the results to improve the business decision.

**Step 11. Telegram Bot:** Creation of a bot on the telegram app, to consult the forecast at any time

# Top Three Data Insights

**Hypothesis 2** - Stores with closer competitors should sell less.

**FALSE**: Stores with closer competitors sell more.

![H2](https://github.com/djalmajr07/rossmann-sales/blob/main/img/H2.PNG)

**Hypothesis H9.** Store stores sell more over the years.

**FALSE**: Stores sell less over the years

![H9](https://github.com/djalmajr07/rossmann-sales/blob/main/img/H9.PNG)

**Hypothesis 11.** - Stores should sell more after the 10th of each month.

**TRUE**: Stores sell more after the 10th of each month.

![h11](https://github.com/djalmajr07/rossmann-sales/blob/main/img/h11.PNG)





# Machine Learning Models Applied
Tests were performed using the following algorithms:

**Linear Regression Model**

**Linear Regression Regularized Model - Lasso**

**Random Forest Regressor**

**XGBoost Regressor**

# 6. Machine Learning Model Performance

**Single Performance**

| Model Name | MAE    | MAPE      | RMSE |
|-----------|---------|-----------|---------|
|  Random Forest Regressor  | 678.296634 | 0.099816   | 1008.248950 |
|  XGBoost Regressor	  | 843.112293 | 0.122609   | 1250.952637 |
|  Average Model  | 1354.800353 | 0.455051   | 1835.135542 |
|  Linear Regression	  | 1867.089774 | 0.292694   | 2671.049215 |
|  Linear Regression - Lasso	  | 1869.571858 | 0.288111	   | 2694.005137 |


**Real Performance - Cross Validation**

| Model Name | MAE CV   | MAPE CV      | RMSE CV |
|-----------|---------|-----------|---------|
|  Random Forest Regressor  | 838.18 +/- 218.74| 0.12 +/- 0.02  | 1256.87 +/- 319.67 |
|  XGBoost Regressor	  | 1030.28 +/- 167.19 | 0.14 +/- 0.02   | 1478.26 +/- 229.79 |
|  Linear Regression	  | 2081.73 +/- 295.63 | 0.3 +/- 0.02   | 2952.52 +/- 468.37 |
|  Linear Regression - Lasso	  | 2088.88 +/- 327.01 | 0.3 +/- 0.01	   | 2988.6 +/- 499.57 |


Although the Random Forest model has proven to be superior to the others, in some cases this model ends up requiring a lot of space to be published, resulting in an extra cost for the company to keep it running. Therefore, the chosen algorithm was the **XGBoost Regressor** which in sequence passed to the Hyperparameter Fine Tunning step.


**Final Performance - Hyperparameter Fine Tunning Cross Validation**

After finding the best parameters for the model through the Random Search method, the final metrics for the model were as follows:

| Model Name | MAE CV   | MAPE CV      | RMSE CV |
|-----------|---------|-----------|---------|
|  XGBoost Regressor	  | 1030.28 +/- 167.19 | 0.14 +/- 0.02   | 1478.26 +/- 229.79 |

# Model performance on business values
It is now possible to analyze the metrics and compare the difference in performance between the current model used by the company (**Average Model**) and the model proposed by the data scientist (**XGBoost Regressor**)

**Current model based on average sales**

| Scenery | Values |
|-----------|---------|
| Predictions | R$ 280,754,389.45|

**Model with XGBoost Regression**

| Scenery | Values |
|-----------|---------|
| Predictions | R$285,860,497.84 |
| Worst Scenario | R$285.115,015.78 |
| Best Scenery | R$286.605,979.91 |


# How to see the prediction

## Pre-requirement
- Sing up telegram;
- Create an account;
- Download telegram on desktop, mobile or use telegram web.

### Telegram

- To access the telegram bot click below:

[<img alt="Telegram" src="https://img.shields.io/badge/Telegram-2CA5E0?style=for-the-badge&logo=telegram&logoColor=white"/>](https://t.me/GetRossmannPred_bot)


![send_message](https://github.com/djalmajr07/rossmann-sales/blob/main/img/link-telegram-message.PNG)

### Prediction In Real Time
- Send one number per time to recieve the store's prediction based on the next six weeks.


![prediction](https://github.com/djalmajr07/rossmann-sales/blob/main/img/prediction.PNG)


### Pay Attention
-If [Rossmann bot](https://t.me/GetRossmannPred_bot) recieve anything different from numbers, it will answer back: Store ID is Wrong. On this bot can occur to have some stores not available to have prediction, so it will answer back: Store Not Available. If it happens you can select another Store Id and move on.


![possible-mistakes](https://github.com/djalmajr07/rossmann-sales/blob/main/img/possible-mistakes.PNG)

#  Conclusion

Finally, it is possible to understand that although the model based on averages is simple, it is still coherent however not sensible enogh to comprehend store's oscilations, but if machine learn models were too expensive it would be a good choice to solve this problem, of course the data scientist and the CFO should consider its leak of precision in some points.

The XGBoost Model for the first cycle (CRISP-DM Methodology) presented a result within the acceptable range, although some stores were difficult to have the expected behavior presenting the MAPE (Mean Absolute Percenage Error) between 0.30 to 0.56, this first result it will be presented to the company, to inform the project status and what is already available as a solution.


#  Next steps

Start a second cycle to analyze the problem, seeking different approaches, especially considering stores with behavior that is difficult to predict. In these stores the Data scientist ought gain plenty of experience.

Possible points to be addressed in the second cycle:

-**Work with NA data differently**

-**Rescaling and Encoding of data with different methodologies**

-**Work with new features for forecasting**

-**Work with a more robust method to find the best Hyper parameters for the model**

# Technologies

- Jupyter;
- Python.
 
# Deployment into production
- Back end: Heroku;
- Front end web: Telegram;
- Database: kaggle csv files.

# Author

Djalma Luiz da Silva Junior



[<img alt="LinkedIn" src="https://img.shields.io/badge/LinkedIn-0077B5?style=for-the-badge&logo=linkedin&logoColor=white"/>](https://www.linkedin.com/in/djalmajunior07)


