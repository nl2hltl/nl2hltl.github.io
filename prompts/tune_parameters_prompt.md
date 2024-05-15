Here is time series data of the task space state and task space control for the current code:

{metric_log}

Now please decide if the time series is desired.
If it is, please answer with one word "yes".
If not, you must rewrite the code blocks that contains parameters and variables that require tuning to correct errors or to improve performance. Do not fear to make mistake. We will evaluate the code block, produce new time series, and iteratively improve the parameters. 

The response must start with <step_name> followed by a code block enclosed by ```python```. <step_name> must be included before each code block so the code block can be recognized. step_name must be enclosed in angle brackets <>. <step_name> must be one of <task_model>, <tracking_model>, <task_controller>, <tracking_controller>, <task_callback>, <tracking_callback>. For <task_callback>, <tracking_callback>, you can only rewrite chosen functions of the codeblock. But for other steps, make sure to rewrite the whole code block because we will directly replace the original block with the rewritten one. Do not miss any variable in the code block.  During "rewriting", you are only supposed to modify the existing content of the code block, such as values assigned to parameters and variables. Do not revise functions and variables not presented in the existing code block.

An example output is:

<tracking_callback>
```python
def tracking_func2(self, context, output):
    # updated function body
```

<task_controller>
```python
# updated whole code block
```