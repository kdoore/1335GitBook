#Class Code Apr 17

Main-Tab code


```java

ButtonGroup btnGroup;  //will refer to a ButtonGroup object instance

Pattern pattern1, pattern2, pattern3, eraserPattern; ///4 patterns to match 4 buttons

///Initialize things - variables
void setup(){
  size( 800, 800);
  colorMode(HSB, 360, 100, 100);
 
  bkgColor = color(50);//dark gray
  background( bkgColor);///sets the background once with bkgCOlor
  //Initialize Pattern Objects 
  //Place-holder PShapes
  PShape s0 = createShape( ELLIPSE, 0,0,50, 50); //this is fine
  PShape s1  = createShape( ELLIPSE, 0,0,100, 50);
  PShape s2  = createShape( RECT, 0,0,50, 50); //call vertexShape function
  PShape s3  = createShape( RECT, 0,0,100, 50); //call vertexShape function
  
  //Call constructors to create the objects
  eraserPattern = new Pattern( s0);  //pattern0
  pattern1 = new Pattern( s1);
  pattern2 = new Pattern( s2);
  pattern3 = new Pattern( s3);
  //the image named below must be in a folder named 'data' 
  //that you will create inside your sketch folder
  PImage img1 = loadImage("pattern1Btn.png" );
  ///image( img1, 200,200); //test the image
  clearButton = new Button( 10, 10, 100, 100, "Clear" );  //initialize by calling a Button constructor
   
   //local variable - we use the ButtonGroup instead of the btnArray in program
   Button[] btnArray;  //declare the variable - of the Base-class type: Button  //null
   btnArray = new Button[4]; //initialize the array so it has 3 button elements
   // PImageButton(float x, float y, float w, float h, PImage img)
   btnArray[0] = new Button( 10, 120, 100, 100, "Eraser" ); 
   btnArray[1] = new PImageButton( 10, 230, 100, 100, img1 );
   btnArray[2] = new Button( 10, 340, 100, 100, "Btn2" );
   btnArray[3] = new Button( 10, 450, 100, 100, "Btn3");
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
  
 switch( activeButton ){ ///connects the buttons to the patterns
        //active button sets curPattern 
   case 0: ///eraser button is ButtonArray[0]
       curPattern = eraserPattern;
       curPattern.fillColor = bkgColor;
       curPattern.strokeColor = bkgColor;
   break;
   
   case 1:
       curPattern = pattern1;
   break;
   
   case 2:
        curPattern = pattern2;
   break;
   
   case 3:
        curPattern = pattern3;
   break;
   
   default: 
       //none of the cases were a match
       println("no match on switch-case");
   break;
   
 } //end of switch
  ////once we know the current pattern, then we are setting the fill and stroke
  if( curPattern != eraserPattern){  //for all other patterns set the stroke and fill
    float hue = 280; //will be set using sliders
    float sat = 100;
    float bright = 100;
    curPattern.fillColor = color( hue, sat, bright);
    curPattern.strokeColor = color(0); //black
     }
  curPattern.display(); //display for every pattern
} //end drawPattern

void displayButtons(  ){
  fill( 0);
  rect( 0,0,120, height);
  clearButton.display(); //have the button instance call it's display( ) method
  btnGroup.display(); //ButtonGroup has each button display itself
}
```

