# Button Class

## Class Button

```java
class Button{
  ///INSTANCE VARIABLES
  float x,y; //position
  float w,h; //size
  boolean selected; //is the button selected / on? true/false
  color selectedColor, defaultColor, currentColor;
  String label; 

  ///CONSTRUCTORS - no return type declared - match Class-name
  Button(float x, float y, float w, float h, String label ){
    this.x = x;
    this.y = y;
    this.w = w;
    this.h = h;
    this.label = label;
    selected = false;
    selectedColor = color( 280, 100, 100); ///must be HSB color
    defaultColor = color( 280, 70, 70); //slightly darker?
    currentColor = defaultColor; 
  }


  ///METHODS
  void display(){
    fill( currentColor);
    rect( x, y, w, h);
    fill( 0);//black for text
    textAlign(CENTER);
    text( label, x + w/2, y + (h/2));
  }

  void clicked( int mx, int my){
    if( mx > x && mx < x + w  && my > y && my < y+h){
      //mouse has been clicked
      selected = !selected;  //toggle the value between true and false
      if( selected){
          currentColor = selectedColor;
      }else{
          currentColor = defaultColor;
      }
    }
  }



}  //end Button class
```

## Main Tab Code - Using Buttons

```java
Button btn1;   //data-type, variable-name   //null
int x;    //data-type, variable-name  //0

///Initialize things - variables
void setup(){
  size( 600, 600);
  colorMode(HSB, 360, 100, 100);
  x= 10; //initialize the variable
  btn1 = new Button( 10, 10, 100, 100, "Press" );  //initialize by calling a Button constructor
}

//makes it a frame-based application
void draw( ){
  btn1.display(); //have the button instance call it's display( ) method
}

//add code for mouseClicked
void mouseClicked( ){
  btn1.clicked( mouseX, mouseY);
}
```
