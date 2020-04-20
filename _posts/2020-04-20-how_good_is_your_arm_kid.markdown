---
layout: post
title:      "How Good is your Arm Kid?"
date:       2020-04-20 06:15:05 +0000
permalink:  how_good_is_your_arm_kid
---


Another complicated round of algorithms and evaluation metrics to learn about, this time for classification models. The great part about this Mod 3 project was that I got to use data from my favorite sport, Baseball. Pitchers to be exact, and the way their performance can be used to classify them and predict what kind of player to be looking for. But I'm getting ahead of myself, what is a Classification model? 

To begin with, classification models are part of Machine Learning which is handled in two ways; Supervised learning and Unsupervised learning. Supervised learning is when we feed labeled data points into our algorithms, unsupervised learning is the opposite, the data points are not labeled and instead uses clusters of data points to look for patterns in the data. 

Given some inputs(data points) the classification model will try to predict the value of the outcomes of those inputs. 
Outcomes are the labels given to the data, for example in my dataset each observation has either a 1, 2, or 3 class label. To break it down a bit more the observations for Clayton Kershaw(pitcher for the Los Angeles Dodgers) are under the class 1 label. The observations are then separated from the labels and then stored and used for validation of the model. Next the observations are split into two sets, one for training the model and the other for testing the model, this is also done to the labels. Feeding the training observations into the algorithm lets it know what to look for in order to classify each pitcher correctly, then it is compared to the test data to evaluate its performance. This is what supervised learning is.

This is just the beginning, this process must be repeated various times in order to find the best model, which is found by measuring it's predictive value. This leads to one of the evaluation metrics used in building my model, **accuracy**.
Accuracy answers how many pitchers were classified correctly out of all the pitchers in the data set.

**Accuracy = (True Positives+True Negatives)/(True Positves+False Postives+False Negatives+True Negatives)**

Accuracy seemed to be the most important metric to use in this multiclass classification because it lets us know how well we were at predicting each kind of pitcher. 

That was my latest venture into the world of Data Science, and it was a great one. After all the self doubt to be here at this stage in the curriculum is has been very fulfilling and a motivating factor to keep me going. See ya next time! 








