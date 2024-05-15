Let's first take a look of all available measurements, dynamic models, and controllers.

Here are all available inputs to the skill: 
{skill_inputs_sample}

Here are all available dynamic model setup functions in yaml format: 
{dynamic_model_brief_str}

Here are all available controllers in yaml format: 
{controller_brief_str}

====================================================

Based on the available measurements, models, and controllers, please think step by step to choose the models and controllers: 
1. Decide the subject of the task controller, is it an object, the end effector, or something else. 
2. Decide the desired task control to be applied on the subject, is it Cartesian position, Cartesian force, or something else. 
3. Decide the task space model that can model the dynamics of the subject with the task control. When the analytical form of the dynamics model is needed, draw upon your extensive knowledge in control theory and system modeling. Think step by step to make sure the model is correct according to the task description.
4. Decide the task controller that can apply the desired task control and realize the goal of the skill. Make sure the controller can realize the goal with the given available measurements. There is no additional inputs or functions provided to the controller. 
5. Decide the tracking space model. 
6. Decide the tracking controller to track the output of the task controller and to satisfy possible constraints.

Detail about how can the chosen models and controllers realize the skill goal. Be specific. 

Please return the choice with the following format. 

<task_model>
```python
task_model = setup_model(arg1, arg2)
```

<tracking_model>
```python
tracking_model = setup_model(arm_type, object_info)
```

<task_controller>
```python
task_controller = ControllerClass(arg1, arg2)
```

<tracking_controller>
```python
tracking_controller = ControllerClass(arg1)
```

Make sure your response comply with the following requirements:
* <step_name> must be included before each code block so the code block can be recognized. step_name must be enclosed in angle brackets <>.
* Choices have been made for all steps. A correct solution exists with the given infomation.
* Pass the arguments (args) when instantiating the controller and the model. The arguments needed are stated in the yaml file (args). **Do not** include items in "input_ports" (such as "controller_parameters") as arguments when instantiating the controllers. They are not arguments for instantiating the controller.
* The arguments should be defined before use, except `arm_type` and `object_info`, which can be used directly without definition.
* Do not use any placeholder or assume any variable is defined. All informations and available variables needed are provided. If your choice of model and controller requires additional information, rethink about it.
* The models and controllers are instantiated correctly as stated in the materials.
* The chosen model matches the required model of the controllers as stated in the materials.