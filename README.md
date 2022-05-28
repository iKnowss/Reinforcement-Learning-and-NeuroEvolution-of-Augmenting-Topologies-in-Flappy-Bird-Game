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

    S — set of states.

    A - set of actions.

    P(s, a) - state—transition probability between each state and action.

    R - reward function that returns a reward based on the current state, the action taken, and/ or the next state.

    𝛾 - discount factor real number between 0 and 1), represents how much value loose the future rewards according to how distant in time they are

----------------------------------------------------
<script type="text/javascript" src="http://cdn.mathjax.org/mathjax/latest/MathJax.js?config=default"></script>

# Q-Learning to Flappy Bird Game
In this paper we apply the Q—Learning approach of RL. Based on experience with
previous games the algorithm creates the Q-table that contains the maximum expected future rewards for each action at each state. The best policy function, i.e. the function that, given a state, returns the action that maximizes the future reward, satisﬁes the Bellman’s equation

$$Q(s,a) = \R(x') + max_{a_i \in A}\left [\gamma  * Q(x', a_i) \right ]$$ 

where s is the current state and s’ is the next state after taking action a.

In our framework, the game state is represented by the difference between the bird’s position and the next lower pipe (dx, dy), and the bird velocity in y axis (vy). The possible actions in any state are jump or do nothing (the bird just falls). The reward function return +1 every time the agent completes a step without dying, and —100 when it dies. According to the rules of the game, the player gets a point only when the bird passes successfully between
two pipes. However, over a. number of frames the bird moves to find the next pipe and in order to learn if it is doing the right action our strategy rewards each step (frame) and not only the score step after the bird passes between two pipes. In the implementation of the Bellman’s Eq. (1), at each iteration instead of completely replacing the previous Q value we introduced a learning rate a (a real number between 0 and 1).

$$Q(s,a) = (1 -\alpha ) * Q(s, a) +\alpha *  \left [R(s') + max_{a_i \in A}\left [\gamma * Q(x', a_i) \right ]  \right ]$$

---
### Performance Evaluation
The learning rate ɑ and the discount factor 𝛾 were chosen after a grid search over the following intervals of discrete values, ɑ = [0.1. 0.3, 0.5, 0.7, 0.9] and 𝛾 = [ 0.1. 0.3, 0.5. 0.7, 0.9. 1]. The heat map in was obtained after training the RL model for each combination of parameters (30 combinations in total) over 1500 episodes. The episode ends whenever the bird hits a pipe. The values inside the rectangles, 