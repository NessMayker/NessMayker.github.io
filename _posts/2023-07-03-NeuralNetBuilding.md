---
layout: post
title:  What is a Neural Network?
date: 2023-07-03
description: Building a Deep Learning Neural Network from Scratch
tags: DeepLearning NeuralNetwork
categories: DeepLearning
thumbnail: assets/img/pumpkin/neuron.jpeg
---

In the most recent lesson from fast.ai’s Practical Deep Learning for Coders, we built a neural network from scratch. 

<h4>Neural Networks</h4>

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/pumpkin/neuron.jpeg" title = "" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

Neural networks are computer models that are designed to mimic the human brain. The models are made up of artificial neurons that receive input, process it, and return an output. Each neuron has a weight that determines its impact and these are adjusted as the model is trained. The neural network has a hierarchal structure built from layers that process the information before passing it to the following layer. Neural networks are capable of parallel computing, where many computations are performed simultaneously, making them a very powerful modeling tool.

<h4>Pumpkin Seeds Dataset</h4>


<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/pumpkin/dataset.jpeg" title = "" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    The Pumpkin Seeds dataset.
</div>

For this project I used the Pumpkin Seeds dataset from Kaggle. This dataset consists of different measurements of pumpkin seeds such as area, perimeter, and roundness, and whether they belong to one of two classes ('Ürgüp Sivrisi’ and ‘Çerçevelik’). The goal is to build a model that can predict if a pumpkin seed is in the first or second class.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/pumpkin/pumpkinSeeds.jpeg" title = "" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    The two classes of Pumpkin Seeds.
</div>

I chose this dataset because the end prediction is a simple binary one; the neural network only has to sort the seed into one of two classes. I am familiar with the dataset because I used it to learn logistic regression modeling during the Erdös Institute’s data science bootcamp, and I wanted to be able to compare the performance between the different models.

<h4>Baseline Model</h4>

We will need something to compare all of our models to. This is called the “baseline model”. Because this problem has only two possible solutions, we can rephrase the problem to predict if the seed is in the Ürgüp Sivrisi class. In the training set 48% percent of the seeds are Ürgüp Sivrisi. Because there are less of this class than the other, we can just predict that the seed will never be in this class. Now, this seems pretty drastic, but if we always predict that the seed will never be in the class Ürgüp Sivrisi we will be right 52% of the time. Obviously this is not a good model, we just want something to compare our future models performances to.

<h4>Simple Linear Model</h4>

Next, we start with a simple linear model and incrementally added more complexity until we build our deep learning neural network. 

For the linear model we try to determine the liner relationship that each feature of the dataset has with the type of seed. From the plot below we can see that the two classes of seeds have overall distinct features, although there is overlap within the sample.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/pumpkin/pairplot.jpeg" title = "" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Exploratory Data Analysis: different seed classes are marked in orange and blue.
</div>

Here are the underlying steps of our linear model: <br>
1) Generate random coefficients <br>
2) Scale the independent features (area, perimeter, etc)<br> 
3) Multiply the independent features by the coefficients<br>
4) Sum the result from step 3 for each seed to predict the probability it is in the class <br>
5) Calculate how off the prediction is from the true result<br>
6) Adjust the coefficients based on how they performed the last cycle<br>
7) Repeat steps 3-6 until the model’s performance stops improving.<br>

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/pumpkin/features.jpeg" title = "" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    The features of the dataset and how much they are positively or negatively correllated with the Ürgüp Sivrisi class.
</div>

The first run of our linear model is 63% accurate. Although this is better than the baseline, it isn’t very good. We make a small change where instead of summing up the outputs to make a prediction, we run the sum of the outputs through a function called a “Sigmoid”. This function “squishes” all numbers to have a range of 0-1 and is essential in binary classification problems. When we test our linear model using the sigmoid function the accuracy jumps up to 73.6%.

Lets see if we can do better with a neural net!

<h4>Neural Network Model</h4>

Our neural network is build on top of the linear model. We start by adding a hidden layer in between out input layer and our output layer. This is similar to the left panel of the image below. Each layer performs a function on the data before passing its results to the following layer. These functions look like step 3 from the linear model, but using many more coefficients. Next the neural network updates all the layers of coefficients based on its performance. We continue training until the performance stops improving.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/pumpkin/neuralNet.jpeg" title = "" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Model of a neural network, image taken from https://cs231n.github.io/neural-networks-1/.
</div>

Our Neural Network model scored an accuracy of 83.8%. This is a 10% improvement over our linear model!

<h4>Deep Learning Neural Network</h4>

The difference between a Neural Network and a Deep Learning Neural Network is that the deep learning neural network has more hidden layers. The right panel of the image above is an example of a deep learning neural network.

We added 10 hidden layers to our deep learning neural net model and achieved an accuracy of 86.8%, making the deep learning neural net model the most accurate out of the models we looked at so far.

<h4>Comparing to Earlier Models</h4>

When I worked with this dataset earlier this year, I did a lot of exploratory data analysis to find the features that seemed to be the most important to determining the seed’s class. I used a type of modeling that is similar to the linear model using the sigmoid function and was able to score an accuracy of 76-86% depending on the features I used. 

I then revisited the dataset using several methods of model optimization which are out of the scope of this blog post, but just to say that I was able to boost the accuracy of my linear model to 88.5%, performing better than the deep neural network we just built. 

This is just to show that there are many ways to model a problem and you don’t always have to use a computationally expensive one to get a good result. 