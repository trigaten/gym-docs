---
layout: env_selection
title: Mujoco Environments
---
<div class="selection-content" markdown="1">

MuJoCo stands for Multi-Joint dynamics with Contact. It is a physics engine for faciliatating research and development in robotics, biomechanics, graphics and animation, and other areas where fast and accurate simulation is needed.

The unique dependencies for this set of environments can be installed via:

````bash
pip install gym[mujoco]
````

These environments also require that the MuJoCo engine be installed. As of October 2021 DeepMind has acquired MuJoCo and is open sourcing it in 2022, making it free for everyone. Instructions on installing the MuJoCo engine can be found at their [website](https://mujoco.org) and [GitHub repository](https://github.com/deepmind/mujoco). Using MuJoCo with OpenAI Gym also requires that the framework `mujoco-py` be installed, which can be found at the [GitHub repository](https://github.com/openai/mujoco-py/tree/master/mujoco_py) (this dependency in installed with the above command).

There are ten Mujoco environments: Ant, HalfCheetah, Hopper, Humanoid, HumanoidStandup, IvertedDoublePendulum, InvertedPendulum, Reacher, Swimmer, and Walker. All of these environments are stochastic in terms of their initial state, with a Gaussian noise added to a fixed initial state in order to add stochasticity. The state spaces for MuJoCo environments in Gym consist of two parts that are flattened and concatented together: a position of a body part ('*mujoco-py.mjsim.qpos*') or joint and its corresponding velocity ('*mujoco-py.mjsim.qvel*'). Often, some of the first positional elements are omitted from the state space since the reward is calculated based on their values, leaviing it up to the algorithm to infer those hidden values indirectly.

Among Gym environments, this set of environments can be considered as more difficult ones to solve by a policy.

Environments can be configured by changing the XML files or by tweaking the parameters of their classes.

</div>
