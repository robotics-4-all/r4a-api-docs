# Sound detection API
---

## *CloudAPI*.**detectSound**

Performs sound detection from an audio file.

#### Input parameters

An `InputMessage`, containing in `data`:

- `file`: The file path of the sound

#### Output

The TekVariables affected are:

- `TekVariables.DETECT_SOUND_DETECTED`: Bool value denoting the detection result
