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

Understanding what self attention is doesn't bring things into perspective, how self attention mechanism is utilised in various settings is something that we need to study. Let's dive in.

__Self-Attention in Sentences (or in general Linear Sequences)__ 

Consider a sentence, "John used a bat to hit a six." We can use a self-attention mechanism to find a contextual representation of each of the word in this sentence. The input to the self-attention method is a sequence of word embeddings representing the sequence of words in this sentence. Let's try to demystify, how can we obtain a contextual representation for the word "bat."

<p align="center">
  <img src="https://raw.githubusercontent.com/LearningTurtle/Blog/master/assets/images/selfattention.png">
</p>

<p align="center">
	Firstly, the word embeddings are projected into respective query, key and value triplets. The query of the word "bat" interacts with the key of each of the words (including "bat" itself) to find the relevance of "bat" with all the words in the sequence. The relevance is a single number between 0 and 1 (after the softmax operation). Usually, a weighted sum (where weights = relevances) of values corresponding to each of the words is taken to obtain the target vector. Usually the target vector is transformed using a few linear layers with activation functions to obtain the updated representation for the word "bat". This updated representation is often referred to as the contextual representation. The contextual representations are parallely calculated for each of the words in the sequence.
</p>

In summary, the input to the attention mechanism is a sequence of embeddings, one for each of the words, and the output is the contextual representation for each of the words. It is interesting to see, how the contextual representation is better than just a transformation using fully connected layers. The word "bat" can have several meanings for example the bird or as the verb to refer to the action of batting. The context however constrains the meaning to a cricket bat.

Since, sentences are a type of linear sequenes, this setting of self-attention can be easily extended to any linear sequence of feature vectors for example a sequence of image regions.

__Self-Attention for Image Features__ 

[Zhang et al.][2] used self-attention mechanism for convolutional feature maps. The following figure from the paper describes the setting.

<p align="center">
  <img src="https://raw.githubusercontent.com/LearningTurtle/Blog/master/assets/images/sagan.png">
</p>

[1]: https://learningturtle.github.io/Blog/
[2]: https://arxiv.org/pdf/1805.08318.pdf
