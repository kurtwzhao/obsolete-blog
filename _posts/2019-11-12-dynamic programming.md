---
title:  "Dynamic Programming"
---

# Markov Decision Process (MDP)
It is natural to understand MDP by proceeding in the order of **Markov Process (MP)**, followed by **Markov Reward Process (MRP)**, and finally the **Markov Decision Process (MDP)**. 

**Markov process** is a stochastic process that satisfies the Markov property. We make two additional assumptions that are very common in the reinforcement learning (RL) setting:

* *Finite state space:* we denote the state space by $$\mathcal{S}=\{s_1,s_2,\dots,s_n\}$$, therefore, $$\vert\mathcal{S}\vert=n$$
* *Stationary transition probabilities:* the transition probabilities are time independent. Mathematically, this means:

$$P(S_1=s'\vert S_0=s)=P(S_t=s'\mid S_{t-1}=s),\qquad\forall s, s'\in\mathcal{S},\qquad\forall t=1, 2, \dots$$

These two additional assumptions lead to a nice characterization of the transition dynamics in terms of *transition probability matrix* $$\mathbf{P}$$ of size $$n\times n$$, whose $$(i,j)$$ entry is given by $$\mathbf{P}_{ij}=P(S_t=s_j\vert S_{t-1}=s_i)$$

A **Markov reward process** is a Markov process with the specification of a reward function and a discount factor.

# Value Iteration

$$V(s)=\max_a\enspace\sum_a\pi(a\vert s)\left[r(s,a)+\gamma\sum_{s'}P(s'\vert s, a)V(s')\right]$$

$$Q(s,a)=\sum_a\pi(a\vert s)\left[r(s,a)+\gamma\sum_{s'}P(s'\vert s, a)\max_{a'}Q(s',a')\right]$$

# Policy Iteration

$$V(s)=\enspace\sum_a\pi(a\vert s)\left[r(s,a)+\gamma\sum_{s'}P(s'\vert s, a)V(s')\right]$$

$$Q(s,a)=\sum_a\pi(a\vert s)\left[r(s,a)+\gamma\sum_{s'}P(s'\vert s, a)Q(s',a')\right]$$



* One policy gradient step does not maximize the objective thoroughly. With improper learning rate, the policy gradient step may be harmful.


### Value function and action-value function (Q-function)

policy iteration ==> SARSA ==> Actor-Critic
value iteration ==> Q-learning ==> DQN

### value iteration
splitting $$I-\lambda P$$ as $$I-\lambda P = Q_d-R_d$$, then $$v^{n+1}=Q_d^{-1}(R_dv^n+r_d)$$:
* Gauss-Seidel
* Jacobi

over-relaxation and inder-relaxation
$$v^{n+1}=v^n+\omega\left[\max_{d\in D}\{Q_d^{-1}(R_dv^n+r_d)\}-v^n\right]$$

### policy iteration and modified policy iteration

### multistep lookahead
