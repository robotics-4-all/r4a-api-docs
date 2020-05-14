# **Time-of-flight API**

---

## *RobotAPI*.**getToFMeasurement**

Gets Time-Of-Flight sensors distance measurements from memory.

#### Input parameters

An `InputMessage`, containing in `data`:

- `deviceId`: The id of a `Devices.TOF` device
- `fromIndex`: From what index the data will be retrieved
- `toIndex`: To  what index the data will be retrieved

#### Output

An `OutputMessage`, containing in `data`:

```
measurements:
  deviceId,
  timestamp,
  value
```
