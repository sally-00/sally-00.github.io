---
layout: post
title: Why norm comes from the assumption that data is drawn from a Gaussian distribution?
date: 2023-03-12
description: 
tags: ML
---

I was reading the paper "A Review on Deep Learning Techniques for Video Prediction" by S. Oprea. 

In Section 2.4 The Devil is in the Loss Function, It says: " Most of distance-based loss functions, such as based on lp norm, come from the assumption that data is drawn from a Gaussian distribution."

I could not understand the how. 
Then I found [this blog](https://chuanting.net/blogs/post/mmse/#:~:text=Minimizing%20L2%20loss%20comes%20from,prediction%20beyond%20mean%20square%20error.) that reminds me the distance minimization comes in when we are trying to fit a data distribution assuming a Gaussian distribution.
I will put the formulas below for refreshing memory.

With a dataset $\Chi = \{ x^{(1)},x^{(2)},...,x^{(m)} \}$  that comes from an unknown distribution $p_{data}(x)$, we want to model it with $p_{model}(x;\theta)$. 
Using max-likelihood,
$$
\theta_{ML} = p_{model}(\Chi;\theta) = \Pi^{m}_{i=1}p_{model}(x^{(i)};\theta)
$$
Using log operation for precision on computer,
$$
\theta_{ML} = \Sigma^{m}_{i=1}log p_{model}(x^{(i)};\theta)
$$
Assuming that $p_{model}(x;\theta)$ follows a Gaussian distribution $p_{model}(x;\theta) \sim \mathcal{N}(\mu,1)$,
$$
\theta_{ML} = arg max_{\theta} \Sigma^{m}_{i=1}log p_{model}(x^{(i)};\theta) \\
\theta_{ML} = arg max_{\theta} \Sigma^{m}_{i=1}log \frac{1}{\sqrt{2\pi}} exp(-(x-\theta)^2) \\
\theta_{ML} = arg max_{\theta} \Sigma^{m}_{i=1}log \frac{1}{\sqrt{2\pi}} +(-(x-\theta)^2) \\
\theta_{ML} = arg max_{\theta} -m log\sqrt{2\pi}-\Sigma^{m}_{i=1}(x-\theta)^2 \\
\theta_{ML} = arg max_{\theta} -\Sigma^{m}_{i=1}(x-\theta)^2 \\
\theta_{ML} = arg min_{\theta} \Sigma^{m}_{i=1}(x-\theta)^2 \\
$$



