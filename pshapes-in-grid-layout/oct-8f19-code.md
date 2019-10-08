Class Code - Tuesday Oct 8 F19

Function to Create 1D array of PShapes - **populateShapeList**

Function to Display 1D array of PShapes in 2D grid layout  **displayShapes:**

```java
//Create 1D array of PShape data with linear variation in color and size


void setup(){
  size( 600, 600);
  colorMode(HSB, 360, 100, 100);
  background(0);
  color purple = color( 280, 100, 100);
  //PShape myShape = createShape1( 100, purple);  //does the shape work?
  //shape( myShape, 0,0);
  int rows = 20;
  int cols = 20;
  PShape[] myShapes = new PShape[ rows*cols ]; //num elements is rows*cols
  float cellSize = width/cols;
  populateShapeList( myShapes, cellSize);
  displayShapes( myShapes, cellSize, rows, cols);
}


//display the 1D array in a 2D grid layout
//use for-loops for grid layout:  
//index i: rows, outer loop
//index j: cols, inner loop
//variable k:  used to step through the 1D array of Data
void displayShapes(  PShape[] shapes, float cellSize, int rows, int cols  ){
  float xPos = 0;  //incrementally add cellSize to move right, along column grid-units, set to 0 for each new row
  float yPos= 0;  //incrementally add cellSize to move down, along rows grid-units
  int k=0; //index to access each PShape in the shapes array
  //loop to display in grid:  
  for( int i=0; i< rows; i++){ //outer loop: rows
    for( int j=0; j< cols; j++){ //inner loop: cols
    
    PShape tempShape = shapes[k]; //get one shape from the array of data
    
    //draw one shape in a grid cell
    shape( tempShape, xPos, yPos); //display one shape at current xPos, yPos
    
    xPos += cellSize; //move to the next column 
    k++; //move to the next PShape in the shapes[]
    } //end inner loop - cols
    //change for next row
    xPos=0; //reset to 0 for columns in next row
    yPos += cellSize; //move down to next row
  } //end outer loop - rows
} //end fuction displayShapes

//populateShapeList: function takes a 1D array of PShapes as input parameter
//After executing populateShapeList, the array elements have been initialize with PShape data.
void populateShapeList( PShape[] shapes, float len   ){
  int numShapes = shapes.length;   //how many elements in the array
  for( int i=0; i< numShapes; i++){
    //use linear changing i value to calculate linear change in hue
    int hue = (int)map( i, 0, numShapes-1,100,260);  
    color curColor = color( hue, 100, 100);
    
     //use linear changing i value to calculate linear change in fraction for changing len
    float fraction = map( i, 0, numShapes-1,0.2, 1.0);
    PShape curShape = createShape1( len * fraction, curColor); //create 1 shape
    shapes[ i ] = curShape; //put a shape in each array element
   } //end for-loop
} //end PopulateShapeList

//create and return a single PShape
PShape createShape1(  float len, color c1){
  //fill(c1);
  PShape s = createShape( RECT, 0,0, len, len);
  s.setFill(c1);
  return s;
}
```

