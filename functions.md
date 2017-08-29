#Functions


Functions allow modular design and re-usability of program components.

Functions should be designed to perform a well-defined, specific task. Functions should be designed so that they are not inter-dependent on code external to the function and so that they don't cause unintended side-effects to code outside of the function.

###Function Syntax

When writing a code for function, the following components define the syntax of a function definition. :
```java
    returnType functionName( int arg1, float arg2){  // int and float input parameters 
        // body code of a function
        return returnValue
    }
    
    ```

For an example function that adds 2 `int`   values, the function syntax is

- **function definition:** `the full code specification of a function.`
-   **function name:** `addNumbers`
-   **function return type:** `int  //the variable type of the function's return type must be declared, or it must specified as void if no value will be returned`
-   **function parameters:** `int val1, float val2 //parameters must have a declared variable-type` 
- **function arguments** `when calling a function, the values placed inside the function parentheses are called arguments, the argument values are used to initialize the function's input parameters`
- **function signature** `the name and parameter list define the signature of a function.  A function's signature specifies information about how to use, or call a function. A compiler compares functions signatures to determine if 2 identically named functions are valid overloaded functions, the parameter lists must be unique, based on data-type or number of parameters.  `  

 ```java
    //function definition
    int addNumbers( int val1, int val2){ // val1, vak2 are the functions parameters 
        int sum= val1 + int(val2);
        return sum;
    }
    
    //function call
    int arg1=4;
    int arg2=2;
    int result = addNumbers(arg1, arg2);  //arg1 and arg2 are arguments
   
   ```    

        
###Functions and Variable Scope

In [Processing](http://processing.org), variable scope is defined by code blocks which are enclosed within curly brackets: `{ }`. When designing functions, it's important to understand that function input parameters and any variables declared within the function body are local variables to the function. When a function is executed, those variables are initialized for use within the function, but when the function execution terminates, those variables are effectively destroyed, and the memory space is returned to the computer system. In contrast, global variables exist for the entire life of the program execution, they aren't destroyed until the program terminates.

When designing programs and functions, it's important to consider which variables should be global, there should be a compelling reason why any variable has global scope, **most variables should be local variables**.

###Function Parameters

When designing functions, it's helpful to think of the input parameters as being values that you'd like to have access to, that exist outside the scope of function. Often when designing functions, as you iterate through several design steps, you may decide to add more input parameters to your function so that you have more flexibility when calling the function. If the Processing `rect()` function only had x,y position as input parameters, then we'd be quite limited in how we could use the function. The addition of width and height parameters gives more flexibility. There's also another version of the `rect()` function that takes and additional parameter to specify the radius of corners so you can create rounded rectangles, this is an example of function overloading which is explained below. :

    rect(float x, float y, float width, float height, float radius); // rounded rectangle version of the rect() function

###Function Overloading

Often when designing functions, we can design multiple versions of a function, where each version of the function takes a different number or type of input parameters. In [Processing](http://processing.org) this conveniently allows for several different versions of the fill function. :

    fill(float grayScale);   //one input parameter corresponds to grayscale colors

    fill(float redVal, float greenVal, float blueVal);  //three input parameters corresponds to RGB.

    /* Using a global state variable, set with colorMode(), allows the same fill( ) function signature 
    create HSB colors while still using the same function definition. */

    colorMode(HSB);   //the the colorMode function changes a global color-state variable to control how fill() behaves

    fill(float hueVal, float saturationVal, float brightnessVal);  // now the fill color is HSB

