# Node-based app creation

The R4A API allows for high-level application creation, using an enhanced FSM-like structure, denoting nodes and transitions.

# Abstract Node Class

The main element of the R4A FSM-like app creation is the **Node**. All possible nodes must inherit from the **TekNode** class, and implement the following methods (with bold the methods which MUST be implemented):

- **`setParameters()`**: This method sets the proper parameters for a node to correctly operate
- `parametersChecks()`: Implements sanity, type or value checks for input parameters
- **`preempt()`**: Dictates how the node stops when preempted
- `setStartingCondition(condition)`: The node will start when the condition is true
- `setNextNode(id, condition)`: Sets a next node to transition to, based on a condition
- `execute()`: Just executes the node and returns the next node, based on the conditions set
- **`internalExecute()`**: Here add the node's core code

# Node executor

Nodes are being executed in a serialized fashion, using a Node executor, i.e. objects of the **NodeExecutor** class. This class contains the following methods:

- `__init__(exe_id)`: Contructor, taking a unique id as input
- `addNode(id, node)`: Adds a node in the execution list, either by id or by reference (node object)
- `setStartingNode(id)`: Denotes the node id to start the execution with
- `execute()`: Just executes the node executor. The nodes are executed, based on their `setNextNode` given ids.
- `threadedExecute()`: Just initiates the execution in a thread

An example of a node executor follows:

```python
#!/usr/bin/python
# -*- coding: utf-8 -*-
import sys
import os
import logging

from r4a_apis.utilities import *
from r4a_apis.tek_nodes import *

from r4a_apis.robot_api import RobotAPI
from r4a_apis.cloud_api import CloudAPI
from r4a_apis.generic_api import GenericAPI

try:
	log = Logger(allow_cutelog = True, level = logging.INFO)
	TekNode.logger = log
	TekNode.robot_api = RobotAPI(logger = log)
	TekNode.cloud_api = CloudAPI(memory = TekNode.robot_api.memory, logger = log)
	TekNode.generic_api = GenericAPI(memory = TekNode.robot_api.memory, logger = log)
	Condition.memory = TekNode.robot_api.memory
	Condition.logger = log
	InputMessage.logger = log
	OutputMessage.logger = log
	TekException.logger = log
	NodeExecutor.logger = log
	log.debug('main', "Hey, app is starting")

	nodes = {}
	nodes[0] = StartTekNode(0)
	nodes[1] = RobotMotionTekNode(1)
	nodes[1].setParameters(distance = None, duration = 5.0, direction = Directions.FORWARDS, speed = 0.2, type = MotionType.BASIC)
	nodes[2] = RobotTurnTekNode(2)
	nodes[2].setParameters(type = MotionType.BASIC, direction = Directions.RIGHT)
	nodes[3] = CameraMotionTekNode(3)
	nodes[3].setParameters(direction =  Directions.NEUTRAL, yaw = None, pitch = None)
	nodes[4] = TalkTekNode(4)
	nodes[4].setParameters(language = Languages.EL, texts = ["Γεια σου"], volume = 100)
	nodes[5] = RecordSoundTekNode(5)
	nodes[5].setParameters(name = "Sound", duration = 5.0)
	nodes[6] = ReplaySoundTekNode(6)
	nodes[6].setParameters(name = "Sound", volume = 100)
	nodes[7] = TurnLedsOnTekNode(7)
	nodes[7].setParameters(brightness = 100, color = Colors.WHITE)
	nodes[8] = TurnLedsOffTekNode(8)
	nodes[9] = StopTekNode(9)

	# Transitions
	nodes[0].setNextNode(id = 1)
	nodes[1].setNextNode(id = 2)
	nodes[2].setNextNode(id = 3)
	nodes[3].setNextNode(id = 4)
	nodes[4].setNextNode(id = 5)
	nodes[5].setNextNode(id = 6)
	nodes[6].setNextNode(id = 7)
	nodes[7].setNextNode(id = 8)
	nodes[8].setNextNode(id = 9)

	# Main execution
	main_executor = NodeExecutor(exe_id = 0)
	for i in nodes:
		main_executor.addNode(id = i, node = nodes[i])
	main_executor.setStartingNode(id = 0)

	# Go for it
	main_executor.execute()
	log.debug('main', "App is done")

except TekException:
	pass
```
Next, the individual Nodes shall be presented.

# TekNodes
---
### ***Camera motion Node***

Moves the pan-tilt servo motors on top of which is the camera.

#### Code template:
```python
from r4a_apis.utilities import *
from r4a_apis.tek_nodes import *

n = CameraMotionTekNode(_id)
n.setParameters(yaw = _yaw, pitch = _pitch, direction = _direction)

n.execute()
```

#### Parameters

- `_id`: Just an integer, denoting the id of the node. Must be unique.
- `_yaw`: Yaw angle in rads
- `_pitch`: Pitch angle in rads
- `_direction`: Direction of type [DetectionType](../enums/#directions-enum)

#### Low-level calls

- [RobotAPI.movePanTilt](../pantilt/#pan-tilt-api)

---
### ***Counter Node***

Implements a counter with a specific name. The first time this node's execute is called, the initial value is given. Each next time, it is increased by `change_by`.

#### Code template:
```python
from r4a_apis.utilities import *
from r4a_apis.tek_nodes import *

n = CounterTekNode(_id)
n.setParameters(name = _name, set_value = _set_value, change_by = _change_by)

n.execute()
```
#### Parameters
- `_id`: Just an integer, denoting the id of the node. Must be unique.
- `_name`: The name of the counter. Must be unique among the counters.
- `_set_value`: The initial value of the counter
- `_change_by`: The step to increase/decrease
#### Low-level calls
---
### ***Detect age Node***

Detects age using the camera. It captures an image, performs face detection and if a face is found it tries to detect its age.

#### Code template:
```python
from r4a_apis.utilities import *
from r4a_apis.tek_nodes import *

n = DetectAgeTekNode(_id)

n.execute()
```
#### Parameters
- `_id`: Just an integer, denoting the id of the node. Must be unique.
#### Low-level calls
---
### ***Detect barcode Node***

#### Code template:
```python
from r4a_apis.utilities import *
from r4a_apis.tek_nodes import *

n = DetectBarcodeTekNode(_id)

n.execute()
```
#### Parameters
- `_id`: Just an integer, denoting the id of the node. Must be unique.
#### Low-level calls
---
### ***Detect dominant color Node***

#### Code template:
```python
from r4a_apis.utilities import *
from r4a_apis.tek_nodes import *

n = DetectDominantColorTekNode(_id)

n.execute()
```
#### Parameters
- `_id`: Just an integer, denoting the id of the node. Must be unique.
#### Low-level calls
---
### ***Detect face Node***

#### Code template:
```python
from r4a_apis.utilities import *
from r4a_apis.tek_nodes import *

n = DetectFaceTekNode(_id)
n.setParameters(duration = _duration)

n.execute()
```
#### Parameters
- `_id`: Just an integer, denoting the id of the node. Must be unique.
- `_duration`: Amount of time to search for face
#### Low-level calls
---
### ***Detect gender Node***

#### Code template:
```python
from r4a_apis.utilities import *
from r4a_apis.tek_nodes import *

n = DetectGenderTekNode(_id)

n.execute()
```
#### Parameters
- `_id`: Just an integer, denoting the id of the node. Must be unique.
#### Low-level calls
---
### ***Detect language from audio Node***

#### Code template:
```python
from r4a_apis.utilities import *
from r4a_apis.tek_nodes import *

n = DetectLanguageFromAudioTekNode(_id)
n.setParameters(duration = _duration)

n.execute()
```
#### Parameters
- `_id`: Just an integer, denoting the id of the node. Must be unique.
- `_duration`: Duration of the captured audio.
#### Low-level calls
---
### ***Detect language from text Node***

#### Code template:
```python
from r4a_apis.utilities import *
from r4a_apis.tek_nodes import *

n = DetectLanguageFromTextTekNode(_id)
n.setParameters(text = _text)

n.execute()
```
#### Parameters
- `_id`: Just an integer, denoting the id of the node. Must be unique.
- `_text`: The text for which language will be detected.
#### Low-level calls
---
### ***Detect motion Node***

#### Code template:
```python
from r4a_apis.utilities import *
from r4a_apis.tek_nodes import *

n = DetectMotionTekNode(_id)
n.setParameters(duration = _duration)

n.execute()
```
#### Parameters
- `_id`: Just an integer, denoting the id of the node. Must be unique.
- `_duration`: Amount of time to capture a video in which the motion detection will be performed.
#### Low-level calls
---
### ***Detect QR code Node***

#### Code template:
```python
from r4a_apis.utilities import *
from r4a_apis.tek_nodes import *

n = DetectQrCodeTekNode(_id)

n.execute()
```
#### Parameters
- `_id`: Just an integer, denoting the id of the node. Must be unique.
#### Low-level calls
---
### ***Detect sentiment from text Node***

#### Code template:
```python
from r4a_apis.utilities import *
from r4a_apis.tek_nodes import *

n = DetectSentimentFromTextTekNode(_id)
n.setParameters(text = _text)

n.execute()
```
#### Parameters
- `_id`: Just an integer, denoting the id of the node. Must be unique.
- `_text`: The text whose sentiment will be detected
#### Low-level calls
---
### ***Detect sound Node***

#### Code template:
```python
from r4a_apis.utilities import *
from r4a_apis.tek_nodes import *

n = DetectSoundTekNode(_id)
n.setParameters(duration = _duration)

n.execute()
```
#### Parameters
- `_id`: Just an integer, denoting the id of the node. Must be unique.
- `_duration`: Amount of time to record the sound in which to detect noise
#### Low-level calls
---
### ***Detect touch Node***

#### Code template:
```python
from r4a_apis.utilities import *
from r4a_apis.tek_nodes import *

n = DetectTouchTekNode(_id)
n.setParameters(parts = _parts, duration = _duration)

n.execute()
```
#### Parameters
- `_id`: Just an integer, denoting the id of the node. Must be unique.
- `_parts`: List of buttons or parts for touch detection. Must be of type [Tactile enum](../enums/#tactile-enum)
- `_duration`: Amount of time for the detection
#### Low-level calls
---
### ***Dice Node***

#### Code template:
```python
from r4a_apis.utilities import *
from r4a_apis.tek_nodes import *

n = DiceTekNode(_id)
n.setNextNodeProbabilistic(_n_id_1, _weight_1)
n.setNextNodeProbabilistic(_n_id_2, _weight_2)

n.execute()
```
#### Parameters
- `_id`: Just an integer, denoting the id of the node. Must be unique.
- `_n_id_#`: Id of the next node, with probability `_weight_#`
#### Low-level calls
---
### ***Display emotion Node***

#### Code template:
```python
from r4a_apis.utilities import *
from r4a_apis.tek_nodes import *

n = DisplayEmotionTekNode(_id)
n.setParameters(emotion = _emotion)

n.execute()
```
#### Parameters
- `_id`: Just an integer, denoting the id of the node. Must be unique.
- `_emotion`: A variable of type [Sentiments enum](../enums/#sentiments-enum)
#### Low-level calls
---
### ***Get weather***

#### Code template:
```python
from r4a_apis.utilities import *
from r4a_apis.tek_nodes import *

n = GetWeatherTekNode(_id)
n.setParameters(location = _location, country = _country, report = _report)

n.execute()
```
#### Parameters
- `_id`: Just an integer, denoting the id of the node. Must be unique.
- `_location`: A location (e.g. a city)
- `_country`: An [ISO 3166 country code](https://en.wikipedia.org/wiki/List_of_ISO_3166_country_codes)
#### Low-level calls
---
### ***Learn emotion Node***

#### Code template:
```python
from r4a_apis.utilities import *
from r4a_apis.tek_nodes import *

n = LearnEmotionTekNode(_id)
n.setParameters(name = _name)

n.execute()
```
#### Parameters
- `_id`: Just an integer, denoting the id of the node. Must be unique.
- `_name`: Name of the emotion to be learned. Must be unique among emotions.
#### Low-level calls
---
### ***Learn Motion Node***

#### Code template:
```python
from r4a_apis.utilities import *
from r4a_apis.tek_nodes import *

n = LearnMotionTekNode(_id)
n.setParameters(name = _name)

n.execute()
```
#### Parameters
- `_id`: Just an integer, denoting the id of the node. Must be unique.
- `_name`: Name of the motion to be learned. Must be unique among motions.
#### Low-level calls
---
### ***Listen Node***

#### Code template:
```python
from r4a_apis.utilities import *
from r4a_apis.tek_nodes import *

n = ListenTekNode(_id)
n.setParameters(duration = _duration, vocabulary = _vocabulary)

n.execute()
```
#### Parameters
- `_id`: Just an integer, denoting the id of the node. Must be unique.
- `_duration`: Duration to listen to command
- `_vocabulary`: A list of strings to perform speech detection from
#### Low-level calls
---
### ***Preemption Node***

#### Code template:
```python
from r4a_apis.utilities import *
from r4a_apis.tek_nodes import *

n = PreemptorTekNode(_id)
n.setParameters(preempt_executors  = _execs, condition  = _cond)

n.execute()
```
#### Parameters
- `_id`: Just an integer, denoting the id of the node. Must be unique.
- `_execs`: List of executors to preempt
- `_cond`: If this condition is valid, the `_execs` will be preempted. Must be of type [Condition](../conditions)
#### Low-level calls
---
### ***Record sound Node***

#### Code template:
```python
from r4a_apis.utilities import *
from r4a_apis.tek_nodes import *

n = RecordSoundTekNode(_id)
n.setParameters(name  = _name, duration  = _dura, part = _part)

n.execute()
```
#### Parameters
- `_id`: Just an integer, denoting the id of the node. Must be unique.
- `_name`: A string denoting a name for the recorded sound
- `_duration`: Duration of the recording
- `_part`: A [Tactile](../enums/#tactile-enum) to be pressed for the recording to stop. Add `None` if this is not desired.
#### Low-level calls
---
### ***Replay motion Node***

#### Code template:
```python
from r4a_apis.utilities import *
from r4a_apis.tek_nodes import *

n = ReplayMotionTekNode(_id)
n.setParameters(name  = _name)

n.execute()
```
#### Parameters
- `_id`: Just an integer, denoting the id of the node. Must be unique.
- `_name`: The name of the recorded motion to be played
#### Low-level calls
---
### ***Replay sound Node***

#### Code template:
```python
from r4a_apis.utilities import *
from r4a_apis.tek_nodes import *

n = ReplaySoundTekNode(_id)
n.setParameters(name  = _name, volume = _volume)

n.execute()
```
#### Parameters
- `_id`: Just an integer, denoting the id of the node. Must be unique.
- `_name`: The name of the recorded sound to be played
#### Low-level calls
---
### ***Robot motion Node***

#### Code template:
```python
from r4a_apis.utilities import *
from r4a_apis.tek_nodes import *

n = RobotMotionTekNode(_id)
n.setParameters(distance  = _distance, duration = _duration, direction = _direction, linear = _linear, rotational = _rotational, type = _type, speed = _speed)

n.execute()
```
#### Parameters
- `_id`: Just an integer, denoting the id of the node. Must be unique.
- `_distance`: The distance to travel
- `_duration`: Amount of time to move
- `_direction`: Of type [Directions enum](../enums/#directions-enum)
- `_linear`: Linear velocity (float)
- `_rotational`: Rotational velocity (float)
- `_type`: Motion type of type [MotionType](../enums/#motiontype-enum)
- `_speed`: Float number denoting the motion speed
#### Low-level calls
---
### ***Robot turn Node***

#### Code template:
```python
from r4a_apis.utilities import *
from r4a_apis.tek_nodes import *

n = RobotTurnTekNode(_id)
n.setParameters(type = _type, angle = _angle, direction = _direction, speed = _speed, duration = _duration)

n.execute()
```
#### Parameters
- `_id`: Just an integer, denoting the id of the node. Must be unique.
- `_type`: Motion type of type [MotionType](../enums/#motiontype-enum)
- `_angle`: Angle to turn in rads
- `_direction`: Of type [Directions enum](../enums/#directions-enum)
- `_speed`: Float number denoting the motion speed
- `_duration`: Amount of time to move
#### Low-level calls
---
### ***Sleep Node***

#### Code template:
```python
from r4a_apis.utilities import *
from r4a_apis.tek_nodes import *

n = SleepTekNode(_id)
n.setParameters(duration = _duration)

n.execute()
```
#### Parameters
- `_id`: Just an integer, denoting the id of the node. Must be unique.
- `_duration`: Amount of time to sleep
#### Low-level calls
---
### ***Start Node***

#### Code template:
```python
from r4a_apis.utilities import *
from r4a_apis.tek_nodes import *

n = StartTekNode(_id)

n.execute()
```
#### Parameters
- `_id`: Just an integer, denoting the id of the node. Must be unique.
#### Low-level calls
---
### ***Stop Node***

#### Code template:
```python
from r4a_apis.utilities import *
from r4a_apis.tek_nodes import *

n = StopTekNode(_id)

n.execute()
```
#### Parameters
- `_id`: Just an integer, denoting the id of the node. Must be unique.
#### Low-level calls
---
### ***Talk Node***

#### Code template:
```python
from r4a_apis.utilities import *
from r4a_apis.tek_nodes import *

n = TalkTekNode(_id)
n.setParameters(texts = _texts, language = _language, volume = _volume)

n.execute()
```
#### Parameters
- `_id`: Just an integer, denoting the id of the node. Must be unique.
- `_texts`: A list of strings to be spoken
- `_language`: A language code of type [Languages](../enums/#languages-enum)
- `_volume`: Volume from 0 to 100
#### Low-level calls
---
### ***Threads Node***

#### Code template:
```python
from r4a_apis.utilities import *
from r4a_apis.tek_nodes import *

n = ThreadsTekNode(_id)
n.setParameters(executors = _execs)

n.execute()
```
#### Parameters
- `_id`: Just an integer, denoting the id of the node. Must be unique.
- `_execs`: Ids of the executors to be started in parallel
#### Low-level calls
---
### ***Transition Node***

#### Code template:
```python
from r4a_apis.utilities import *
from r4a_apis.tek_nodes import *

n = TransitionTekNode(_id)

n.execute()
```
#### Parameters
- `_id`: Just an integer, denoting the id of the node. Must be unique.
#### Low-level calls
---
### ***Translate from audio Node***

#### Code template:
```python
from r4a_apis.utilities import *
from r4a_apis.tek_nodes import *

n = TranslateFromAudioTekNode(_id)
n.setParameters(recording_time = _rec_time, source_lang = _s_lang, target_lang = _t_lang)

n.execute()
```
#### Parameters
- `_id`: Just an integer, denoting the id of the node. Must be unique.
- `_rec_time`: Time to record
- `_s_lang`: Language of the recording, of type [Languages](../enums/#languages-enum)
- `_t_lang`: Target language, of type [Languages](../enums/#languages-enum)
#### Low-level calls
---
### ***Translate from text Node***

#### Code template:
```python
from r4a_apis.utilities import *
from r4a_apis.tek_nodes import *

n = TranslateFromTextTekNode(_id)
n.setParameters(text = _text, source_lang = _s_lang, target_lang = _t_lang)

n.execute()
```
#### Parameters
- `_id`: Just an integer, denoting the id of the node. Must be unique.
- `_text`: Text to be translated
- `_s_lang`: Language of the text, of type [Languages](../enums/#languages-enum)
- `_t_lang`: Target language, of type [Languages](../enums/#languages-enum)
#### Low-level calls
---
### ***Turn leds off Node***

#### Code template:
```python
from r4a_apis.utilities import *
from r4a_apis.tek_nodes import *

n = TurnLedsOffTekNode(_id)

n.execute()
```
#### Parameters
- `_id`: Just an integer, denoting the id of the node. Must be unique.
#### Low-level calls
---
### ***Turn leds on Node***

#### Code template:
```python
from r4a_apis.utilities import *
from r4a_apis.tek_nodes import *

n = TurnLedsOnTekNode(_id)

n.execute(color = _color, brightness = _bright)
```
#### Parameters
- `_id`: Just an integer, denoting the id of the node. Must be unique.
- `_color`: A color of type [Colors](../enums/#colors-enum)
- `_bright`: Brightness between [0, 100]
#### Low-level calls
