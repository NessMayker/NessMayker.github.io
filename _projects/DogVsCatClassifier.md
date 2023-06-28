---
layout: page
title: Dog vs Cat 
description: A simple image classifier using fast.ai 
img: assets/img/Nashoba.jpg
importance: 1
category: Deep Learning
---

I started taking the Practical Deep Learning course from fast.ai (https://course.fast.ai/).

The first two lessons introduce a simple image classifier that checks if an image is a cat or a dog. Followng the tutorial, I reproduce the classifier and make an interactive predicter using a huggingface space and gradio (https://huggingface.co/spaces/NessMaykerChen/CatVsDogClassifier).

<script type= "module"
src = "https://gradio.s3-us-west-2.amazonaws.com/3.12.0/gradio.js">
</script>

<gradio-app src="https://nessmaykerchen-catvsdogclassifier.hf.space/"></gradio-app>

The classifier performs well when the images are cats or dogs, but has not been trained to classify other images, so it basically tries to measure how dog like or cat like the rest of the examples are and returns some humourous results.

I'm looking forward to building more sophisticated image classifiers in the future!