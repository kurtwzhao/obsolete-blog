---
title:  "Dynamic Programming"
---

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
