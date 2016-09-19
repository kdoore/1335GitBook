# Simple Button Behavior

Below is a very simple program that creates an interactive button.


```java
// Declare Global Variables

boolean on;  //buttonState
int x, y, bWidth, bHeight;

void setup () {  //initialize all values
    size (400, 400);
    colorMode(HSB);   //use HSB colorMode
    background (255, 0, 255);
    
    on=false;       //initialize to off
    //button physical dimensions
    x=50;y=50;
    bWidth=50; bHeight=50;
    stroke(150); 
}

void draw () {
   drawButton (x, y, 50, 50); 
}

//Draw 
void drawButton (int _x, int _y, int _width, int _height) {
  int hueValue, brightValue;
  brightValue = 255;
  if(on){  //checking global button state
        hueValue=100; // on color, green
        }   
        else{
        hueValue=255; // off color, red
         }
   // check to see if the mouse is over the button

  fill(hueValue, 255, brightValue);  //set fill with hueValue, brightValue
  //draw button shape
  rect(_x, _y, _width, _height);
  }


 //Event Handler Code
void mouseClicked (){  
   //check global dimensions of button 
   if (mouseX > x && mouseX < (x + bWidth) && (mouseY > y && mouseY < (y+bHeight))){
      on=!on; //change the button state
      println ("button state " + on);  
      } 
    }


```