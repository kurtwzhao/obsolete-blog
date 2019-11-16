---
title:  "Dynamic Programming"
---

> Markov decision process is a convenient and formal environment for reinforcement learning and dynamic promming is the only general approach for solving this kind of problems, and even when it is computationally prohibitive, it can serve as the basis for more practical suboptimal approachs.

{: class="table-of-content"}
* TOC
{:toc}


# Markov Decision Process (MDP)

It is natural to understand MDP by proceeding the definition in the order of **Markov Process (MP)**, followed by **Markov Reward Process (MRP)**, and finally the **Markov Decision Process (MDP)**. 

## Markov Process

A **Markov process** is defined as a tuple $$(\mathcal{S},\mathbf{P})$$, where $$\mathcal{S}$$ is the state space and $$\mathbf{P}$$ is the transintion probability. We make two additional assumptions that are very common in the reinforcement learning (RL) setting:

* *Finite state space:* we denote the state space by $$\mathcal{S}=\{s_1,s_2,\dots,s_n\}$$, therefore, $$\vert\mathcal{S}\vert<\infty$$
* *Stationary transition probabilities:* the transition probabilities are time independent. Mathematically, this means:

$$P(S_2=s'\vert S_1=s)=P(S_{t+1}=s'\mid S_t=s),\qquad\forall s, s'\in\mathcal{S},\qquad\forall t=1, 2, \dots$$

These two additional assumptions leadto a nice characterization of the transition dynamics in terms of *transition probability matrix* $$\mathbf{P}$$ of size $$\vert\mathcal{S}\vert\times\vert\mathcal{S}\vert$$, whose $$(i,j)$$ entry is given by $$\mathbf{P}_{ij}=P(S_{t+1}=s_j\vert S_t=s_i)$$.

## Markov Reward Process

A **Markov reward process** is defined as a tuple $$(\mathcal{S},\mathbf{P},\textcolor{red}{\mathscr{R}},\textcolor{red}{\gamma})$$, where $$\mathscr{R}$$ is a reward funcition that maps states to rewards, i.e. $$\mathscr{R}:S\to\mathbb{R}$$ and $$\gamma$$ is discount factor between $$0$$ and $$1$$. In Markov reward process, whenever a transition happens from a current state $$s$$ to a successor state $$s'$$, a reward is obtained depending on the current state $$s$$. The reward can be either deterministic or stochastic. If stochastic, tt can be a random variable or even depend on the successor state $$s'$$ and $$R_t(s)$$ is regraded as the expected reward conditioning on the current state $$s$$. The expectation takes on both the distribution of the random variable and the transition probability on the current state.

The return $$G_t$$ is the total discounted reward from time-step $$t$$.

$$G_t\doteq R_{t+1}+\gamma R_{t+2}+\dots=\sum_{k=t+1}^\infty\gamma^{k-t-1}R_k$$

The discount factor $$\gamma\in[0,1)$$



## Markov Decision Process

## Three Tpyes of Markov Decision Process

## Stationary Distribution and Discounted Stationary Distribution

# Dynamic Programming

## Value Iteration


$$V(s)=\max_a\enspace\sum_a\pi(a\vert s)\left[r(s,a)+\gamma\sum_{s'}P(s'\vert s, a)V(s')\right]$$

$$Q(s,a)=\sum_a\pi(a\vert s)\left[r(s,a)+\gamma\sum_{s'}P(s'\vert s, a)\max_{a'}Q(s',a')\right]$$

## Policy Iteration

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
