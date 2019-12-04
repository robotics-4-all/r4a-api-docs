# Enumerations and Variables

R4A APIs contain a lot of variables, as well as enumerations, to handle specific values. Their description follows. All of these are called as such:

If the name of the class is `Class` and the member is `member`, you can get the specific item by `Class.member`.

## Devices enum

Holds the different device types (sensors / effectors) that R4A API enables. The possible items are:

- Devices.SONAR
- Devices.IR
- Devices.TOF
- Devices.ENV
- Devices.IMU
- Devices.MICROPHONE
- Devices.SPEAKERS
- Devices.CAMERA
- Devices.MOTION
- Devices.PAN_TILT
- Devices.LED
- Devices.LINE_FOLLOWER
- Devices.SCREEN
- Devices.TOUCH_SCREEN
- Devices.ENCODER
- Devices.BUTTON
- Devices.UNKNOWN

`Devices` enum offers the `getTypeFromString` static function that takes as input one string and returns the type. An example follows:

```python
from utilities import Devices

str = "SONAR"
item = Devices.getTypeFromString(str)
print(item)
```

The result is `<Devices.SONAR: `sonar`>`.

## DevicePlacement enum

Holds the different placements of the devices that may have on the robot. The possible places follow. For the next items, F stands for Front, L for Left, R for Right, B for Back and G for Generic.

- DevicePlacement.F
- DevicePlacement.FL
- DevicePlacement.FR
- DevicePlacement.B
- DevicePlacement.BL
- DevicePlacement.BR
- DevicePlacement.R
- DevicePlacement.L
- DevicePlacement.G1
- DevicePlacement.G2
- DevicePlacement.G3
- DevicePlacement.G4
- DevicePlacement.FRONT
- DevicePlacement.CENTER
- DevicePlacement.RIGHT
- DevicePlacement.LEFT
- DevicePlacement.BACK
- DevicePlacement.UNDER
- DevicePlacement.PAN_TILT
- DevicePlacement.UNKNOWN

## Directions enum

Directions hold the different directions to be used either from sensors or effectors. The different options are:

- Directions.FORWARDS
- Directions.BACKWARDS
- Directions.LEFT
- Directions.RIGHT
- Directions.UP
- Directions.DOWN
- Directions.NEUTRAL

## DetectionType enum

This is used in order to specify input type for specific algorithms. The options here are:

- DetectionType.IMAGE
- DetectionType.AUDIO

## MotionType enum

Holds the possible motion types of the robot or of specific parts of it. The options are:

- MotionType.BASIC
- MotionType.SPEED_BASED
- MotionType.FOLLOW_LINE
- MotionType.ANGLE_BASED
- MotionType.TIME_BASED

## Languages enum

Holds the different languages R4A API supports. For now we have:

- Languages.EL
- Languages.EN

## Sentiments enum

Holds the different sentiments used by the algorithms. These are:

- Sentiments.HAPPY
- Sentiments.SAD
- Sentiments.CRYING
- Sentiments.NEUTRAL
- Sentiments.DELIGHTED

## Colors enum

Holds the different colors supported by the R4A API. There are:

- Colors.RED
- Colors.WHITE
- Colors.GREEN
- Colors.BLUE
- Colors.BLACK
- Colors.YELLOW
- Colors.MAGENTA
- Colors.CYAN
- Colors.UNKNOWN

## Sex enum

Holds the different sexes. These are:

- Sex.MALE
- Sex.FEMALE

## Resolutions enum

Holds the different resolutions the camera supports. These are:

- Resolutions.R_800_480
- Resolutions.R_640_480

## Format enum

Holds the different formats an image may have. These are:

- Format.JPG
- Format.PNG

## Sonars enum

Holds the different sonar placements (specific to TekTrain project). These are:

- Sonars.FL
- Sonars.FR
- Sonars.BR
- Sonars.BL
- Sonars.R
- Sonars.L

## Tofs enum

Holds the different Time of Flight sensor placements (specific to TekTrain project). These are:

- Tofs.F

## Irs enum

Holds the different IR sensor placements (specific to TekTrain project). These are:

- Irs.F
- Irs.B
- Irs.R
- Irs.L

## Tactile enum

Holds the different tactile (buttons) positions (specific to TekTrain project). These are:

- Tactile.F
- Tactile.FL
- Tactile.FR
- Tactile.B
- Tactile.BL
- Tactile.BR
- Tactile.R
- Tactile.L
- Tactile.G1
- Tactile.G2
- Tactile.G3
- Tactile.G4

## TekVariables enum

Apart from the above enumeration, there is a large enumeration that holds all the variables that are stored in [memory](memory.md). All data is stored in [Redis](https://redis.io/) and the keys the variables are stored in exist next to the variables in the list below. These variables are:

- Robot motion related
    - TekVariables.MOTION_DISTANCE_THRES = `variables.motion.distance_thres`
    - TekVariables.MOTION_DURATION_THRES = `variables.motion.duration_thres`
    - TekVariables.MOTION_LINEAR = `variables.motion.linear`
    - TekVariables.MOTION_ROTATIONAL = `variables.motion.rotational`
    - TekVariables.MOTION_DIRECTION = `variables.motion.direction`
    - TekVariables.MOTION_SPEED = `variables.motion.speed`
    - TekVariables.MOTION_TYPE = `variables.motion.type`
- Robot turn related
    - TekVariables.MOTION_TURN_TYPE = `variables.motion_turn.type`
    - TekVariables.MOTION_TURN_ANGLE = `variables.motion_turn.angle`
    - TekVariables.MOTION_TURN_DIRECTION = `variables.motion_turn.direction`
    - TekVariables.MOTION_TURN_SPEED = `variables.motion_turn.speed`
    - TekVariables.MOTION_TURN_DURATION = `variables.motion_turn.duration`
- Sleep related
    - TekVariables.SLEEP_DURATION = `variables.sleep.duration`
- Talk related
    - TekVariables.TALK_TEXTS = `variables.talk.texts`
    - TekVariables.TALK_LANGUAGE = `variables.talk.language`
    - TekVariables.TALK_VOLUME = `variables.talk.volume`
- LEDs related
    - TekVariables.LEDS_COLOR = `variables.leds.color`
    - TekVariables.LEDS_BRIGHTNESS = `variables.leds.brightness`
- Detect touch related
    - TekVariables.DETECT_TOUCH_PARTS = `variables.detect_touch.parts`
    - TekVariables.DETECT_TOUCH_DURATION = `variables.detect_touch.duration`
    - TekVariables.DETECT_TOUCH_DETECTED = `variables.detect_touch.detected`
    - TekVariables.DETECT_TOUCH_F = `variables.detect_touch.f`
    - TekVariables.DETECT_TOUCH_FL = `variables.detect_touch.fl`
    - TekVariables.DETECT_TOUCH_FR = `variables.detect_touch.fr`
    - TekVariables.DETECT_TOUCH_B = `variables.detect_touch.b`
    - TekVariables.DETECT_TOUCH_BR = `variables.detect_touch.br`
    - TekVariables.DETECT_TOUCH_BL = `variables.detect_touch.bl`
    - TekVariables.DETECT_TOUCH_L = `variables.detect_touch.l`
    - TekVariables.DETECT_TOUCH_R = `variables.detect_touch.r`
    - TekVariables.DETECT_TOUCH_G1 = `variables.detect_touch.g1`
    - TekVariables.DETECT_TOUCH_G2 = `variables.detect_touch.g2`
    - TekVariables.DETECT_TOUCH_G3 = `variables.detect_touch.g3`
    - TekVariables.DETECT_TOUCH_G4 = `variables.detect_touch.g4`
    - TekVariables.DETECT_TOUCH_PRESSED_PART = `variables.detect_touch.pressed_part`
- Camera motion related
    - TekVariables.CAMERA_MOTION_DIRECTION = `variables.camera_motion.direction`
    - TekVariables.CAMERA_MOTION_YAW = `variables.camera_motion.yaw`
    - TekVariables.CAMERA_MOTION_PITCH = `variables.camera_motion.pitch`
- Record sound related
    - TekVariables.RECORD_SOUND_NAME = `variables.record_sound.name`
    - TekVariables.RECORD_SOUND_DURATION = `variables.record_sound.duration`
    - TekVariables.RECORD_SOUND_PART = `variables.record_sound.part`
- Replay sound related
    - TekVariables.REPLAY_SOUND_NAME = `variables.replay_sound.name`
    - TekVariables.REPLAY_SOUND_VOLUME = `variables.replay_sound.volume`
- Display emotion related
    - TekVariables.DISPLAY_EMOTION_EMOTION = `variables.display_emotion.emotion`
- Weather report related:
    - TekVariables.WEATHER_REPORT = `variables.cloud.weather_report`
- Detect face related
    - TekVariables.DETECT_FACE_DURATION = `variables.detect_face.duration`
    - TekVariables.DETECT_FACE_DETECTED = `variables.detect_face.detected`
    - TekVariables.DETECT_FACE_DETECTED_FACES = `variables.detect_face.faces`
    - TekVariables.FACE_DETECTION_NFACES = `variables.cloud.face_detection.number`
    - TekVariables.FACE_DETECTION_COORDS = `variables.cloud.face_detection.coords`
- Detect age/gender related
    - TekVariables.AGE_DETECTION = `variables.cloud.age_detection`
    - TekVariables.GENDER_DETECTION = `variables.cloud.gender_detection`
- OCR detection related
    - TekVariables.OCR_DETECTION = `variables.cloud.ocr_detection`
- QR/Barcode detection related
    - TekVariables.QR_DETECTION = `variables.cloud.qr_detection`
    - TekVariables.BARCODE_DETECTION = `variables.cloud.barcode_detection`
- Detect sentiment related
    - TekVariables.DETECT_SENTIMENT_TYPE = `variables.detect_sentiment.type`
    - TekVariables.DETECT_SENTIMENT_DURATION = `variables.detect_sentiment.duration`
    - TekVariables.DETECT_SENTIMENT_DETECTED = `variables.detect_sentiment.detected`
    - TekVariables.DETECT_SENTIMENT_DETECTED_SENTIMENT = `variables.detect_sentiment.detected_sentiment`
    - TekVariables.DETECT_SENTIMENT_DETECTED_SENTIMENT_IMAGE = `variables.detect_sentiment.detected_sentiment.image`
    - TekVariables.DETECT_SENTIMENT_DETECTED_SENTIMENT_SOUND = `variables.detect_sentiment.detected_sentiment.sound`
    - TekVariables.DETECT_SENTIMENT_DETECTED_SENTIMENT_TEXT = `variables.detect_sentiment.detected_sentiment.text`
- Detect sound related
    - TekVariables.DETECT_SOUND_DURATION = `variables.detect_sound.duration`
    - TekVariables.DETECT_SOUND_DETECTED = `variables.detect_sound.detected`
    - TekVariables.SOUND_DETECTION = `variables.cloud.sound_detection`
- Detect motion related
    - TekVariables.DETECT_MOTION_DURATION = `variables.detect_motion.duration`
    - TekVariables.DETECT_MOTION_DETECTED = `variables.detect_motion.detected`
- Detect dominant color related
    - TekVariables.DETECT_DOMINANT_COLOR_DETECTED_COLOR = `variables.detect_dominant_color.color`
    - TekVariables.DOMINANT_COLOR_RAW = `variables.cloud.dominant_color.raw`
    - TekVariables.DOMINANT_COLOR = `variables.cloud.dominant_color.parsed`
    - TekVariables.MOTION_DETECTION = `variables.cloud.motion_detection`
- Speech to text related
    - TekVariables.SPEECH_TO_TEXT = `variables.cloud.speech_to_text`
- HW related
    - TekVariables.HW_BUTTON_PRESS = `variables.hw.button_press`
    - TekVariables.HW_CAMERA_IMAGE = `variables.hw.camera_image`
    - TekVariables.HW_ENCODER = `variables.hw.encoder`
    - TekVariables.HW_ENV_TEMPERATURE = `variables.hw.env.temperature`
    - TekVariables.HW_ENV_HUMIDITY = `variables.hw.env.humidity`
    - TekVariables.HW_ENV_PRESSURE = `variables.hw.env.pressure`
    - TekVariables.HW_ENV_GAS = `variables.hw.env.gas`
    - TekVariables.HW_ACCELERATION_X = `variables.hw.imu.acceleration.x`
    - TekVariables.HW_ACCELERATION_Y = `variables.hw.imu.acceleration.y`
    - TekVariables.HW_ACCELERATION_Z = `variables.hw.imu.acceleration.z`
    - TekVariables.HW_COMPASS_YAW = `variables.hw.imu.compass.yaw`
    - TekVariables.HW_COMPASS_PITCH = `variables.hw.imu.compass.pitch`
    - TekVariables.HW_COMPASS_ROLL = `variables.hw.imu.compass.roll`
    - TekVariables.HW_GYROSCOPE_YAW = `variables.hw.imu.gyro.yaw`
    - TekVariables.HW_GYROSCOPE_PITCH = `variables.hw.imu.gyro.pitch`
    - TekVariables.HW_GYROSCOPE_ROLL = `variables.hw.imu.gyro.roll`
    - TekVariables.HW_IR = `variables.hw.ir`
    - TekVariables.HW_SONAR = `variables.hw.sonar`
    - TekVariables.HW_TOF = `variables.hw.tof`
    - TekVariables.HW_LEDS_SET = `variables.hw.leds.set`
    - TekVariables.HW_LEDS_WIPE = `variables.hw.leds.wipe`
