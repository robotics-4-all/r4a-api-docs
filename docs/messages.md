# Input and Output messages

There are two classes to handle input and output, which can be found in the `utilities` module. These are `InputMessage` and `OutputMessage`.

## `InputMessage` class

You can create an input message as such:

```python
from utilities import InputMessage

i = InputMessage()
```

Every input message contains the following:

- `timestamp`: Contains the timestamp of the message's creation
- `data`: The data. This usually is a Python dictionary.
- `print()`: Function to print the input message

An example follows:

```python
from utilities import InputMessage

i = InputMessage({'duration': 3})
i.data['another'] = 2
i.print()
```

The output in console is:
```bash
Input message:
  [1575288958.9064102] Data:  {'duration': 3, 'another': 2}
```

## `OutputMessage` class

Every call of the Robot, Cloud or Generic API returns an `OutputMessage`. Each output message contains:

- `timestamp`: Contains the timestamp of the message's creation
- `sequence`: A unique number that characterizes the message
- `errors`: A list of possible errors
- `logs`: A list of logs. Usually contains trace-back information.
- `data`: The data that the message contains
- `print()`: Prints the output message

An example code that utilizes an output message is the following:

```python
from utilities import Devices, InputMessage
from robot_api import RobotAPI

rapi = RobotAPI()
rapi.devicesObj.enableDevicesType(Devices.TOUCH_SCREEN)

out = rapi.showOptions(InputMessage({
    'options': ['Option 1', 'Option 2'],
    'duration': 5
}))
out.print()
```

This snippet initializes a touch screen, shows 2 options and waits for 5 seconds for the user to select one. The output is:

```bash
Output message:
	[1575290784.5641167] #5
	{'reaction_time': 0.9212639331817627, 'selected': 'Option 1'}
	Errors:
	Logs:
		[1575290784.5652816] setOptions @ RobotAPITouchScreenController
		[1575290784.5658484] showOptions @ RobotAPI
```
