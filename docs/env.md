# **Environmental sensor API**

---

## *RobotAPI*.**getTemperatureMeasurement**

Gets temperature measurements from memory.

#### Input parameters

An `InputMessage`, containing in `data`:

- `deviceId`: The id of a `Devices.ENV` device
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

---

## *RobotAPI*.**getHumidityMeasurement**
Gets humidity measurements from memory.

#### Input parameters

An `InputMessage`, containing in `data`:

- `deviceId`: The id of a `Devices.ENV` device
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

---

## *RobotAPI*.**getPressureMeasurement**
Gets pressure measurements from memory.

#### Input parameters

An `InputMessage`, containing in `data`:

- `deviceId`: The id of a `Devices.ENV` device
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

---

## *RobotAPI*.**getGasMeasurement**
Gets gas measurements from memory.

#### Input parameters

An `InputMessage`, containing in `data`:

- `deviceId`: The id of a `Devices.ENV` device
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
