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
People have developed various visual representations of RNN, each having its own pros and cons but in my opinion the easiest way to understand RNNs is to look at the equations. Keep in mind these are matrix equations. A good way to understand them is to note the dimensions of the matrices.

<div>
$$h_{t} = \sigma (W^{(hh)} \cdot h_{t-1} + W^{(hx)}\cdot x_t)$$        
$$y_t = softmax(W^{(S)} \cdot h_t)$$

Where,
<ul>
<li> \(h_t \in \mathbb{R}^{D_h}\) . \(h_t\) is called the hidden state of the RNN (it is a vector). Here \(D_h\) is the dimension of hidden state vector (something you are free to chose while creating an RNN). It must be kept in mind that a fresh hidden state vector is calculated after every timestep and fed back again in the next time step. (see the first equation)</li>
<li> \(x_t \in \mathbb{R}^{d}\) where $d$ is dimension of input vector. The input to the RNN is in form of a vector. This vector might represent anything, it can be words, characters etc. Basically it will represent the discrete unit of input. </li>
<li> \(h_{t-1} \in \mathbb{R}^{D_h}\). In the equations given above this represents the hidden state vector computed after the previous time step.</li>
<li> \(W^{hx} \in \mathbb{R}^{D_h \times d}\). This is the weight matrix applied to the input vector \(x_t\)
 (see the equations).</li>
<li>\(W^{hh} \in \mathbb{R}\). This is the weight matrix applied to the hidden state from previous time step.</li>
<li>\(W^{(S)} \in \mathbb{R}^{D_y \times D_h}\). This is applied to the hidden state to generate the output for a particular timestep</li>
<li> \(y_t \in \mathbb{R}^{D_y}\). This is the output of the current timestep.</li>
<li> \(\sigma\) is the non-linearity we intorduce in a neural network. </li>
</ul>
The weight matrices are the parameters of the RNN which it learns through training. In practice one concatenates \(h_t\) and \(x_t\) and instead of 2 W's in the first equation we use a larger weight matrix \(W \in \mathbb{R}^{D_h \times (D_h + D_x)}\). If you know what simple neural networks are you can see that these equations essentially correspond to a 1-layer simple neural network having \(W^{D_h \times (D_h+D_x)}\) as weight matrix. 
</div>
Remember that these equations are to be applied at every timestep of the sequence. For example if we apply a 'character level RNN' (which we will do shortly), on a sequence _"I love maths"_, then after we compute hidden state for timestep 'o', we use the same hidden state (and also the same W's) to compute hidden state and output for next timestep 'v' (using the equations). Of course one has to pass the inputs as vectors and not as raw string.

![Internals of RNN]({{site.baseurl}}/assets/playing-with-rnn/internal-rnn.svg)


Let's see how this looks in code.

{% highlight python %}
class RNN:
	def __init__(self,input_size,hidden_size,output_size):
		self.input_size  = input_size
		self.hidden_size = hidden_size
		self.output_size = output_size
		# here we initialize the weights with random numbers
		self.Whhx = np.randn(hidden_size, input_size+hidden_size)
		self.Why  = np.randn(output_size, hidden_size) 
{% endhighlight %}

This is the initialisation part where we define the parameters of our RNN Cell. Now the forward propagation part; 
{% highlight python %}
class RNN:
	def __init__(self,input_size,hidden_size,output_size):
		# .....

	def forward(x,h):
		# x is (input_size X 1) and h is (hidden_size X 1)
		h_t = np.dot(self.Whhx, np.concatenate(h,x))
		y_t = np.dot(self.Why, h)

		return y_t, h_t

.....................................

# in the main function
rnn = RNN(input_size, hidden_size, output_size)
......................................

# inside the training loop
h = np.zeros(hidden_size,1)
for t in range(timesteps):
	y,h = rnn.forward(x_t,h)
{% endhighlight %}

Take time to digest it. It is perfectly fine if you can't. Come back to it later but make sure you do because the beauty of RNNs (like other Machine Learning models/algorithms) lies in their characteristic equations.

> "Read Euler, Read Euler, he is the master of us all"
>                                                     - #RandomQuotewithNoMeaning

# LSTMs and GRUs

The hidden state of the RNN is the vector that keeps track of the past input (due to its dependence on the previous timestep). So it essentially acts as a memory bank that gets updated at each timestep.
Through the hidden state vector, an RNN (the one described above) can (theoretically) model any sequence, It turns out that in practice they are hard to train. The problem is called 'The Vanishing Gradient Problem'. What it essentially means is that RNNs have a really short memory (of the past) and can't model sequences effectively.<br>

In order to overcome this deficiency, researchers over the years have developed many variants of the simple RNN. The most successful (and also the most popular ones) are Long Short Term Memory (LSTM) and Gated Recurrent Units. Nobody actually uses the simple RNN we discussed above (but understanding it is a pre-requisite for understanding LSTMs and GRUs). Also GRUs and LSTMs are almost equivalent (when it comes to accuracy) and there is no particular advantage in using  one over the other, except for the fact GRUs have simpler equations.

## GRUs

