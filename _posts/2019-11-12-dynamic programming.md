---
title:  "Dynamic Programming"
---

> Markov decision process is a convenient and formal environment for reinforcement learning and dynamic promming is the only general approach for solving this kind of problems, and even when it is computationally prohibitive, it can serve as the basis for more practical suboptimal approaches.

{: class="table-of-content"}
* TOC
{:toc}


# Markov Decision Process

It is natural to understand MDP by proceeding the definition in the order of **Markov Process**, followed by **Markov Reward Process**, and finally the **Markov Decision Process**. 

## Markov Process

A **Markov process** is defined as a tuple $$(\mathcal{S},\mathbf{P})$$, where $$\mathcal{S}$$ is the state space and $$\mathbf{P}$$ is the transintion probability. We make two additional assumptions that are very common in the reinforcement learning (RL) setting:

* *Finite state space:* we denote the state space by $$\mathcal{S}=\{s_1,s_2,\dots,s_n\}$$, therefore, $$\vert\mathcal{S}\vert<\infty$$
* *Stationary transition probabilities:* the transition probabilities are time independent. Mathematically, this means:

$$P(S_2=s'\vert S_1=s)=P(S_{t+1}=s'\mid S_t=s),\qquad\forall s, s'\in\mathcal{S},\qquad\forall t=1, 2, \dots$$

These two additional assumptions leadto a nice characterization of the transition dynamics in terms of *transition probability matrix* $$\mathbf{P}$$ of size $$\vert\mathcal{S}\vert\times\vert\mathcal{S}\vert$$, whose $$(i,j)$$ entry is given by $$\mathbf{P}_{ij}=P(S_{t+1}=s_j\vert S_t=s_i)$$.

## Markov Reward Process

A **Markov reward process** is defined as a tuple $$(\mathcal{S},\mathbf{P},\textcolor{red}{\mathscr{R}},\textcolor{red}{\gamma})$$, where $$\mathscr{R}$$ is a reward funcition that maps states to rewards, i.e. $$\mathscr{R}:\mathcal{S}\to\mathbb{R}$$ and $$\gamma$$ is discount factor between $$0$$ and $$1$$. In Markov reward process, whenever a transition happens from a current state $$s$$ to a successor state $$s'$$, a reward is obtained depending on the current state $$s$$. The reward can be either deterministic or stochastic. If stochastic, tt can be a random variable or even depend on the successor state $$s'$$ and $$R(s)$$ is regraded as the expected reward conditioning on the current state $$s$$. The expectation takes on both the distribution of the random variable and the transition probability on the current state. We assume that the reward is also stationary, i.e. it is also a function of the current state and don't depend on time-step $$t$$.

The return $$G_t$$ is the total discounted reward from time-step $$t$$:

$$G_t\doteq R_{t+1}+\gamma R_{t+2}+\dots=\sum_{k=t+1}^\infty\gamma^{k-t-1}R_k$$

The discount factor $$\gamma\in[0,1)$$ plays two roles: mathematically, it guarantees the return is finite; biologically, humans are impatient or face unvertainty in the future. I want to emphasis here that $$R_t$$ may not be the same as the real realization of the reward if it is stochastic. It is a prior expectation conditioning on the current state. Note that $$G_t$$ is a random variable and its value depends on the realization of the trajectory $$(s_t, s_{t+1},s_{t+2}, \dots)$$. Now we define the value function $$v(s)$$ as the expected return starting from state $$s$$:

$$v(s)\doteq\mathbb{E}[G_t\vert S_t=s]$$

Let $$\mathbf{R}$$ denote a vector of size $$\vert\mathcal{S}\vert\times1$$ whose $$i$$th elemet is $$R(s_i)$$ and $$\mathbf{v}$$ a vector of size $$\vert\mathcal{S}\vert\times1$$ whose $$i$$th elemet is $$v(s_i)$$. Then the value function can be expressed explicitly as:

$$\begin{aligned}\mathbf{v}&=\mathbf{R}+\gamma\mathbf{PR}+\gamma^2\mathbf{P^2R}+\dots\\&=(\mathbf{I}+\gamma\mathbf{P}+\gamma^2\mathbf{P^2+\dots)\mathbf{R}}\\&=(\mathbf{I}-\gamma\mathbf{P})^{-1}\mathbf{R}\end{aligned}$$

This last equality comes from the *Neumann series*, it can be regarded as a matrix version of the *geometric series*. Similar to geometric series, it holds when $$\Vert\gamma\mathbf{P}\Vert<1$$, which is true. Since $$\mathbf{P}$$ is a transition matrix, so as $$\mathbf{P^t}$$, and each row of a transitin matrix sums to $$1$$. From the second equlity above one can tell that the summation of each row of the matrix $$(\mathbf{I}-\gamma\mathbf{P})^{-1}$$ equals $$\frac{1}{1-\gamma}$$. Hence the value function can be regraded as a weighted discounted summation of the rewards and the weight is the frequency the state appears.

Another way to derive this result is using the recursive formula. The value function can be expressed recursively:

$$v(s)=R(s)+\gamma\sum_{s'}P(s'\vert s)v(s')$$

if written in the matrix form

$$\mathbf{v}=\mathbf{R}+\gamma\mathbf{Pv}$$

and we obtain the same result. 


## Markov Decision Process
A **Markov decision process** is defined as a tuple $$(\mathcal{S},\textcolor{red}{\mathcal{A}},\mathbf{P},\mathscr{R},\gamma)$$, where $$\mathcal{A}$$ is the action space. Compared with the Markov reward process, there are two main changes with respect to the action $$a$$. First, the reward function depend on not only the current state, but also the action, $$\mathscr{R}:\mathcal{S}\times\mathcal{A}\to\mathbb{R}$$. Second, the transition probability is also affected by the action, $$P(S_{t+1}=s'\vert S_t=s,A_t=a)$$. As that in the Markov reward process, the real reward can also depend on the next state $$s'$$, and we still define $$R(s,a)$$ as the expected reward conditioning on the current state $$s$$ and action $$a$$. The popular Sutton & Barto (2018) textbook defines the transition probability as the joint distribution $$P(s',r\vert s,a)$$, since taking expectation is a linear operator, these two kinds of definition are equivalent. The information in the joint distribution of $$(s',r)$$ is unnecessary and only the marginal distribution matters. [I'm curious about that if the return is not defined as the discounted summation of the reward but some other forms, say, the cumulative multiplication, the information in the joint distribution of $$(s',r)$$ can matter. Generally, $$\mathbb{E}[XY]\neq\mathbb{E}[X]\mathbb{E}[Y]$$.]

<center>
![Illustration of a reinforcement learning problem](/images/RL_illustration.png){:height="50%" width="50%"}
<\center>

**Figure 1. An agent interacts with the environment, trying to take smart actions to maximize cumulative rewards.**

aa
Policy is a function  open loop and closed loop


## Three Tpyes of Markov Decision Process

## Stationary Distribution and Discounted Stationary Distribution

# Dynamic Programming

## Value Iteration


$$V(s)=\max_a\enspace\sum_a\pi(a\vert s)\left[r(s,a)+\gamma\sum_{s'}P(s'\vert s, a)V(s')\right]$$

$$Q(s,a)=\sum_a\pi(a\vert s)\left[r(s,a)+\gamma\sum_{s'}P(s'\vert s, a)\max_{a'}Q(s',a')\right]$$

## Policy Iteration

Although we have the analytic solution for the value function, the computation of the inverse matrix is very expensive, which is $$\mathcal{O}(\vert\mathcal{S}\vert^3)$$. Usually an iterative algorithm is implemented. 

$$V(s)=\enspace\sum_a\pi(a\vert s)\left[r(s,a)+\gamma\sum_{s'}P(s'\vert s, a)V(s')\right]$$

$$Q(s,a)=\sum_a\pi(a\vert s)\left[r(s,a)+\gamma\sum_{s'}P(s'\vert s, a)Q(s',a')\right]$$

## Policy Improvement Theorem



* One policy gradient step does not maximize the objective thoroughly. With improper learning rate, the policy gradient step may be harmful.

## Generalized Policy Iteration
whether this is good

### Value function and action-value function (Q-function)

policy iteration ==> SARSA ==> Actor-Critic
value iteration ==> Q-learning ==> DQN

### value iteration
splitting $$I-\lambda P$$ as $$I-\lambda P = Q_d-R_d$$, then $$v^{n+1}=Q_d^{-1}(R_dv^n+r_d)$$:
* Gauss-Seidel
* Jacobi

over-relaxation and inder-relaxation $$v^{n+1}=v^n+\omega\left[\max_{d\in D}\{Q_d^{-1}(R_dv^n+r_d)\}-v^n\right]$$

policy iteration and modified policy iteration

multistep lookahead

## Value Function Can Decrease in  GPI

# References

[1] Richard S. Sutton and Andrew G. Barto. [Reinforcement Learning: An Introduction; 2nd Edition](http://incompleteideas.net/book/the-book.html). 2018.