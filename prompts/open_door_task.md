Please help me write code for a robot skill designed to pull open a door.
Coordinate System Orientation:
The x-axis points forward.
The y-axis points to the left.
The z-axis points upward.
Currently, the door is closed, and the robot has successfully grasped the handle. When viewed from above, the robot base is at [0, 0], the door handle's position is approximately [0.8, 0.2], the hinge (rotation axis) is positioned at [0.8, 0.2 - radius], with "radius" being the handle's rotation radius, which fluctuates between 0.3 and 0.5 meters, and the door opens by rotating anticlockwise around the hinge. Therefore the vector from the hinge to the handle is currently [0, radius]. The height of the door handle is 0.5, which should remain unchanged during the pulling process. Given the uncertainty in the radius, the skill should not only determine a rough trajectory to pull the door open approximately 90 degrees, but also be compliant to avoid damaging the door during the pulling process. 