Main Tab code for Apr. 15 - You must also add code for the Pattern Class



```java

Button clearButton;   //data-type, variable-name   //null
int x;    //data-type, variable-name  //0


ButtonGroup btnGroup;  //will refer to a ButtonGroup object instance

Pattern pattern0, pattern1, pattern2, eraserPattern; ///4 patterns to match 4 buttons

///Initialize things - variables
void setup(){
  size( 600, 600);
  colorMode(HSB, 360, 100, 100);
  x= 10; //initialize the variable
  
  //Initialize Pattern Objects 
  //Place-holder PShapes
  PShape s0 = createShape( ELLIPSE, 0,0,50, 50);
  PShape s1  = createShape( ELLIPSE, 0,0,100, 50);
  PShape s2  = createShape( RECT, 0,0,100, 50);
  PShape s3  = createShape( RECT, 0,0,100, 50);
  
  //Call constructors to create the objects
  pattern0 = new Pattern( s0);
  pattern1 = new Pattern( s1);
  pattern2 = new Pattern( s2);
  eraserPattern = new Pattern( s3);
  
  //the image named below must be in a folder named 'data' 
  //that you will create inside your sketch folder
  PImage img1 = loadImage("pattern1Btn.png" );
  ///image( img1, 200,200); //test the image
  clearButton = new Button( 10, 10, 100, 100, "Clear" );  //initialize by calling a Button constructor
   
   //local variable - we use the ButtonGroup instead of the btnArray in program
   Button[] btnArray;  //declare the variable - of the Base-class type: Button  //null
   btnArray = new Button[3]; //initialize the array so it has 3 button elements
   // PImageButton(float x, float y, float w, float h, PImage img)
   btnArray[0] = new PImageButton( 10, 120, 100, 100, img1 ); 
   btnArray[1] = new Button( 10, 230, 100, 100, "Btn1" );
   btnArray[2] = new Button( 10, 340, 100, 100, "Btn2" );

   btnGroup = new ButtonGroup(btnArray); //Call constructor for ButtonGroup, pass in array
}

//makes it a frame-based application
void draw( ){
  if( mousePressed){
    pushMatrix();
    translate( mouseX, mouseY);
    fill(100, 100, 100);//set some color
    drawPattern();
    popMatrix();
  }
  displayButtons();
}

void mouseClicked( ){
  clearButton.clicked( mouseX, mouseY); 
  clearButton.reset(); //turn off like a doorbell
  btnGroup.clicked( mouseX, mouseY);
}

//Contains logic to connect ButtonGroup buttons to control which patterns is drawn
void drawPattern(){
  int activeButton = btnGroup.activeBtnIndex;
  Pattern curPattern = eraserPattern;//initailize with eraserPattern
  
 switch( activeButton ){
    
   case 0:
       ellipse( 0,0, 30, 30);
   break;
   
   case 1:
       ellipse( 0,0, 90, 30); 
   break;
   
   case 2:
        rect( 0,0, 50, 50); //square
   break;
   
   case 3:
         rect( 0,0, 100, 50); //rectangle
   break;
   
   default: 
       //none of the cases were a match
       println("no match on switch-case");
   break;
   
 } //end of switch
  
  
} //end drawPattern

void displayButtons(  ){
  clearButton.display(); //have the button instance call it's display( ) method
  btnGroup.display(); //ButtonGroup has each button display itself
}
```

