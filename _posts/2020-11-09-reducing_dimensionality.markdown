---
layout: post
title:      "Reducing Dimensionality"
date:       2020-11-09 21:39:21 +0000
permalink:  reducing_dimensionality
---


One of the problems you might run into in data science projects is the increasing dimensionality of datasets(Curse of Dimensionality). This basically means that as our features increase so does the dimensionality of our dataset, which also means that our data points in n-dimensions become increasingly sparse. This leads to our models overfitting and ultimately not being able to generalize the data properly. Visualization also becomes very difficult, most of the plotting we perform is from 2D to 3D planes. 

How do we remedy this? The most commonly known method is through Principal Component Analysis (PCA). This is an unsupervised learning technique that transforms the dataset along the principal axes, it takes the first component to capture the max variance within the data, then the additional components, which are independent to the previous components, are used to account for as much as the remaining variance as possible. Before perfoming this process the data that will be transformed must be standarized so that components that are on a different scale won't be given more importance than a component that should actually have more importance. 

## Steps:
1. Recenter each feature of the dataset by subtracting that feature's mean from the feature vector.
2. Calculate the covariance matrix for the centered dataset.
3. Calculate eigenvectors of the covariance matrix.
4. Project the dataset into the new feature space; multiply the eigenvectors by the mean-centered features.


After transforming the data you must calculate the explained variance ratio which will let you know how much of the information from the original dataset is accounted for. A good threshold is in between 70-80% of the variance. 

This is one of the many methods to reduce dimensionality to insure great results from our machine learning models.

In my next blog I will talk about how we can use another method of dimensionality reduction to visualize high dimensional data into a 2D space.


