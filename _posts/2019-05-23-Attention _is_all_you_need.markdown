---
layout: post
title:  "Attention? An Intuitive Explanation"
date:   2020-06-02 15:03:36 +0530
---

Attention based mechanisms have become quite popular in the field of machine learning. From 3D-Pose Estimation to question answering attention mechanisms have been found quite useful. Let's dive right into what is attention and how has it become such a popular concept in machine learning.

"Pay attention, it's an important chapter." Ring some bells? We have always been asked to focus on the important part whether it is an examination or a speech. Similar is the concept of attention in machine learning, focussing on the important part. Let's consider a problem -- you are given the following image and asked the question "What is the color of the shirt, the person kicking the ball is wearing?"

<p align="center">
  <img width="650" height="450" src="https://raw.githubusercontent.com/LearningTurtle/Blog/master/assets/images/football.jpg">
</p>

You would realize that there are a bunch of regions in the image that are more important to put focus on to answer the question, like shown in the following image. 

<p align="center">
  <img width="850" height="600" src="https://raw.githubusercontent.com/LearningTurtle/Blog/master/assets/images/football_imp.jpg">
</p>

In machine learning we often think of "information" as feature vectors. For a given bunch of feature vectors, attention mechanisms allow us to determine which feature vectors are more relevant to a particular feature vector. The relevance between two vectors can be found using several methods as we later see in this blog. In the mentioned example, if $$q$$ represents the feature vector for the question and $$v_i$$ represent the feature vectors for each of the region $$i$$ in the image, the attention mechanism might help us to determine which regions are more relevant to $$q$$.

## Attention Mechanisms as Information Retrieval Methods

A database is used to store data so that search queries can be used to efficiently retrieve the information from it. For example, Arxiv is a database of articles which allows us to query over it so that we can find relevant articles.

Analogously, an image can be thought of as information-rich source (database) and the question as the query. The attention mechanism will be similar to an information retrieval method that will allow us to find out the relevant regions of the image based on the question.
