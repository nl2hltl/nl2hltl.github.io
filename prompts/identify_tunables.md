Here is the summary of the control system to explain the expected way of how do the controllers works, and how the ports are connected:

{implementation_summary}

Here is a yaml file describing what the inputs to the skill are:
```yaml
{skill_input_summary}
```

Here we print the port name, type and sample value for all the input port: 

{input_port_sample}


Here are the detailed implementation of the task_model, tracking_model, task_controller, tracking_controller, task_callback (the callback functions for the task input port), and tracking_callback (callback functions for the tracking input ports).

{code_blocks}

Here is time series data of the task space state and task space control, which can be used as metric to determine if the system is running as expected.

{metric_log}

Please first think step by step about the expected time series and determine if the current series is desired. 
Then please analyze one by one if any of followings happen. 

* Mismatch of order. The order of the state is inconsistent in model definition, controller definition, or callback function. Double check if the order is consistant. For example, an error can be modeling the task space with [pos_a, vel_a, pos_b, vel_b], but composed the task state by [pos_b, vel_b, pos_a, vel_a] in task callbacks. In this case, the GPT needs to redefine the state, the model, or the callback function.
* Error in definition. Double check if the assignment is correct for the model, the state, and the callback functions. Make sure the signs are correct, the numbers are desired, there is no missing assignments or careless mistakes. Especially pay attention to the dynamic model. Think step by step of the meaning of each element in the dynamic function.
* Messed up rotation and translation order. In pydrake, for pose, velocity and force vectors, rotation always comes first, such as [roll, yaw, pitch, x, y, z] or [x-rotation, y-rotation, z-rotation, x-translation, y-translation, z-translation]
* Modeling is inaccurate, that is, when the model involves estimated parameters and it turns out the estimation is inaccurate.
* The controller parameter is not optimal to finish the task. For example, the system diverges with the current controller gain.

If the GPT thinks any one of these happens, then identify the parameters and variable assignments that require tuning to correct errors and improve the performance. The identified code blocks that contain these parameters and variables will be updated in later conversations.