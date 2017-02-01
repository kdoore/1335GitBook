#Drawing Application

Based on the simple idea of drawing patterns when the mouse is pressed, we will now create an application which gives the user more options to fine-tune their drawing. We'll start by adding functionality to clear the canvas to restart the drawing. To do that, we need to add a menu area where we'll put the drawing controls, and we'll need to create a button that can control the clearCanvas task.  

##Programming Project

Currently, the drawing application below has a default pattern which is drawn when the mouse is pressed and it is over the drawing-canvas area.  The program below has been extended to include a clear button which clears the canvas.   It will be necessary to a new state variable: ``clearBtnOn`` to keep track of the state of the clearButton which controls execution within the clearCanvas function. The ClearBtnOn is set within the mouseClicked( ) processing function.  Within the clearCanvas( ) function, we must reset the clearBtnOn state to false, once we have completed the function's task of drawing a white rectangle over the entire canvas.
In addition, we've added a button that lets us toggle the pattern that is drawn - in one state, squares are drawn, in the other state, circles are drawn.


##Starter Code for Drawing Application
We have refactored our code so that all code is now executed using functions that are called from the draw( ) function, this allows us to look at the draw function and understand the general logic of the program because we've created a separate function for each main task and we've named our functions with names that convey the task being done.  We can easily draw a flow-chart of our program's logic using the function names to describe the flow of logic in our program.

The starter code below provides the function specifications for the functions and provides an outline of the logic necessary to add a menu and a clear button to clear the canvas.  How can you modify the program so that there are even more available patterns, how can you customize the code so the patterns provide good design tools?


```java

///Drawing Application using functions
//Declare global variables - need several global variables for each button

boolean buttonState = false;  //clear button state variable
boolean pButtonState = false; //patternButton state variable 

//variables for button size and locations
int btnX, btnY, btnSize; //clear button position and size
int pBtnX,pBtnY;  //pattern button position

void setup() {
  size(600, 600);
  colorMode(HSB);
  ///initialize global variables
  btnX = 20;
  btnY = 20; 
  btnSize = 100;
  pBtnX = 20;
  pBtnY = btnY * 2 + btnSize;
}

void draw() {
  if (mousePressed) {
    translate(mouseX, mouseY);
    drawPattern();
    resetMatrix();
  }
  if(buttonState){
    clearCanvas();
  }
  drawMenu();
  drawButton(btnX, btnY, btnSize);  //draw clear button
  drawButton(pBtnX, pBtnY, btnSize);  //drawPattern button
}

//draw either rectangles or ellipses depending on the state of pButtonState
void drawPattern() {
   fill( mouseX %255, 255, 255, 100);
  if(pButtonState == true){
     rect( 0, 0, 50, 50);
  }
  else if(pButtonState == false){
     ellipse( 0, 0, 50, 50);
  }
}

void drawMenu() {
  fill(0);
  rect(0,0,150, height);  //black background
 }

void drawButton( int bX, int bY, int bSize  ){
  fill(200);
  rect( bX,bY, bSize,  bSize);  //button shape
}

void clearCanvas(){
  println("Clear canvas is executed");
  fill(255);
  rect(0,0,width, height);  //draw rectangle over canvas
  buttonState=false;  ///completed the task so turn it off
}

void mouseClicked( ){
  
  //event trigger button logic for clear button
  if(mouseX > btnX && mouseX < btnX+btnSize && mouseY > btnY && mouseY< btnY + btnSize){
    println("button has been clicked");
    buttonState =true;  //always set to true - must set to false somewhere else
  }
  
  
  //toggle logic for pattern button
  if(mouseX > pBtnX && mouseX < pBtnX+btnSize && mouseY > pBtnY && mouseY< pBtnY + btnSize){
    println("button has been clicked");
    pButtonState = !pButtonState;  //toggle between 2 states
  }
  
  
}

```


