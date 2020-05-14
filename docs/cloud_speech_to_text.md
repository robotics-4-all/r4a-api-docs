# Speech-2-text API
---

## *CloudAPI*.**speechToText**

Performs automatic speech recognition in an audio file.

#### Input parameters

An `InputMessage`, containing in `data`:

- `lang`: The language of recognition
- `file`: The file path of the audio

#### Output

The TekVariables affected are:

- `TekVariables.SPEECH_TO_TEXT`: The string result of speech to text
