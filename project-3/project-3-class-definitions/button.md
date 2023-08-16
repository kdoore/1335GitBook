# Button

## Button

For this project, you will create 4 buttons. 1 Button, the clearButton, will be a basic Button using the constructor to set the x, y, w, h for the button's position and size, and then specifying 2 colors and a String, label, that's used to display text on the Button. You will also define a child class, either PImageButton or PShapeButton so you can create Buttons that display an image.

## Example Use

```java
//Button Constructor showing parameter details
//Button( int x, int y, int w, int h, color c1, color c2, String label)

//Declare and initialize
Button button1 = new Button( 10, 10, 100, 100, color1, color2, "Button1");

//display the button
button1.display();

//click the button
button1.click( mouseX, mouseY);
```

## Class Code

```java
class Button{
  ////Instance Variables - Properties
  float x, y;   //position
  float w, h;   //size dimensions
  boolean selected;
  color defaultColor, selectedColor, currentColor;
  String label;  ///text to display

  /////Constructor Methods
  /////Initialize our instance variables
  ////Overloaded versions of constructors - unique parameter lists

  Button( float _x, float y, float w, float h,  String label){
    x = _x;   //set value for class variable x, using parameter _x
    this.y = y;
    this.w = w; 
    this.h = h;
    selectedColor = color(280, 100, 100);
    defaultColor = color(280, 50,50);
    currentColor = defaultColor;  ///button is off to begin with, so use default color 
    selected = false;
    this.label = label;
  }

  Button( float _x, float y, float w, float h, color onColor, color offColor, String label){
    x = _x;   //set value for class variable x, using parameter _x
    this.y = y;
    this.w = w; 
    this.h = h;
    selectedColor = onColor;
    defaultColor = offColor;
    currentColor = defaultColor;  ///button is off to begin with, so use default color 
    selected = false;
    this.label = label;
  }

////Class Methods
  void display(){
    fill(currentColor);
    rect( x, y, w, h);
    fill(0); //black
    textAlign(CENTER);
    textSize(20);
    text(label, x + w/2, y + h/2);  //display label
  }

  //checks to see if mouse is within the button geometry
  //returns the final selected state of button //true or false
  boolean clicked(int mx, int my){
    if( mx > x && mx < x+w && my >y && my < y+h){   //button has been clicked
     selected = ! selected; //change to opposite value
      if( selected ){ //now set to selected is true
        currentColor = selectedColor;
       }else{      //not selected
         currentColor = defaultColor;
      } //end else
    }  //end outer if
    return selected; //returns true if selected 
  } ///end of clicked

    //sets the button to off state
    void reset(){
       selected = false;
       currentColor = defaultColor;
    }

    //allows us to set a button as active via code
    void setActive(){
         selected = true;
         currentColor = selectedColor;
    }


}  ///end of the Button Class
```
