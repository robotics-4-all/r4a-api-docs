## **Microphone API**

---

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
