---
layout: post
title:  "Playing with Recurrent Neural Networks"
date:   2017-07-01 01:00:00 +0530
categories: cs
author: "Nilay Shrivastava"
---
Recurrent Neural Networks are amusing. They are amongst the finest examples of how simple mathematical models can achieve exciting and useful results. Recurrent Neural Networks (or RNNs for short) are a type of Neural Network architecture that are used for sequential data. That is inputs that occur as a sequence like language, audio, video frames. These simple ( I would rather prefer the term 'cute') models are used to generate new language sequences, music in the style of Mozart, translate a sentence/document in one language to another, classify video and even play games!!!.

> In this post we will learn about RNNs, use them to generate text and visualise its working.

I assume that you have a basic understanding about simple Neural Networks, matrices and matrix multiplication. Even if you don't, feel free to jump over to fun part of the post where we trained an RNN to
talk about Special Relativity, prepare a speech in the style of Indian Prime Minister Narendra Modi and whatsapp messages.

The code for this post is available [ __here__ ](https://github.com/euler16/CharRNN). 



# What is hidden behind an RNN?

Nothing except a bunch of matrix multiplication!!!.<br>
Let's discuss a simple RNN (yes there are complicated ones too!).
People have developed various visual representations of RNN, each having its own pros and cons but in my opinion the easiest way to understand RNNs is to look at the equations.

<div>
$$f(x) = \sum_{k=1}^{K}\alpha_{k}$$
</div>