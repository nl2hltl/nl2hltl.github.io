### Summary of Controllers and Callbacks

#### Task Controller (`LQRController`)
The `LQRController` is designed to stabilize a cart-pole system, focusing on keeping the pole in an upright position while controlling the cart's position along the y-axis. This controller receives a state vector that encapsulates the dynamic state of the cart-pole system: `[cart position, cart velocity, pole angle, pole angular velocity]`. It computes the necessary force to be applied along the y-axis to achieve stabilization based on the Linear Quadratic Regulator (LQR) control law. This force serves as a control input to the tracking controller for executing the desired action on the physical system.

#### Tracking Controller (`PoseForceController`)
The `PoseForceController` aims at controlling the robot's end-effector to apply the necessary force as computed by the task controller (`LQRController`), while also maintaining the end-effector's pose. This controller receives input for the desired end-effector pose, the target force to be applied, and the current arm position and velocity. It then adjusts the robot's actuators to apply the computed force on the actual system while striving to keep the end-effector's pose as close as possible to the desired pose.

### Callback Functions

#### Task Callback (`task_state`)
The `task_state` callback function serves to process inputs related to the cart-pole system's current state and compute the state vector required by the `LQRController`. This state vector is derived from:

- The cart's position and velocity in the y-axis direction, obtained from `measured_body_poses` and `measured_body_velocities`.
- The pole's angle and angular velocity, derived from 'PolePin' measurements in `measured_joint_states`.

These quantities are then assembled into a state vector and passed to the task controller to compute the control input (force along y-axis).

#### Tracking Callbacks
The tracking callbacks engage with both the inputs to the skill and the control output of the task controller to compute the inputs required by the tracking controller (`PoseForceController`). These inputs facilitate the control of the end-effector's pose and the application of force as determined necessary by the task controller. Specifically:

- `tracking_ee_pose_target` computes the desired pose for the end-effector. This target is static, aiming to keep the end-effector close to a specified position and orientation.
- `tracking_ee_force_target` translates the control input from the task controller into a force target for the end-effector, specifically along the y-axis, where the task controller determines force needs to be applied.
- `tracking_arm_position` and `tracking_arm_velocity` pass through the current state of the robot's arm (its joint positions and velocities) without modification. These are necessary for the `PoseForceController` to accurately control the robot.

### Data Flow Summary
The system starts with the acquisition of real-time state information about the cart-pole system and the robot arm (through the inputs to the skill). This data feeds into the task callback to compute the state vector needed by the `LQRController`. The `LQRController` uses this state vector to compute the necessary control action (force along the y-axis) to stabilize the cart-pole system. This control action is then used by the tracking callbacks to formulate the desired end-effector force target for the `PoseForceController`. Meanwhile, the current state of the robot's arm is directly passed to the `PoseForceController` to execute the computed control action effectively, managing both force application and maintaining the end-effector's desired pose.

This hierarchical control scheme, with its corresponding data flow and signal processing via callbacks, represents a robust strategy for achieving complex robotic tasks that require simultaneous attention to dynamic system stabilization and precise manipulation.