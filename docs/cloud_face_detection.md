# Face detection API
---

## *CloudAPI*.**detectFaceFromImage**

Detects human faces from camera.

#### Input parameters

An `InputMessage`, containing in `data`:

- `file`: The file path of the image

#### Output

The TekVariables affected are:

- `TekVariables.DETECT_FACE_DETECTED`: Bool value denoting the detection success
- `TekVariables.DETECT_FACE_DETECTED_NFACES`: The number of faces detected
