###Class Code - Main Tab:  Apr 10;

This code assumes you have created tabs for the following classes, and have the correct code in these tabs.

**Tabs:  Button, ButtonGroup, PImageButton**

#Main tab code
You'll need to change the name of the image file so it matches the filename for the image that you've put in a folder named: data, in your sketch folder.


```java

Button clearButton;   //data-type, variable-name   //null
int x;    //data-type, variable-name  //0

Button[] btnArray;  //declare the variable  //null
ButtonGroup btnGroup;  //will refer to a ButtonGroup object instance

///Initialize things - variables
void setup(){
  size( 600, 600);
  colorMode(HSB, 360, 100, 100);
  x= 10; //initialize the variable
  
  //the image named below must be in a folder named 'data' 
  //that you will create inside your sketch folder
  PImage img1 = loadImage("pattern1Btn.png" );//must match filename of your image
  ///image( img1, 200,200); //test the image
  
  clearButton = new Button( 10, 10, 100, 100, "Clear" );  //initialize by calling a Button constructor
  
   btnArray = new Button[3]; //initialize the array so it has 3 button elements
   // PImageButton(float x, float y, float w, float h, PImage img)
   btnArray[0] = new PImageButton( 10, 120, 100, 100, img1 ); 
   btnArray[1] = new Button( 10, 230, 100, 100, "Btn1" );
   btnArray[2] = new Button( 10, 340, 100, 100, "Btn2" );

   btnGroup = new ButtonGroup(btnArray); //Call constructor for ButtonGroup, pass in array
}

//makes it a frame-based application
void draw( ){
  displayButtons();
}

void mouseClicked( ){
  clearButton.clicked( mouseX, mouseY); 
  clearButton.reset(); //turn off like a doorbell
  btnGroup.clicked( mouseX, mouseY);
}

void displayButtons(  ){
  clearButton.display(); //have the button instance call it's display( ) method
  btnGroup.display(); //ButtonGroup has each button display itself
}
```

