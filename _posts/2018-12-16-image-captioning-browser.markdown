---
layout: post
title:  "Image Captioning in Browser using Tensorflow.js"
date:   2018-12-16 01:00:00 +0530
categories: cs
author: "Nilay Shrivastava"
comments: true
---
The holy grail of Computer Science and Artificial Intelligence research is to develop programmes that can combine knowledge/information from multiple domains to perform actions that currently humans are good at. In this spirit, Image Captioning stands as a great test-bed for AI algorithms since it involves building understanding of an image and then generating meaningful sentences on top of it. 

## TLDR; Demo

To run the demo, click [here](https://euler16.github.io/demos/image-captioning/)

> Deploying deep learning models on web is challenging since web imposes size constraints. This forced me to reduce number of parameters of the model substantially which in turn decreased accuracy. So the captions may sometimes be wayward. 

> Moreover since the model uses LSTMs, TensorFlow.js warns about slowness resulting from Orthogonal Initialization. So your browser (especially Firefox) may warn you about this page slowing down your browser or your UI might get unresponsive for sometimes. Don't worry that is happening because JavaScript is performing heavy blocking computation!



The aim of this post is not to provide a full tutorial on Image Captioning. For that I would encourage you to go through Andrej Karpathy's [presentation](https://www.youtube.com/watch?v=yk6XDFm3J2c) and Google's Show and Tell [paper](https://arxiv.org/pdf/1609.06647.pdf).

This post documents my approach for implementing a captioning model for browser using Tensorflow.js

Since automatically describing the content of a picture connects both Computer Vision and Natural Language Processing...

## Dataset Used

Most state-of-the-art neural architectures have been trained using __Microsoft Common Objects in Context__ ([MSCOCO](http://cocodataset.org/#home)) dataset. The dataset weighs around 25GB and contains more than 200k images across 80 object categories having 5 captions per image. Since I am an undergrad I don't have access to computational power to process such a huge dataset.

Therefore I used __Flickr8k__ [Dataset]() provided by University of Illinois Urbana-Champaign. The dataset is 1GB large and consists of 8k images each having 5 captions. Due to its relatively small size I could easily use Flickr8k with Google Colab notebooks.

## Model Architecture
<img src="../../../../assets/image-captioning/image_cap_arch.png">

As shown above the complete neural captioning architecture can be divided into two parts.
1. __The Feature Extractor__ : which takes an image as input and outputs a low dimensional condensed repersentation of the image.
2. __The Language Model__ : which takes the condensed representation and a special __START__ token and generates a caption.

We stop the caption generation process when the language model emits an __END__ token or the length of the caption increases a threshold. In the demo, this threshold has been set to 40 which is the maximum length of captions in Flickr8k dataset.


## Feature Extraction from Image: MobileNets

Since the input data is an image, it is clear Convolutional Neural Networks (CNNs) are an attractive option as feature extractors. For high accuracy, most image captioning projects on Github use [Inception](https://ai.googleblog.com/2016/03/train-your-own-image-classifier-with.html) or Oxford's [VGG](http://www.robots.ox.ac.uk/~vgg/research/very_deep/) Model. Though good for a desktop demonstration, these models aren't suited for browser demonstration as they are quite heavy and compute intensive.

So I turned to [MobileNet](https://ai.googleblog.com/2017/06/mobilenets-open-source-models-for.html) which is a class of light low-latency convolutional networks specially designed for resource constrained use-cases. In the complete model, MobileNet generates a low-dimensional representation of input image, which is fed to the language model.

## Natural Language Generation: LSTMs

## Skeleton Code for the Model and Model Summary

## Caption Generation in Browser

## The Hard Part: Engineering Issues

The primary issue 

## Complete Code

{% if page.comments %}
<div id="disqus_thread"></div>
<script>

/**
*  RECOMMENDED CONFIGURATION VARIABLES: EDIT AND UNCOMMENT THE SECTION BELOW TO INSERT DYNAMIC VALUES FROM YOUR PLATFORM OR CMS.
*  LEARN WHY DEFINING THESE VARIABLES IS IMPORTANT: https://disqus.com/admin/universalcode/#configuration-variables*/
/*
var disqus_config = function () {
this.page.url = PAGE_URL;  // Replace PAGE_URL with your page's canonical URL variable
this.page.identifier = PAGE_IDENTIFIER; // Replace PAGE_IDENTIFIER with your page's unique identifier variable
};
*/
(function() { // DON'T EDIT BELOW THIS LINE
var d = document, s = d.createElement('script');
s.src = 'https://euler16.disqus.com/embed.js';
s.setAttribute('data-timestamp', +new Date());
(d.head || d.body).appendChild(s);
})();
</script>
<noscript>Please enable JavaScript to view the <a href="https://disqus.com/?ref_noscript">comments powered by Disqus.</a></noscript>
{% endif %}