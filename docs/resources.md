# Enabling resources

In order to use a resource, you must enable it. The easier way to do this is via the `devicesObj` object, that exists in a `RobotAPI` object. Specifically there is a function called `enableDevicesType`, that takes as input a [Device](enums.md#devices-enum) and activates all respective devices.

For example, if we were to enable all microphones, we would write:

```python
import utilities
import robot_api

r = robot_api.RobotAPI()
r.devicesObj.enableDevicesType(Devices.MICROPHONE)
```
