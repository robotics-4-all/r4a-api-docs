# **IMU API**

---

## *RobotAPI*.**getImuMeasurement**

Gets last IMU measurements from memory.

#### Input parameters

An `InputMessage`, containing in `data`:

- `deviceId`: The id of a `Devices.IMU` device
- `fromIndex`: From what index the data will be retrieved
- `toIndex`: To  what index the data will be retrieved

#### Output

An `OutputMessage`, containing in `data`:

```
measurements: [
  deviceId,
  timestamp,
  acceleration: {
    x,
    y,
    z
  }
  compass: {
    yaw,
    pitch,
    roll
  }
  gyroscope: {
    yaw,
    pitch,
    roll
  }
]
```
