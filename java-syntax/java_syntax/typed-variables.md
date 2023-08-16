# Typed-Variables

Variables can be considered as named containers to hold values that can be modified. Since [Processing](http://processing.org) is based on the Java language, it uses strongly-typed variables, this means that a variable must be declared as a specific data-type before it can be used in a program; in addition, once declared, the variable cannot be modified to refer to a different type of data later in the program.

When representing data in our programs, we can consider hard-coded values as _literal_ values, and we can consider 2 main categories of variables: _primitive-type_ (value-type) , or _composite_ (reference-type) variables,.

## Literal Values

When we initialize variables, we often write a number or character symbol to represent a fixed value such as `10` for the numeric value 10. When we use literal values, these are associated with a specific type of data, for example, 10 is an integer-type literal, while 10.0 is a floating-point type of literal value.

## Primitive-Data Types

Primitive-type variables involve a single piece of information like integers: `int`, decimal numbers: `float, double`, booleans: `boolean`, and characters: `char`. Primitive-types use a fixed, system-defined size of memory-space. Primitive data-types (also called value-types) are pre-defined as part of the Java language, the primitive-type names are Java reserved keywords. [Java Reference](http://docs.oracle.com/javase/tutorial/java/nutsandbolts/datatypes.html)

## Object Data Types

Composite-type values refer to more complex data-types like arrays and objects; the memory-size required storing the data elements for complex variables, is not as easy for the system to determine when the program is being compiled. For this reason, a variable of this type actually refers to the memory-address of the starting location in memory where the data is stored. If the reference-variable does not contain a valid memory address, then it has a value of 'null'. Typically the remainder of the data is stored in adjacent memory locations. Composite-type variables are commonly called `reference` data types, these include Array, ArrayList, String, and custom Class-Objects. `Reference` variables `refer` to a location in memory where the data is stored.

## Primitive vs. Reference Data-types: Function Parameters

A major difference in behavior exists between primitive and reference data-types when they are defined as input parameters for a function. Primitive-type variables are `passed-by-value` into a function, this means that only a copy of the argument value is passed into a function, so any changes made to a local parameter within a function do not modify the value of the original variable. This is related to variable scope, when a primitive-type variable is passed as an argument to a function, changes made to the function parameter within the function body do not impact the original primitive variable. However, when composite, reference-type variables are passed into a function as arguments, then a copy of the reference-type variable is passed into the function, this means the memory address of the object is passed into the function. **Therefore, changes made within the function body to the referenced element are actually being made to the original data element.** However, it's important to notice that _it is a copy of the reference variable_ that is passed into the function, so, changes to the actual local function reference variable, such as setting it to null, do not affect the original data element.

## Object Variables

When we create custom Java Classes, we can define variables that will be associated with object-instances when a custom object is created in our code. There are 2 primary types of variables associated with Objects: Instance variables and static-Class variables. Instance variables are associated with an instance of an object, so the values of instance variables is likely different for each instance of an object that is created. Static variables can be created as a special type of class variable, these are associated with the Class itself.

## Declaration and Initialization

In the example code below, the first line of code prints the sum of 2 integer literal values. In the code that follows, `int` and `float` variables are declared and assigned values.

```
println( 5 + 7 );  //two integer literal values are added together

int num1;  //declare an integer variable

int num2 = 5;   // declare an integer and assign it a literal integer value

float num3 = 5.0 //declare a floating point variable and assign it a literal decimal value;
```

## Typed Variables

When using P5js and the Khan-Academy Javascript Tutorials, variables were all of the type `var`. There was no distinction between different types of variables. However, with The Java Version of Processing, all variables must be declared as a specific data-type such as `int`, `float`, `boolean`, `char`, etc. Typed variables allows the computer to allocate enough memory to hold the value.

## Type Conversion

When our programs are executing, the system will try to convert variables to the same data-type, and there are important reasons why we need to be aware of how the system does automatic type-conversion. In Java, the compiler checks our code to insure our code doesn't do any auto-type conversions that might cause a mathematical error in our program. The compiler follows strict rules to determine the validity of our mixed-type expressions.

## Integers

Whole numbers like -1, 0, 1, 2.

## Integer Division

When using the math division operator with integers, the resulting value is also an integer, so any fractional division remainder is truncated

```
println( 5 / 3 );     // 1 

int num1 = 5 / 2;   // 2   the remainder from division is truncated.

int num2 = 5.0 / 2  // error cannot convert from a float to an int
```

## Floats

Decimal numbers like 1.0, 5.5, -1.0. Also, whole numbers like 1, 0, 1 can be stored as floating point numbers.

When initializing floating point numbers which are created using math operators, it's important to realize that integer division can cause unexpected results. Multiplying each division expression by the `float` value _1.0_ can help insure no truncation occurs.

In the code below, since both 2 and 5 are written as integer literals, then expression 5/2 is evaluated using integer division. Make sure that at least 1 value is a decimal value to insure correct division of numbers assigned to `float` variables:

```java
float someFraction = 5 / 2;   // 2.0   integer division of 5/2 is truncated so the result is 2.0

float correctFraction = 5.0 / 2;    // 2.5  

float correctFraction2 = 5 / (2 * 1.0)  // 2.5  multiplication by 1.0 insures decimal division
```

## Integer and Float Type-Conversion

Care must be taken when using `float` and `int` variables in expressions or mathematical operations together, particularly when doing division. In general, an error will be generated if an operation will result in truncation. Processing can automatically convert an `int` to a `float` value, however an error will occur when trying to convert a `float` value to an `int` value.

```java
int num1 = 5; 
int num2 = 2;
```

```
float val1 = num1 / num2;   //2.0  integer division expression is evaluated then assigned to val1.
```

```java
int num3 = val1;    // error cannot convert from a float to an int
```

Processing provides type conversion functions to allow conversion between `int` and `float` variable types. There are 2 different but equivalent syntax conventions for type conversion displayed in the example code below:

```java
float val1 = 5.2;  

int num1 = int( val1 );  // 5   With this syntax, int( ) works like a function to convert a float value to an integer.  The value is truncated.

int num2 = ( int )val1;   //5   This syntax also works to convert a float to an  int, and results in truncation of the number.

int num3 = int( 3.0) + val1; //ERROR, val1 wasn't converted to an int

//Safe approach, use parenthesis around full expression
int num3 = int ( 3.0 + val1 ); //this converts the sum to
```

## Modulus Operator

The modulus operator `%` calculates the remainder of integer division. Modulus is often used to determine if a number is odd or even where n % 2 equals 0 if n is even. Modulus restricts values to within a limited range, example: someVal % 12; In the case where 12 is the value to the right of the modulus operator, values can range from 0 to 11, always 1 less than the modulus variable.

```java
println( 5 % 2 );   // 1    2 goes into 5 two times with a remainder of 1 (range 0 -1)
println( 5 % 3 );   // 2    3 goes into 5 one time with a remainder of 2 (range 0-2)
println( 12 % 2 );  // 0    test to determine if 12 is even, for any number n, if n % 2 = 0 then n is even. (range 0-1)
println( 2 % 5 );   // 2    5 goes into 2 zero times with a remainder of 2 (range 0-4)
```

## Boolean

Boolean variables can have the value `true` or `false`; Boolean variables are useful for storing the state some program element to control some branch option within the program, often within a conditional branch, the boolean variable value is changed to indicate the state of the program has changed.:

```java
boolean isActive = true;
if(isActive){ 
    doSomething();  //trigger some state dependent behavior     
    isActive=false  //change the state variable after the state behavior has been triggered
}
```

## Character

Single letters or other unicode symbol like 'a', 'b', 'A', '%' . The `char` variable type must use single quotes around a single character. When multiple characters are used in a single variable, then the :code: String variable type should be used.

```
char someChar = 'a';
    char otherChar = '&';
    char notAChar = "A";  //this is a string and not a charchar literal.
```

## Operators

## Random Numbers

The `random( )` function in [Processing](http://processing.org) can be used to generate psudo-random variables. The `random(float min, float max)` function takes 2 input parameters and returns a floating point number ranging from the first argument to the second argument. If only 1 argument is used, then 0 is the default minimum value.:

```
float randVal1 = random( 1 , 100 );   //returns a float between 1 and 100.
float randVal2 = random( 100 ); //returns a float between 0 and 100.
```

## Questions

> What are the values of the following?
>
> > 1. `int num1 = 2 % 10;`
> > 2. `int num2 = 10 % 2;`
> > 3. `int num3 = int(4.999);`
