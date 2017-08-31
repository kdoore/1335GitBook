# Recursion

The artwork below, created by M.C.Escher, can be considered to contain recursive patterns which have been further analyzed in the following linked research papers. Researchers have been able to design programs based on recursive functions to create computer generated versions of Escher's amazing artwork.  The white blur in the center of the first image has been analyzed by researchers who have determined that further iterations of the artwork's pattern can be integrated into the existing artwork by use of recursive functions which draw spirals of smaller versions to continue the larger existing pattern. 

###Escher:  Print Gallery From Wikipedia

![](https://upload.wikimedia.org/wikipedia/en/0/02/Print_Gallery_by_M._C._Escher.jpg)

 Article Link: [The Mathematical Structure of Escher’s Print Gallery, B. de Smit and H. W. Lenstra Jr](http://www.ams.org/notices/200304/fea-escher.pdf) 
 		 
###Escher: Circle Limit III from Wikipedia	
 		 
 ![](https://upload.wikimedia.org/wikipedia/en/5/55/Escher_Circle_Limit_III.jpg)		 
 		 
 Article Link:  [How to Create Repeating Hyperbolic Patterns Douglas Dunham](https://www.d.umn.edu/~ddunham/eccad09.pdf)
 
###Recursive Drawing
[Toby Schachman](http://tobyschachman.com/) created an interactive application that provides a visual interface for playing with recursion via 2D shape primitives. It's surprising how quickly the designs become disorienting, illustrating the power of recursion.   

![](/assets/Screenshot 2017-08-31 13.08.06.png)

###Recursion in Programming
Recursive programs refer to programs that contain at least 1 recursive function.  A recursive function is a function that has a function call to itself within the function definition. 

###Factorial:  N!
Factorial is a mathematical formula that is used when determining probabilities. One example of the use of factorials can be observed when looking at a distinct set of `n` objects, the objects can be arranged in `n!` different configurations, so there are `n permutations` of arrangements for n distinct objects.    Factorials provide a nice example of a mathematical calculation that can be easily understood, and which can be written using a recursive function, factorial can also be calculated using standard for-loops.  In section 13.6 of Shiffman's book, he provides examples of both types of functions to calculate Factorial values, a recursive version of the factorial program code is included below.  

###Recursion Call-Stack
When our program is executing, a special section of the computer's memory-space is allocated just for our program called the program's `Call Stack`.  It is important to understand how a program's `Call-Stack` operates, in order to understand how recursive functions behave when they are executing.

###Simplified Call Stack

![](stack.png)

Each time a function is called, the code for the function, as well as space for function arguments and return values, is pushed onto the top of the call stack.  When the function finishes execution, then that code it is removed or popped-off of the top of the stack.  A stack only allows items to be added to the top-end, so it is called a Last-In-First-Out (LIFO) data structure.  In contrast, a queue is a First-In-First-Out data structure. In our programs, the draw() function is constantly being pushed onto the stack, then it is popped off the stack when it's completed executing the code. We can imagine other functions may be called by processing, after the draw function has completed executing, to do such tasks as to render our image to the screen.  Then the draw() function would be pushed back onto the stack when it was called to execute again.  We can imagine the draw() function is being called by processing within a while loop, that stops running when our program is stopped. 

###Simplified Stack: Loop vs. Recursive Factorial Function

![](recursiveStack.png)

Similarly, if we use a factorial function that doesn't use recursion, but uses a for-loop, then only 1 instance of the function is repeatedly pushed onto the stack, and it remains on the stack until it has completed executing, we can see this in the diagram above, where 1 instance of the Factorial(n) function is on the top of the call-stack.  However, when we execute a recursive function, then we have many distinct instances of our function's code pushed onto the stack, with the code on the top-most instance being executed until it completes.

###Order of Execution

Below is code for the Recursive version of Factorial Program, we have added several println statements so we can better understand how the code actually executes

```java
int n;
void setup(){
  n=6;
  noLoop();
}
void draw(){
   int finalResult = factorial( n );
   println("final result " + finalResult);
}

int factorial( int n){
  println("start of factorial n= " + n);  //here is the recursive function call
  if( n == 1){  //base case 1! = 1  //return 1
    println( "base case result = 1");
    return 1;
  }
  int result = n * factorial(n - 1);
  println("end of factorial, result= " + result + " n " + n);
  return result;
}

```
![](Screenshot 2016-01-20 15.00.39.png)

From the above image we can see that the println statement within the factorial function that is located before the function calls itself gets printed in the order that the functions are called.  However, we can see that once we reach the base case, then the order changes.  As each function is completing it's calculation, it prints the end of factorial statement and then returns that value to the calling instance of the function.  So when we design recursive functions, the order of statements: before or after the recursive call has a large impact on the ordering of when the code is actually executed.

###Writing Recursive Functions
When writing recursive functions there are several factors to consider:
1. Identify the base-case or stopping condition
2. Insure that the variable that controls the stopping condition will be modified in the recursive function so that it will eventually reach the stopping condition.
3. Locate the conditional test for the stopping condition before the recursive call to prevent the recursive call from occuring when the stopping condition has been met.
4. Determine whether the function task should be performed before or after the recursive call. 
5. Insure that input parameters to the recursive function provide all information needed at each step, and be careful when modifying values passed as arguments. 
6. Be aware that each instance of a recursive function call causes a unique instance of the function's code to be placed on the `call-stack`, this can potentially cause stack-overflow errors if the program runs out of available program-execution memory space.


###Recursive Patterns:
With Recursion, we can often think of a set of rules being executed for each function call. This can be used to create interesting patterns, because we can often decompose graphic patterns to be expressed as a set of rules.  In the artwork below, a simple pattern of concentric rectangles is created wherever the mouse is pressed. 

![](Screenshot 2016-01-23 09.23.52.png)

###Recursive Pattern Drawing Application 

The recursive function: `Pattern(length, level)` takes input parameters that control the size of the rectangle and an integer value `level`, which controls the number of concentric rectangles drawn.  By adding slight random variation in the rotation angle, rectangle size, and hueValue of the fill and stroke for each drawn rectangle, the user can create a unique artwork each time they run the program.  The hueValue is mapped to the `x` position of the mouse.  Using the `Hue, Saturation, Brightness: colorMode(HSB)` allows for slight random variations of the hueValue to give slight variations in the hue of the drawn pattern.  The rules for the pattern above are:
1. When the user presses the mouse, draw a Pattern with: `level` number of concentric rectangles, the largest is size `length` 
2. Draw this pattern the current location of the mouse, so move the canvas origin to the current mouse position. 
    - translate(mouseX, mouseY) 
3. We can use frameCount and modulus to create a timer that limits the frequency that Pattern is called, this gives the user more control)
    - if( frameCount % 10 == 0) { //draw pattern at mouse position   }
3. Pattern( length, level ):
        - Save current transformation matrix: 
            - pushMatrix();
        - Determine a HueValue based on MouseX
            - hueValue=map(mouseX, 0,width, 0, 255);
        - Create a slight random variation in hueValue
            - hueValue +=random(0,30);
        - Create a slight random variation in rectSize
            - rotate(radians(randomAlphaRange))
        -Set Fill / Stroke:
            - Fill(hueValue,200,200,100);  //HSB, alpha
            - Stroke(hueVal, 200,100,200);  //same hue, darker brightness, less transparancy
        - Draw a rectangle rect(0,0,rectSize, rectSize)
        - reset to the previous transformation 
            - popMatrix();
4. Then we need to add a recursive call to Pattern so that it calls itself for `level-1` number of times, with a smaller value of length:
        - Pattern( length * .8, level-1) 
5. We need to add a test for the termination condition as the first task in the function:     
        - if(level <= 1) { return }

###Save Drawing
If we want to save our image, we can use the processing save() function and we can call it whenever we press a certain key, like 's'.  This will save our image to our sketch folder. The file can be saved in a variety of file formats.
[Processing Reference: save()](https://processing.org/reference/save_.html)

```java
void keyPressed(){
  if( key == 's' || key == 'S'){
    save("big.png");
  }
  
  ```
#Additional Examples of Recursion using Processing
For additional examples of patterns created using Recursive programs in Processing, see:  The Nature of Code, Daniel Shiffman.  Online eBook: [Chapter 8 , Section 2](http://natureofcode.com/book/chapter-8-fractals/)
