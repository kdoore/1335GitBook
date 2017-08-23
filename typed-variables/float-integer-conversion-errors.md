#Float to Integer Conversion, Truncation, and Errors

When using mixed-types of data - integers and decimal values, it's important to understand how java handles data-type conversions when math expressions are evaluated.

###Integer Division 
When dividing 2 integer values, the result must be an integer value, so any fractional remainder is truncated.

We can think of integer division as long division where we have remainder values, the remainder is truncated: 

5 / 2 = 2  remainder  1  

5 / 2 = 2    _(remainder is truncated or thrown away)_

```java
//integer division - truncation occurs
int myIntValue = 5 / 2;  //myIntValue = 2; 
  
```
The code statement above has 2 components: 

  1. A math expression: division operation:` 5 / 2 `
  2. Assignment operation: `myValue = ` 

The _right-hand-side_: math expression is evaluated first.
The _left-hand-size:_ assignment operation occurs after the math expression has been evaluated.

1. **Expression** - code that is evaluated to result in a value.

2. **Assignment** - operation that initializes or modifies the value stored in a variable.


```java
// integer division - truncation occurs
float myFloatVal = 5 / 2;
println( "myFloatVal " + myFloatVal); // myFloatVal = 2.0

```
In the code above, the expression: 5 / 2 is evaluated first, it is integer division, since both 5 and 2 are integer literals.  The result of 5 / 2 = 2, as shown above.  Then the result of  5 / 2 is assigned to the float variable.  Since float variables have a decimal component, the value of myFloatVal is 2.0 after the assignment operation has been completed.


```java
//this is equivalent code, showing intermediate integer result 

int tempResult = 5 / 2;
float myFloatVal = tempResult;
println( "myFloatVal " + myFloatVal); // myFloatVal = 2.0
```


 3. **Mathematical Operators** - must operate on operands of the same data-type. Java will do _**implicit type-conversions**_. **Java will convert operands of smaller data-types to larger types, to match the size of the largest operand. ** This applies to both literal and variable operands.





