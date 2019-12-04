# The RobotAPI

Robot API offers services / calls, with which you can manipulate the robot/device. As explained [here](messages.md), all calls get an [InputMessage](messages.md#inputmessage-class) as input and an [OutputMessage](messages.md#outputmessage-class) as output.

# Enabling resources

In order to use a resource, you must enable it. The easier way to do this is via the `devicesObj` object, that exists in a `RobotAPI` object. Specifically there is a function called `enableDevicesType`, that takes as input a [Device](enums.md#devices-enum) and activates all respective devices.

For example, if we were to enable all microphones, we would write:

```python
import utilities
import robot_api

r = robot_api.RobotAPI()
r.devicesObj.enableDevicesType(Devices.MICROPHONE)
```

# The API calls

Next, the API calls, sorted by device categories are presented.

---

## - **Speakers API**

### *RobotAPI*.**speak**

A text-to-speech algorithm is used, in order for the device to "speak" in different languages.

#### Input arguments
- `texts`: A list of arguments. These may be strings or [TekVariables](enums/#tekvariables-enum)
- `volume`: The volume from 0 to 100
- `language`: A [Language](enums/#languages-enum)

#### Output / Variables

This call has no output and does not change any TekVariables.

#### Examples
```python
import robot_api
import utilities

rapi = robot_api.RobotAPI()

out = rapi.speak(utilities.InputMessage({
    'texts': ['the number', 'is', utilities.TekVariables.SLEEP_DURATION],
    'volume': 100,
    'language': utilities.Languages.EN
}))
```

### *RobotAPI*.**replaySound**

This call reproduces a sound from the speakers. The sound can either be a wav file, or a base64-encoded string.

#### Input arguments

- `is_file`: True if we want to play a file, false if we have a raw base64 string
- `string`: Either the absolute path of the file, or the base64 string.
- `volume`: The volume from 0 to 100

#### Output / Variables

This call has no output and does not change any `TekVariables`.

#### Examples

```python
import robot_api
import utilities

rapi = robot_api.RobotAPI()

out = rapi.replaySound(utilities.InputMessage({
    'is_file': True,
    'string': '/tmp/tmp.wav',
    'volume': 100
}))
```

---

## - **Microphone API**

### *RobotAPI*.**recordSound**

This call records a sound from a microphone.

#### Input arguments

- `duration`: How many seconds the recording will be
- `name`: A name to store the sound (can be later used to retrieve it)
- `save_file_url`: Absolute path to store the sound as a wav. If `None`, the sound is not locally stored.

#### Output / Variables

This call returns an `OutputMessage`, containing the following data:
```
{
  'record': The base64 encoded sound file
}
```

In does not change any `TekVariables`.

#### Examples

```python
import robot_api
import utilities

rapi = robot_api.RobotAPI()

out = rapi.recordSound(utilities.InputMessage({
    'name': 'test_sound_1',
    'duration': 3,
    'save_file_url': '/tmp/tmp.wav'
}))
sound_str = out.data['record']
```

---

## - **Camera API**

### *RobotAPI*.**captureImage**

This call captures an image from the camera.

#### Input arguments

- `width`: Desired width of captured image
- `height`: Desired height of captured image
- `save_file_url`: An absolute path for the image to be saved. If `None`, the image is not saved.

#### Output / Variables

The call returns an `OutputMessage` with the following data:

- `deviceId`: the id of the device,
- `timestamp`: the timestamp of the capture,
- `image`: the image as base 64 string,
- `width`: the width of the captured image,
- `height`: the height of the captured image,
- `format`: usually `rgb`,
- `per_rows`: True if stored by rows or by columns

#### Examples

```python
import robot_api
import utilities

rapi = robot_api.RobotAPI()

out = rapi.captureImage(utilities.InputMessage({
    'width': 800,
    'height': 480,
    'save_file_url': '/tmp/file.jpg'
}))
out.print()
```

### *RobotAPI*.**getImages**

Retrieves images from memory.

#### Input arguments

- `fromIndex`: The most recent index
- `toIndex`: The oldest index

#### Output / Variables

An `OutputMessage` as such:
```python
{
	'measurements': [
		{
            'deviceId': ID,
            'timestamp': 0,
            'image': "as base64 string format",
            'width': 0,
            'height': 0,
            'format': 'rgb',
            'per_rows': True # If stored by rows or by columns
		},
		...
	]
}
```

#### Examples
```python
import robot_api
import utilities

rapi = robot_api.RobotAPI()

out = rapi.getImages(utilities.InputMessage({
    'fromIndex': 0,
    'toIndex': 0
}))
```

---

## - **Touch screen API**

### *RobotAPI*.**showImage**

Shows an image in touch screen

#### Input arguments

- `image`: The image as base64 string
- `width`: The width of the captured image
- `height`: The height of the captured image
- `duration`: How many seconds the image will be shown
- `touch`: True if touches are accepted.

#### Output / Variables

Returns an `OutputMessage` containing the following data:

```
{
  'reaction_time': The reaction time - time between the display and the touch,
  'selected': None
}
```

#### Examples

```python
import robot_api
import utilities

rapi = robot_api.RobotAPI()

out = rapi.captureImage(utilities.InputMessage({
    'width': 800,
    'height': 480,
    'save_file_url': None
}))
out.print()

out = rapi.showImage(utilities.InputMessage({
    'image': out.data['image'],
    'width': out.data['width'],
    'height': out.data['height'],
    'duration': 10,
    'touch': True
}))
out.print()
```

### *RobotAPI*.**showOptions**

Shows up to 4 options in the touch screen and waits for a touch.

#### Input arguments

- `options`: A list of strings
- `duration`: For how much time the options will wait for touch

#### Output / Variables

Returns an `OutputMessage` containing the following data:

```
{
  'reaction_time': The reaction time - time between the display and the touch,
  'selected': The option selected (as string)
}
```

#### Examples

An `InputMessage` as such:

```python
import robot_api
import utilities

rapi = robot_api.RobotAPI()

out = rapi.showOptions(utilities.InputMessage({
    'options': ['Option 1', 'Option 2'],
    'duration': 5
}))
out.print()
```

### *RobotAPI*.**showColor**

#### Input arguments

- `color`:
- `duration`: For how much time the color will wait for touch

#### Output / Variables

```
{
  'reaction_time': The reaction time - time between the display and the touch,
  'selected': The option selected (as string)
}
```

#### Examples

```python
import robot_api
import utilities

rapi = robot_api.RobotAPI()

out = rapi.showColor(utilities.InputMessage({
    'color': utilities.Colors.GREEN.value,
    'duration': 5
}))
out.print()
```

---

## - **LEDs API**

### *RobotAPI*.**lightLeds**


### *RobotAPI*.**ledsColorWipe**


### *RobotAPI*.**getLeds**

- fromIndex
- toindex

---

## - **Buttons API**

### *RobotAPI*.**getButtonChanges**

---

## - **Environmental sensor API**

### *RobotAPI*.**getTemperatureMeasurement**

- fromIndex
- toindex

### *RobotAPI*.**getHumidityMeasurement**

- fromIndex
- toindex

### *RobotAPI*.**getPressureMeasurement**

- fromIndex
- toindex

### *RobotAPI*.**getGasMeasurement**

- fromIndex
- toindex

---

## - **Encoders API**

### *RobotAPI*.**getEncoderMeasurement**

- fromIndex
- toindex

---

## - **Line follower API**

### *RobotAPI*.**getLineFollowerMeasurement**

- fromIndex
- toindex

---

## - **Time-of-flight API**

### *RobotAPI*.**getToFMeasurement**

- fromIndex
- toindex

---

## - **Sonars API**

### *RobotAPI*.**getSonarMeasurement**

- fromIndex
- toindex

---

## - **IRs API**

### *RobotAPI*.**getIrMeasurement**

- fromIndex
- toindex

---

## - **Pan-tilt API**

### *RobotAPI*.**getPanTilt**

- fromIndex
- toindex

### *RobotAPI*.**movePanTilt**

- yaw
- pitch

---

## - **Body motion API**

### *RobotAPI*.**moveBody**

- linearVelocity
- rotationalVelocity

### *RobotAPI*.**getBodyVelocities**

- fromIndex
- toindex

---

## - **IMU API**

### *RobotAPI*.**getImuMeasurement**

- fromIndex
- toindex
