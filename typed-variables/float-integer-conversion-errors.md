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


 3. **Mathematical Operators** - must operate on operands of the same data-type. Java will do _**implicit type-conversions**_. **Java will convert operands of smaller (narrower) data-types to larger (wider) types, to match the size of the largest operand. ** This applies to both literal and variable operands.
 
 In the code below, we have 2 different types of operands, 5.0 is a decimal value, (a double by default), and 2 is an integer value.  The java compiler does a conversion, it converts the smaller data-type: integer value, to match the other operand.  So the actual expression that's evaluated is 5.0 / 2.0;  This is floating point division, the result is 2.5, and it's valid for 2.5 to be stored in a floating point type variable. No error occurs

```java

float floatVal = 5.0 / 2;  
println("floatVal " + floatVal); // floatVal = 2.5;

///Error
int intVal = 5.0 / 2; ///error occurs

```

In the code above, the error occurs when the result of the expression is assigned to a integer value...since the integer has no place to store the decimal part of the number, we're given an error to notify us that we're 'throwing away data'.

###Explicit Type-Casting
If we know that we're ok with losing data - due to truncation issues, we can use explicit type-casting, to let the compiler know that we are intensionally discarding the truncated data.  We are converting from a wider/ larger data-type to a smaller / narrower data-type:
Example float to integer conversion

**Explicit Type-Casting:  2 methods**

```java
int myIntVal1 = int( someFloatVal ); 
int myIntVal2 = (int) someFloatVal;  

//Example

int myIntVal = (int) 5.0 / 2;   //no error 

myIntVal = int( 5.0 / 2.0 );  //no error

myIntVal = (int) 5.0 / 2.0; ///error occurs since 2.0 hasn't been converted to an int
```


