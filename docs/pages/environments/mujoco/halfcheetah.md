HalfCheetah
---
|Title|Action Type|Action Shape|Action Values|Observation Type| Observation Shape|Observation Values|Average Total Reward|Import|
| ----------- | -----------| ----------- | -----------|-----------| ----------- | -----------| ----------- | -----------|
|HalfCheetah-v3,HalfCheetah-v2|Continuous|(6,)|[-1,1], [-1,1], [-1,1], [-1,1], [-1,1], [-1,1]| Box |(17,)|[(-inf,inf), (-inf,inf), (-inf, inf), (-inf,inf), (-inf,inf), (-inf,inf), (-inf, inf), (-inf,inf), (-inf,inf), (-inf,inf), (-inf, inf), (-inf,inf), (-inf,inf), (-inf,inf), (-inf, inf), (-inf,inf), (-inf,inf)]| |`from gym.envs.mujoco import half_cheetah`|
---

### Description

This environment is based on the work by P. Wawrzy´nski in ["A Cat-Like Robot Real-Time Learning to Run"](http://staff.elka.pw.edu.pl/~pwawrzyn/pub-s/0812_LSCLRR.pdf). The HalfCheetah is a 2-dimensional robot consisting of 9 links and 8
joints connecting them (including two paws). The goal is to apply a torque on the joints to make the cheetah run forward (right) as fast as possible, with a positive reward allocated based on the distance moved forward and a negative reward allocated for moving backward. The torso and head of the cheetah are fixed, and the torque can only be applied on the other 6 joints over the front and back thighs (connecting to the torso), shins (connecting to the thighs) and feet (connecting to the shins).

### Action Space
The agent take a 6-element vector for actions.
The action space is a continuous `(action, action, action, action, action, action)` all in `[-1.0, 1.0]`, where `action` represents the numerical torques applied between *links*

| Num | Action                    | Control Min | Control Max | Name (in corresponding XML file) | Joint | Unit |
|-------|----------------------|---------------|----------------|---------------------------------------|-------|------|
| 0   | Torque applied on the back thigh rotor  | -1 | 1 | bthigh | hinge | torque (N m) |
| 1   | Torque applied on the back shin rotor  | -1 | 1 | bshin | hinge | torque (N m) |
| 2   | Torque applied on the back foot rotor | -1 | 1 | bfoot | hinge | torque (N m) |
| 3   | Torque applied on the front thigh rotor  | -1 | 1 | fthigh | hinge | torque (N m) |
| 4   | Torque applied on the front shin rotor  | -1 | 1 | fshin | hinge | torque (N m) |
| 5   | Torque applied on the front foot rotor  | -1 | 1 | ffoot | hinge | torque (N m) |

### Observation Space

The state space consists of positional values of different body parts of the cheetah, followed by the velocities of those individual parts (their derivatives) with all the positions ordered before all the velocities.

The observation is a `ndarray` with shape `(17,)` where the elements correspond to the following:

| Num | Observation           | Min                  | Max                | Name (in corresponding XML file) | Joint| Unit |
|-----|-----------------------|----------------------|--------------------|----------------------|--------------------|--------------------|
| 0     | x-coordinate of the center of mass               | -Inf                 | Inf                | rootx | slide | position (m) |
| 1     | y-coordinate of the center of mass               | -Inf                 | Inf                | rootz | slide | position (m) |
| 2     | angle of the front tip                           | -Inf                 | Inf                | rooty | hinge | angle (rad) |
| 3     | angle of the back thigh rotor                   | -Inf                 | Inf                | bthigh | hinge | angle (rad) |
| 4     | angle of the back shin rotor                     | -Inf                 | Inf                | bshin | hinge | angle (rad) |
| 5     | angle of the back foot rotor     | -Inf                 | Inf                | bfoot | hinge | angle (rad) |
| 6     | velocity of the tip along the y-axis     | -Inf                 | Inf                | fthigh | hinge | angle (rad) |
| 7     | angular velocity of front tip                | -Inf                 | Inf                | fshin | hinge | angle (rad) |
| 8     | angular velocity of second rotor        | -Inf                 | Inf                | ffoot | hinge | angle (rad) |
| 9     | x-coordinate of the front tip               | -Inf                 | Inf                | rootx | slide | velocity (m/s) |
| 10   | y-coordinate of the front tip               | -Inf                 | Inf                | rootz | slide | velocity (m/s) |
| 11   | angle of the front tip                           | -Inf                 | Inf                | rooty | hinge | angular velocity (rad/s) |
| 12   | angle of the second rotor                   | -Inf                 | Inf                | bthigh | hinge | angular velocity (rad/s) |
| 13   | angle of the second rotor                   | -Inf                 | Inf                | bshin | hinge | angular velocity (rad/s) |
| 14   | velocity of the tip along the x-axis     | -Inf                 | Inf                | bfoot | hinge | angular velocity (rad/s) |
| 15   | velocity of the tip along the y-axis     | -Inf                 | Inf                | fthigh | hinge |angular velocity (rad/s) |
| 16   | angular velocity of front tip                | -Inf                 | Inf                | fshin | hinge | angular velocity (rad/s) |
| 17   | angular velocity of second rotor        | -Inf                 | Inf                | ffoot | hinge | angular velocity (rad/s) |


**Note:**
In practice (and Gym implementation), the first positional element is omitted from the state space since the reward function is calculated based on that value. This value is hidden from the algorithm, which in turn has to develop an abstract understanding of it from the observed rewards.Therefore, observation space has shape `(8,)` and looks like:

| Num | Observation           | Min                  | Max                | Name (in corresponding XML file) | Joint| Unit |
|-----|-----------------------|----------------------|--------------------|----------------------|--------------------|--------------------|
| 0     | y-coordinate of the front tip               | -Inf                 | Inf                | rootz | slide | position (m) |
| 1     | angle of the front tip                           | -Inf                 | Inf                | rooty | hinge | angle (rad) |
| 2     | angle of the second rotor                   | -Inf                 | Inf                | bthigh | hinge | angle (rad) |
| 3     | angle of the second rotor                   | -Inf                 | Inf                | bshin | hinge | angle (rad) |
| 4     | velocity of the tip along the x-axis     | -Inf                 | Inf                | bfoot | hinge | angle (rad) |
| 5     | velocity of the tip along the y-axis     | -Inf                 | Inf                | fthigh | hinge | angle (rad) |
| 6     | angular velocity of front tip                | -Inf                 | Inf                | fshin | hinge | angle (rad) |
| 7     | angular velocity of second rotor        | -Inf                 | Inf                | ffoot | hinge | angle (rad) |
| 8     | x-coordinate of the front tip               | -Inf                 | Inf                | rootx | slide | velocity (m/s) |
| 9     | y-coordinate of the front tip               | -Inf                 | Inf                | rootz | slide | velocity (m/s) |
| 10   | angle of the front tip                           | -Inf                 | Inf                | rooty | hinge | angular velocity (rad/s) |
| 11   | angle of the second rotor                   | -Inf                 | Inf                | bthigh | hinge | angular velocity (rad/s) |
| 12   | angle of the second rotor                   | -Inf                 | Inf                | bshin | hinge | angular velocity (rad/s) |
| 13   | velocity of the tip along the x-axis     | -Inf                 | Inf                | bfoot | hinge | angular velocity (rad/s) |
| 14   | velocity of the tip along the y-axis     | -Inf                 | Inf                | fthigh | hinge |angular velocity (rad/s) |
| 15   | angular velocity of front tip                | -Inf                 | Inf                | fshin | hinge | angular velocity (rad/s) |
| 16   | angular velocity of second rotor        | -Inf                 | Inf                | ffoot | hinge | angular velocity (rad/s) |

### Rewards
The reward consists of two parts:
- *reward_run*: A reward of moving forward which is measured as *(x-coordinate before action - x-coordinate after action)/dt*. *dt* is the time between actions and is dependeent on the frame_skip parameter (default is 5), where the *dt* for one frame is 0.01 - making the default *dt = 5*0.01 = 0.05*. This reward would be positive if the cheetah runs forward (right) desired.
- *reward_control*: A negative reward for penalising the swimmer if it takes actions that are too large. It is measured as *-coefficient x sum(action<sup>2</sup>)* where *coefficient* is a parameter set for the control and has a default value of 0.1

The total reward returned is ***reward*** *=* *reward_run + reward_control*

### Starting State
All observations start in state (0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0,) with a noise added to the initial state for stochasticity. As seen before, the first 8 values in the state are positional and the last 9 values are velocity. A uniform noise in the range of [-0.1, 0.1] is added to the positional values while a standard normal noise with a mean of 0 and standard deviation of 0.1 is added to the initial velocity values of all zeros.

### Episode Termination
The episode terminates when the episode length is greater than 1000.

### Arguments

No additional arguments are currently supported (in v2 and lower), but modifications can be made to the XML file in the assets folder at `gym/envs/mujoco/assets/half_cheetah.xml` (or by changing the path to a modified XML file in another folder).

```
env = gym.make('HalfCheetah-v2')
```

v3 and beyond take gym.make kwargs such as xml_file, ctrl_cost_weight, reset_noise_scale etc.

```
env = gym.make('HalfCheetah-v3', ctrl_cost_weight=0.1, ....)
```


### Version History

* v3: support for gym.make kwargs such as xml_file, ctrl_cost_weight, reset_noise_scale etc. rgb rendering comes from tracking camera (so agent does not run away from screen)
* v2: All continuous control environments now use mujoco_py >= 1.50
* v1: max_time_steps raised to 1000 for robot based tasks. Added reward_threshold to environments.
* v0: Initial versions release (1.0.0)
