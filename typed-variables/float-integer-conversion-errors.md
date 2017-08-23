###Float to Integer Conversion and Errors

When using mixed types of data - integers and decimal values, it's important to understand how java handles data-type conversions when math expressions are evaluated.


```java

int myValue = 5 / 2;    
  
```

The code statement above has 2 operations:

  1. A math expression: division operation:` 5 / 2 `
  2. Assignment operation: `myValue = ` 

The right-hand-side: math expression is evaluated first, the left-hand-size: assignment operation occurs after the math expression has been evaluated.

1. **Expression** - code that is evaluated to result in a value.

2. **Assignment** - operation that initializes or modifies the value stored in a variable.

3. **Mathematical Operators** - must operate on operands of the same data-type. Java will do _implicit type-conversions_. Java will convert operands of smaller data-types to larger types, to match the size of the largest operand.  This applies to both literal and variable operands.
 


