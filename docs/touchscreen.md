# **Touch screen API**

---

## *RobotAPI*.**showImage**

Shows an image in touch screen

#### Input arguments

- `image`: The image as base64 string
- `width`: The width of the captured image
- `height`: The height of the captured image
- `duration`: How many seconds the image will be shown
- `touch`: True if touches are accepted.

#### Output / Variables

Returns an `OutputMessage` containing the following data:

```
{
  'reaction_time': The reaction time - time between the display and the touch,
  'selected': None
}
```

#### Examples

```python
import robot_api
import utilities

rapi = robot_api.RobotAPI()

out = rapi.captureImage(utilities.InputMessage({
    'width': 800,
    'height': 480,
    'save_file_url': None
}))
out.print()

out = rapi.showImage(utilities.InputMessage({
    'image': out.data['image'],
    'width': out.data['width'],
    'height': out.data['height'],
    'duration': 10,
    'touch': True
}))
out.print()
```

---

## *RobotAPI*.**showOptions**

Shows up to 4 options in the touch screen and waits for a touch.

#### Input arguments

- `options`: A list of strings
- `duration`: For how much time the options will wait for touch

#### Output / Variables

Returns an `OutputMessage` containing the following data:

```
{
  'reaction_time': The reaction time - time between the display and the touch,
  'selected': The option selected (as string)
}
```

#### Examples

An `InputMessage` as such:

```python
import robot_api
import utilities

rapi = robot_api.RobotAPI()

out = rapi.showOptions(utilities.InputMessage({
    'options': ['Option 1', 'Option 2'],
    'duration': 5
}))
out.print()
```

---

## *RobotAPI*.**showColor**

#### Input arguments

- `color`:
- `duration`: For how much time the color will wait for touch

#### Output / Variables

```
{
  'reaction_time': The reaction time - time between the display and the touch,
  'selected': The option selected (as string)
}
```

#### Examples

```python
import robot_api
import utilities

rapi = robot_api.RobotAPI()

out = rapi.showColor(utilities.InputMessage({
    'color': utilities.Colors.GREEN.value,
    'duration': 5
}))
out.print()
```
