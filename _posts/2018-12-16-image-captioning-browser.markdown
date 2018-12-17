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

> Deploying model on web 

The aim of this post is not to provide a full tutorial on Image Captioning. For that I would suggest you to go through Andrej Karpathy's well written [paper]() and

Since automatically describing the content of a picture connects both Computer Vision and Natural Language Processing...

## Dataset Used

## Feature Extraction from Image: MobileNets

## Natural Language Generation: LSTMs

## Skeleton Code for the Model and Model Summary

## Caption Generation in Browser

## Issues faced

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