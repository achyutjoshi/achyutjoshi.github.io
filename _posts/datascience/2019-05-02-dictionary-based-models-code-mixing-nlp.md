---
layout: post
title:  "Dictionary Based Models for Analysing Multi-Lingual Texts"
date:   2019-05-02 19:13:39
categories: datascience
comments : true

excerpt_separator: <!--more-->


---

With the increase in the accessibility of technology, language barriers have slowly started to break down. The world has started to mix these languages in order to make communication more intuitive and easy. This can very evidently be seen in multi lingual countries like India, Turkey, etc. I spent the early months of 2019 trying to understand and learn the processes to analyse such multi-lingual texts. I am planning to write a series of posts explaining my findings and learning.

<!--more-->

In the world of complex models, bag-of-words or dictionary based models are still one of the most intuitive language models one can think of. A bag-of-words model, or BoW for short, is a way of extracting features from text for use in modelling, such as with machine learning algorithms. The model is only concerned with whether known words occur in the document, not where in the document.


__What is code mixing?__

Code-Mixing or Code-Switching is a phenomenon of mixing grammatical structures of two or more languages under varied social constraints. To simplify, whenever you use more than one language in a sentence, you are code mixing. Computationally, natural language analysis has progressed exponentially in terms of mono-lingual texts. However, the research community is still finding ways to process multi-lingual texts. One of the major bottleneck is - data. When it comes to mono-lingual data, it is widely and easily available. But when it comes to code-mixed data, it is a tad bit harder to find. It becomes even more difficult for languages like Hindi that has a different script (Devnagri script) and it is transliterated into roman script when it is code mixed with English.

__Why dictionary based models?__

Dictionary based models provide a simple baseline model for such cases. The motivation behind such a model is that we create dictionaries for words of individual languages. For instance if we were analysing a potential candidate for English-Spanish code mixing, we will have two separate dictionaries of words - one for English and another for Spanish. Further, we would create a token based algorithm that compares every word with these dictionaries and returns a metric that captures the code mixing.

Surprisingly this simple method has been used in various domains within the world of Natural language processing - topic modelling, text classification, spam/hate speech detection, etc. Although with the increase in computational capabilities, the state of the art has slowly moved towards deep learning and neural nets, simple bag of words model prove to be a great way to quickly build a baseline model.

Some of the advantages of such an approach are -
1. Easy and intuitive - You exactly know what is going on inside your algorithm and why the results are accurate or not. On the other hand, neural nets and deep learning models are harder to understand.
2. Computationally easy - Since there are not many parameters to learn, they are much faster than other complex models.

Some drawbacks -
1. Need of large corpus - Unlike neural nets, such models don’t learn and adapt on their own. The model is as good as the data is.
2. Close association with rule based models - And hence models are more susceptible to human biases.
3. The independence assumption - all features about order or structure of words in the document are discarded and only mapping with the dictionary corpus is considered


__Dictionary based model in identifying Code mixing__

I worked with a specific use case of identifying code mixing in social media conversation between English and Hindi. I worked with three datasets - r/India Reddit comments from January 2017, Bollywood songs lyrics and tweets from select handles. Due to the work by [Deepthi Mave,etal](https://www.aclweb.org/anthology/W18-3206){:target="_blank"}, I could use the annotated dataset to test the performance. I also gathered various different corpuses which provided me with English & Hindi (in roman script) words. Using this dataset, I used the idea presented by [Gamback etal](http://www.lrec-conf.org/proceedings/lrec2016/pdf/669_Paper.pdf){:target="_blank"} to calculate CMI index to quantify code-mixing.

This specific post is to discuss various challenges faced while working with the specific Hindi and English words corpuses. I would be following this blog post with detailed description of the model.

1. **Tackling Transliteration and small corpus size.** In spite of the fact that Hindi has a native script, most of the Hindi social media text is transliterated. Due to lack of standardisation in transliteration, a single Hindi word can have multiple surface forms (e.g. Khushboo, Khushbu, Khushbuu etc.). Moreover, because of this, there are no exhaustive datasets available for transliterated Hindi words.

2. **Overlapping words.**
There are many words which overlaps in both languages. When 1 million most frequently used words from Google n-gram data was cross referenced with the corpus of transliterated Hindi words, there were around 5000 English words that were in the Hindi corpus. Some examples were -  rat (night), hue(happened), man(mind), is (this), etc. Moreover, among these words there were instances of words like rani, rasta, etc that has origins in Hindi however because of its common usage are considered to be english words too.

Keeping in mind the motive of identifying code mixing instances, I followed a multi-step process of creating a filtered version of these word dictionaries to tackle the above mentioned challenges.

<image height = "300em" src="/assets/images/nlp1.png"> </image>

Some key assumptions and their reasons -

1. Why removing english words occurring in Mieliestronk’s list? The list contains 58000 English words which have no words having origins from Hindi words. Since the Hindi dictionary was created using social media conversations, it had common english words like road, engineering etc.  Using this list, such words were removed.

2. In the English dictionary that was created using Google n-grams dataset, there were common Hindi-origin words that were considered to be English words (rani (queen), rasta(road), cheetah(tiger)). To get rid of such instances, all words having less frequency(number of occurrences in Google n-gram dataset) than the 50 percentile and also occurring in the Hindi dictionary were removed. The 50 percentile cutoff was chosen because other words were either proper nouns (like yahoo, usa, elizabeth etc) or single letter words (like a, i, etc).


__Further improvements__

1. Get more data - I am currently working on developing a model that transliterates devnagri script into roman literals for Hindi.
2. Further we can use phonetic similarity to tackle non-standard spellings in transliterated Hindi words.

I am also developing an open source tool [LangRazor](https://github.com/achyutjoshi/LangRazor){:target="_blank"} which eases the process of calculating such indexes. Currently it only works for bi-lingual data, but I am hoping to extend it to analyse code-mixing between more than two languages.
