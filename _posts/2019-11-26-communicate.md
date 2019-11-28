---
title: "Why do Animals Communicate? A Game Theory Approach"
date: 2019-11-26
permalink: /2019-11-26-communicate/
---

> The reasons why animals, especially human beings, communicate are variant. According to my knowledge of economics and game theory, I give two reasons with some simple and pedagogical examples. First, when (partial) cooperation is beneficial, agents use communication to coordinate their behaviors to cooperate. Second, when the information about the environment (state) is incomplete and different agents have diverse information about the environment, they communicate to exchange information to get a better knowledge of the world.



# Preliminary
## Nash Equilibrium and Correlated Equilibrium
The following analysis and examples all depend on the framework of game theory. When analyzing a game, we usually don't care about communication and hence the definition of **Nash equilibrium** is widely used. Intuitively, a Nash equilibrium is a stable outcome (strategy profile) in which no agent can improve his reward by unilaterally deviating from the equilibrium strategy profile. Note that here the strategy of each agent is independent and hence the outcome (strategy profile) can be expressed as the product of each agent's strategy. Just like that in probability theory, the joint distribution is the product of each marginal distribution if all components are independent.

How to incorporate communication into game theory? [[Myerson (1997), Chapter 6](https://www.hup.harvard.edu/catalog.php?isbn=9780674341166)]: "In principle, we argued , anything that a player can do to communicate and coordinate with other players could be described by moves in an extensive-form game, so planning these communication moves would become part of his strategy choice itself. Although this perspective can be fully general in principle, it is not necessarily the most fruitful way to think about all games. ...... It might be more useful to leave communication and coordination possibilities out of our explicit game model. If we do so, then we must instead use solution concepts that express an assumption that players have implicit communication opportunities, in addition to the strategic options explicitly described in the game model." This new solution concept is **correlated equilibrium**. The correlated equilibrium is a solution concept that generalizes the Nash equilibrium. Some people feel that this is the most fundamental solution concept of all. In fact the Nobel-prize-winning game theorist, R. Myerson, has gone so far as to say that “if there is intelligent life on other planets, in a majority of them, they would have discovered correlated equilibrium before Nash equilibrium.” As its name illustrated, correlated equilibrium allows the correlation between different agents' strategies. Communication is closely related to correlated equilibrium. Hence, ***mathematically, the benefit of communication is the advantage of correlated equilibrium to Nash equilibrim.***

The following analysis is restricted on static games which tries to give some intuitions of why agents in the game want to communicate. A general results for stochastic games, which is widely used as a framework for multi-agent reinforcement learning, is unknown depending on my knowledge. [If you know literatures about some general results on communication in stochastic games, I'll express my gratitude for having me known.] The strict definition of Nash equilibrium and correlated equilibrium can be found in almost any game theory textbooks, to name a few, [Myerson (1997)](https://www.hup.harvard.edu/catalog.php?isbn=9780674341166), [Fudenberg & Tirole (1991)](https://mitpress.mit.edu/books/game-theory), and [Shoham & Leyton-Brown (2009)](http://www.masfoundations.org/). I will give a short definition of the *normal form game*, *Nash equilibrium*, and *correlated equilibrium* in the **Appendix** if you want to have a reivew.

## The Meaning of Message: Revelation Principle

A message is meaningful only if both the send and the receiver map a certain message to certain meaning. The [revelation principle](https://en.wikipedia.org/wiki/Revelation_principle) in mechanism design is also a good idea in this case. For example, the sender lives in our world and the receiver lives in a parallel world in which cat is called dog and dog is called cat. If they both know this, they can easily invent a translation machine which substitutes cat with dog and dog with cat. The revelation principle says we can always find a direct (communication) mechanism in which dog means dog and cat means cat. If not, we can first find the direct communication mechanism and the translation machine can inversely translate the message such that both the sender and the receiver understand it correctly. Hence when we design a mechanism, we can only care about the direct mechanism.

# Communication for Coordination

In general, games can be classified into three categories according to agents' desire of cooperation and/or competition and we discuss the benefit of communicating in these three situations. Since this section focuses on the role of coordination, we assume the state or environment is deterministic. That is, there is only one state in the state space. We also assume there are two agents and two actions for each agent such that the rewards can be represented by a $$2\times2$$ matrix clearly.

## Pure Cooperation
**Pure Coordination Game**, which is also called the **common-payoff game**. In such games, every agent's reward is the same for each outcome. The game below is such a game, in which agent 1 chooses the column actions and agent 2 chooses the row actions. The paired number in each element is the two agents' reward. There are two pure strategy Nash equilibrium: *Equilibrium 1* and *Equilibrium 2*, and a mixed strategy Nash equilibrium: *Equilibrium 3*. The number in each outcome illustrate the probability of that outcome. Note that for the Nash equilibrium, the joint must be the product of the marginal distribution since each agent's strategy is independent. These three equilibria achieve rewards $$(1,1)$$, $$(1,1)$$, and $$(\frac12,\frac12)$$, respectively. The first two equilibria reach the best rewards, but there is no guarantee that these equilibria are always realized since each agent execute his action independently. This situation illustrate the necessity of communication. Through communication, agent 1 can tell agent 2 that he will play action 1 and agent 2 will play action 1 as well. Note that if agent 1 tells that he would play action 1, he has no incentive to cheat, i.e. deviating to action 2 when really executing the action. This equilibrium is also on the Pareto Frontier of the correlated equilibrium and hence its is the best outcome that can be achieved by communication.

<p style="text-align:center;">
<img src="{{site.url}}/images/game1.png" width="90%" alt="game1">
</p>

**Observation:** In the pure cooperation situation, there usually exists multiple Nash equilibrium. Agents' reward can be impaired because of coordination failure. The role of communication is to coordinate such that the best Nash equilibrium can be reached. The best Nash equilibrium is on the Pareto frontier of the correlated equilibrium set.

**Remark1:** If we change the game as follows, there are still three Nash equilibria. Although the last two seem unreasonable, they indeed satisfy the definition of Nash equilibrium. In game theory, we call the first equilibrium the *focal point* and it is the desirable outcome that can be realized by communication as well as on the Pareto frontier of correlated equilibrium set.

<p style="text-align:center;">
<img src="{{site.url}}/images/game2.png" width="90%" alt="game2">
</p>

**Remark 2:** Every (mixed strategy) Nash equilibrium is a correlated equilibrium, but not vice versa.

**Remark 3:** Every game has an odd number of Nash equilibria (both the pure and the mixed strategy equilibria) due to Sperner’s lemma. The correlated equilibrium is a convex set in the simplex whose vertices are the pure-stretegy profiles.


## Pure Competition
**Pure Competition Game**, which is also called the **constant-sum games**. Since a positive affine transformation doesn't change the agents' preference, this is also called **zero-sum game**. In such games, for each outcome, the summation of all agent's reward is zero. The following *matching pennies game* can be regarded as a two-action version of the Rock-Paper-Scissors. It has no pure strategy Nash equilibrium and one mixed strategy Nash equilibrium. It is easy to show that this is also the only correlated equilibrium. Hence in the pure competitive case, communication is useless. An intuitive explanation is that suppose agent 1 tells agent 2 that he will play action 1, consequently, agent 2 prefers action 2 and now agent 1 has an incentive to play action 2, which means his message is not believable.

<p style="text-align:center;">
<img src="{{site.url}}/images/game3.png" width="90%" alt="game3">
</p>


**Observation:** In the pure competition situation, communication is useless. Usually there only exists one mixed strategy Nash equilibrium, which is also the only correlated equilibrium.

## Between
In general, games can include elements of both coordination and competition. This is the most interesting and complicated situation to analyze the role of communication. The following *battle of sexes* is one of such games. Husband and wife wish to go to the movies, and they can select among two movies: a love moive and a war moive. They much prefer to go together rather than to separate movies, but while the wife (agent 1) prefers love moive (action 1), the husband (agent 2) prefers war moive (action 2). The reward matrix and equilibria are shown below. The first three are Nash equilibria.

<p style="text-align:center;">
<img src="{{site.url}}/images/game4.png" width="90%" alt="game4">
</p>

None of these three equilibria are desirable. It seems that *equilibrium 4* is a pretty good and fair equilibrium, but it is not a Nash equilibrium because the two agents' strategy are not independent. How to achieve this equilibrium? Suppose there is a third party device which flips a fair coin. If it is head then the device suggests that both agents should play action 1 and otherwise both should play action 2. It is easy to verify that both agent would like to follow the suggestion from the third party device and hence it is a correlated equilibrium and also on the Pareto frontier. The next question is whether such a correlated equilibrium can be implemented by a communication mechanism. The answer is positive. Suppose that both agents flip a fair coin independently and tell each other their result, if it is head, both play action 1 and otherwise both play action 2.

**Observation:** In the between case, Nash equilibria are usually not desirable since they are either not fair or not Pareto efficient. Communication usually can help achieve the fair and efficient equilibrium.

**Remark:** Wait! An important question is can every correlated equilibrium be implemented by a communication mechanism? Unforturately, the answer is negative. But there is a pretty good answer: for games with at least three players [[Vida and Forges (2013)](https://econtheory.org/ojs/index.php/te/article/view/20130095)]. I'll give you the intuition with the following example.

Consider the *game of chicken*. In this game two individuals are challenging each other to a contest where each can either dare or chicken out. If one is going to Dare (action 1), it is better for the other to chicken out (action 2). But if one is going to chicken out it is better for the other to Dare. This leads to an interesting situation where each wants to dare, but only if the other might chicken out. In this game, there are three Nash equilibria. But a fair and Pareto efficient equilibrim is *equilibrium 4*. How to achieve this equilibrium? Suppose there is a third party device which flips two fair coins. If there are two heads then the device suggests that agent 1 should play action 1 and agent 2 should play action 2. If there are two tails, the device suggests that agent 1 should play action 2 and agent 2 should play action 1. If there is one head and one tail, the device suggests both agents that they should play action 2. That is, the outcome (Action 1, Action 2) and (Action 2, Action 1) both appear with a quarter probability and the outcome (Action 2, Action 2) appears with a half probability. In this case, the expected reward is $$(5\frac14,5\frac14)$$, which is higher than the mixed strategy Nash equilibrium. This correlated equilibrium is on the Pareto frontier and hence one cannot achieve a better reward with harming the other.

<p style="text-align:center;">
<img src="{{site.url}}/images/game5.png" width="90%" alt="game5">
</p>

 To verify it is indeed a correlated equilibrium, first I want to emphasis that although each agent knows how the device works, they only observe their own suggestion given by the device but not the result of the flipping coins. This is important to explain why this  correlated equilibrium can not be implemented by a communicatiion mechanism. [Limited by my intelligence, I cannot find a communication mechanism without a third party which can achieve this information structure.] Let's verify the equilibrium: if agent 1's suggestion is action 1, then by bayesion updating, his belief about agent 2's suggestion that is action 1 with probability 1/3 and action 2 with probability 2/3. [Given there is at least one head, what is the probability that there are two heads, and one tail and one head?]. Given this belief, agent 1's reward is 14/3 for both action and hence he doesn't have the incentive to deviate to action 2. Since the game is symmetric, it is also true for agent 2.

The intuition why not all correlated equilibrium can be implemented by some communication mechanism is obvious: to implement the correlated equilibrium like above, agent 1 should be uncertain about the message that agent 2 receives, which is impossible in the two-players game. Within games of more than three players, you may receive a message but do not know the sender, which makes this possible.


# Communication for Sharing Information
In this part, we illustrate how communication is helpful for sharing information and hence increasing the agents' reward. The following example comes from the widely cited [Crawford & Sobel (1982)](https://www.jstor.org/stable/1913390?seq=1).

We still assume the game has one stage. But now the state of the world is stochastic. Let $$\mathcal{S}\triangleq[0,1]$$ denote the state space and a state realized from the uniform distribution $$s\sim U[0,1]$$. There is a sender who knows exactly the state realization of the world and a receiver who doesn't have any information about the state. The sender cannot conduct any actions except for sending information to the receiver. The receive can choose action $$a$$ from the action space $$\mathcal{A}\triangleq[0,1]$$. The receiver and sender have reward function $$u^R(s,a)=-(a-s)^2$$ and $$u^S(s,a)=-[a-(s+b)]^2$$, respectively. The receiver wants to match his action to the state as close as possible, but the sender's interest conflicts with the receiver's and is measured by the bias $$b\ge0$$. The smaller the $$b$$ is, the higher their interests aligns. Note that since the receiver has a quadratic reward function, his best action is $$a^*=\mathbb{E}[s\vert \text{message}]$$, which is the conditional expectation of the state depending on the sender's message.

<p style="text-align:center;">
<img src="{{site.url}}/images/game6.png" width="60%" alt="game6">
<br>
The Reward Function of the Receiver and the Sender
</p>

## Pure Cooperation
That $$b=0$$ indicates the case of pure cooperation. Now the best equilibrium is the full revealing equilibrium, in which the sender tells the receiver the state of the world accurately $$m=s$$ and the receiver chooses the action $$a=m=s$$. But this is not the only equilibrium, there are many others and the most obvious one is the babbling equilibrium, in which no matter what message the sender send, the receiver regards it as meaningless information and chooses action $$a=\frac12$$, which is the expection of the state depending on the prior. You will see how to construct the other equilibria from the following section.

## With Interest Conflict
When $$b>0$$, the sender and the receiver's interest does not align perfectly. The full-revealing message can not be a equilibrium. To see this, suppose the sender always send the message $$m=s+b$$ where $$s$$ is the true state. If the receiver just take the action $$a=s+b$$, it will fit the sender's interest exactly. But the receiver knows that the sender always adds $$b$$ to the true state and would like to execute the action $$a=m-b=s$$ which maximize his own reward. Babbling equilibrium is still an equilibrium in this situation. But except for babbling equilibrium, are there any other meaningful and better equilibria and how to construct them? 

An simple idea is to assume $$\mathcal{M}=\{m_1,m_2\}$$. The sender send message $$m_1$$ if the true state is below some threshold $$t$$ and otherwise send message $$m_2$$. If receiver receives message $$m_1$$, then he knows that the state is uniformly distributed on $$[0,t]$$ and hence execute action $$a=\frac t2$$. If he receives message $$m_2$$, he chooses $$a=\frac{t+1}{2}$$. Note that the equilibrium requires that the sender is indifferent of sending either message when the true state is $$t$$, that is $$-[\frac t2-(t+b)]^2=-[\frac{t+1}2-(t+b)]^2$$. Since $$\frac{t+1}{2}>t+b$$, it is equivalent to $$\frac t2-(t+b)=(t+b)-\frac{t+1}{2}$$, which gives

$$t=\frac12-2b$$

This equilibrium exists if $$b<\frac14$$, i.e. the sender and the receiver's interest cannot conflict too much.


<p style="text-align:center;">
<img src="{{site.url}}/images/game7.png" width="60%" alt="game7">
<br>
The Construction of Partial Revealing Equilibrium
</p>

In general, we can construct more informative equilibria depending on the value of $$b$$. Let $$t_{i-1}$$, $$t_{i}$$, and $$t_{i+1}$$ be three equilibrium cutoffs, then we should have

$$t_i+b-\frac12(t_{i-1}+t_i)=\frac12(t_i+t_{i+1})-(t_i+b)$$

and hence

$$4b=t_{i-1}+t_{i+1}-2t_i$$

which gives a difference equation about $$t_i$$'s. The solution to this difference equation is $$t_i=it_1+2i(i−1)b$$. Notice that the last cutoff $$t_N=Nt_1+2N(N−1)b=1$$, which implies that:

$$2N(N−1)b<1\Rightarrow N<\frac{1+\sqrt{1+\frac{2}{b}}}{2}$$
That is , there are more partial-revealing equilibria depending on how large $$b$$ is. The most informative equilibrium takes the largest $$N$$ possible.


## Some Interesting Observations
In this special game, agents communicate becasue they want to share information about the state of the world and make better decisions. Some interesting observations:

* Babbling equilibrium is always a equilibrium in any cases. In such a equilibrium, communication does not contain any information.
* When $$b=0$$, the sender and the receiver's interest totally aligns and full-revealing equilibrim is possible. 
* When $$b>0$$, full-revealing equilibrim does not exist. But some partial-revealing equilibria exist. In such equilibria, the sender does not reveal the state accurately but partially.
* The smaller the $$b$$ is, the more informative the communication can be, and consequently the higher reward for both agents. (which can be verified easily by computing their expected reward in the most informative equilibrium)


# How does Communication Emerge?
The above game theory only gives the equilibria, but does not explain how thses equilibria are reached. I think an interesting and exciting idea is to apply reinforcement learning algorithms to such situations and test which equilibria can appear. If not the most efficient one, how to adjust the algorithm to achieve that one?

A naive story of how language appears can be like this: two agents live in a game world and play the Nash equilibrium. One day one agent changes his action by accident and in the meanwhile utters some noisy. The other agent receives this meaningless nosie and chances his acton as well. The miracle happens: they find they both receives a higher reward and they believe it is this noise that helps them reach this achievement. This meaningless noise becomes some meaningful information from now on, which means "we should choose this action profile that gives us both a higher reward". 

# Brainstorms

## Folk Theorem

[Folk theorem](https://en.wikipedia.org/wiki/Folk_theorem_(game_theory))

## agree to disagree

## More information may be harmful social value of information


