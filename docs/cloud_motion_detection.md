# Motion detection API
---

## *CloudAPI*.**detectMotion**

Performs motion detection in a video file.

#### Input parameters

An `InputMessage`, containing in `data`:

- `file`: The file path of the video

#### Output

The TekVariables affected are:

- `TekVariables.MOTION_DETECTION`: Bool denoting the motion detection success
