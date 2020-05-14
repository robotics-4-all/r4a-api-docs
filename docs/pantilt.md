# **Pan-tilt API**

---

## *RobotAPI*.**getPanTilt**

Gets Pan/Tilt angles from memory.

#### Input parameters

An `InputMessage`, containing in `data`:

- `deviceId`: The id of a `Devices.PAN_TILT` device
- `fromIndex`: From what index the data will be retrieved
- `toIndex`: To  what index the data will be retrieved

#### Output

An `OutputMessage`, containing in `data`:

```
measurements:
  deviceId,
  timestamp,
  yaw,
  pitch
```

---

## *RobotAPI*.**movePanTilt**

Sets angles for the pan/tilt system

#### Input parameters

An `InputMessage`, containing in `data`:

- `deviceId`: The id of a `Devices.PAN_TILT` device
- `yaw`: The desired yaw angle
- `pitch`: The desired pitch angle

#### Output

Physical: The pan-tilt mechanism moves to the desired angles.
