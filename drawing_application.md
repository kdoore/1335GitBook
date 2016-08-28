#Drawing Application

Based on the simple idea of drawing patterns when the mouse is pressed, we will now create an application which gives the user more options to fine-tune their drawing. We'll start by adding functionality to clear the canvas to restart the drawing. To do that, we need to add a menu area where we'll put the drawing controls, and we'll need to create a button that can control the clearCanvas task.  

##Programming Project

Currently, the drawing application below has a default pattern which is drawn when the mouse is pressed and it is over the drawing-canvas area.  The program below has been extended to include a clear button which clears the canvas.   It will be necessary to a new state variable: ``clearBtnOn`` to keep track of the state of the clearButton which controls execution within the clearCanvas function. The ClearBtnOn is set within the mouseClicked( ) processing function.  Within the clearCanvas( ) function, we must reset the clearBtnOn state to false, once we have completed the function's task of drawing a white rectangle over the entire canvas.

[Link to live-code example](http://jsbin.com/vuqoyu/edit?js,output)

##Starter Code for Drawing Application
We have refactored our code so that all code is now executed using functions that are called from the draw( ) function, this allows us to look at the draw function and understand the general logic of the program because we've created a separate function for each main task and we've named our functions with names that convey the task being done.  We can easily draw a flow-chart of our program's logic using the function names to describe the flow of logic in our program.

The starter code below provides the function specifications for the functions and provides an outline of the logic necessary to add a menu and a clear button to clear the canvas.  How can you modify the program so that there are even more available patterns, how can you customize the code so the patterns provide good design tools?


```

//global variables 
int menuX, clearBtnX, clearBtnY, btnSize;
boolean clearBtnOn;

void setup(){
  size(800, 600);
  menuX= width -150;
  btnSize=100;
  clearBtnX= menuX + 25;
  clearBtnY= 25;
  clearBtnOn=false;
  colorMode(HSB);
  background(255);
}

void draw(){
  if(mousePressed){
     drawPattern();
  } 
  clearCanvas();
  drawMenu(menuX, 0, 150, height);
  drawClearBtn(clearBtnX, clearBtnY, btnSize);
  
} ///end draw()

void clearCanvas(){
  if( clearBtnOn==true){
    fill(122, 0, 255,100);
    rect(0,0, width, height);
    clearBtnOn=false;
  }
}  //end clearCanvas()

//function to draw menu  //parameter list
void drawMenu(int x,int y, int w, int h){
  fill(0);
  rect(x, y, w, h);
}

void drawClearBtn(int x,int y, int size){
  fill(100);
  rect(x, y, size, size);
}  //end drawClearBtn

void drawPattern(){
  ///local function variables
  float hueVal = map( mouseX, 0, width, 100, 200);
  float satVal = map( mouseY, 0, height, 50,255);
  float distance= dist( mouseX, mouseY, width/2, height/2);
  float size= map( distance,0, 500, 120,12);
  float brightVal=map(distance, 0, 200, 255,200); ///darker towards edges based on distance
  float someRandVal=random(-5,10);
  
  fill(hueVal, satVal, brightVal);  //set fill with mapped values
    
  translate(mouseX, mouseY);  //move origin to mouse position
    ellipse(0,0, size+someRandVal, size-someRandVal);
  resetMatrix();  //reset origin to initial position
}  //end drawPattern

void mouseClicked(){
  if( (mouseX >= clearBtnX && mouseX<=(clearBtnX + btnSize) ) && (mouseY >= clearBtnY && mouseY <= (clearBtnY + btnSize) ) ){
    
    println("inside button, and pressed and released");
    clearBtnOn=true;  
    }
}  


```


