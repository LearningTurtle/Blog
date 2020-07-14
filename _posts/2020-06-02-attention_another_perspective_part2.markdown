---
layout: post
title:  "Attention? An Other Perspective! [Part 2]"
description: Categorisation of attention mechanisms and explanation of self and cross attention mechanisms.
date:   2020-06-03 15:03:36 +0530
---

In the [previous part][1] of this series, we looked at an intuitive explanation of attention mechanisms and how to determine relevance between two feature vectors. Next, we classify attention mechanisms and study the types in detail. 

## Categorisation of Attention

<p align="center">
  <img width="750" height="370" src="https://raw.githubusercontent.com/LearningTurtle/Blog/master/assets/images/attention_categorisation.png">
</p>

## Self-Attention and Cross-Attention

Self and Cross are loosely defined terms to associate to attention mechanisms when the query and the key, value pair are obtained from the same and different "sources" respectively.

Let's say we have a bunch of feature vectors to represent an entity such as a sentence or an image. Self-attention can be thought of as making each of the feature vectors in this bunch "aware" of the others. The representation of each input feature vector obtained after a self-attention mechanism applied on the inputs can be termed as the contextual representation of the input.

<p align="center">
  <img src="https://raw.githubusercontent.com/LearningTurtle/Blog/master/assets/images/selfattention.gif">
</p>
<p align="center">
  Demonstration of self attention mechanism. <a href="https://ai.googleblog.com/2017/08/transformer-novel-neural-network.html">GIF Source</a>
</p>

In cases like that of the image and the question, where we wish to find the relevant parts of the image based on the question, the key, value pair (from image) and the query (from question) are obtained from different sources, and the corresponding attention mechanism is called cross-attention.

### Self-Attention in Different Settings

[1]: https://learningturtle.github.io/Blog/
