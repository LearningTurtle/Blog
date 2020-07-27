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

Self and Cross are loosely defined terms to associated to the attention mechanisms when the query and the key, value pair are obtained from the same and different "sources" respectively.

### Self-Attention: An Overview

<p align="center">
  <img src="https://raw.githubusercontent.com/LearningTurtle/Blog/master/assets/images/selfattention_diag.png">
</p>

Let's say we have a bunch of feature vectors to represent an entity such as a sentence or an image. Self-attention can be thought of as making each of the feature vectors in this bunch "aware" of the others. The representation of each input feature vector obtained after a self-attention mechanism applied on the inputs can be termed as the contextual representation of the input.


### Self-Attention in Different Settings

Understanding what self attention is doesn't bring things into perspective, how self attention mechanism is utilised in various settings is something that we need to study. Let's dive in.

__Self-Attention in Sentences__ 

Consider a sentence, "John used a bat to hit a six." We can use a self-attention mechanism to find a contextual representation of each of the word in this sentence. The input to the self-attention method is a sequence of word embeddings representing the sequence of words in this sentence. Let's try to demystify, how can we obtain a contextual representation for the word "bat."

<p align="center">
  <img src="https://raw.githubusercontent.com/LearningTurtle/Blog/master/assets/images/selfattention.png">
</p>

Firstly, the word embeddings are projected into respective query, key and value triplets. The projection matrices are shared across words, allowing sequences of varying lengths. The query of the word *bat* interacts with the key of each of the words (including *bat* itself) to find the relevance of *bat* with all the words in the sequence. The relevance is a single number between 0 and 1 (after the softmax operation). Usually, a weighted sum (where weights = relevances) of values corresponding to each of the words is taken to obtain the target vector, and the target vector is transformed using a few linear layers with activation functions to obtain the updated representation for the word *bat*. This updated representation is often referred to as the contextual representation. The contextual representations are parallely calculated for each of the words in the sequence.

In summary, the input to the attention mechanism is a sequence of embeddings, one for each of the words, and the output is the contextual representation for each of the words. It is interesting to see, how the contextual representation is better than just a transformation using fully connected layers. The word *bat* can have several meanings for example the bird or as the verb to refer to the action of batting. The context however constrains the meaning to a cricket bat.

__Self-Attention for Image Features__ 

[Zhang et al.][2] used self-attention mechanism for convolutional feature maps. The following figure from the paper describes the setting.

<p align="center">
  <img src="https://raw.githubusercontent.com/LearningTurtle/Blog/master/assets/images/sagan.png">
</p>

In this case, the linear sequence comprises of multiple feature maps. Each feature map in this sequence is analogous to a word in the sentence from the previous example. Each feature map is then projected into its corresponding query, key and value. $$1 \times 1$$ convolution filters are used to project the feature map into query, key and value in order to retain the 2D structure of the feature map.

Mathematically, for an input sequence of feature map, $$\mathbb{x}$$

$$\textbf{key:	} f(\mathbb{x}) = \mathbb{W}_f\mathbb{x}$$

$$\textbf{query:	} g(\mathbb{x}) = \mathbb{W}_g\mathbb{x}$$

$$\textbf{value:	} h(\mathbb{x}) = \mathbb{W}_h\mathbb{x}$$

Similar to the case of sentences, the convolution filters used for projection into query, key and value triplets are shared across feature maps. This allows attention mechanisms to handle input feature maps of varying depths. Next, the dot product of query and key is take to determine the relevance scores which collectively are often referred to as the attention maps.

$$\alpha_{i,j} = \mathrm{softmax}(f(x_i)^Tg(x_j))$$

$$o_j = \mathbb{W}_v\left(\displaystyle\sum_{i=1}^{N}\alpha_{i,j}h(x_i)\right)$$


### Cross-Attention: An Overview



[1]: https://learningturtle.github.io/Blog/
[2]: https://arxiv.org/pdf/1805.08318.pdf
