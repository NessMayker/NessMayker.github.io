---
layout: post
title:  Produce Classifier
date: 2023-06-29
description: A simple image classifier using fast.ai and the fruits360 dataset
tags: DeepLearning fastai
categories: DeepLearning
thumbnail: assets/img/Fruits360.jpg
---

I started taking the Practical Deep Learning course from fast.ai (https://course.fast.ai/) and I have been so excited to practice what I have been learning.

For this project I am expanding on the Dog vs Cat classifier, instead training a model to classify fruit using the Fruits 360 dataset as my training data.

<!-- <script type= "module"
src = "https://gradio.s3-us-west-2.amazonaws.com/3.12.0/gradio.js">
</script>

<gradio-app src="https://nessmaykerchen-produceclassifier.hf.space/"></gradio-app> -->

<iframe
    src="https://nessmaykerchen-produceclassifier.hf.space/"
    frameborder="0"
    width="850"
    height="550"
></iframe>

The fruits360 data set consists of 131 types of produce that are placed on a white background and have many images captured at different angles for each object. This is a decently sized training set with a total of 67,692 images, but the training set lacks diversity of different backgrounds and different groupings of multiple fruits.

To save time, I made a very basic model using the ResNet34 archetecture with a batch size of 16 and only one round of fine-tuning. 

The first six example images are taken from the testing set, which the model was not allowed to interact with. As you can see the model performs brilliantly when tested with the same population of produce imaged with the same background. 

The last two images are from a purple sweet potato I had at home. I tried to reproduce the white background for the first image, but it does have a different white balance. For the second image I used a noisy background to test how different the results would be. For the first sweet potato image, the model is split between 10 types of produce, with a preference toward labeling it as a red potato. Surprisingly, the model performed better for the second image with a split between only two types with a high certainty that it is a red potato. This is overall a good approximation considering there were no purple sweet potatoes in the training set.

The classifier performs much better when the images are very closely related to those in the training set. I am curious to know if the largest room for improvement in the model could be found by using a deeper neural net, or by introducing more diversity in the training set. 

I definitely want to play around with this more in the future. For now, I need to pivot to NLP to keep up with the fast.ai course. :)


