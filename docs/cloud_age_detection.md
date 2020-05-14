# Age detection API
---

## *CloudAPI*.**detectAgeFromImage**

Detects age using the camera. It captures an image, performs face detection and if a face is found it tries to detect its age.

#### Input parameters

An `InputMessage`, containing in `data`:

- `file`: The file path of the image

#### Output

The TekVariables affected are:

- `TekVariables.AGE_DETECTION_DETECTED`: Bool value denoting the detection success
- `TekVariables.AGE_DETECTION`: The age
