# **IRs API**

---

## *RobotAPI*.**getIrMeasurement**

Gets IR sensors distance measurements from memory.

#### Input parameters

An `InputMessage`, containing in `data`:

- `deviceId`: The id of a `Devices.IR` device
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
