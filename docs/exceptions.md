# The TekException class 

We also have custom exceptions that handle errors that occur in the R4A API. These are `TekException` objects that exist in the `utilities` module.

In order to raise an exception you can write:

```python
from utilities import TekException

raise TekException("String that explains the error")
```

In order to catch TekExceptions you can write something like this:

```python
try:
  pass
  # Code here
except TekException:
  pass
  # Catches only TekExceptions
except Exception:
  pass
  # Catches all other exceptions
```

Each time a TekException is raised, a message is printed in console, containing information about which function raised the exception, in what line and what is the error message.
