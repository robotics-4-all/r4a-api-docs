## The Memory functionality

In order to locally store a) all information generated from the sensors of the device, b) all input information from the app's calls and c) whatever the user that creates apps wants, we have created a key/value storage, using [Redis](https://redis.io/).

The memory object is initialized when a RobotAPI object is created and can be found as such:

```python
import robot_api

r_api = robot_api.RobotAPI()
memory = r_api.memory
```

All data are written under a **key**, which which you can retrieve the data. Also each key denotes a topic in memory, which holds a queue of **10** items. So when you write a piece of data, it is written in place 0 and the item in place -9 is destroyed.

Robot memory offers the following functionalities:

### **Memory.listGet**

`listGet` retrieves data from memory using a key.

#### - Input arguments

- `key`: A string denoting the key that identifies the data
- `frm`: The most recent index of the desired data
- `to`: The oldest index of the desired

#### - Output

Output is a list containing the data, along with the timestamp of the storage.

#### - Example

```python
from robot_api import RobotAPI

robot_api = RobotAPI()

robot_api.memory.setKey(key = 'test', value = 1)
robot_api.memory.setKey(key = 'test', value = 2)
# Asking for the last two values
o = robot_api.memory.listGet(key = 'test', frm = 0, to = -1)
print(o)
```

The output is
```
[{'data': 2, 'timestamp': 1575364271.5788426}, {'data': 1, 'timestamp': 1575364271.5521088}]
```

### **Memory.setKey**

This call either sets a new key or writes in an already existent key.

#### - Input arguments

- `key`: A string denoting the key that identifies the data
- `value`: The value to be written. This value should be JSON serializable

#### - Example

```python
from robot_api import RobotAPI

robot_api = RobotAPI()

robot_api.memory.setKey(key = 'test', value = 1)
robot_api.memory.setKey(key = 'test', value = 2)
```

### **Memory.getKey**

This call retrieves the **last** piece of data from memory using a key.

#### - Input arguments

- `key`: A string denoting the key that identifies the data

#### - Output

Output is a list of size 1, along with the timestamp of the storage.

#### - Example

```python
from robot_api import RobotAPI

robot_api = RobotAPI()

robot_api.memory.setKey(key = 'test', value = 1)
robot_api.memory.setKey(key = 'test', value = 2)

o = robot_api.memory.getKey(key = 'test')
print(o)
```

The output is:
```
[{'data': 2, 'timestamp': 1575365240.3306623}]
```

### **Memory.setVariable**

This call sets a [TekVariable](enums.md#tekvariables-enum).

#### - Input arguments

- `variable`: The TekVariable identifying the data
- `value`: The value to be written. This value should be JSON serializable

#### - Example

```python
from utilities import TekVariables
from robot_api import RobotAPI

robot_api = RobotAPI()

robot_api.memory.setVariable(variable = TekVariables.SLEEP_DURATION, value = 1)
```

### **Memory.getVariable**

This call gets a [TekVariable](enums.md#tekvariables-enum) from the memory.

#### - Input arguments

- `variable`: The TekVariable identifying the data

#### - Output

Output is a list of size 1, along with the timestamp of the storage.

#### - Example

```python
from utilities import TekVariables
from robot_api import RobotAPI

robot_api = RobotAPI()

robot_api.memory.setVariable(variable = TekVariables.SLEEP_DURATION, value = 1)
o = robot_api.memory.getVariable(variable = TekVariables.SLEEP_DURATION)
```

The output is:
```
[{'data': 1, 'timestamp': 1575366048.6832085}]
```
