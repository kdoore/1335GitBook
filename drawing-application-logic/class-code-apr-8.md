#Class Code Monday Apr 8

Here is the code in the Main tab:
You should also include the code in the following tabs:  Button, ButtonGroup



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
  //  Button(float x, float y, float w, float h, String label ){
  clearButton = new Button( 10, 10, 100, 100, "Clear" );  //initialize by calling a Button constructor

  int btnCount = 3;
  btnArray = new Button[3]; //initialize the array so it has 3 button elements
   btnArray[0] = new Button( 10, 120, 100, 100, "Btn0" ); 
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

