# **Camera API**

---

## *RobotAPI*.**captureImage**

This call captures an image from the camera.

#### Input arguments

- `width`: Desired width of captured image
- `height`: Desired height of captured image
- `save_file_url`: An absolute path for the image to be saved. If `None`, the image is not saved.

#### Output / Variables

The call returns an `OutputMessage` with the following data:

- `deviceId`: the id of the device,
- `timestamp`: the timestamp of the capture,
- `image`: the image as base 64 string,
- `width`: the width of the captured image,
- `height`: the height of the captured image,
- `format`: usually `rgb`,
- `per_rows`: True if stored by rows or by columns

#### Examples

```python
import robot_api
import utilities

rapi = robot_api.RobotAPI()

out = rapi.captureImage(utilities.InputMessage({
    'width': 800,
    'height': 480,
    'save_file_url': '/tmp/file.jpg'
}))
out.print()
```

---

## *RobotAPI*.**getImages**

Retrieves images from memory.

#### Input arguments

- `fromIndex`: The most recent index
- `toIndex`: The oldest index

#### Output / Variables

An `OutputMessage` as such:
```python
{
	'measurements': [
		{
            'deviceId': ID,
            'timestamp': 0,
            'image': "as base64 string format",
            'width': 0,
            'height': 0,
            'format': 'rgb',
            'per_rows': True # If stored by rows or by columns
		},
		...
	]
}
```

#### Examples
```python
import robot_api
import utilities

rapi = robot_api.RobotAPI()

out = rapi.getImages(utilities.InputMessage({
    'fromIndex': 0,
    'toIndex': 0
}))
```
