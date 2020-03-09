# Example Code S2020

```java

//setup is called one time to initialize config and variables
void setup(){
  size( 600, 600);
  colorMode(HSB, 360, 100, 100); 
 
  //we will display in a grid 
  int rows; //declare variable - default value of 0
  rows = 10; //initialize the variable
  int cols = 10; 
  int cellSize = width/cols; //red flag - integer division - truncation
  ///Initialize the array
  PShape[] myShapes; ///declare the array - default value: null
  myShapes = new PShape[  rows * cols ]; //initialize array
  
  populateShapeList( myShapes, cellSize); //call the function
  shape( myShapes[0], 0, 0); //display one shape
}

void displayShapes(  PShape[] shapes, int cellSize, int rows, int cols ){
  
}


void populateShapeList(  PShape[] shapes, int cellSize  ){
  int count = shapes.length;  //the array knows how many elements
  for( int i=0; i< count;  i++){
    
    float hue = map( i, 0, count-1, 0, 360); //full ROYGBIV hue
    color curColor = color( hue, 100, 100); //
    
    PShape s = createShape( RECT, 0,0, cellSize *.9, cellSize *.9);
    s.setFill( curColor);
    
    shapes[ i ] = s; //set one element of the array to the current PShape
    
  } //end for-loop


} //end function
```

