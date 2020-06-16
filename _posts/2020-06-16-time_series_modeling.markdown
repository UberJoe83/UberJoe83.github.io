---
layout: post
title:      "Time Series Modeling"
date:       2020-06-16 18:04:25 +0000
permalink:  time_series_modeling
---


![](https://www.stubhub.co.uk/magazine/sites/default/files/styles/default_teaser/public/2019-05/los-angeles-city-guide.jpg?h=9db7e49d&itok=qVphGTDB)


The penultimate stage in my journey to be a Data Scientist. After seeing the kind of information we can extract from looking back through time and forecasting possible outcomes, I am glad that I chose this project. Not only do I get to work with data from my home town, this will add a great skill to my toolbox and will definitely come in handy. 

The task was to act as a real estate consultant. The stakeholders are curious about the real estate market in Los Angeles and want to know if it's a good place for investments and what zip codes might be the best to consider. Seems straighfoward enough but there are things to consider, one of them being the kind of returns to be seen and if those returns are worth the risk.  

First of course was the data, a dataset from Zillow with zip codes and their mean home values was provided and imported into my notebook. Then I filtered out the zip codes I wanted to work with. Los Angeles is a big sprawling city so I narrowed it down to two areas. The Downtown L.A. area and Santa Monica, which is known for it's long strech of palm trees along Ocean Blvd. and of course the pier, complete with an amusement park. I chose these two areas because it would give us a good view of the difference of living by the beach or the city's center. 

With the data from these zip codes I performed my EDA and saw that historically, Downtown showed to be a sound investment, but my stakeholders want to see the future. Enter the ARIMA model. 

ARIMA is a linear equation that helps predict future points using the past values in the time series. In order to model a time series we must make sure it is stationary, that is,  the series' statistical properties like mean and variance are constant over time. This is very rare in real world situations, so we try to get as close to perfect stationarity as possible. 
We can achieve this using the ARIMA model, which will account for the trends that make our series non-stationary. 

The parameters p, d, and q are esentially what ARIMA is. 

 - **p:** number of Auto-regressive terms (AR); this is the number of lags of the dependent variable to be used as predictors
 - **d:** this is the integrated part of the model (I); the parameter makes our series stationary by using the differencing technique to detrend the data. It is the number of times we subtract the previous value by the current value. 
 - **q:** number of moving average terms (MA); the lagged forecast errors included in the ARIMA model.
 
 Finding the right values for the p, d, and q parameters can be done with various techniques, [some of which are explained here](https://www.machinelearningplus.com/time-series/arima-model-time-series-forecasting-python/#:~:text=ARIMA%2C%20short%20for%20'Auto%20Regressive,used%20to%20forecast%20future%20values.).
 
 I used a function that automated the process for me, the code for the function can be found [here.](https://machinelearningmastery.com/grid-search-arima-hyperparameters-with-python/) The code gave me an output with the optimal parameters for my model based on the lowest mean squared error(MSE) achieved, after I ran the model with those parameters I saw some interesting results. 
 
 Santa Monica ended up being the better choice for investment, despite its high property value the model forecasted a 20% gain over 5 years as supposed to Downtown L.A. 's forecast of a 224% loss. Ouch that's a lot of green! This model has room for improvement and will definitely be a project I will be working on in the future. 
 





