# Awesome RL Envs

This is a collection of **RL envs** which are frequently used in **academic researches**.
And the repository will be continuously updated.

Welcome to follow and star!

## Table of Contents

- [Format and Terminology](#format-and-terminology)
- [Envs](#envs)
    - [Atari](#atari)
    - [MuJoCo](#mujoco)
    - [MPE](#mpe)
    - [SMAC](#smac)
- [Contributing](#contributing)

## Format and Terminology

### Format
Env Name
- Description Table
- Overview
- Spaces
  - Observation Space
  - Action Space
  - Reward Range
- Useful Links
  - Env Repo
  - Blog/Doc
  - Public Agent
- (optional) Special Subenv


### Terminology in the description table
1. Scale. Time cost to train a fair policy, with 1 NVIDIA V100 + 32-core CPU.

| Micro        | Small       | Middle     | Large     |
|--------------|-------------|------------|-----------|
| < 30 minutes | 1-4 hours   | 8-24 hours | > 1 day   |
| Pendulum, CartPole, Gym hybrid | [MPE](#mpe), Slimevolley, [MuJoCo](#mujoco)   | Procgen, D4rl, [Atari](#atari), [SMAC](#smac) | MineRL, CARLA, GRF   |

2. State/Observation. 

| Vector             | Image                        | Nested     |
|--------------------|------------------------------|------------|
| A list of numbers. | Often 3-channel RGB image.   | Like `struct` in C language: Containing multiple members, and each member can be Vector or Image. |
| [MPE](#mpe), [MuJoCo](#mujoco)   | [Atari](#atari), DMControl | MineRL, CARLA   |

3. Action.
 
| Discrete  | Continuous   | Hybrid        |
|-----------|--------------|---------------|
| Integer   |  Float       | Contains both |
| [Atari](#atari), [SMAC](#smac)   | [MuJoCo](#mujoco), DMControl | Gym hybrid, CARLA   |

4. Reward.

| Many orders of magnitude (Magnitude)  | Sparse reward (Sparse)   | Multi-reward mixture (Multi)        |
|-----------|--------------|---------------|
| Magnitudes and frequencies of rewards vary wildly between different games or episodes. You can refer to [Learning values across many orders of magnitude](https://arxiv.org/abs/1602.07714). |  Rewards extrinsic to the agent are extremely sparse, or absent altogether. You can refer to [ICM paper](https://arxiv.org/abs/1705.05363v1) and [RND paper](https://arxiv.org/abs/1810.12894).    | More than one type of reward is measured. You can refer to [Efficient Reinforcement Learning with Multiple Reward Functions for Randomized Controlled Trial Analysis](http://people.seas.harvard.edu/~samurphy/papers/lizotte10multipleFINAL.pdf). |
| `Centipede` of [Atari](#atari)   | Minigrid, [SMAC](#smac) | CARLA   |

5. Termination.

| Finite  | Infinite  | 
|---------|-----------|
| An episode will end at some point.    |  An episode will not end until you terminate it.   |
| [Atari](#atari), [SMAC](#smac)   | `HalfCheetah` of [MuJoCo](#mujoco) |

6. Others.

| Procedural Content Generation (PCG)  | Large Difference among sub-envs (LD)   | Multi Agent (MA)     |
|-----------|--------------|---------------|
| Sub-environments are randomly created, encouraging agent to robustly learn a relevant skill, other than memorizing specific trajectories. You can refer to [Procgen paper](https://arxiv.org/abs/1912.01588).   |  Different sub-envs vary a lot. You can refer to the radar plot in [bsuite](https://github.com/deepmind/bsuite).    | You must control more than one agent at a time. You can refer to [An Overview of Multi-Agent Reinforcement Learning from Game Theoretical Perspective](https://arxiv.org/abs/2011.00583). |
| Procgen   | [MuJoCo](#mujoco), [MPE](#mpe), DMControl | [MPE](#mpe), [SMAC](#smac), GRF   |


## Envs
### Atari


| Pong   | Qbert | SpaceInvaders   | MontezumaRevenge    | 
|--------|-------------|----------|-----------|
| <img src=./image/atari_pong.gif height="200px"/> | <img src=./image/atari_qbert.gif height="200px"/> | <img src=./image/atari_space_invaders.gif height="200px"/> | <img src=./image/atari_montezuma_revenge.gif height="200px"/>      | 

| Scale  | Observation | Action   | Reward    | Termintaion | Others |
|--------|-------------|----------|-----------|-------------|--------|
| Middle | Image       | Discrete | Fluctuate | Finite      | LD     |

- Overview: Atari 2600 has been the standard environment to test new Reinforcement Learning algorithms since Deep Q-Networks were introduced by Mnih et al. in 2013. Atari 2600 has been a challenging testbed due to its **high-dimensional video input**  (size 210 x 160, frequency 60 Hz) and the **discrepancy of tasks between games**. The OpenAI Gym wrap Atari 2600 with a more standardized interface, and provides 59 Atari 2600 games as RL environments.
- Spaces (take `Pong` for example)
  - Observation space: ``Box(0, 255, (210, 160, 3), uint8)``
  - Action space: ``Discrete(6)``
  - Reward range: ``(-inf, inf)``
- Useful Links
  - Env Repo: [The Arcade Learning Environment (ALE)](https://github.com/mgbellemare/Arcade-Learning-Environment)
  - Blog/Doc: [Official Gym Documentation](https://www.gymlibrary.ml/environments/atari/)
  - Blog/Doc: DI-engine [doc](https://di-engine-docs.readthedocs.io/en/latest/13_envs/atari.html) | [文档](https://di-engine-docs.readthedocs.io/zh_CN/latest/13_envs/atari_zh.html)
  - Public Agent: [Stable Baselines 3](https://github.com/DLR-RM/stable-baselines3), RL Baselines3 Zoo [DQN](https://github.com/DLR-RM/rl-baselines3-zoo/blob/master/hyperparams/dqn.yml) | [PPO](https://github.com/DLR-RM/rl-baselines3-zoo/blob/master/hyperparams/ppo.yml) | [A2C](https://github.com/DLR-RM/rl-baselines3-zoo/blob/master/hyperparams/a2c.yml)
  - Public Agent: [DI-engine](https://github.com/opendilab/DI-engine/tree/main/dizoo/atari)
  - Public Agent: [tianshou](https://github.com/thu-ml/tianshou/tree/master/examples/atari)
- Special Subenv: `MontezumaRevenge`
  - Key: Sparse reward
  - Useful links:
    - Blog/Doc: [Prediction-Based Rewards (By OpenAI)](https://openai.com/blog/reinforcement-learning-with-prediction-based-rewards/)
    - Public Agent: [Random Network Distillation (RND)](https://github.com/openai/random-network-distillation)
    - Public Agent: [Go-Explore](https://github.com/uber-research/go-explore)

### MuJoCo

| Hopper   | HalfCheetah | Ant   | Walker2D    | 
|--------|-------------|----------|-----------|
| <img src=./image/mujoco_hopper.gif height="200px"/> | <img src=./image/mujoco_half_cheetah.gif height="200px"/> | <img src=./image/mujoco_ant.gif height="200px"/> | <img src=./image/mujoco_walker2d.gif height="200px"/> | 


| Scale  | Observation | Action     | Reward           | Termintaion | Others |
|--------|-------------|------------|------------------|-------------|--------|
| Small  | Vector      | Continuous | Fluctuate, Multi | Finite      | LD     |


- Overview: Mujoco is a physics engine on robotics, biomechanics, graphics, animation, etc. that require fast and accurate simulation. It is often used as a benchmarking environment for continuous-space Reinforcement Learning algorithms. It is a collection of 20 sub-environments. Commonly used ones are `Ant`, `Half Cheetah`, `Hopper`, `Huanmoid`, `Walker2D`, etc.
- Spaces (take `Hopper` for example)
  - Observation space: ``Box(-inf, inf, (11, ), float32)``
  - Action space: ``Box(-1.0, 1.0, (3,), float32)``
  - Reward range: ``(-inf, inf)``
- Useful Links
  - Env Repo: [mujoco (by DeepMind)](https://github.com/deepmind/mujoco), [mujoco-py (by OpenAI)](https://github.com/openai/mujoco-py)
  - Blog/Doc: [Official Gym Documentation](https://www.gymlibrary.ml/environments/mujoco/)
  - Blog/Doc: DI-engine [doc](https://di-engine-docs.readthedocs.io/en/latest/13_envs/mujoco.html) | [文档](https://di-engine-docs.readthedocs.io/zh_CN/latest/13_envs/mujoco_zh.html)
  - Public Agent: [Stable Baselines 3](https://github.com/DLR-RM/stable-baselines3), RL Baselines3 Zoo [TD3](https://github.com/DLR-RM/rl-baselines3-zoo/blob/master/hyperparams/td3.yml) | [PPO](https://github.com/DLR-RM/rl-baselines3-zoo/blob/master/hyperparams/ppo.yml) | [SAC](https://github.com/DLR-RM/rl-baselines3-zoo/blob/master/hyperparams/sac.yml)
  - Public Agent: [DI-engine](https://github.com/opendilab/DI-engine/tree/main/dizoo/mujoco)
  - Public Agent: [ChainerRL](https://github.com/chainer/chainerrl/tree/master/examples/mujoco)


### MPE
(PettingZoo version)

| Simple Adversary   | Simple Speaker Listener | Simple Spread  | Simple World Comm | 
|--------|-------------|----------|-----------|
| <img src=./image/mpe_simple_adversary.gif height="200px"/> | <img src=./image/mpe_simple_speaker_listener.gif height="200px"/> | <img src=./image/mpe_simple_spread.gif height="200px"/> | <img src=./image/mpe_simple_world_comm.gif height="200px"/> | 


| Scale  | Observation | Action              | Reward           | Termintaion | Others |
|--------|-------------|---------------------|------------------|-------------|--------|
| Small  | Vector      | Discrete/Continuous | Fluctuate, Multi | Finite      | LD, MA |


- Overview: **PettingZoo** is a library of different multi-agent environments under a single elegant Python API, which is similar to OpenAI Gym library. PettingZoo is for Multi-Agent Eeinforcement Learning, while Gym is for Single-Agent. **Multi Particle Environments (MPE)** are also integrated in PettingZoo. MPE are a set of communication oriented environment where particle agents can (sometimes) move, communicate, see each other, push each other around, and interact with fixed landmarks.
- Spaces (take `SimpleSpread` for example)
  - Agent number: 3
  - Observation space: ``Box(-inf, inf, (18, ), float32)``
  - Action space: ``Discrete(5)`` (Discrete) / ``(0.0, 1.0, (5,), float32)`` (Continuous)
  - Reward range: ``(-inf, inf)``
- Useful Links
  - Env Repo: [PettingZoo](https://github.com/Farama-Foundation/PettingZoo)
  - Blog/Doc: [Official Documentation](https://www.pettingzoo.ml/mpe/)
  - Blog/Doc: DI-engine doc | [文档](https://di-engine-docs.readthedocs.io/zh_CN/latest/13_envs/multiagent_particle_zh.html)
  - Public Agent: [DI-engine](https://github.com/opendilab/DI-engine/tree/main/dizoo/petting_zoo)
  - Public Agent: [MAPPO](https://github.com/marlbenchmark/on-policy)


### SMAC

| 3s_vs_5z   | 2c_vs_64zg | corridor   | 
|------------|------------|------------|
| <img src=./image/smac_3s_vs_5z.jpg height="200px"/> | <img src=./image/smac_2c_vs_64zg.jpg height="200px"/> | <img src=./image/smac_corridor.jpg height="200px"/> |

| Scale  | Observation | Action   | Reward           | Termintaion | Others |
|--------|-------------|----------|------------------|-------------|--------|
| Middle | Vector      | Discrete | Sparse           | Finite      | MA     |


- Overview: SMAC is an environment for Multi-Agent collaborative Reinforcement Learning (MARL) on Blizzard StarCraft II, which is short for "StarCraft Multi-Agent Challenge". SMAC uses Blizzard StarCraft II’s machine learning API and DeepMind’s PySC2 to provide a friendly interface for the interaction between agents and StarCraft II. Compared to PySC2, SMAC focuses on a decentralized micro-operation scheme, where each agent of the game is controlled by a separate RL agent.
- Spaces(take `XXXX` for example)
  - Observation space:
  - Action space:
  - Reward range:
- Useful Links
  - Env Repo: [SMAC](https://github.com/oxwhirl/smac)
  - Blog/Doc: DI-engine [doc](https://di-engine-docs.readthedocs.io/en/latest/13_envs/smac.html) | [文档](https://di-engine-docs.readthedocs.io/zh_CN/latest/13_envs/smac_zh.html)
  - Public Agent: [DI-engine](https://github.com/opendilab/DI-engine/tree/main/dizoo/smac)
  - Public Agent: [PyMARL2](https://github.com/hijkzzz/pymarl2)
  - Public Agent: [RLlib](https://github.com/oxwhirl/smac/tree/master/smac/examples/rllib)


## Contributing

Our purpose is to make this repo even better. If you are interested in contributing, please refer to [HERE](CONTRIBUTING.md) for instructions in contribution.

## License

Awesome Decision Transformer is released under the Apache 2.0 license.
