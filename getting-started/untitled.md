# Untitled

### Event-based Programming - Repeated Execution

### Global Variables:

* Variables declared at the top of the script
* variables declared outside of any function have global scope
* Global Variables should be initialized in the setup function
* Animation Variables - a variable's value gets re-initialized each frame if it is declared inside draw\( \)

### Initialization: setup is executed one time

`void setup( ) {   //code   }`     
 **Processing event function - for initialization - auto-executed once**

### Draw Loop

`void draw( ){  //code }`      
 **Processing event function - auto-executed: event looping: 60 frames/second**

### Static vs Active Mode

**static vs. active mode -** all code, other than global variable declaration/ initialization must be within functions.  
Do not have any code outside of a function definition

println\( “label “ + value\)  for debugging

comments for labeling and debugging

