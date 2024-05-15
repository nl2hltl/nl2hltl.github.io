To perform the skill of moving a robot arm to reach a goal position in Cartesian space while avoiding obstacles in a cluttered scene, we have chosen the following controllers:

### Task Controller: KinematicTrajectoryModelPredictiveController

**Input Ports:**
1. **controller_parameters**: Takes in parameters such as the desired goal pose for the end effector. The goal pose is obtained from `controller_parameters` skill input, specifically `controller_parameters['goal_pose']`.
2. **measured_arm_position**: The current joint positions of the robot arm, directly available from the available measurements as `measured_arm_position`.
3. **measured_arm_velocity**: The current joint velocities of the robot arm, directly available from available measurements as `measured_arm_velocity`.

**Constant Parameters Used:**
- **resolve_period**: Set to 3.0. This parameter determines the frequency at which the MPC solves the trajectory optimization problem.
- **num_steps**: Set to 20. This dictates the number of discrete steps used by the MPC for planning the trajectory.

**Description:**
The `KinematicTrajectoryModelPredictiveController` generates a trajectory in joint space that accounts for collision avoidance, aiming to reach the desired end-effector pose specified in Cartesian coordinates. This controller is ideal for environments with obstacles, planning a safe path for the robot arm.


### Tracking Controller: SafeController

**Input Ports:**
1. **arm_target**: The desired joint target for the arm. This input comes from the output of the `KinematicTrajectoryModelPredictiveController` (`q_nom`), representing the next set of target joint positions to follow the computed trajectory.
2. **arm_target_type**: Specifies the type of target (position, velocity, or torque). For this setup, we use `JointTarget.kPosition` as we are providing target joint positions from the task controller.
3. **arm_position**: The current joint positions of the arm, obtained from `measured_arm_position`.
4. **arm_velocity**: The current joint velocities of the arm, taken from `measured_arm_velocity`.

**Description:**
The `SafeController` ensures the execution of the trajectory computed by the task controller while allowing for dynamic collision avoidance. It adjusts the control outputs to prevent collisions with obstacles in real-time based on the robot and objects' models and current state.

### Connection Summary:

- The `controller_parameters` skill input is fed into the task controller to specify the goal pose.
- The `measured_arm_position` and `measured_arm_velocity` are fed into both controllers to provide real-time state information about the arm.
- The `q_nom` output from the task controller (`KinematicTrajectoryModelPredictiveController`) serves as the `arm_target` input for the tracking controller (`SafeController`).
- Constants such as `resolve_period` and `num_steps` are intrinsic to the controller's setup and influence its resolution and planning horizon.

By leveraging real-time measurements and predefined constants, these controllers collaborate to precisely and safely navigate the robot arm through cluttered environments to the target location.