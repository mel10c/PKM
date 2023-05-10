# Abstract Syntax Trees

- Strings have a ***linear*** (a sequence of characters)
- Programs have a naturally ***recursive*** structure. Most data types have the potential to be nested, which mega the program recursive
- First step Python interpreter takes is to create <u>Abstract Syntax Tree (AST)</u> to represent the program

## The `Expr` class

- <u>Expression</u> - a piece of code which is meant to be evaluated, returning the value of an expression
  - Every expression would use a different attribute, so not attribute in abstract class

```python
class Expr:
    """An abstract class representting a Python expression"""
    def evaluate(self) -> Any:
        """Return the *value* of this expression
        
        The returned value should be the result of hwo this expression
        would be evaluated by the Python interpreter
        """
        raise NotImplementedError
```

### `Num` numerical literals

- Literals are the bases cases of leaves, of an AST

```python
class Num(Expr):
    """A numeric literal.
    
    Instance Attributes:
    	- n: the value of the literal
    """
    n: Union[int, float]
        
    def __init__(self, number: Union[int, float]) -> None:
        """Initialize a new numerical literal."""
        self.n = number
    
    def evaluate(self) -> Any:
        """Return ... (same as abstract class Expr)
        
        >>> expr = Num(10.5)
        >>> expr.evaluate()
        10.5
        """
        return self.n  # literal, so simply return value itself
```

### `BinOp`:  arithmetic operations

- <u>Arithmetic operation</u> - expression that consists of 3 parts: a left and right subexpression

  - The 2 operands of the expression and the operator itself

- `BinOP` is basically a binary tree. 

  - "root" - operator name; left and right "subtrees" reps the 2 operand subexpressions
  - Its "subtrees" are `Expr`, which can make the data type recursive

  > ```python
  > BinOp(Num(3), '+', Num(5.5))  # 3 + 5.5
  > 
  > # ((3 + 5.5) * (0.5 + (15.2 * -13.3)))
  > BinOP(BinOp(Num(3), '+', Num(5.5)),
  >       "*",
  >       BinOp(Num(0.5), "+",
  >             BinOp(Num(15.2), '*', Num(-13.3)))
  > ```

```python
class BinOp(Expr):
    """An arithmetic binary operation
    
    Instance Attributes:
    	- left: the left operand
    	- op: the name of the operator
    	- right: the right operand
    	
  	Representation Invariants:
  		- self.op in {'+', "*"}
    """
    left: Expr
    op: str
    right: Expr
        
    def __init__(self, left: Expr, op: str, right:Expr) -> None:
        """Initialize a new binary operation expression.
        
        Preconditions:
        	- op in {'+', "*"}
        """
        self.left = left
        self.op = op
        self.right = right
```

#### Evaluating `BinOp`

- Base case for `evaluate`

  > When `self.left.evluate()` is called, it would refer to `BinOp.evaluate` OR `Num.evaluate`, depending on the types of `self.left` and `self.right`

  - While since `Num` is a literal, the `evaluate` function does not make any change, it just returns the object's `n` attribute, this is the **base case** of the `evaluate` function.

- Recursive step is the assignment statement `self.left.evaluate()` & `self.right.evaluate()`

```python
class BinOp:
    def evaluate(selfe) -> Any:
        """Return ... (same as abstract class Expr)
        
        >>> expr = BinOp(Num(10.5), '+', Num(30))
        >>> expr.evaluate()
        40.5
        """
        left_val = self.left.evaluate()
        right_val = self.right.evaluate()
        
        if self.op == '+':
            return left_val + right_val
        elif self.op == '*':
            return left_val * right_val
        else:
            # We shouldn't reach this branch due of our representation invariant
            raise ValueError(f'Invalid operator {self.op}')
```

### Variables and the `Name` class

```python
class Name(Expr):
    """A variable expression.
    
    Instance Attributes:
    	- id: The variable name
    """
    id: str
        
    def __init__(self, id_: str) -> None:
        """Initialize a new variable epxression."""
        self.id = id_
```

#### Evaluating variables by dictionary lookup

> ```python
> >>> x + 5.5
> ```

- Ways the Python interpreter compute the value of the expression
  1. If `x` has not been defined yet, get a `NameError`
  2. Looks up a variables current value to evaluate it (requires **mapping**, use `dic`)

- If the variable has a value, it's variable name is been *mapped* to the its value using a dictionary
  - Call it <u>variable environment</u>, call each key-value pair in the environment a <u>binding</u> between the variable and its current value

```python
class Name:
    def evaluate(self, env: dic[str, Any]) -> Any:
        """ Return ... (same as abstract class Expr)
        
        The name should be looked up in the `env` argument to 
        Raise a NameError if the name is not found
        
        >>> expr = Name('x')
        >>> expr.evaluate({'x': 10})
        10
        >>> binop = BinOp(expr, '+', Num(5.5))
        >>> binop.evaluate({'x': 100})
        105.5
        """
        if self.id in env:
            return env[self.id]
        else:
            raise NameError(f"name '{self.id}' is not defined")
```

## The Statement abstract class

- All expressions are statement, but not all statement are expressions
- Create a new abstract class `Statement`, as a parent of `Expr`
  - `Statement` may have many different subclasses beyond `Expr`

```python
class Statement:
    """An abstract class representing a Python statement
    
    Think of a python statement as being a more general code than a 
    single expression, and can have some kind of "effect".
    """
    def evaluate(self, env: dic[str, Any]) -> Optional[Any]:
        """Evaluate this statement with the given environment.
        
        Should have the same effect as evaluating the statement by the real
        Python interpreter.
        
        Note that the return stype here is Optional[Any]
        evaluating could produce a value (this is true for all expressions), 
        but it might only have a *side effect* (no value produced), like mutating
        `env` or printing something
        """
        raise NotImplementedError
        
# Modified this class to be a subclass of Statement.
def Expr(Statement):
    """An abstract class representing a Python expression."""
```

### `Assign`: an assignment statement

```python
class Assign(Statement):
    """An assignment statement (with a single target).
    
    Instance Attributes:
    	- target: the variable name on the left-ahnd side of the equals sign
    	- value: the expression on the right-hand sdie of the equals sign
    """
    target: str
    value: Expr
        
    def __init__(self, target: str, value: Expr) -> None:
        """Initialize a new Assign node."""
        self.target = target
        self.value = value
    
    def evaluate(self, env: dic[str, Any]) -> ...:
        """Evaluate this statement with the given environment"""
```

