---
layout: post_math
title:  "Machine Learning Takeaways - Following the Feynman Learning Technique"
date:   2019-05-05 19:13:39
categories: datascience
comments : true

excerpt_separator: <!--more-->


---

Many would reckon that Machine Learning is now the new oil these days. And I would most likely support that. Personally I got exposed to the world of ML in my undergrad days but it had always remained a black box for me. One of the major motivation of joining a Masters program was my intent to peep into this black box.

I signed up for this course called Computational Data Analysis(CSE6740) offered by Prof. Negar Kivyansh. Every lecture I attended, I had this eureka moment where I understood the why behind a particular method. This blog (or blog series) is my attempt to follow the Feynman Learning Technique. So lets see if that works!

<!--more-->


Important Caveat : I am assuming that the reader knows the basics of Machine Learning and have some (minimal) exposure to working with data.


__What are we trying to do in Machine Learning?__

In a very overarching way, we are basically extracting different relationships from the data using mathematical & statistical rules. Everyone loves to divide machine learning into two big paradigms - Supervised and Unsupervised learning.

Lets assume you are a store manager and want to do apply machine learning to improve the money you earn every day. Understand the two problem statements carefully -

1. You want to have an estimate on the amount you shall earn this quarter so that you can understand the amount you need to invest in the business from your savings.
2. You want to understand different customer behaviour and how you can best satisfy their buying needs, which indirectly increases your revenue

The first one is supposed to be Supervised while the later is supposed to be Unsupervised. While there are no hard margins for methods to solve these two problem statements, their only purpose here is to differentiate between the two paradigms. A supervised learning will always have a target variable (ie. something to predict or classify). Like in our case, we want to estimate quarterly earning. While unsupervised learning can be thought as an exploratory algorithm to group or rank the datasets. We shall be focusing on supervised learning for this blog.

__Paradigms within Supervised Learning__

There are different paradigms within Supervised Learning -

1. Empirical or close-form solution based models - eg: Linear Regression
2. Probabilistic Approach - world of General Linear Models
3. Distance/Margin based - Support Vectors and corresponding kernel methods
4. Neuron based - Neural networks and the world of Deep Learning


__Essence of the Probabilistic Approach in Machine Learning__

It is all about maximising $$P(y ~\vert X)$$. If you understand conditional probability, you will realise that this statement is equivalent to saying - probability of y given X. If you closely understand any of the probabilistic algorithm, all we are trying to do is finding the $$ P(y ~\vert X, ~\theta)$$ or $$ P(y ~\vert X; ~\theta)$$. Since most approaches seldom have a closed form solution, probabilistic view is one of the most common ways of understanding the heuristics.

Now let me prove my point by seeing some of the most common models -

1. Linear Regression - Here $$P(y ~\vert X ; ~\theta)$$ is assumed to be normally distributed which leads to the formulation of the likelihood function
2. Logistic Regression - Here we use a transformation function to map all the y’s between [0,1) and yet the essence remains the same. We still are maximising $$P(y \vert X ; \theta)$$ which is in the form - $$P(y \vert X ; \theta) = (h_\theta(x))^y(h_\theta(x))^{1-y}$$            

3. General Linear Model - It is a much general version of linear regression where $$P(y ~\vert X ; ~\theta)$$ can be any probability distribution. For instance, it can be a poisson distribution.

__Every Algorithm has an optimisation element__

In essence the goal of the process it to achieve the best configurations(read parameter values) which are learnt from the data. So how do we define “best”? We usually develop a loss function or the likelihood function. We generally want to minimise the loss function or maximise the likelihood function.

For instance -

1. General linear regression has a loss term associated within. (the most commonly used is the RMSE $$(y - \hat{y})^2$$).
2. Logistic regression has a probabilistic view point and hence it has a maximisation of likelihood.
3. Support Vector Machines - We maximise the margins between the support vectors
4. Decision Trees and Random Forests - You find the best parameter/subset of parameter to branch on. Here the “best” is defined by indexes like gini impurity or information gain.

For anyone who has studied advanced optimisation knows that they are really nasty. There are numerous assumptions that go behind making a function computationally possible to optimise. And inspite of these assumptions, many complex models cannot be optimised and hence heuristics like sampling or vartional inference are used. Even feature selection as a different stage of data science has optimisation involved.

My two cents - before diving into the fancy stuff of machine learning and deep learning, take one advanced course on optimisation. Even though you won’t remember much and you won’t directly be involved in optimisation, you will learn to appreciate the complexity of the problem at hand.


__Difference between Decision function and Modeling Function__

In case of probabilistic models, lets say we somehow approximate $$P(y \vert X)$$, what next?  In the case of linear regression it is straight forward, because what we get from maximising $$P(y \vert X)$$ are values of the parameters. So we simply have to plug the new $$X$$ in that equation.

However in case of logistic regression we need one more step to decide the label. That is, $$argmax_{y} P(y \vert X)$$. Which means, for which label is this probability maximum. And label the new data point as that particular label. The following figure will give you a better perspective of the differences that exists between the two.

The model fitting section is popularly known as training. There are various different ways to learn such a function - parametric(linear regression, logistic regression, etc) or non-parametric.

<image height = "200em" src="/assets/images/ml2.png"> </image>


__Generative Learning vs Discriminative Learning__

As shown above, within the class of functions in the modelling part, there are two types of approaches that can be done - Generative and Discriminative  -

1. A Generative model learns the joing probability distribution $$P(X,y)$$. It predicts the conditional probability with the help of Bayes Theorem.
2. A Discriminative model learns the conditional probability distribution ($$P(y \vert X)$$)

Again, to make a very clear distinction, the above two approaches are a part of the Modelling section. Once we use either of these to calculate $$P(y \vert X)$$, we will use the decision rule for prediction. I found the example mentioned in Andrew Ng’s paper very intuitive. One can refer [his paper](https://ai.stanford.edu/~ang/papers/nips01-discriminativegenerative.pdf){:target = "_blank"} to read through a worked out example.

One key difference to note here is that a generative algorithm is a much stronger modelling because once we know $$P(X,y)$$, we can theoretically generate the data. While in a discriminative model, we only learn the conditional probability from the data. A very intuitive example -  Suppose we are trying to learn how to differentiate between Chinese and Korean. If we end up learning all the syntaxes and grammars, we are taking a generative approach. While if we end up learning certain patterns about what words belong to each language, we are taking a discriminative approach.








__Links__

1. [Prof. Negar Kivyansh](https://sites.google.com/site/negarkiyavash/){:target="_blank"}
2. [Feynman Learning Technique](https://fs.blog/2012/04/feynman-technique/){:target= "_blank"}
