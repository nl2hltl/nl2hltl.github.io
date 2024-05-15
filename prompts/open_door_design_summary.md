To implement the skill of pulling open a door, we have selected two controllers: the `CartesianInterpolationController` as the task controller and the `CartesianStiffnessController` as the tracking controller. Here’s how they are expected to work together based on their input and output ports:

### Task Controller: `CartesianInterpolationController`
- **Input Ports:**
  - `controller_parameters`: includes information that triggers the generation of a new trajectory. It’s directly passed from the `controller_parameters` in the skill inputs.
  - `measured_ee_pose`: the current pose of the end effector in `[roll, pitch, yaw, x, y, z]` format. This is obtained from `measured_ee_pose` in the skill inputs.
  - `execution_time`: the temporal duration of the interpolated trajectory. It should be planned according to the task requirements but is set constant for simplicity here.
  - `target_position`: the target position `[X, Y, Z]` the end effector should reach. It should be determined based on the door opening requirements.

- **Output Ports:**
  - `ee_pose_nom`: Nominal end-effector pose `[roll, pitch, yaw, x, y, z]` along the interpolated trajectory.

### Tracking Controller: `CartesianStiffnessController`
- **Input Ports:**
  - `ee_target`: The desired end-effector target `(pose or twist)`. This should be connected to `ee_pose_nom` output of the task controller.
  - `ee_target_type`: Indicates the type of the end effector target (pose in our case). This is a constant parameter set to `EndEffectorTarget.kPose`.
  - `arm_position`: Current joint position of the robot arm, obtained from `measured_arm_position` in the skill inputs.
  - `arm_velocity`: Current joint velocity of the robot arm, obtained from `measured_arm_velocity` in the skill inputs.
  - `controller_parameters`: parameters that affect the control behavior, such as `cartesian_stiffness` and `cartesian_damping`, which are directly passed from the `controller_parameters` in the skill inputs.

- **Output Ports:**
  - `applied_arm_torque`: Control torques applied to the joints of the robot arm.

### Connecting Ports and Constant Parameters
1. The `ee_pose_nom` output from `CartesianInterpolationController` should connect to the `ee_target` input of `CartesianStiffnessController`.
2. The `ee_target_type` for `CartesianStiffnessController` must be set to `EndEffectorTarget.kPose`, indicating we are controlling the pose, not the twist of the end effector.
3. Parameters such as `execution_time`, `ee_target_type`, `controller_parameters` (including `cartesian_stiffness` and `cartesian_damping`) require careful selection as they directly influence the system's performance.

By establishing these connections and setting parameters accordingly, the system should effectively pull open the door by generating a trajectory with the task controller and following this trajectory compliantly with the tracking controller.