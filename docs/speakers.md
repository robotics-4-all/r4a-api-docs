# **Speakers API**

---

## *RobotAPI*.**speak**

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

---

## *RobotAPI*.**replaySound**

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

## *RobotAPI*.**getSound**

Retrieves a soud file from memory, using a specific speaker.

#### Input arguments

- `deviceId`: The id of a `Devices.SPEAKERS` device
- `fromIndex`: From what index the data will be retrieved
- `toIndex`: To  what index the data will be retrieved

#### Output / Variables

Returns an `OutputMessage`, of the following datframe:

```
measurements: [
  deviceId
  timestamp
  is_file
  file
  volume
]
```
