# **Encoders API**

---

## *RobotAPI*.**getEncoderMeasurement**

Retrieves encoders information from memory.

#### Input parameters

An `InputMessage`, containing in `data`:

- `deviceId`: The id of a `Devices.BUTTON` device
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
