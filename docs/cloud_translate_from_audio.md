# Translate audio API
---

## *CloudAPI*.**translateAudio**

Translates the dictated text from a given audio.

#### Input parameters

An `InputMessage`, containing in `data`:

- `file`: The file path of the audio
- `src`: The source language in the form of [Languages enum](../enums/#languages-enum)
- `dest`: The target language in the form of [Languages enum](../enums/#languages-enum)

#### Output

The TekVariables affected are:

- `TekVariables.TRANSLATE_AUDIO`: The result of the translation
