---
layout: post
title: Reinforcement learning grade 1
---

# Reinforcement learning grade 1: MAB problem $\epsilon$-greedy

Talking about Multi-armed Bandits problem solving in reinforcement learning, there's no better book than the [Sutton & Barto book](http://incompleteideas.net/book/the-book.html).

I will skip the $\epsilon$-greedy algorithm background introduction, and focus on the algorithm implementation in python.

In a stationary probability distribution of k-arms environment, a bandit was chose for each step. The purpose of chosen is to maximize returns in long run, with e-greedy, a threshold of $\epsilon$ will be set to determine how to make choices:

1. If a random choice value is greater than e, then pick the bandit with max average rewards from start, this is called "exploit".

2. Else randomly pick a bandit, to explore other potential candidates, this is called "explore".

We are making a balance between explore and exploit by setting an appropriate "$\epsilon$".
As in 2nd scenario, there's really nothing to do with random selection, we will focus on how to calculate out max historic average rewards, aka:

$$ Q_{n+1} = \frac{1}{n} * (R_1+R_2+R_3+...+R_n) $$

$Q_{n+1}$ denotes estimation of action value after n selections, $R_i$ denotes reward received of $i$th selection.

Basically this is the simplest version of e-greedy, in order to make it computational effective, that is avoid of recording and accumulating actions and rewards from each beginning, the previous formula could be transformed into:

$$ Q_{n+1} = \frac{1}{n}\sum_{i=1}^nR_i $$

$$ Q_{n+1} = \frac{1}{n}(R_n+(n-1)\frac{1}{n-1}\sum_{i=1}^{n-1}R_i)$$

$$ Q_{n+1} = \frac{1}{n}(R_n+(n-1)Q_n) $$

$$ Q_{n+1} = Q_n + \frac{1}{n}(R_n - Q_n) $$

And till now, the derivation is perfectly done, on calculating each Q, we will only need 2 parameters: the number of selections "n" and the current reward R.

Now let's start the code implementation.

There are 3 objects in MAB problem, each with different responsibilities:

* Bandit:
  * Give reward upon certain selection

* Agent:
  * Make a choice
  * Update action value assessment, formula (5)

* Plan:
  * Propose how many steps for agent to proceed, i.e. n = 1000
  * Propose how many runs for agent to execute repeatedly, i.e. 5 runs, for each run contains 1000 steps

Here will be nice to have a diagram to indicate relationships between this 3, will try to get one later.

```ipynb
# MAB in e-greedy
# author: hifreedo git: hifreedo

%matplotlib inline
import matplotlib.pyplot as plt
import random
import numpy as np

# global settings
epsilon = 0.1
bandit_prob = [0.1, 0.2, 0.5, 0.6, 0.3, 0.4, 0.6, 0.8, 0.55, 0.65]
n_bandits = len(bandit_prob)
n_steps = 1000
n_runs = 2000

class Bandit:
    def __init__(self, bandit_prob):
        self.bandits = len(bandit_prob)
        self.bandit_prob = bandit_prob
    def giveReward(self, action):
        rand = random.random()
        reward = 1 if (rand < self.bandit_prob[action]) else 0
        return reward

class Agent:
    def __init__(self, epsilon, n_bandits):
        self.epsilon = epsilon
        self.K = np.zeros(n_bandits, dtype = int) # action chose history
        self.Q = np.zeros(n_bandits, dtype = float) # action value history
        
    def makeChoice(self, n_bandits):
        rand = random.random()
        if rand < self.epsilon:
            return np.random.randint(n_bandits)
        else:
            # return np.argmax(self.Q)
            return np.random.choice(np.flatnonzero(self.Q == self.Q.max()))
        
    def updateQ(self, action, reward):
        self.K[action] += 1
        self.Q[action] += 1. / self.K[action] * (reward - self.Q[action]) # formula (5)
        
def run(bandit, agent):
    # experiment
    reward_history = []
    choice_history = []
    
    for i in range(n_steps):
        action = agent.makeChoice(n_bandits)
        reward = bandit.giveReward(action)
        agent.updateQ(action, reward)
        
        # recording for plotting algorithm performance
        choice_history.append(action)
        reward_history.append(reward)
        
    return(np.array(choice_history), np.array(reward_history))

reward_over_steps = np.zeros(n_steps, dtype=float)
action_over_steps = np.zeros((n_bandits, n_steps))

for i in range(n_runs):
    # initialize for each run
    bandit = Bandit(bandit_prob)
    agent = Agent(epsilon, n_bandits)
    choice_history, reward_history = run(bandit, agent)
    
    reward_over_steps += reward_history
    for index, action in enumerate(choice_history):
        action_over_steps[action][index] += 1
        
avg_reward_over_runs = reward_over_steps / np.float(n_runs)

# plot average reward
plt.plot(avg_reward_over_runs)
plt.xlabel("steps")
plt.ylabel("rewards")
plt.title("Average reward over {} runs".format(n_runs))
plt.xlim([1, n_steps])
ax = plt.gca()
ax.set_xscale("log")
plt.show()

# plot bandit chose history
plt.figure(figsize=(18, 12))
for i in range(n_bandits):
    plt.plot(100*action_over_steps[i]/n_runs, linewidth = 5, label="Bandit #{}".format(i+1))
plt.title("Bandit action over steps", fontsize = 26)
plt.xlabel("steps", fontsize = 26)
plt.ylabel("bandit chose %", fontsize = 26)
leg = plt.legend(loc="upper left", fontsize = 26)
for lg in leg.legendHandles:
    lg.set_linewidth(10)
ax = plt.gca()
plt.xlim([1, n_steps])
plt.ylim([0, 100])
plt.xticks(fontsize=24)
plt.yticks(fontsize=24)
ax.set_xscale("log")
plt.show()

```
Following are the results of the code:

Average rewards over steps:

<img src="{{site.url}}/img/mab_e_01.png">

Bandit chose percentage over steps:

<img src="{{site.url}}/img/mab_e_02.png">
