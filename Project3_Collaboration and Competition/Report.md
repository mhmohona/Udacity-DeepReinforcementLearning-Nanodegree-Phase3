# Project three: Collaboration and Competition

This report documents the course project 'Collaboration and Competition' where you train two agents to control rackets to bounce a ball over a net(play Tennis).

## Problem

In this game of Tennis, if an agent hits the ball over the net, it receives a reward of +0.1. If an agent lets a ball hit the ground or hits the ball out of bounds, it receives a reward of -0.01. Thus, the goal of each agent is to keep the ball in play.

The observation space consists of 8 variables corresponding to the position and velocity of the ball and racket. Each agent receives its own, local observation. Two continuous actions are available, corresponding to movement toward (or away from) the net, and jumping.

The task is episodic, and in order to solve the environment, your agents must get an average score of +0.5 (over 100 consecutive episodes, after taking the maximum over both agents)

## Solution

Based on the provided hints, [Deep Deterministic Policy Gradient(DDPG)](https://arxiv.org/abs/1509.02971) was selected to solve the problem of continous control involving two agents.

## Learning Algorithm

In this project, the same algorithm (i.e. Deep Deterministic Policy Gradient - DDPG) is being used as Project 'Continous Control'. \
DDPG is an actor-critic, model-free algorithm based on the deterministic policy gradient that can operate over continuous action spaces.
# Project One: Colaboration and Competition

The learning algorithm used for this project uses a Multi Agnet Actor-Critic network with a local and target network for both the Actor and Critic (for both agents) along with a replay buffer to store experience tuples. I used the algorithm from https://github.com/udacity/deep-reinforcement-learning/tree/master/ddpg-pendulum as a template and experimented on it using different hyperparameters for both actor and critic networks. The way the MADDPG algorithm works is as follows:

- Say we have an environment with multiple with a state space and and a continuous actions space for both agents.
- The MADDPG algorithm initializes four neural networks (two local networks and two target networks for the Actor and Critic) for all agents separately.
- The states of all the agents are used to train the agent during training time. But that information is not used during the testing or execution phase.
- During training the critic for each agent, uses some extra information like states observed and actions taken by all the other agents.
- During execution time, only the actors are present and hence only local observations and actions are used.
- Since the MADDPG is an off-policy algorithm, we will train on the local networks and "softly" update the target network for all agents every few timesteps based on a hyperparameter, TAU.
- This algorithm can be used in Cooperative, Competitive and Mixed scenrios

In this implementation, there are two neural networks(local and target) each for Actor and Critic. \
Number of hidden layers: 2 \
Hidden Layer 1: 512 units \
Hidden Layer 2: 256 units \
Activation function(both layers): ReLU

Ornstein-Uhlenbeck noise is injected in the action space as per the DDPG paper for better Exploration.

Replay buffer and Soft update are implemented for sample efficiency and stability.

## Plot of Rewards

The algorithm took 1177 episodes to solve.

![](plot_p3.JPG)

## Ideas for Future Work

- Change network sizes and choose different hyperparameters
- Trying other algorithms like PPO, A3C or D4PG
- Use parameter space noise rather than noise on action. https://vimeo.com/252185862
- Current our replay buffer is dumb. We can use prioritised experience buffer. https://github.com/Damcy/prioritized-experience-replay
- Different replay buffer for actor/critic
- Try adding dropouts in critic network
