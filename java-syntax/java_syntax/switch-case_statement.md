# Switch-Case Statement

The Switch-Case Statement is a control structure that can be used in place of a set of nested if, else-if statements, under certain conditions.

## Test Condition

In situations where a set of if, if-else statements are each testing to check the value of a single variable, and then executing specific statements when the test value matches the a valid value, then a Switch-Case statement can be used. This is often the case when using code that implements logic for a Finite State Machine, where the system is always in one state, out of a fixed set of possible states.

In the code below, in every conditional-test, we're always comparing a single value: testCondition. We are testing to see if it is equal to one of the following values: value1, value2, value3.

```java
//nested if, else-if structure

if(testCondition == value1){
    doThing1();
}
else if(testCondition == value2){
    doThing2();
}
else if(testCondition == value3){
    doThing3();
}
else{
    doDefaultThing();
}

////Implement using switch-case

switch(testCondition){
    case value1:
        doThing1();
    break;

    case value2:
        doThing2();
    break;

    case value3:
        doThing3();
    break;

    case value4:  
    case value5:  //case 4 falls through to case5 
        doThing4_5();
    break;

    default:
        doDefaultThing();

}  //end switch
```

## Fixed Set of Integral Values

The testCondition and acceptible set of values must be of `Integral Data Types`: These include: integer, char, bool.

switch-case cannot be used with: floating-point / fractional values or object data-types.

As of Java 7, switch-case can be used with string values:

```
String color = "red";  

 switch (color) {  
    case "red":  
        println("Color is Red");  
    break; 

    case "green":  
        println("Color is Green"); 
    break;  

    default:  
    println("Color not found");  
 }
```
