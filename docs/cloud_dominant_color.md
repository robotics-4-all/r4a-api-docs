# Dominant color detection API
---

## *CloudAPI*.**detectDominantColor**

Captures an image and detects the dominant color in it.

#### Input parameters

An `InputMessage`, containing in `data`:

- `file`: The file path of the image

#### Output

The TekVariables affected are:

- `TekVariables.DOMINANT_COLOR_RAW`: The dominant color in raw form
- `TekVariables.DOMINANT_COLOR`: The dominant color in the form of [Colors enum](../enums/#colors-enum)
