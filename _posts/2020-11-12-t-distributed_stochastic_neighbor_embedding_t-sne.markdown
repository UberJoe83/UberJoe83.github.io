---
layout: post
title:      "t-Distributed Stochastic Neighbor Embedding (t-SNE)"
date:       2020-11-12 20:08:47 +0000
permalink:  t-distributed_stochastic_neighbor_embedding_t-sne
---


Recently, I was working on a Cannabis recommendation system for my capstone project and it was a challenging task to take on because of the data that is available to work on. There are not many datasets out there that pertain to this topic. I worked with a [dataset](https://www.kaggle.com/kingburrito666/cannabis-strains) that I found on kaggle and let's just say it needed some manipulation in order to begin to explore and visualize. 

At first it was pretty straightfoward but as I proceeded to build my recommender I needed a way to be able to visually see if my recommendations in fact made any sense. The problem was that the data was mostly categorical and after performing some one-hot encoding the features increased from 5 to 69. 

Here is where t-SNE(tisnee) came to the rescue. It is a non-linear technique for dimensionality reduction that is great for visualization and gaining insight from high dimensional data. It is applied very ofter with NLP, image processing, genomic data, and speech processing. How it works is that it minimizes the divergence between two distributions: a distribution that measures pairwise similarities of the input objects and a distribution that measures pairwise similarities of the corresponding low-dimensional points. Then it maps the multi-dimensional data to a lower dimensional space and attempts to find patterns in the data by identifying observed clusters based on similarity of data points with multiple features. One drawback is that one this is done there is no way of identifying the input features and you can't make deductions solely based on the output of t-SNE. This is what makes this process mainly a data exploration and visualization technique.

After performing t-SNE and with the help of cosine similarity scores on my data I was able to make my recommendations and then view them on the t-SNE plot in order to gain insight and make sure the suggestions made sense. 


Scikit learn has a great implementation of t-SNE:

```
from sklearn.manifold import TSNE
```

It has some hyperparameters to set but these are the ones that I used for my project:

```
tsne = TSNE(random_state=1, n_iter=2000, metric="cosine")
```

Since my data was all one-hot encoded I created an array of all the features that I wanted to use:

```
feature_mask = ['hybrid_Type', 'indica_Type', 'sativa_Type', 'Aroused_effect',
       'Creative_effect', 'Dry_effect', 'Energetic_effect', 'Euphoric_effect',
       'Focused_effect', 'Giggly_effect', 'Happy_effect', 'Hungry_effect',
       'Mouth_effect', 'Relaxed_effect', 'Sleepy_effect', 'Talkative_effect',
       'Tingly_effect', 'Uplifted_effect', 'Ammonia_flavor', 'Apple_flavor',
       'Apricot_flavor', 'Berry_flavor', 'Blue_flavor', 'Blueberry_flavor',
       'Butter_flavor', 'Cheese_flavor', 'Chemical_flavor', 'Chestnut_flavor',
       'Citrus_flavor', 'Coffee_flavor', 'Diesel_flavor', 'Earthy_flavor',
       'Flowery_flavor', 'Fruit_flavor', 'Grape_flavor', 'Grapefruit_flavor',
       'Honey_flavor', 'Lavender_flavor', 'Lemon_flavor', 'Lime_flavor',
       'Mango_flavor', 'Menthol_flavor', 'Mint_flavor', 'Minty_flavor',
       'None_flavor', 'Nutty_flavor', 'Orange_flavor', 'Peach_flavor',
       'Pear_flavor', 'Pepper_flavor', 'Pine_flavor', 'Pineapple_flavor',
       'Plum_flavor', 'Pungent_flavor', 'Rose_flavor', 'Sage_flavor',
       'Skunk_flavor', 'Spicy/Herbal_flavor', 'Strawberry_flavor',
       'Sweet_flavor', 'Tar_flavor', 'Tea_flavor', 'Tobacco_flavor',
       'Tree_flavor', 'Tropical_flavor', 'Vanilla_flavor', 'Violet_flavor',
       'Woody_flavor']
			 
			 X = final_strain[feature_mask].to_numpy()
			 
			 array([[1, 0, 0, ..., 0, 0, 0],
       [1, 0, 0, ..., 0, 1, 0],
       [0, 0, 1, ..., 0, 0, 1],
       ...,
       [0, 1, 0, ..., 0, 0, 0],
       [0, 1, 0, ..., 0, 0, 0],
       [0, 1, 0, ..., 0, 0, 0]], dtype=int64)
```

With my array created I went ahead and fit and transformed my data and went from 69 dimensions to 2:

```
X_embedded = tsne.fit_transform(X)
X_embedded.shape

(2263, 2)
```

In order to access the embedding created I did the following:

```
final_strain["x"] = X_embedded[:,0]
final_strain["y"] = X_embedded[:, 1]
```

Using a scatter plot I was then able to visualize the results:

```
ax.scatter(final_strain.x, final_strain.y, alpha = 0.1)
```

![](https://i.imgur.com/qZG0rgx.png?1)

As you can see from the plot all the data points were successfully visualized and with different plots indicating the three different types of strains of cannabis, with sativas on the upper region, hybrids in the middle and indicas on the bottom. 

After I wrote the recommender function I went ahead and made a recommendation for Super Silver Haze(sativa) and proceeded to use my t-SNE plot to see how good the suggestions were. 

![](https://i.imgur.com/7GDyFoq.png)

Looks pretty good to me! The plot clearly shows the similiarity in the strains and even gives us a look at the variety the recommender is giving the user. 

The full project can be viewed [here.](https://github.com/UberJoe83/Cannabis-Recommendation-System)

Thanks for reading!


