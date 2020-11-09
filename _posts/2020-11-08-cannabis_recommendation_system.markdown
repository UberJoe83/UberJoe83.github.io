---
layout: post
title:      "Cannabis Recommendation System"
date:       2020-11-09 01:45:09 +0000
permalink:  cannabis_recommendation_system
---


Recommendation systems are seen everywhere in our everyday life, from what movie to watch next to what t-shirt or pair of shoes to buy next. Companies like Netflix and Amazon are constantly throwing out new suggestions based on what we have already seen, bought, and rated to give customers a quick and easy way to make a decision. 

As of October of 2020, 33 states have legalized the use of medicinal cannabis, including 11 states that have also legalized its recreational use for adults the age of 21 and over. The legal cannabis industry is very young and in constant growth and expansion and it is only a matter of time until it becomes legal on a Federal level. There are countless dispensaries that sell cannabis products through websites like Weedmaps and Leafly, you simply choose a dispensary and check out their menu and make an order, which you can then either pick up or have delivered. The website also has a section which is dedicated to the many strains of the cannabis plant to rate, report on the effects, and describe the flavors associated with the strain that the user has tried. This section is usually curated by experts in the field with the use of their experience and knowledge about marijuana. My project was focused on trying to use other methods to suggest a new strain or new type of strain to customers. 

The problem I ran into working with topic was that there was no user-based content to help with my recommendations. This means that Collabrative-Filtering, which produces very personalized results, was not an option. Instead I had to use a Content-Based Recommender, which uses item features to recommend other items that are similiar to what the user likes. It focuses on the user's past actions or explicit feedback. 

In order to find the data points nearest to the input I used the cosine similarity distance metric which measures the cosine of the angle between two vectors, if the angle between the vectors is 0 then the similarity is calculated as 1 because the cosine of 0 = 1. This means that the vectors are the same. Similarity will be between 0 and 1, meaning that the closer you are to 1 the more similar the vectors are.

Using the cosine similarity function from scikit learn, I calculated the cosine similarity of each item with every other item in the dataset. 

```
from sklearn.metrics.pairwise import cosine_similarity
co_sim = cosine_similarity(final_copy, final_copy)
co_sim
co_sim.shape
```

This produced the following array that was later used to arrange the strains according to their similiarity.
```
array([[1.        , 0.44444444, 0.33333333, ..., 0.44444444, 0.44444444,
        0.22222222],
       [0.44444444, 1.        , 0.44444444, ..., 0.22222222, 0.22222222,
        0.22222222],
       [0.33333333, 0.44444444, 1.        , ..., 0.33333333, 0.22222222,
        0.33333333],
       ...,
       [0.44444444, 0.22222222, 0.33333333, ..., 1.        , 0.77777778,
        0.55555556],
       [0.44444444, 0.22222222, 0.22222222, ..., 0.77777778, 1.        ,
        0.77777778],
       [0.22222222, 0.22222222, 0.33333333, ..., 0.55555556, 0.77777778,
        1.        ]])
```

The way the metadata was stored in the dataset was a bit cumbersome to work with, so to be able to visualize and explore the data I had to split each one of the effects and flavors and create dictionaries to easy manipulate for visualization.


```
Strain	   Type	     Rating	   Effects	  Flavor
0	100-Og	hybrid	4.0	Creative,Energetic,Tingly,Euphoric,Relaxed	Earthy,Sweet,Citrus
1	98-White-Widow	hybrid	4.7	Relaxed,Aroused,Creative,Happy,Energetic	Flowery,Violet,Diesel
2	1024	sativa	4.4	Uplifted,Happy,Relaxed,Energetic,Creative	Spicy/Herbal,Sage,Woody
3	13-Dawgs	hybrid	4.2	Tingly,Creative,Hungry,Relaxed,Uplifted	Apricot,Citrus,Grapefruit
4	24K-Gold	hybrid	4.6	Happy,Relaxed,Euphoric,Uplifted,Talkative	Citrus,Earthy,Orange
```

```
# Function to extract the effects from the current column
def split_effs(df):
    
    """This function takes a dataframe as an input and 
    will extract the effects that are separated by a comma, 
    place them in a dictionary and count the times they appear."""
    
    eff_dict = {}
    for eff_list in df["Effects"]:
        effects_list = eff_list.split(",")
        for effect in effects_list:
            if not effect in eff_dict:
                eff_dict[effect] = 1
            else:
                eff_dict[effect] += 1
    
    return eff_dict
```

After implementing this function on both the effects and flavors of each of the strains I was able to visualize and analyze the data. 

```
ind_effs = split_effs(indicas_set)
ind_effs

{'Relaxed': 628,
 'Happy': 562,
 'Euphoric': 516,
 'Uplifted': 331,
 'Giggly': 94,
 'Tingly': 143,
 'Focused': 106,
 'Aroused': 69,
 'Creative': 128,
 'Sleepy': 468,
 'Hungry': 210,
 'Talkative': 58,
 'Energetic': 36}
```

After looking through the data it was time to go ahead and build the recommendation system, using the following function, the similarity scores were used to suggest the ten nearest strains to the input. 

```
# Function that takes in strain name as input and outputs most similar strains
def get_recommendations(strain, cosine_sim=co_sim):
    # Get the index of the strain that matches the input
    idx = indices[strain]

    # Get the pairwise similarity scores of all strains with that initial strain
    sim_scores = list(enumerate(cosine_sim[idx]))

    # Sort the strains based on the similarity scores
    sim_scores = sorted(sim_scores, key=lambda x: x[1], reverse=True)

    # Get the scores of the 10 most similar strains
    sim_scores = sim_scores[1:11]

    # Get the strain indices
    strain_indices = [i[0] for i in sim_scores]

    # Return the top 10 most similar strains
    print(sim_scores)
    return final_strain["Strain"].iloc[strain_indices]    
```

Calling on the function and inputing a certain strain would produce a list of the 10 most similiar strains.

```
# Recommendations for a sativa type strain
sup_sil_haze_recommends = get_recommendations("Super-Silver-Haze")

1974    Super-Silver-Haze
25          Acapulco-Gold
60            Alaskan-Ice
169                Bay-11
170             Bay-Dream
283         Blue-Hawaiian
521         Cinderella-99
524                 Cinex
680           Dream-Queen
692        Dutch-Hawaiian
Name: Strain, dtype: object
```

I then printed out the strains along with their effects and flavors to make the necessary comparisons.

```
*******************************************************
Strain                             Super-Silver-Haze
Type                                          sativa
Rating                                           4.4
Effects    Happy,Uplifted,Energetic,Euphoric,Relaxed
Flavor                           Citrus,Earthy,Sweet
Name: 1975, dtype: object
*******************************************************
Strain                                   Alaskan-Ice
Type                                          sativa
Rating                                           4.4
Effects    Euphoric,Uplifted,Happy,Relaxed,Energetic
Flavor                     Sweet,Earthy,Spicy/Herbal
Name: 60, dtype: object
*******************************************************
Strain                                 Blue-Hawaiian
Type                                          hybrid
Rating                                           4.3
Effects    Happy,Uplifted,Relaxed,Euphoric,Energetic
Flavor                           Citrus,Earthy,Sweet
Name: 284, dtype: object
*******************************************************
Strain                                   Dream-Queen
Type                                          hybrid
Rating                                           4.3
Effects    Happy,Uplifted,Euphoric,Relaxed,Energetic
Flavor                           Citrus,Sweet,Earthy
Name: 681, dtype: object
```

As you compare the different strains you can see that not only did the recommender suggest very similiar strains, but it also managed to give some variety to the user as it suggested strains other than sativas. This is an important added value to the recommendation system.


## Advantages of Content Based Filtering
**User independence:** Collaborative filtering needs other users’ ratings to find similarities between the users and then give suggestions. Instead, the content-based method only has to analyze the items and a single user’s profile for the recommendation, which makes the process less cumbersome. Content-based filtering would thus produce more reliable results with fewer users in the system.

**Transparency:** Collaborative filtering gives recommendations based on other unknown users who have the same taste as a given user, but with content-based filtering items are recommended on a feature-level basis.

**No cold start:** As opposed to collaborative filtering, new items can be suggested before being rated by a substantial number of users.

## Disadvantages of Content Based Filtering
**Limited content analysis:** If the content doesn’t contain enough information to discriminate the items precisely, the recommendation itself risks being imprecise.


You can find the repository that contains the full jupyter notebook for this project [here.](https://github.com/UberJoe83/Cannabis-Recommendation-System)
