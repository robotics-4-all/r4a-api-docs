# The conditions class

In R4A APIs you can create conditions using two classes, `Condition` that denotes a single condition or `ConditionGroup`, denoting a composite condition. Let's see both of them in detail.

## The `Condition` class

The `Condition` class implements a single condition. The constructor of the class is as follows:

```python
def __init__(self,
  left_operant = None,
  right_operant = None,
  operator = None,
  left_op_type = None,
  right_op_type = None,
  left_index = 0,
  right_index = 0)
```

Let's discuss on each parameter:

`left_operant` and `right_operant` are the two operants of the Condition. An operant can be either a constant value (number or string) a [TekVariable](../enums/#tekvariables-enum) or a counter variable.

The specific type of each operant is declared via the `left_op_type` and `right_op_type` parameters, which must be of type `OperantTypes enum`. The possible items are:

- OperantTypes.CONSTANT
- OperantTypes.TEK_VARIABLE
- OperantTypes.COUNTER

In case of the `OperantTypes.COUNTER`, the `left/right_operant` must be assigned the name of the counter.

The `operator` parameter declares the logical operator and is of type `RelationalOperators enum`, with items:

- RelationalOperators.EQUAL
- RelationalOperators.SMALLER
- RelationalOperators.SMALLER_EQUAL
- RelationalOperators.LARGER
- RelationalOperators.LARGER_EQUAL
- RelationalOperators.NOT_EQUAL

Finally, `left/right_index` parameters are used when an operant is of type `OperantTypes.TEK_VARIABLE`, specifying the index of the value that is going to be retrieved from memory (0 is the latest, -1 the previous etc.)

Each condition is checked, using the `check()` method, returning either True or False.

Some examples are:

```python
# Counter == 4
condition_cg62  = Condition (
  left_operant = "Counter",
  left_op_type = OperantTypes.COUNTER,
  operator = RelationalOperators.EQUAL,
  right_operant = 4.0
)
```

```python
# Latest face detection result == True
condition_cg1012  = Condition (
  left_operant = TekVariables.DETECT_FACE_DETECTED,
  left_index = 0,
  operator = RelationalOperators.EQUAL,
  right_operant = True
)
```

## The `ConditionGroup` class

The `ConditionGroup` implements composite conditions, based on more than 1 `Condition` objects. This class takes a `LogicalOperators enum` parameter in its constructor:

```python
def __init__(self, type)
```

Thus, `type` can be one of the following:

- LogicalOperators.AND
- LogicalOperators.OR
- LogicalOperators.XOR

Furthermore, conditions can be added using the `addCondition(condition, opp)` member, where condition must be of type `Condition` and if `opp` is True, the negation of the condition shall be tested.

An example is the following:

```python
condition_cg62  = Condition (
  left_operant = "Counter",
  left_op_type = OperantTypes.COUNTER,
  operator = RelationalOperators.EQUAL,
  right_operant = 4.0
)

condition_cg1012  = Condition (
  left_operant = TekVariables.DETECT_FACE_DETECTED,
  left_index = 0,
  operator = RelationalOperators.EQUAL,
  right_operant = True
)

cond = ConditionGroup(type = LogicalOperators.AND)
cond.addCondition(condition_cg62)
cond.addCondition(condition_cg1012, opp = True)
```

This condition evaluates to True if Counter is equal to 4 and face detection did not find a face in the previous check.
