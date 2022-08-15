# Awesome RL Envs

This is a collection of **RL envs** which are frequently used in **academic researches**.
And the repository will be continuously updated.

Welcome to follow and star!

## Table of Contents

- [Format and Terminology](#format-and-terminology)
- Envs
    - [Atari](#atari)
    - [MuJoCo](#mujoco)
    - [MPE](#mpe)
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
- (opt.)Special Subenv


### Terminology in the description table
1. Scale. Time cost to train a fair policy, specifically:
      - **Micro**: <30minutes
      - **Small**: 1-4 hours
      - **Middle**: 8-24 hours
      - **Large**: >1 day
2. State/Observation. Can be **Vector**, **Image**, or **Nested**.
3. Action. Can be **Discrete**, **Continuous**, or **Hybrid**
4. Reward. There are some special types of rewards:
      - **Fluctuating reward scale(Fluctuate)**
      - **Sparse reward(Sparse)**
      - **Multi-reward mixture(Multi)**
5. Termination. Can be **Finite** or **Infinite**.
5. Others.
      - **Procedural Content Generation(PCG)**
      - **Large Difference among sub-envs(LD)**
      - **Multi Agent(MA)**


## Atari


| Pong   | Qbert | SpaceInvaders   | MontezumaRevenge    | 
|--------|-------------|----------|-----------|
| <img src=./image/atari_pong.gif height="200px"/> | <img src=./image/atari_qbert.gif height="200px"/> | <img src=./image/atari_space_invaders.gif height="200px"/> | <img src=./image/atari_montezuma_revenge.gif height="200px"/>      | 

| Scale  | Observation | Action   | Reward    | Termintaion | Others |
|--------|-------------|----------|-----------|-------------|--------|
| Middle | Image       | Discrete | Fluctuate | Finite      | LD     |

- Overview: Atari 2600 has been the standard environment to test new Reinforcement Learning algorithms since Deep Q-Networks were introduced by Mnih et al. in 2013. Atari 2600 has been a challenging testbed due to its **high-dimensional video input** (size 210 x 160, frequency 60 Hz) and the **discrepancy of tasks between games**. The OpenAI Gym wrap Atari 2600 with a more standardized interface, and provides 59 Atari 2600 games as RL environments.
- Spaces(take Pong for example)
  - Observation space: ``Box(0, 255, (210, 160, 3), uint8)``
  - Action space: ``Discrete(6)``
  - Reward range: ``(-inf, inf)``
- Useful Links
  - Env Repo: [The Arcade Learning Environment(ALE)](https://github.com/mgbellemare/Arcade-Learning-Environment)
  - Blog/Doc: [Official Gym Documentation](https://www.gymlibrary.ml/environments/atari/)
  - Blog/Doc: DI-engine [doc](https://di-engine-docs.readthedocs.io/en/latest/13_envs/atari.html) | [文档](https://di-engine-docs.readthedocs.io/zh_CN/latest/13_envs/atari_zh.html)
  - Public Agent: [DI-engine doc](https://di-engine-docs.readthedocs.io/en/latest/13_envs/atari.html)
  - Public Agent: 
  - Public Agent: 
- Special Subenv: MontezumaRevenge
  - Key: Sparse reward
  - Useful links:
    - Blog/Doc: [OpenAI RND](https://openai.com/blog/reinforcement-learning-with-prediction-based-rewards/)
    - Public Agent: e.g. go-explore

## MuJoCo

| Hopper   | HalfCheetah | Ant   | Walker2D    | 
|--------|-------------|----------|-----------|
| <img src=./image/mujoco_hopper.gif height="200px"/> | <img src=./image/mujoco_half_cheetah.gif height="200px"/> | <img src=./image/mujoco_ant.gif height="200px"/> | <img src=./image/mujoco_walker2d.gif height="200px"/> | 


| Scale  | Observation | Action     | Reward           | Termintaion | Others |
|--------|-------------|------------|------------------|-------------|--------|
| Small  | Vector      | Continuous | Fluctuate, Multi | Finite      | LD     |


- Overview: Mujoco is a physics engine on robotics, biomechanics, graphics, animation, etc. that require fast and accurate simulation. It is often used as a benchmarking environment for continuous-space Reinforcement Learning algorithms. It is a collection of 20 sub-environments. Commonly used ones are `Ant`, `Half Cheetah`, `Hopper`, `Huanmoid`, `Walker2D`, etc.
- Spaces(take Hopper for example)
  - Observation space: ``Box(-inf, inf, (11, ), float32)``
  - Action space: ``Box(-1.0, 1.0, (3,), float32)``
  - Reward range: ``(-inf, inf)``
- Useful Links
  - Env Repo: [mujoco py](https://github.com/openai/mujoco-py)
  - Blog/Doc: [Official Gym Documentation](https://www.gymlibrary.ml/environments/mujoco/)
  - Blog/Doc: DI-engine [doc](https://di-engine-docs.readthedocs.io/en/latest/13_envs/mujoco.html) | [文档](https://di-engine-docs.readthedocs.io/zh_CN/latest/13_envs/mujoco_zh.html)
  - Public Agent: 
  - Public Agent: 
  - Public Agent: 


## MPE
(PettingZoo version)

| Simple Adversary   | Simple Speaker Listener | Simple Spread  | Simple World Comm | 
|--------|-------------|----------|-----------|
| <img src=./image/mpe_simple_adversary.gif height="200px"/> | <img src=./image/mpe_simple_speaker_listener.gif height="200px"/> | <img src=./image/mpe_simple_spread.gif height="200px"/> | <img src=./image/mpe_simple_world_comm.gif height="200px"/> | 


| Scale  | Observation | Action              | Reward           | Termintaion | Others |
|--------|-------------|---------------------|------------------|-------------|--------|
| Small  | Vector      | Discrete/Continuous | Fluctuate, Multi | Finite      | LD, MA |


- Overview: **PettingZoo** is a library of different multi-agent environments under a single elegant Python API, which is similar to OpenAI Gym library. PettingZoo is for Multi-Agent Eeinforcement Learning, while Gym is for Single-Agent. **Multi Particle Environments(MPE)** are also integrated in PettingZoo. MPE are a set of communication oriented environment where particle agents can (sometimes) move, communicate, see each other, push each other around, and interact with fixed landmarks.
- Spaces(take SimpleSpread for example)
  - Agent number: 3
  - Observation space: ``Box(-inf, inf, (18, ), float32)``
  - Action space: ``Discrete(5)``(Discrete) / ``(0.0, 1.0, (5,), float32)``(Continuous)
  - Reward range: ``(-inf, inf)``
- Useful Links
  - Env Repo: [PettingZoo](https://github.com/Farama-Foundation/PettingZoo)
  - Blog/Doc: [Official Documentation](https://www.pettingzoo.ml/mpe/)
  - Blog/Doc: DI-engine doc | [文档](https://di-engine-docs.readthedocs.io/zh_CN/latest/13_envs/multiagent_particle_zh.html)
  - Public Agent: 
  - Public Agent: 
  - Public Agent: 


## Contributing

Our purpose is to make this repo even better. If you are interested in contributing, please refer to [HERE](CONTRIBUTING.md) for instructions in contribution.

## License

Awesome Decision Transformer is released under the Apache 2.0 license.
