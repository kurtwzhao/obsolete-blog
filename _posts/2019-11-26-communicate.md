---
title: "Why do Animals Communicate?"
date: 2019-11-26
permalink: /2019-11-26-communicate/
---

> The reasons why animals, especially human beings, communicate are variant. According to my knowledge of economics and game theory, I give two reasons with some simple and pedagogical examples. Firstly, when cooperation is beneficial, agents use communication to coordinate their behaviors. Secondly, when the information about the environment or state is incomplete and different agents have different information, they communicate to exchange informations to get a better knowledge of the world.




# Preliminary
The following analysis and examples all depend on the framework of game theory. When analyzing a game, we usually don't care about communication and hence the definiton of **Nash equilibrium** is widely used. Intuitively, a Nash equilibrium is a stable outcome (strategy profile) in which no agent would want to change his strategy if he knew what strategies the other agents were following. Note that here the strategy of each agent is independent and hence the outcome (strategy profile) can be expressed as the product of each agent's strategy. Just like that in probability, the joint distribution is the product of each marginal distribution if all components are independent.

How to incorporate communication into game theory? [[Myerson (1997), Chapter 6](https://www.hup.harvard.edu/catalog.php?isbn=9780674341166)]: "In principle, we argued , anything that a player can do to communicate and coordinate with other players could be described by moves in an extensive-form game, so planning these communication moves would become part of his strategy choice itself. Although this perspective can be fully general in principle, it is not necessarily the most fruitful way to think about all games. ...... It might be more useful to leave communication and coordination possibilities out of our explicit game model. If we do so, then we must instead use solution concepts that express an assumption that players have implicit communication opportunities, in addition to the strategic options explicitly described in the game model." This new solution concept is **correlated equilibrium**. The correlated equilibrium is a solution concept that generalizes the Nash equilibrium. Some people feel that this is the most fundamental solution concept of all. This Nobel-prize-winning game theorist, , R. Myerson, has gone so far as to say that “if there is intelligent life on other planets, in a majority of them, they would have discovered correlated equilibrium before Nash equilibrium.” As its name illustrated, correlated equilibrium allows the correlation between different agents' strategies. ***Mathematically, the advantage of correlated equilibrium to Nash equilibrim is the benefit of communication.***

The following analysis is restricted on static games which tries to give some intuitions of why agents in the game want to communicate. A general results for stochastic games, which is widely used as a framework for multi-agent reinforcement learning, is unknown depending on my knowledge. [If you know literatures about some general results on communication in stochastic games, I'll express my gratitude for having me known.] The strict definition of Nash equilibrium and correlated equilibrium can be found in almost any game theory textbooks, to name a few, [Myerson (1997)](https://www.hup.harvard.edu/catalog.php?isbn=9780674341166), [Fudenberg & Tirole (1991)](https://mitpress.mit.edu/books/game-theory), and [Shoham & Leyton-Brown (2009)](http://www.masfoundations.org/).

# Communication for Coordination

In general, games can be classified into three categories according to agents's disire of cooperation and competition and we discuss the benefit of communicating in these three situations. Since this section focuses on the role of coordination, we assume the state or environment is deterministic. That is, there is only one state in the state space. We also assume there are two agents and two actions for each agent such that the rewards can be represented by a matrix clearly.

## Pure Cooperation
**Pure Coordination Game**, which is also called the **common-payoff game**. In such gamme, every agent's reward is the same for each outcome. Game 1 below is such a game, in which there are two pure strategy Nash equilibrium $$[(1,0),(1,0)]$$ and $$[(0,1),(0,1)]$$, and a mixed strategy Nash equilibrium $$[(\frac12,\frac12),(\frac12,\frac12)]$$. The outcome (strategy profile) is written in the form $$[(a_1^1, a_2^1),(a_1^2, a_2^2)]$$, where $$a_i^j$$ is the probability that agent $$i$$ plays action $$j$$. These three equilibrium achieves rewards $$(1,1)$$, $$(1,1)$$, and $$(\frac12,\frac12)$$, respectively. The first two equilibria reach the best rewards, but there is no guarantee that these equilibria are always realized. This situation illustrate the necessarity of communication. Through communication, agent 1 can tell agent 2 that he will play action 1 and agent 2 will play action 1 as well. Note that if agent 1 tells that he would play action 1, he has no incentive to cheat, i.e. not playing action 1 when really executing the action. Therefore, the outcome $$[(1,0),(1,0)]$$ is in the set of correlated equilibrium and it can be realized by communication.



**Conclusion:** In the pure cooperation sitution, there usually exists multiple Nash equilibrium. Agents' reward can be impaired because of coordination failure. The role of communication is to coordinate such that the best Nash equilibrium can be reached. The best Nash equilibrium is on the Pareto frontier of the correlated equilibrium set.

**Remark 1:** Every (mixed strategy) Nash equilibrium is a correlated equilibrium, but not vice versa.

**Remark 2:** If we change the game as follows, there are still three Nash equilibria, which are $$[(1,0),(1,0)]$$ and $$[(0,1),(0,1)]$$, and a mixed strategy Nash equilibrium $$[(\frac13,\frac23),(\frac13,\frac23)]$$. Although the last two seem unreasonable, they indeed satisfy the definition of Nash equilibrium. In game theory, we call the first equilibrium the *focal point*.

**Remark 3:** The conclusions from each section are just empirical, no mathematical proof will be provided and there may exist counterexamples.

## Pure Competition
**Pure Competition Game**, which is also called the **constant-sum games**. Since a positive affine transmation doesn't change the agents' preference, this is also called **zero-sum game**. In such games, for each outcome, the summation of all agent's utility is zero. The following *matching pennies game* can be regarded as a two-action version of the Rock-Paper-Scissors. It has no pure strategy nash equilibrium and one mixed stratefgy Nash equilibrium, which is $$[(\frac12,\frac12),(\frac12,\frac12)]$$. It is easy to show that this is also the only correlated equilibrium. Hence in the pure competitive case, communication is useless. An intuitive explanation is that suppose agent 1 tells agent 2 that he will play action 1, consequently, agent 2 prefers action 2 and now agent 1 has an incentive to play action 2, which means his words are not believable.

**Conclusion:** In the pure competition sitution, communication is useless. Usually there only exists one mixed strategy Nash equilibrium, which is also the only correlated equilibrium.

## Between
In general, games can include elements of both coordination and competition. This is the most interesting and complicated situation to analyze the role of communication. The follow *game of chicken* is one of such game. In this game two individuals are challenging each other to a contest where each can either dare or chicken out. If one is going to Dare (action 1), it is better for the other to chicken out (action 2). But if one is going to chicken out it is better for the other to Dare. This leads to an interesting situation where each wants to dare (compete), but only if the other might chicken out (coordinate). In this game, there are three Nash equilibria. The two pure strategy Nash equilibria are $$[(1,0),(0,1)]$$ and $$[(0,1),(1,0)]$$. There is also a mixed strategy equilibrium $$[(\frac13,\frac23),(\frac13,\frac23)]$$. The rewards are $$(7,2)$$, $$(2,7)$$, and $$(4\frac13,4\frac13)$$, respectively.

Can each agent become better by coordination? Yes! Suppose there is a third party device which flips an even coin. If it is head then the device suggests that agent 1 should play action 1 and agent 2 should play action 2. If it is tail, the device suggests that agent 1 should play action 2 and agent 2 should play action 1. That is, the outcome (Action 1, Action 2) and (Action 2, Action 1) both appear with a half probability and the expected reward is $$(4\frac12,4\frac12)$$, which is higher than the mixed strategy Nash equilibrium. Without the third party device, this correlated equilibrium can also be implemented by communication. For example, each agents flips an even coin and tell the other the result. If the coins are the same, then play (Action 1, Action 2) and otherwise play (Action 2, Action 1). Since this is a correlated equilibrium, you can verify that both agents don't have an incentive to lie.

Can we do better? Yes! Suppose there is a third party device which flips two even coins. If there are two heads then the device suggests that agent 1 should play action 1 and agent 2 should play action 2. If there are two tails, the device suggests that agent 1 should play action 2 and agent 2 should play action 1. If there is one head and one tail, the device suggests both agents that they should play action 2. That is, the outcome (Action 1, Action 2) and (Action 2, Action 1) both appear with a quarter probability and the outcome (Action 2, Action 2) appears with a half probability. In this case, the expected reward is $$(5\frac14,5\frac14)$$, which is higher than the mixed strategy Nash equilibrium. This correlated equilibrium is on the Pareto frontier and hence one cannot achieve a better reward with harming the other. Can this correlated equilibrium [let's believe that this is true for now and we will verify it soon] be implemented by communication without a third party device? Limited by my intelligence, I cannot find a mechanism.

Let's verify the above outcome is really a correlated equilibrium. Here I want to emphasis that although each agent knows how the device works, they only observe their own suggestion given by the device but not the result of the flipping coins. This is important to explain why this  correlated equilibrium can not be implemented by communicating. Let's verify the equilibrium first: if agent 1's suggestion is action 1, then by bayesion updating, his belief about agent 2's suggestion is action 1 with probability 1/3 and action 2 with probability 2/3. [Given there is at least one head, what is the probability that there are two heads, and one tail and one head?]. Given this belief, agent 1's reward is 14/3 for both action and hence he doesn't have the incentive to deviate to action 2. Since the game is symmetric, it is also true for agent 2.

The last and most important question is: *can every correlated equilibrium be impletemented by communication?* The general answer is negative, but there is a positive answer for games with at least three players [[Vida and Forges (2013)](https://econtheory.org/ojs/index.php/te/article/view/20130095)]. The intuition is obvious: to implement this correlated equilibrium, agent 1 should be uncertain about agent 2's action, which is impossible in the two-players game. With games of more than three players, you may receive an information but do not know the sender, which makes this possible.

**Conclusion:** In the between case, communication can benefit both agent since the best Nash equilibrium is usually not on the Pareto frontier of the correlated equilibrium. But for the two-players case, not all correlated equilibrium on the Pareto frontier can be implemented by communication.

**Remark:** For some games, correlated equilibrium on the Pareto frontier can be implemented by communication. For example if we change the reward of (Action 2, Action 2) to (0, 0), then the above first correlated equilibrium is on the Pareto frontier and can be implemented by communication.


# Communication for Shared Information
In this part, we assume

# incomplete information about state, share information

# agree to disagree

# More information may be harmful social value of information

