README

# RL (Q - Learning) VS NN (NEAT)
----------------------------------------------------
## Abstract
Games have shown to be a useful technique to track artificial intelligence progress. Chess, AtariZGOO, and G0 are just a few of the most well-known examples of AI computer systems defeating human players. In this work, we include the famous Flappy Bird game to the list of games used to measure an AI player's performance. 
Artificial agents were educated to adopt the most advantageous action at each game moment using Q—Reinforcement Learning and Neuroevolution (neural network fitted by genetic algorithm). The Neuroevolution agent surpassed the Reinforcement Learning agent by a large margin (111 points average result) and scored an astonishing 28700 points on average.


## Introduction

Games are rapidly being viewed as the ideal test-bed for artificial intelligence (AI) algorithms, and they are also becoming an important application field. Game AI is a vast field that encompasses anything from the difficulty of creating superhuman AI for difficult games like Go or Atari to innovative applications like automated game creation. With the addition of video games over the last decade, this area of study has witnessed significant extension and enrichment, allowing us to address a larger variety of difficulties with great commercial, social, economic, and scientific relevance.

Flappy Bird, a mobile game, was introduced in May of 2013 and immediately gained a lot of attention, as well as a lot of criticism due to its high degree of difficulty. Dong Nguyen, the game's inventor, pulled the game from smartphones in 2014 because it had become too addicting. The game appears straightforward; the player must guide a bird across gaps between regularly spaced pipes by either doing nothing (allowing the bird to drop) or pushing the "up" key (the bird jumps upward). Despite this, due to the quick game dynamics, significant environment fluctuation, and large search space, the scores obtained are typically poor. To set up the challenge for developing a computer software that can play the game, detailed feature definitions are required.

The purpose of this work is to train an AI agent how to play the Flappy Bird game better than non-expert human players and get a score that is at least good enough for a platinum medal (the highest game prize).

The remainder of the paper is laid out as follows: The second section examines similar works. Sections 3 and 4 discuss the Reinforcement Learning (RU-based agent) and the Neuroevolutiou(NE)-based agent's training and performance evaluation, respectively. encapsulates the work

## Flappy Bird Game

The Flappy Bird game is a side-scrolling platformer in which the player controls a bird that must fly through columns of pipes without colliding with them. If the bird lands on the pipes, the game will end and a new episode will begin. The player controls the bird's verticalposition (height), the bird is continually falling, and the bird jumps when the key (space bar or up arrow) is pushed. The pipes are arranged in a random order, with the same spacing between the bottom and higher pipes and the same horizontal distance between the current pipe and the next. We have access to the bird and pipe locations in the game's python code. The scatter plot in displays the histogram of the following game variables: bird's coordinates (x, y), bird's vertical (y) velocity, closest lower pipe coordinates (x,y), and nearest upper pipe vertical (y) position. The nearest upper and lower pipes have the same x coordinates. These figures were taken during a game in which the player had a 64-point performance (number of pipes the bird passed successfully).

<p  align="center">
  <img src="src\game screenshot.jpg" width="150" title="game screenshot" >
  <img src="src\game representation model.jpg" width="150" title="game representation model">
</p>

<p align="center">
<img  title="data visualization" src="src\data visualization.jpg"/>
</p>

----------------------------------------------------

# Reinforcement Learning to Flappy Bird Game

In the reinforcement learning (RL) framework the algorithms (the agent) is not provided with the ‘right answer’ (as with the supervised learning) instead it receives feedback in the form of rewards, that indicate to the learning agent when it is doing well, and when it is doing poorly Agent’s utility is deﬁned by the reward function. The goal of the agent is to learn to act so as to maximize the expected rewards. The RL problem deﬁned as Markov decision process has
the following elements:

- S — set of states.
- A - set of actions.
- P(s, a) - state—transition probability between each state and action.
- R - reward function that returns a reward based on the current state, the action taken, and/ or the next state.
- 𝛾 - discount factor real number between 0 and 1), represents how much value loose the future rewards according to how distant in time they are

----------------------------------------------------
<script type="text/javascript" src="http://cdn.mathjax.org/mathjax/latest/MathJax.js?config=default"></script>

# Q-Learning to Flappy Bird Game
In this paper we apply the Q—Learning approach of RL. Based on experience with
previous games the algorithm creates the Q-table that contains the maximum expected future rewards for each action at each state. The best policy function, i.e. the function that, given a state, returns the action that maximizes the future reward, satisﬁes the Bellman’s equation

$$Q(s,a) = R(x') + max_{a_i \in A}\left [\gamma  * Q(x', a_i) \right ]$$ 

where s is the current state and s’ is the next state after taking action a.

In our framework, the game state is represented by the difference between the bird’s position and the next lower pipe (dx, dy), and the bird velocity in y axis (vy). The possible actions in any state are jump or do nothing (the bird just falls). The reward function return +1 every time the agent completes a step without dying, and —100 when it dies. According to the rules of the game, the player gets a point only when the bird passes successfully between
two pipes. However, over a. number of frames the bird moves to find the next pipe and in order to learn if it is doing the right action our strategy rewards each step (frame) and not only the score step after the bird passes between two pipes. In the implementation of the Bellman’s Eq. (1), at each iteration instead of completely replacing the previous Q value we introduced a learning rate a (a real number between 0 and 1).

$$Q(s,a) = (1 -\alpha ) * Q(s, a) +\alpha *  \left [R(s') + max_{a_i \in A}\left [\gamma * Q(x', a_i) \right ]  \right ]$$

---
### Performance Evaluation
The learning rate ɑ and the discount factor 𝛾 were chosen after a grid search over the following intervals of discrete values, ɑ = [0.1. 0.3, 0.5, 0.7, 0.9] and 𝛾 = [ 0.1. 0.3, 0.5. 0.7, 0.9. 1]. The heat map in was obtained after training the RL model for each combination of parameters (30 combinations in total) over 1500 episodes. The episode ends whenever the bird hits a pipe. The values inside the rectangles, 

<p  align="center">
  <img src="src\discount factor.jpg" title="discount factor" >
  <img src="src\Learning Curve for varioud Discount Factors.jpg"title="Learning Curve for varioud Discount Factors">
  <img src="src\Learning Curve for varioud Learning Rates.jpg"title="Learning Curve for varioud Learning Rates">
  <img src="src\learing rate.jpg"title="learing rate">
</p>
RL agent with the optimal hyper-parameters: average score over sequences of 20 episodes.

mapped by color (the darker the color, the higher the value), are the average scores of 10 consecutive episodes after training. The score over one episode corresponds to the number of pipes the bird passed before hitting a pipe, The best performance was achieved for the combination ɑ = 0.7 and 𝛾 = 1. In the picture illustrates in more details the learning curves achieved when the discount factor is set to 1 and or varies, Note that the learning rate significantly affects the score with the best performance achieved for a : 0.7. Subsequently, the learning rate was set to its optimal values of 0.7 and the discount factor alternates between [ 0.1, 0.3, 0.5, 0.7, 0.9, 1]. The results shown in the picture validate 𝛾 : 1 as the most relevant choice.

The RL agent with the optimal hyper-parameters was tested over 20000 episodes. 
In order to eliminate score fluctuations between subsequent episodes and get statistically more relevant trends in the agent performance, in picture are shown moving average scores over sequences of 20 episodes. The AI player needs around 1000 episodes to stabilize its playing performance and then keeps the learned strategy over long number of episodes. Table 1 summarizes the scores over the last 10 episodes and the relevant statistics (average, standard deviation, best and worst score). There is not an official statistics, however 110 points in average before hitting a pipe is a respectful result, according to wikipedia players who achieve a score of forty or higher receive a platinum medal. Nevertheless, dedicated human players can achieve much better results, therefore we consider the RL agent not as a potential game Wilmer but as a stimulating partner in AI—human competitions.

---
# Neuroevolution Applied to Flappy Bird Game
Neuroevolution (NE) is an unsupervised machine learning approach to ﬁt a neural network model based on genetic optimization  
Genetic Optimization
The major nature-inspired natural selection principles encoded into the genetic
algorithm are:

- Heredity — The process for the Children to inherit the parent’s properties.

- Variation - Varicty of traits must exist in the population.

- Selection — The probability for some of the population members become
parents and pass down their genetic information (referred also as Survival of
the ﬁttest).

The basic steps of the NE algorithm applied to ﬁt the NE Flappy Bird player are summarized in Algorithm. We start with a population of N neural network models (represented in the game by their bird avatars) with randomly generated initial properties. In our implementation, the properties that will undergo evolution are the NN weights and the number of hidden layer units. For each element of the population we evaluate its ﬁtness (how well or bad is it in doing a given task) and its relative ﬁtness (how well or bad is it in a given task compared
to the other elements of the same population). The next step (crossover) is to pick two parents and combine their properties to create a child. The parents are chosen according to their relative fitness, the higher the ﬁtness, the higher the probability of being selected. Based on a predeﬁned mutation probability, the Child’s properties undergo mutation (small Changes in their properties), which deﬁnes the new generation. This iterative process is repeated until we ﬁnd a
generation (a model) that satisﬁes our demands (e.g. the NE agent reaches a target score). The NE training is illustrated in picture.

## Algorithm 1. Neuroevolution
```
procedure GENETIC ALGORITHM
   Setup:
   population <-- Create a population of N element (NN model)
   with randomly generated properties

   Loop:
   for element in population do
      evaluate element's fitness.
   new population <-- Empty population 

   for i = 0 to N do
        parents <-- Pick to parents according to relative fitness
        (crossover)
            child <-- Create a child by combining the properties 
            of these two parents
            mutatedChild <-- Mutate the child's properties base on
            given probability
            newPopulation <-- Add mutatedChild to new population 
    population <-- newPopulation
    goto Loop.
```
---
### Performance Evaluation
The state representation of the game (the inputs of the NN model) are the same
as the ones used in the RL approach, namely the difference between the bird’s position and the next lower pipe (dx, dy) and the bird velocity in y axis (vy). The NNs have three layers, the input layer has 3+1 (the bias) units, the hidden layer is

<p  align="center">
  <img src="src\gameCapture-1.jpg" width="150" title="game screenshot" >
  <img src="src\gameCapture-2.jpg" width="150" title="game representation model">
  <img src="src\gameCapture-3.jpg" width="150" title="game representation model">
</p>

initialized with 4 sigmoid nodes and the output layer has one sigmoid node. The population size and the mutation probability, considered as hyperparameters of model, were chosen after a grid search over intervals of discrete values.

Illustrates the learning curves when the population size is ﬁxed to 300 birds for each generation and the mutations probability is set to (0.3, 0.5, 0.7, 0.9). The mutation probability represents the likelihood of a mutation occurring in the NN weights or in the number of the hidden layer units. Note that the mutation probability significantly affects the score with the best performance achieved for mutation probability of 0.3.

Theoretically, the higher the population size, the better are the chances to
ﬁnd a satisfactory NE agent, however, in practice the computational cost limits this choice. In Fig. 6(b) are shown the learning curves where the mutation probability is set to 0.3 and the population varies in the interval (50, 100, 200, 300, 500). The plots show that a population size between 100 and 200 is enough to maintain a consistent growth. In order to illustrate the trend in the learning process, the curves in Fig. 6 represent moving average scores over sequences of 5 episodes.

The NE model with the optimal hyper-parameters (mutation probabil-
ity :03, population size = 200) was trained and the results are shown in
Fig. 6(c). After 280 generations the NE agent demonstrated a qualitative jump
in its competitive properties and achieved impressive scores in the range. of 105.
The scores over the last 10 episodes are given in Table 1, with the best result
of 149652 points and the average of 28694 points. At this stage7 the NE agent
has found the key performance parameters, the episodes has become very long
before it lose and the game was stopped.

There isn’t an ofﬁcial statistics regarding Flappy Bird competition between
human players, some sources claim 1940 points as the best recorded score for the
game. Even if this information may not be sufﬁciently reliable we believe that
the average score reached by the NE agent proposed in this paper has not been
ever achieved by a human.

<p  align="center">
  <img src="src\Cuve mutation probabilities.jpg"title="Cuve mutation probabilities">
  <img src="src\cuve population numbers.jpg"title="cuve population numbers">
  <img src="src\NE best mobel.jpg"title="NE best mobel">
</p>

---

### Reinforcement Learning and Neuroevolution in Flappy Bird Game

### Result	

| # | RL Score | NE Score |
|:-:| :------: | :------: |
| 1 |    120   |   4112   |
| 2 |    120   |   1939   |
| 3 |    245   |   2200   |
| 4 |    68    |   1812   |
| 5 |    70    |   18     |
| 6 |    105   |   21     |
| 7 |    100   |   1301   |
| 8 |    120   |   46321  |
| 9 |    90    |   79844  |
| 10|    75    |   149652 |


| Model | Average | SD   | Best| Worst |
|:-----:| :-----: |:---: | :--:| :---: |
|RL     | 11.3    |51.23 |  245| 68    |
|NE     | 28694   |50235.52 |  149652| 18    |

---
# Conclusion

Because we can readily measure their performance, applying AI approaches to games is a straightforward way to test and compare them. To play the Flappy Bird game, we compare the performance of Reinforcement Learning and Neuroevolution learning setups in this research.

The ability of these algorithms to encapsulate the general game logic, as well as the feature engineering used in this research, is the key to their high scores. e. In contrast to prior research, where deep models had to learn significant characteristics from high-dimensional picture data (game snapshots), here the AI agents' inputs were distance and velocity. Furthermore, the NE agent achieved a surprise high performance by using NNs' strong generalization ability in the game's continuous state space. Despite losing to the NE agent, the RL agent reached a platinum medal level of competitive performance.


# Team 
- Natchanon Wongsasri 6252500208
- Chakkarin Tumsungnoen 6252500232
- Korakod Khemkeaw 6252500330
- Juthathip Panyapunyarat 6252500453
- Aekpawin Phoomala 6252500500