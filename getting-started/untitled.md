---
description: Processing Development Environment
---

# PDE - Code Editor

### Event-based Programming - Repeated Execution

### Global Variables:

* Variables declared at the top of the script
* variables declared outside of any function have global scope
* Global Variables should be initialized in the setup function
* Animation Variables - a variable's value gets re-initialized each frame if it is declared inside draw\( \)

### Initialization: Setup is executed one time

`void setup( ) {   //code   }`     
 **Processing event function - for initialization - auto-executed once**

### Draw Loop

`void draw( ){  //code }`      
 **Processing event function - auto-executed: event looping: 60 frames/second**

### Static vs Active Mode

**static vs. active mode -** all code, other than global variable declaration/ initialization must be within functions.  
**Do not have any code outside of a function definition**

### Debugging:

**`println( “label “ + value)`**    
shows in the console when the program is executing  
helpful for debugging

**Comment syntax**:  Use for labeling and debugging  
`// single line comment  
/*  multi  
line comment */` 

