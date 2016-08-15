---
layout: post
title:  "One Hot Encoding in Data Science"
date:   2016-08-14 19:13:39
categories: datascience
excerpt_separator: <!--more-->


---

I consider myself a newbie for the data analysis world. What I have understood so far is that data preparation is the most important step while solving any problem. Each predictive  model requires a certain type of data and in a certain way. For instance, tree based boosting models like xgboost require all the feature variables to be numeric. While solving the San Francisco Crime Classification problem on Kaggle, I stumbled upon different ways to handle categorical variables. One of the method to convert a categorical input variable into a continuous one is One Hot Encoding/ Dummy coding.

<!--more-->

Many a times we have categorical variables with many levels. For example in the SF Crime Classification problem, there were 39 different levels of crime. Now many learning algorithms either learn a single weight per feature, or they use distances between samples. In both cases having a categorical variable with more levels will decrease the accuracy of the model. Let us look into both cases.

__Linear Model__ :

Suppose you have a dataset having only a single categorical feature "colour", with values "Blue", "Green" and "Red". Assume, that these are encoded as 0, 1 and 2. You then have a weight w for this feature in a linear classifier, which will make some kind of decision based on the constraint w×x + b > 0, or equivalently w×x < b.

The problem now is that the weight w cannot encode a three-way choice. The three possible values of w×x are 0, w and 2×w. Either these three all lead to the same decision (they're all < b or ≥b) or "Blue" and "Green" lead to the same decision, or "Green" and "Red" give the same decision. There's no possibility for the model to learn that "Blue" and "Red" should be given the same label, with "French" the odd one out.

Dummy coding will convert this colour feature into three features – ‘isgreen’ ‘isred’ and ‘isblue. By this, we effectively blow up the feature space to three features, which will each get their own weights, so the decision function is now w[Blue]x[Blue] + w[Green]x[Green] + w[Red]x[Red] < b, where all the x's are booleans. This easily caters the problem we were having before.

__Distance-Based__ :

Similarly, any learner based on standard distance metrics (such as k-nearest neighbors) between samples will get confused without one-hot encoding. With the naive encoding and Euclidean distance, the distance between Green and Red is 1. The distance between Red and Blue is 2. But with the one-hot encoding, the pairwise distances between [1, 0, 0], [0, 1, 0] and [0, 0, 1] are all equal to √2.

However, this is not true for all models. Decision trees and derived models such as random forests, if deep enough, can handle categorical variables without one-hot encoding.


__Other Methods used for Encoding__ – 

1.	Ordinal Coding – Assign Numbers to each categories
2.	Binary: first the categories are encoded as ordinal, then those integers are converted into binary code, then the digits from that binary string are split into separate columns.  This encodes the data in fewer dimensions that one-hot, but with some distortion of the distances.



References: Quora & Analytics Vidya

