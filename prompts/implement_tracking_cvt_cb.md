Now please implement callback functions of a `LeafSystem` that acts as a connector which I have already constructed for the tracking controller. The input ports correspond to inputs to the skill (observations and controller parameters) and task control (the output of the task controller). The output ports correspond to the input ports of the tracking controller. 

Recall the input port of the skill given previously, and the following is a description of the task control port. You can use all skill input ports and the task control port.
```yaml
{task_control_port_summary}
```

Here is the summary of the input ports of the tracking controller:
```yaml
{tracking_controller_input_summary}
```

The functions you need to implement are: 
```python
{functions_to_write}
```
Here is an example response:

<tracking_callback>
```python
def place_holder_function(self, context, output: BasicVector):
    abstract_input_port_value = self.place_holder_port.Eval(context)
    output.SetFromVector(abstract_input_port_value["place_holder_key"])
def place_holder_function2(self, context, output: BasicVector):
    vector_input_port_value = self.place_holder_port.Eval(context)
    out = np.zeros(6)
    out[3] = vector_input_port_value[0]
    output.SetFromVector(out)
def place_holder_function3(self, context, output: AbstractValue):
    value = self.place_holder_port.Eval(context)
    output.set_value(value)   
```

Follow the previously given tips for implementing the callback functions. Further more:
* Note that output ports of the task controller have been renamed by adding prefix: 'task_' + port_name.

Now please implement the call-back functions. Please think step by step then write the code. 