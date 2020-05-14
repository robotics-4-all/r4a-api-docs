# Language detection API
---

## *CloudAPI*.**detectLanguage**

Detects the language from a given text or audio.

#### Input parameters

An `InputMessage`, containing in `data`:

- `file`: The file path of the text or audio

#### Output

The TekVariables affected are:

- `TekVariables.LANGUAGE_DETECTION`: The result of the detection
