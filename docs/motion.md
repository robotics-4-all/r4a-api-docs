# **Body motion API**

---

## *RobotAPI*.**moveBody**

Moves the robot's chassis

#### Input parameters

An `InputMessage`, containing in `data`:

- `linearVelocity`: Linear velocity of the differential wheels vehicle
- `rotationalVelocity`: Rotational velocity of the differential wheels vehicle

#### Output

Physical: The robot moves.

---

## *RobotAPI*.**getBodyVelocities**

Gets last chassis velocities from memory.

#### Input parameters

An `InputMessage`, containing in `data`:

- `deviceId`: The id of a `Devices.MOTION` device
- `fromIndex`: From what index the data will be retrieved
- `toIndex`: To  what index the data will be retrieved

#### Output

An `OutputMessage`, containing in `data`:

```
measurements:
  deviceId,
  timestamp,
  linearVelocity,
  rotationalVelocity
```
