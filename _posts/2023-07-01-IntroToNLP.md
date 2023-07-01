---
layout: post
title:  Intro to Natural Language Processing (NLP)
date: 2023-07-01
description: Introcuding NLP with Patent Phrase Matching 
tags: DeepLearning NLP
categories: DeepLearning
thumbnail: assets/img/NLPpatent/Slide0.png
---

The Practical Deep Learning for Coders class introduces NLP via the U.S. Patent Phrase to Phrase Matching Kaggle Competition. This competition aims to match key phrases in patent documents in an effort to more easily identify if a patent has been described before.

The dataset consists of sets of two phrases that have been scored from 0-1 depending on the level of their similarity. The idea is to train a language model to predict what the phrases scores would be without knowing in advance.


<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/NLPpatent/Slide2.jpeg" title = "" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    A glimpse into the dataset.
</div>

To do this we split the dataset into a training and a testing set. The model learns from the training set and then is scored via the testing set. There are many different ways to score a model, but it is common to include a “loss” and a “metric”. The loss is a score that is meaningful to the computer, it is the difference between the predicted and actual values. The model tries to minimize that loss. The metric is used to interpret the results of the model. Some examples of metrics are accuracy or false positive rates. For this project we are using the Pearson Correlation Coefficient. This number equals 1 when the model makes a correct prediction. 

We tackled this problem by joining the two phrases along with their patent classification entry and feeding them into a transformer. Because computers speak a different kind of language than you or I, we need to convert the text to numerical values.

Familiar text is often separated word for word like this Cecilia Payne-Gaposchkin quote shown on the image on the left, while unfamiliar text is often broken into smaller pieces such as the title of my last paper shown in the middle. These texts are then converted to numbers that represent indexes in the model’s vocabulary as shown on the right.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/NLPpatent/Slide1.jpeg" title = "" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Examples of tokenization and numericalization of text ran through a transformer.
</div>

For the first round of modeling we used the dberta transformer. This transformer is a machine learning model that has already been trained with language. This means that it should perform pretty good right out of the box! But the cool part is that we get to continue to train it more on our own dataset so that it learns to make better predictions as it becomes familiar with the data we are using.

When we train the model is to keep a subset of the data separate. We call this the validation set. We allow the model to assign different levels of importance (or weights) to each entry in the training set and then we score its predictions on the validation set. The model adjusts the weights based on the results from the scoring.

For the first model we use a validation set that is randomly chosen. For the next model we tried, we more carefully selected the validation set, keeping only entries for the validation set that did not occur in the training set. Before, any phrase might have shown up in both the training set and validation set when the validation set was randomly chosen, this time we decide to keep the phrases in the validation set separate from the training set. We ran both of these models for four training cycles.

The results show that as the model trains it performs slightly better over the first three epochs. The validation loss values are decreasing and the pearson value is increasing closer to 1. On the fourth epoch they seem to stop improving. Interestingly the unique values validation set did not improve the model over the long run, although for the first iteration the model performed slightly better on this validation set.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/NLPpatent/Slide3.jpeg" title = "" class="img-fluid rounded z-depth-1" %}
    </div>
</div>


 I decided to play around with another transformer called patentSBERT. I was excited about this one because it is a language model trained specifically for patent documents. I repeated the same two experiments as before, one with a randomly chosen validation set and one that had only unique phrases.

I was surprised that the patentSBERT model did not outperform the dberta3 baseline model, especially because it was trained specifically for patent documents. Overall these results are similar to if not a little worse than the earlier rounds.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/NLPpatent/Slide4.jpeg" title = ""  class="img-fluid rounded z-depth-1" %}
    </div>
</div>

To improve this model I would first try to look at different learning rates. The learning rate tells the computer how much to adjust the weights after each epoch. I would also look at different transformer models, although the baseline model seems to be working quite well.

One thing I have noticed in my very recent explorations into modeling, is that it isn't always clear or intuitive how to adjust a model to improve performance. When my team participated in the CAFA5 kaggle competition last month, we were unable to ever improve on the baseline model and we weren't exactly sure why the model was outperforming all the others that seemed to have a lot more going for them.

I hope that with continued study, I will learn more about model improvement and develop more intuition about the process.


