# Example - March9

```java

//setup is called one time to initialize config and variables
void setup(){
  size( 600, 600);
  colorMode(HSB, 360, 100, 100); 
  background(0); //grayscale white?
  //we will display in a grid 
  int rows; //declare variable - default value of 0
  rows = 10; //initialize the variable
  int cols = 10; 
  float cellSize = width/cols; //red flag - integer division - truncation
  ///Initialize the array
  PShape[][] myShapes; ///declare the array - default value: null
  myShapes = new PShape[ rows][cols ]; //initialize array
  
  populateShapeMatrix( myShapes, rows, cols, cellSize); //call the function
  //shape( myShapes[0], 0, 0); //display one shape
  displayShapeMatrix( myShapes, rows, cols, cellSize);
}


void displayShapeMatrix(  PShape[][] shapes, int rows, int cols, float cellSize ){
  int xPos = 0; //where to draw each shape
  int yPos = 0; 
  for( int i=0; i< rows; i++){
    for( int j=0; j< cols; j++){
      shape( shapes[i][j], xPos, yPos); //draw one shape
      xPos += cellSize;
    } //end inner for-loop - cols
      xPos=0;
      yPos += cellSize;
  }//end outer for-loop - rows
  
}//end displayShapes



void populateShapeMatrix(  PShape[][] shapes, int rows, int cols , float cellSize ){
 
  for( int i=0; i< rows;  i++){
    for( int j=0; j< cols; j++){
    int k = i + j;
    float hue = map( k, 0, rows+cols-2, 200, 300); //full ROYGBIV hue
    color curColor = color( hue, 100, 100); //
    
    PShape s = createShape( RECT, 0,0, cellSize *.9, cellSize *.9);
    s.setFill( curColor);
    
    shapes[i][j] = s; //set one element of the array to the current PShape
    
    }//end inner for-loop
  } //end outer for-loop


} //end function
```

