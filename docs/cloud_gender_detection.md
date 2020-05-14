# Gender detection API
---

## *CloudAPI*.**detectSexFromImage**

Detects human gender from camera.

#### Input parameters

An `InputMessage`, containing in `data`:

- `file`: The file path of the image

#### Output

The TekVariables affected are:

- `TekVariables.GENDER_DETECTION_DETECTED`: Bool value denoting the detection success
- `TekVariables.GENDER_DETECTION`: The gender in the form of [Sex enum](../enums/#sex-enum)
