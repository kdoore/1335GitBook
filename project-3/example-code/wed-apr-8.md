---
description: First versions of code for Project 3
---

# Wed Apr 8

Main Tab - Version 1

```text
//Main Tab
//Make objects, objects call methods

//Make an object instance

Button btn1;//declare the variable as global - btn is null

void setup(){
  size( 600, 600);
  colorMode(HSB, 360, 100, 100);
  // Button( float x, float y, float w, float h, String label  )
  btn1 = new Button( 20, 20, 100, 50, "Hello");  //initialize
}

void draw(){
  btn1.display();
  
  fill( color( 280, 100, 100));
  rect( 150, 50, 100 ,50);
  
 }
 
 void mouseClicked(){
   btn1.clicked( mouseX, mouseY);
 }
```

#### Button Class version 1

Does not include code for text label

```text
class Button{
  
  //Variables, Properties, Data stored in memory
  float x,y;   //position
  float w, h; //size
  String label;
  
  color selectedColor, defaultColor, currentColor; //HSB
  
  boolean selected;  //false by default
  
  //Constructors
  Button( float x, float y, float w, float h, String label  ){
    this.x = x;
    this.y = y;
    this.w = w;
    this.h = h;
    this.label = label;
    
    selectedColor = color( 280, 100, 100); //purple
    defaultColor = color( 280, 80,80);//dull, dark version
    currentColor = defaultColor;
    
    selected = false; //button starts in off state
  } //end constructor
  
  //METHODS , functions an object can execute for behaviour
  
  void display(  ){
    fill(currentColor);
    //TODO text for label
     rect( x, y, w, h); 
  }
  
   void clicked( int mx, int my){  //mouseX, mouseY
   println("btn has been clicked");
    if( mx > x && mx < x+w && my> y && my< y+h){  //mouse is inside button box
      selected = !selected; //toggle the value 
      if( selected){
        currentColor = selectedColor;
      }else{
        currentColor = defaultColor;
      } //end else
    }//if 
  } //clicked method
    
}//end class
```

