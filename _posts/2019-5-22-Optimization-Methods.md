---
layout: post
title: Some popular Gradient-based Optimization Methods
---

Gradient descent is use to optimize deep learning model. In the following, we will outline some methods that are widely used in model training.

### SGD

$$
\theta_{t+1} = \theta_{t} - \eta \cdot \nabla_{\theta} J\left(\theta_{t}\right)
$$

#### Momentum

$$ 
\begin{aligned} v_{t} &=\gamma v_{t-1} + \eta \nabla_{\theta}J(\theta_{t}) \\ 
\theta_{t+1} &=\theta_{t} -v_{t} \end{aligned}
$$

The momentum term $$ \gamma $$ is usually set to 0.9.


#### Nesterov Accelerated Gradient

$$
\begin{aligned} v_{t} &=\gamma v_{t-1}+\eta \nabla_{\theta} J\left(\theta_{t}-\gamma v_{t-1}\right) \\
\theta_{t+1} &=\theta_{t} - v_{t} \end{aligned}
$$

Ref: [On the importance of initialization and momentum in deep learning](http://www.cs.toronto.edu/~hinton/absps/momentum.pdf).


### Adagrad

$$
\begin{aligned} g_{t,i} &=\nabla_{\theta} J\left(\theta_{t,i}\right) \\
\theta_{t+1,i} &=\theta_{t,i}-\frac{\eta}{\sqrt{\sum_{t=1}^t{g_{t,i}^2}+\epsilon}} g_{t,i} \end{aligned}
$$

Ref: [Adaptive Subgradient Methods for Online Learning and Stochastic Optimization](http://www.jmlr.org/papers/volume12/duchi11a.html).

### Adadelta

use $$ R M S[\Delta \theta]_{t-1} $$ to approximate $$ \Delta_{t} $$, multiply $$ \Delta_{t} $$ to correct units.

$$
\begin{aligned} E\left[\Delta \theta^{2}\right]_{t} &=\gamma E\left[\Delta \theta^{2}\right]_{t-1}+(1-\gamma) \Delta \theta_{t}^{2} \\
R M S[\Delta \theta]_{t} &=\sqrt{E\left[\Delta \theta^{2}\right]_{t}+\epsilon} \\
\theta_{t+1} &=\theta_{t}- \frac{R M S[\Delta \theta]_{t-1}}{R M S[g]_{t}} g_{t} \end{aligned}
$$

Ref: [ADADELTA: An Adaptive Learning Rate Method](https://arxiv.org/abs/1212.5701).


### RMSprop

$$
\begin{aligned} E\left[g^{2}\right]_{t} &=\gamma E\left[g^{2}\right]_{t-1}+\left(1-\gamma \right) g_{t}^{2} \\ 
\theta_{t+1} &=\theta_{t}-\frac{\eta}{\sqrt{E\left[g^{2}\right]_{t}+\epsilon}} g_{t} \end{aligned}
$$

Ref: [G.Hinton's course](http://www.cs.toronto.edu/~tijmen/csc321/slides/lecture_slides_lec6.pdf).


### Adam

$$
\begin{aligned} m_{t} &=\beta_{1} m_{t-1}+\left(1-\beta_{1}\right) g_{t} \\ v_{t} &=\beta_{2} v_{t-1}+\left(1-\beta_{2}\right) g_{t}^{2} \\
\hat{m}_{t} &=\frac{m_{t}}{1-\beta_{1}^{t}} \\ \hat{v}_{t} &=\frac{v_{t}}{1-\beta_{2}^{t}} \\
\theta_{t+1} &=\theta_{t}-\frac{\eta}{\sqrt{\hat{v}_{t}}+\epsilon} \hat{m}_{t} \end{aligned}
$$

Ref: [Adam: A Method for Stochastic Optimization](https://arxiv.org/abs/1412.6980).

#### *External links*
* [An overview of gradient descent optimization algorithms](http://ruder.io/optimizing-gradient-descent/index.html#gradientdescentvariants)

<br>