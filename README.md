# EmoJeneration-DecisionTrees

## Table of Contents
* [Introduction](#Introduction)
* [EmoJeneration/TwitterTwin](#EmoJeneration/TwitterTwin)
* [Creating the Dataset](#Creating_The_Dataset)
* [Acknowledgements](#Acknowledgements)

## Introduction
Communicating with Modern-Day Hieroglyphics 

In today's digital age, online communication has become a fundamental part of our lives. In effect, the concept of an online voice, comprised by words and emojis, has become an integral and nuanced aspect of one’s identity. Because tone is easily lost over online communication, emojis in particular have become an extremely valuable tool to communicate clearly and effectively.

We aim to investigate if there are generational differences in the understanding and functionality of emojis. We designed and implemented a predictive classification model utilizing gradient-boosted decision trees. This model classifies an inputted piece of text into one of five distinct generational groups. To ensure the model's accuracy and relevance, we constructed a dataset composed exclusively of tweets containing emojis. This dataset formed the basis for training and testing for the multiple models we experimented with, allowing us to finely tune their predictive capabilities. During the development phase, we employed advanced data processing, downsampling, and data augmentation techniques to optimize the model's performance.

Our research delves into the intricate relationship between emoji usage and generational characteristics, shedding light on the nuanced ways in which emojis function as a means of expression across different age groups. Understanding these dynamics is pivotal not only for interpersonal communication, but also for businesses seeking to connect with specific audiences and decode the intricate language of emojis in the digital era.


## EmoJeneration/TwitterTwin
# Creating the Dataset

Data Collection
We chose to extract data from Twitter because of the conversational and personal writing style it allows for, which provides excellent context for each user’s usage of emojis. To create our dataset, we recorded twitter handles and age groups (0-4, based on generational boundaries) from online lists of celebrities by age in order to verify the age of each user. 

To obtain our dataset, we scraped 2100 of each celebrity's most recent emoji-containing, original tweets using rtweet. To ensure that we preserved the authentic voices of celebrities, we excluded retweets from our dataset. We only included tweets with emojis so as to focus the model’s understanding on the meaning and functionality of emojis, rather than their prevalence. 

Cleaning 
We built a function to remove special characters, seeing as there are certain special characters, namely emojis, that are important to the model. We used langid to filter our dataset so that it was made up entirely of English tweets. Given that the list of Twitter users from which we scraped included many global celebrities, the language identification model flagged a considerable number of non-English tweets. The dataset went from 139,000 to 85,000 unique tweets.  We used NLTK to remove stop words and tokenize the tweets.

We found that groups 1 and 2 had both the highest number of users and the most active twitter usage. Conversely, celebrities from groups 0 and 4, the oldest and youngest groups, had the lowest volume of tweets. This disproportionate representation resulted in an uneven dataset weighted towards groups 1 and 2. To amend this issue, we cut the dataset so that each group had the same number of tweets, and would therefore be represented equally by the model.

<img width="570" alt="Screenshot 2023-09-18 at 2 25 22 PM" src="https://github.com/EmoJeneration/EmoJeneration-DecisionTrees/assets/114313385/58c992a7-3d1e-4913-acd6-b52e3bddf321">



## Acknowledgements
Thank you to everyone at Data Science UCSB, especially our mentors Mehir Arora and Mateo Wang!
