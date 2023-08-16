---
description: Started code for PImageButton Child Class
---

# Code Mon Apr 13

#### Summary:           &#x20;

* This code has 3 tabs, the PImageButton tab will have errors
* Make sure to grab the image from the PImageButton page and put in a data folder in your    project
* Main tab shows logic to display a PImage as a test that the image file is loaded correctly.
* Fixed errors in the Button class that caused colors not to display correctly
* Added logic in Button class to display the text: label

Main Tab&#x20;

```
//Main Tab
//Make objects, objects call methods

//Make an object instance

Button btn1;//declare the variable as global - btn is null

void setup(){
  size( 600, 600);
  colorMode(HSB, 360, 100, 100);
  
  PImage img1 = loadImage( "pattern1Btn.png");
  image( img1, 100, 100);  //test to make sure you can display image
  
  // Button( float x, float y, float w, float h, String label  )
  btn1 = new Button( 20, 20, 100, 100, "Hello");  //initialize
}

void draw(   ){
  btn1.display();
 }
 
 void mouseClicked(   ){
   btn1.clicked( mouseX, mouseY);
 }
```

```
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
    defaultColor = color( 280, 70,50);//dull, dark version
    currentColor = defaultColor;
    
    selected = false; //button starts in off state
  } //end constructor
  
  //METHODS , functions an object can execute for behaviour
  
  void display(  ){
    fill(currentColor);
    rect( x, y, w, h); 
    fill(0); //set fill to black
    textAlign(CENTER); //x,y specifies center line of text
    text( label, x+ w/2.0, y+ h/2.0 + 10);
  }
  
   void clicked( int mx, int my){  //mouseX, mouseY
    if( mx > x && mx < x+w && my> y && my< y+h){  //mouse is inside button box
      selected = !selected; //toggle the value 
      //println("btn has been clicked, selected value " + selected);
      if( selected){
        currentColor = selectedColor;
      }else{
        currentColor = defaultColor;
      } //end else
    }//if 
  } //clicked method
    
}//end class
```

```
//This tab will cause errors, it's missing code
//child class of Button class

class PImageButton extends Button{
  //Variables - Data
  PImage img;
  
  //CONSTRUCTORS
  //Button( float x, float y, float w, float h, String label  )
  PImageButton( float x, float y, float w, float h, PImage img   ){
    
  } //end constructor
  
  //METHODS - Behaviours
  
} //end class
```
