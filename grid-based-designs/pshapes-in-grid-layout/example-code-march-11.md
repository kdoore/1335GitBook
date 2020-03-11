# Example Code March 11

```java
//MARCH 11, 2020

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
  
  populateShapeMatrix1( myShapes, rows, cols, cellSize); //call the function
  //shape( myShapes[0], 0, 0); //display one shape
  displayShapeMatrix( myShapes, rows, cols, cellSize);
}

//layout in grid
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

//logic for the pattern in the data
void populateShapeMatrix1(  PShape[][] shapes, int rows, int cols , float cellSize ){
 
  for( int i=0; i< rows;  i++){
    for( int j=0; j< cols; j++){
    int k = i + j; //diagonal pattern
    color c1 = color(290, 100, 100);//magenta
    color c2 = color(240, 100, 100);//blue
    color c3 = color(0); //black
    color c4 = color(100); //dark gray
    
    float fraction = map( k, 0, rows+cols-2, 0.0, 1.0); //full ROYGBIV hue
    color fgroundColor = lerpColor( c1, c2, fraction);
    color bgroundColor = lerpColor( c3, c4, fraction);
    PShape s = vertexShape1(cellSize*fraction, fgroundColor, bgroundColor); //call custom shape function
    shapes[i][j] = s; //set one element of the array to the current PShape
    
    }//end inner for-loop
  } //end outer for-loop
} //end function

//Placeholder function - you will replace with your own custom function
PShape vertexShape1(  float len, color c1, color c2){
   PShape g = createShape(GROUP); //can have children PShapes
   PShape s0 = createShape( RECT, 0,0, len, len); //background
   s0.setFill( c2); //background color
   PShape s = createShape( ELLIPSE, 0,0, len *.6, len *.6);
   s.setFill( c1);
   
   //add children to the Group
   g.addChild( s0);
   g.addChild(s);
   
   return g;
}
```

