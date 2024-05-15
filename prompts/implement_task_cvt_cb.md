Now please implement callback functions of a `LeafSystem` that acts as a connector which I have already constructed. The input ports correspond to inputs to the skill (observations and controller parameters). The output ports correspond to the input ports of the task controller. 
Here is a yaml file describing what the inputs to the skill are:
```yaml
{skill_input_summary}
```
Here we print the port name, type and sample value for all the input port. You can get the value of the port by `value = self.GetInputPort(port_name).Eval(context)` when impelementing the call back functions: 
```python
{input_port_sample}
```

The chosen task model, tracking model, task controller, and tracking controller are
```python
{code_blocks}
```

Here is the design summary to explain the expected way of how do the controllers works, and how to connect the ports:

{design_summary}

Here is the summary of the input ports of the task controller:
```yaml
{task_controller_input_summary}
```

The functions you need to implement are: 
```python
{functions_to_write}
```
Here is an example response:

<task_callback>
```python
def place_holder_function(self, context, output: BasicVector):
    abstract_input_port_value = self.GetInputPort(port_name).Eval(context)
    output.SetFromVector(abstract_input_port_value["place_holder_key"])
def place_holder_function2(self, context, output: BasicVector):
    vector_input_port_value = self.GetInputPort(port_name).Eval(context)
    out = np.zeros(6)
    out[3] = vector_input_port_value[0]
    output.SetFromVector(out)
def place_holder_function3(self, context, output: AbstractValue):
    value = self.GetInputPort(port_name).Eval(context)
    output.set_value(value)   
```
Please implement all the task callback functions in one code block begin with <task_callback>.

Here are some tips to implement the callback functions:
* When use a port, make sure the name of the port is correct and the port is avialble in the current function.
* Note that some of the ports should be passed through without any modification like control_parameters. Some of the ports need to be modified.
* Make sure the dimensions of the output matches the port. The output value may be only partially available from input port. You need to decide the value for the remainings. Be careful of which dimension to set value, make sure it complies with the description of the port in the controller summary.
* For pose, velocity and force vectors, rotation always comes first, such as [roll, yaw, pitch, x, y, z] or [x-rotation, y-rotation, z-rotation, x-translation, y-translation, z-translation]. 
* If the input port is a dictionary, make sure only use keys that has shown in the printed port value sample. 
* If the output should be a enum type, you can use the enum type mentioned in the controller summary directly without any import. 
* Recall the task requirements given in the beginning. Make sure the call back functions correctly solve the task. 
* Please avoid using placeholders or simplified examples that require modifications by others. Ensure all calculations are conclusive. In case of any uncertainties about parameters, utilize the information provided to derive the most informed inference available.
* You can use `self.num_q` to denote the number of joints


Please implement the call-back functions. Please think step by step then write the code. 