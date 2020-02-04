---
layout: post
title:      "P-values, Effect Sizes and Power OH MY!"
date:       2020-02-04 00:48:53 +0000
permalink:  p-values_effect_sizes_and_power_oh_my
---


Where do I start, this was confusing, hard, complicated, but at the same time fun. Another round of new concepts, new code and new ways of explaining and proving hypotheses and the underlying data that is in everything we do. Like everything in Data Science, this is new to me. Probability, Statistics and a whole bunch of formulas and symbols I haven't ever seen before. This project has been the most interesting and fun so far. 

I like SQL, in fact I love it, which is one of the reasons why I had fun with this project. Querying the data necessary for the experiments that I would be conducting was the best part. Manipulating the data from the query was an option but I found it was easier with the use of Pandas in Python. After collecting and transforming the data, it was explored and the questions to be answered were formulated. 

Now comes the interesting part, the experiment. Here is when we decide what kinds of tests will be performed. One question that needed to be answered was about the effect discounts had on product quantities in an order. You would think that by just looking at the numbers you can guess whether or not it's true, but nope, that's not how it works. 

We need the data yes, but we need the right kind of data, which means exploring, transforming and manipulating that data to be able to prove our theories. After querying the database for the general info, I took the data and began to shape it to what I needed. With pandas this task wasn't so hard. Once the data was right I proceeded into the tests.

Two sample t-test to be exact. A way to compare two means(averages) to see if they are different from each other. This test was ideal for these experiments because the samples used were relatively small. Since we were using two unrelated samples the test was independent and compared the orders without discounts to orders with discounts. 
The test resulted in a difference in between the groups, but how big was the difference, was it really accurate and was there a chance this result was a false positive. 

That where these three concepts came into play:

1. Effect Size - the magnitude of the difference between the groups being compared, the higher the value the more the difference. 

2. Power - measures the test's ability to detect a difference when there is in fact a difference. Accuracy of your experiment basically.

3. P-values - this value is connected to the alpha we set or our confidence level, which is commonly set to a = 0.05 or a 95% confidence level. Results below the alpha reject the null hypothesis and the alternative is accepted, which in this case was that Discounts do have an effect on the quantity of a product in an order. 

Whoa! I still can't believe I understand some of this but it all comes with more and more practice! 


