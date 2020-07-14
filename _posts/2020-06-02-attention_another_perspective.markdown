---
layout: post
title:  "Attention? An Other Perspective! [Part 1]"
description: An intuitive as well as mathematical explanation to attention mechanisms in machine learning.
date:   2020-06-02 15:03:36 +0530
---

Attention based mechanisms have become quite popular in the field of machine learning. From 3D-Pose Estimation to question answering attention mechanisms have been found quite useful. Let's dive right into what is attention and how has it become such a popular concept in machine learning.

"Pay attention, it's an important chapter." Ring some bells? We have always been asked to focus on the important part whether it is an examination or a speech. Similar is the concept of attention in machine learning, focussing on the important part. Let's consider a problem -- you are given the following image and asked the question "What is the color of the shirt, the person kicking the ball is wearing?"

<p align="center">
  <img width="650" height="450" src="https://raw.githubusercontent.com/LearningTurtle/Blog/master/assets/images/football.jpg">
</p>

You would realize that there are a bunch of regions in the image that are more important to put focus on to answer the question, like shown in the following image. 

<p align="center">
  <img width="850" height="600" src="https://raw.githubusercontent.com/LearningTurtle/Blog/master/assets/images/football_imp.png">
</p>

In machine learning we often think of "information" as feature vectors. For a given bunch of feature vectors, attention mechanisms allow us to determine which feature vectors are more relevant to a particular feature vector. The relevance between two vectors can be found using several methods as we later see in this blog. In the mentioned example, if $$q$$ represents the feature vector for the question and $$v_i$$ represent the feature vectors for each of the region $$i$$ in the image, the attention mechanism might help us to determine which regions are more relevant to $$q$$.

## Attention Mechanisms as Information Retrieval Methods

A database is used to store data so that search queries can be used to efficiently retrieve the information from it. For example, Arxiv is a database of articles which allows us to query over it so that we can find relevant articles.

Analogously, an image can be thought of as information-rich source (database) and the question as the query. The attention mechanism will be similar to an information retrieval method that will allow us to find out the relevant regions of the image based on the question.

### Key, Query and Value

Information in a database is often stored as the pair $$key$$, $$value$$ for example title + abstract and the article in Arxiv. Similarity or correlation between the query and each of the keys is found to determine the relevance of corresponding values. 

Taking inspiration from database management systems, the concept of key, query and values was introduced for attention mechanisms is the paper [Attention is all you need][1]. For feature vectors like that of image regions where $$key$$ and the $$value$$ can not be explicitly seen, the feature vectors are usually transformed using a fully-connected layer to obtain the $$keys$$ and the $$values$$.

<p align="center">
  <img width="750" height="370" src="https://raw.githubusercontent.com/LearningTurtle/Blog/master/assets/images/attention_information.png">
</p>

It is worth mentioning that the feature vectors are not always projected into key, query and values and are used directly sometimes. However, in this blog, we shall assume that the feature vectors are projected into key, query and values since not projecting is equivalent to learning an identity projection.

## Attention: A Mathematical View

Suppose we have $$N$$ feature vectors $$x_i \in R^d$$, $$i=1,2,..,N$$ representing each of the $$N$$ word from a sentence. Let $$k_i \in R^{d_k}$$, $$q_i \in R^{d_q}$$ and $$v_i \in R^{d_v}$$ for $$i=1,2,..,N$$ represent the corresponding key, query and value vectors which can be obtained by projecting the original feature vectors $$x$$. 

To calculate the relevance $$\alpha_{ij}$$ of the $$ith$$ query vector with $$jth$$ key vector,

$$\alpha_{ij} = f(q_i, k_j)$$

Where $$f$$ is a function used to determine the relevance between two vectors as we discuss later in this blog. To determine the relative importances of key vectors for the $$ith$$ query vector, softmax function can be used.

$$\alpha_i = \left[\alpha_{ij}\right], \forall i \in \{1,2,..,N\}$$

$$\alpha_i = \mathbf{softmax}(\alpha_i)$$

Thus, $$\alpha_{i}$$ is a vector of $$N$$ numbers $$\alpha_{ij}$$, for $$j=1,2,..,N$$ all between 0 and 1 such that $$\sum_{j=1}^{N} \alpha_{ij} = 1$$. Once we have a single number representing the importance of each of the feature vectors, we can use the weighted sum of all the vectors to obtain a target vector. We shall overview different strategies as to how this target vector is obtained and used later in this blog.



## Determining Relevance

The first step to attending to a bunch of vectors based on a vector is to find the relevance between two vectors. Two of the most popular approaches to find the relevance are __Additive Attention__ and __Dot Product Attention__. Let's see it in a little more detail.

### Additive Attention

First introduced in [Learning to Align and Translate][2], the additive attention mechanism utilises the fact that the neural networks are good function approximators. It uses a single feedforward layer to compute a relevance score.

$$\alpha_{ij} = W^T(\tanh(q_i + k_j))$$

where $$d_q = d_k$$ and $$W \in R^{d_k}$$. A simple variation of this additive attention is to replace the addition operation by concatenation.

$$\alpha_{ij} = W^T(\tanh([q_i ; k_j]))$$

### Dot Product Attention

Dot product attention was first introduced in [Effective approaches to attention-based neural machine translation][3]. The intuition for the dot product based attention comes from the fact that a dot product geometrically represents cosine similarity while also taking in account the magnitude of the vectors. The relevance score between $$ith$$ query and $$jth$$ key using dot product attention can be written as, 

$$\alpha_{ij} = q_i \cdot k_j$$

where $$d_q = d_k$$. Vaswani et. al in [Attention is all you need][1] proposed a variant of it called the scaled dot product attention. They introduced a scaling factor to prevent softmax from reaching to the regions where gradients are extremely small when the dot product increases.

$$\alpha_{ij} = \frac{q_i \cdot k_j}{\sqrt{d_k}}$$



[1]: https://papers.nips.cc/paper/7181-attention-is-all-you-need.pdf
[2]: https://arxiv.org/abs/1409.0473
[3]: https://arxiv.org/pdf/1508.04025.pdf
