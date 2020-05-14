# Counter API
---

## *GenericAPI*.**counter**

Implements a counter functionality.

#### Input parameters

An `InputMessage`, containing in `data`:

- `name`: The name fo the counter
- `set_value`: The initial value of the counter
- `change_by`: The counter change

The first time the *GenericAPI*.**counter** call is invoked with a specific counter name, this counter is initialized and `set_value` is given. Every next time, the specific counter's value changes by `change_by`.

#### Output

Alters the memory, under this key: `counters.NAME`, where the counter's value is kept.
