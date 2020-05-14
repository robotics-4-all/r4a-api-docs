# **LEDs API**

---

## *RobotAPI*.**lightLeds**

Lights a number of LEDS on the device.

#### Input parameters

An `InputMessage`, containing in `data`:

- `devices`: List containing:
  - `deviceId`: The id of the specific LED
  - `r`: Red component of light
  - `g`: Green component of light
  - `b`: Blue component of light
  - `intensity`: The light's intensity

#### Output

Physical: The LEDs corresponding to the devices provided light up.

---

## *RobotAPI*.**ledsColorWipe**

Lights all leds in a wiping manner.

#### Input parameters

An `InputMessage`, containing in `data`:

- `r`: Red component of light
- `g`: Green component of light
- `b`: Blue component of light
- `brightness`: The light's intensity

#### Output

Physical: All LEDs light up.

---

## *RobotAPI*.**getLeds**

Gets data from leds activations which are stored in memory.

#### Input parameters

An `InputMessage`, containing in `data`:

- `deviceId`: The id of a `Devices.SPEAKERS` device
- `fromIndex`: From what index the data will be retrieved
- `toIndex`: To  what index the data will be retrieved

#### Output

An `OutputMessage`, containing in `data`:

```
measurements:
  deviceId,
  timestamp,
  value:
    r,
    g,
    b,
    intensity
```
