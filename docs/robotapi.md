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

## - **Speakers API**
### RobotAPI.speak
- texts [strings]
- volume
- language

Outputs a list of string from the speakers.

#### Input
An `InputMessage` such as:
```python
out = rapi.replaySound(InputMessage({
    'deviceId': ID,
    'strings': ['this', 'is', 'an', 'example'],
    'volume': 100,
    'language': Languages.EL
}))
```
The `language` option must be an enum object, and can have the following values:
- Languages.EL
- Languages.EN

### RobotAPI.replaySound
- is_file
- string
- volume

An `InputMessage` such as:
```python
out = rapi.playSoundFromFile(InputMessage({
    'deviceId': ID, # The Id of the SPEAKERS device
    'file': "test.wav",
    'volume': 100
}))
```

## - **Microphone API**
### RobotAPI.recordSound
- duration
- name
- save_file_url

Records a sound by giving duration and a name.

#### Input
An `InputMessage` such as:
```python
out = rapi.recordSound(InputMessage({
    'deviceId': ID,
    'duration': 3, # seconds
    'name': 'test_name'
}))
```

### RobotAPI.getSound
Gets last sounds from memory encoded as a **base64 string**.

#### Input
An `InputMessage` such as:
```python
out = rapi.getSound(InputMessage({
    'deviceId': d.id,
    'fromIndex': 0,
    'toIndex': 0
}))
```
#### Output
An `OutputMessage` such as:
```python
{
  'measurements':[
    {
    	'deviceId': 0,
    	'timestamp': 0,
    	'is_file': 0,
    	'file': 'The file\'s path or the base64 sound string',
    	'volume': 100
    },
    ...
  ]
}
```
The sound is also written in robot memory.

## - **Camera API**
### RobotAPI.captureImage
- width
- height
- save_file_url

Captures an image from the camera.

#### Input
An `InputMessage` such as:
```python
out = rapi.captureImage(InputMessage({
    'deviceId': ID
}))
```
#### Output
An `OutputMessage` as such:
```python
{
    'deviceId': ID,
    'timestamp': 0,
    'image': "as base64 string format",
    'width': 0,
    'height': 0,
    'format': 'rgb',
    'per_rows': True # If stored by rows or by columns
}
```
The image is also stored in the robot memory.

### RobotAPI.getImages
Retrieves images from memory

#### Input
```python
out = rapi.getImages(InputMessage({
    'deviceId': ID,
    'fromIndex': 0,
    'toIndex': 0
}))
```
#### Output
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

## - **Touch screen API**
### RobotAPI.showImage
- image
- width
- height
- duration
- touch

Outputs an image in the screen.

#### Input
An `InputMessage` such as:
```python
out = rapi.showImage(InputMessage({
    'deviceId': ID,
    'image': 'the image as absolute file or base64 string',
    'is_file': True or False,
    'duration': 10, # Visualization stops after 10 seconds
    'wait_for_touch': True # If we wait for touch
}))
```

### RobotAPI.showOptions
- options []
- duration

Shows a number of options in touch screen and waits for a touch.

#### Input

An `InputMessage` as such:

```python
out = rapi.showOptions(InputMessage({
    'deviceId': ID,
    'options': ['option 1', 'option 2'],
    'duration': 10 # Times out after 10 seconds
}))
```

#### Output

Returns the option selected by an `OutputMessage`:

```python
{
	'option': 1 # -1 if nothing is pressed
}
```

### RobotAPI.showColor
- color
- duration

## - **LEDs API**
### RobotAPI.lightLeds

#### Input
An `InputMessage` such as:
```python
out = robot_api.lightLeds(InputMessage({
    'devices': [
        {
            'deviceId': ID, # The ID of the LED device
            'r': 0,
            'g': 255,
            'b': 0,
            'intensity': 100
        },
        ...
    ]
}))
```

### RobotAPI.ledsColorWipe
An `InputMessage` such as:
```python
out = robot_api.ledsColorWipe(InputMessage({
    'r': 0,
    'g': 255,
    'b': 0,
    'intensity': 100
}))
```

### RobotAPI.getLeds
- fromIndex
- toindex

## - **Buttons API**
### RobotAPI.getButtonChanges

An `InputMessage` such as:

```python
out = robot_api.getButtonChanges(InputMessage({
                'deviceId': ID, # The ID of the device
                'fromIndex': 0,
                'toIndex': -1
            }))
```

```python
{
  'measurements':[
    {'deviceId': 0, 'timestamp': 0, 'change': 0},
    ...
  ]
}
```

## - **Environmental sensor API**
### RobotAPI.getTemperatureMeasurement
- fromIndex
- toindex

### RobotAPI.getHumidityMeasurement
- fromIndex
- toindex

### RobotAPI.getPressureMeasurement
- fromIndex
- toindex

### RobotAPI.getGasMeasurement
- fromIndex
- toindex

## - **Encoders API**
### RobotAPI.getEncoderMeasurement
- fromIndex
- toindex

## - **Line follower API**
### RobotAPI.getLineFollowerMeasurement
- fromIndex
- toindex

## - **Time-of-flight API**
### RobotAPI.getToFMeasurement
- fromIndex
- toindex

## - **Sonars API**
### RobotAPI.getSonarMeasurement
- fromIndex
- toindex

## - **IRs API**
### RobotAPI.getIrMeasurement
- fromIndex
- toindex

## - **Pan-tilt API**
### RobotAPI.getPanTilt
- fromIndex
- toindex

### RobotAPI.movePanTilt
- yaw
- pitch

## - **Body motion API**
### RobotAPI.moveBody
- linearVelocity
- rotationalVelocity

### RobotAPI.getBodyVelocities
- fromIndex
- toindex

## - **IMU API**
### RobotAPI.getImuMeasurement
- fromIndex
- toindex
