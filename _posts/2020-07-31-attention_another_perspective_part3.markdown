---
layout: post
title:  "Attention? An Other Perspective! [Part 3]"
description: An explanation of soft and hard attention mechanisms.
date:   2020-07-31 15:03:36 +0530
categories: [Soft Attention, Hard Attention]
author: Nikhil Shah
---

In the [previous part][4] of this blog series, we looked into the details of self and cross attention mechanisms. We discussed how these attention mechanisms are utilised in various settings. In the examples that we discussed earlier, we have used weighted average to calculate the target vector from a sequence of feature vectors (values) and their corresponding relevance scores. But, is that the only way to calculate the target vector? If there is another method then is it better? We try to find out the answers to these questions in this blog.

## Target vector calculation

Suppose in an attention procedure, we have obtained the relevance scores $$\alpha_1, \alpha_2,...,\alpha_N$$ for $$N$$ feature vectors, $$v_1, v_2,...,v_N$$. The task is to find the target vector $$z$$ using a function $$f$$ which takes in input these relevance scores and feature vectors.

$$z = f(\mathbf{\alpha}, \mathbf{v})$$

To mathematically formulate this problem, we create a [multinoulli distribution][1] parametrized by $$\alpha$$. A point sampled from this distribution is an $$N$$ dimensional vector $$s$$ containing exactly one 1 and rest 0 values, such that

$$p(s_i = 1 | \mathbf{v}) = \alpha_i$$

where the dimension $$i$$ which contains the value 1 indicates that the feature vector $$v_i$$ is relevant to the query. A random variable $$\hat{z}$$ can be constructed as

$$\hat{z} = \displaystyle\sum_{i=1}^{N}s_iv_i$$

Our task is to find the value $$z$$ of this random variable that minimizes the overall loss function. We mention two ways to find $$z$$ during the forward pass and briefly look at how these methods are optimized during backpropogation.

## Soft-Attention

<p align="center">
  <img src="https://raw.githubusercontent.com/LearningTurtle/Blog/master/assets/images/softattention.png">
</p>

First introduced in [Bahdanau et al. (2014)][2], this approach treats the relevance scores as the relative importances. The target vector is calculated as the weighted sum of the feature vectors.

$$z = \displaystyle\sum_{i=1}^{N}\alpha_i v_i$$

If you look closely, $$z$$ is actually the expectation of the random variable $$\hat{z}$$. Expectation (or mean) is a popular statistic used to represent a distribution which makes it a considerable choice to estimate the target vector.

Since a weighted sum is a deterministic, continuous and differentiable operation, it is easy to optimize using standard backpropagation techniques.

## Hard-Attention

Introduced in [Xu et al. (2015)][3], hard attention replaces the deterministic method to calculate target vector with a stochastic sampling method. It treats the relevance scores as the sample rates to pick one of the input features, $$v_i$$ as the target vector.

<p align="center">
  <img src="https://raw.githubusercontent.com/LearningTurtle/Blog/master/assets/images/hardattention.png">
</p>

Stochastic sampling is not deterministic and hence not a differentiable operation. To optimize this method using backpropogation, a Monte Carlo based sampling approximation of gradients with respect to the overall loss is used. 

## Which one to use?

Experiments performed in [Xu et al. (2015)][3] demonstrate that hard-attention performs slightly better than soft-attention on certain tasks. On the other hand, soft-attention is relatively very easy to implement and optimize when compared to hard-attention which makes it more popular.

## References

1. [Bahdanau, D., Cho, K., & Bengio, Y. (2014). Neural Machine Translation by Jointly Learning to Align and TranslatearXiv e-prints, arXiv:1409.0473.][2]

2. [Xu, K., Ba, J., Kiros, R., Cho, A., Salakhutdinov, R., & Zemel, Y. (2015). Show, Attend and Tell: Neural Image Caption Generation with Visual AttentionarXiv e-prints, arXiv:1502.03044.][3]

---

### Cited as:

```bibtex
@article{nikhil_attention,
	title={Attention! An Other Perspective},
	url={https://learningturtle.github.io/Blog/posts/attention_another_perspective_part3/},
	journal={Learning Turtle},
	author={Nikhil},
	year={2020}
}
```
### Postscript

If you find any mistakes/complicacies in our blogs or if you have any suggestions/feedback, do not hesitate to contact us at [learningturtle.yt@gmail.com](mailto:learningturtle.yt@gmail.com).


[1]: https://en.wikipedia.org/wiki/Categorical_distribution
[2]: https://arxiv.org/abs/1409.0473
[3]: https://arxiv.org/abs/1502.03044
[4]: https://learningturtle.github.io/Blog/posts/attention_another_perspective_part2/
