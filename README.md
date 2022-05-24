README

RL (Q - Learning)
NN (NEAT)
----------------------------------------------------
### RL
The reward function was defined to penalise -100 for a death and 0 otherwise, such that the agent's focus is the get as high a score as possible. This ensures that the reward function has sufficient impact each episode vs an implementation where rewarding +1 for a score increase means that panelisation has little to no effect.
Through undertaking this project the most difficult part was defining a good reward function and how this links to the agent learning.

### Initial Training

The agent was initially trained for around 20,000 episodes without any exploration and the learning rate alpha = 0.7 and the discount factor = 1. 

## Getting Started

Added modules:
- [anaysis.py](analysis.py): Analysis file for investigating agent performance
- [config.py](config.py): Config file for changing the agent training parameters
- [flappy_rl.py](flappy_rl.py): [FlapPyBird](https://github.com/sourabhv/FlapPyBird) implementation with agent training/runner code included
- [q_learning.py](q_learning.py): An implementation of a Q-learning agent class made with reference to [rl-flappybird](https://github.com/kyokin78/rl-flappybird)

Change the training parameters in [config.py](config.py) and run the [flappy_rl.py](flappy_rl.py) module.

### How-to (as tested on MacOS)

1. Install Python 3.x (recommended) 2.x from [here](https://www.python.org/download/releases/)

2. Install [pipenv]

2. Install PyGame 1.9.x from [here](http://www.pygame.org/download.shtml)

3. Clone the repository:

```bash
$ git clone https://github.com/sourabhv/FlapPyBird
```

or download as zip and extract.

4. In the root directory run

```bash
$ pipenv install
$ pipenv run python flappy.py
```

5. Use <kbd>&uarr;</kbd> or <kbd>Space</kbd> key to play and <kbd>Esc</kbd> to close the game.
----------------------------------------------------
### NEAT
# NEAT-Flappy-Bird
An AI that plays flappy bird! Using the NEAT python module.

# Instructions
Simply run *flappy_bird.py* and watch an AI start training itself to play the game of flappy bird!
