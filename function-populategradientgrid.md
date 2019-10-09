#Function: Populate2DArray( ) 

The code in the previous sections needs should be refactored so it's using functions, this will allow us to separate the code-logic:

- creating the shape-color units using design logic
  - Notice, there are no `xPos, yPos` variables used in `Populate2DArray`, instead, this function only populates our 2D data-structure.
  
  
- displaying the shape-color units in a grid layout
   - The layout and positioning in grid configuration will be done using a different function: [displayShapeMatrix( )](/function-displayshapematrix.md)

```java

 Populate2DArray(PShape[][] shapeMatrix, int rows, int cols, int cellSize){
  
  color c1=color(157, 83, 56);
  color c2 = color(258, 66, 96);
  for( int i=0; i< rows; i++){
    for( int j=0; j< cols; j++){
         int k = i + j;
         //calculate fill color
         float kFraction = map( k, 0, (rows-1) + (cols-1),0.0, 1.0);
         color c3 = lerpColor(c1, c2, kFraction);
         //fill( c3 ); ///use map? max of k is 10
         PShape curShape;
         if( k %2==0){
         //create Shape and setFill 
          curShape = cirPattern( cellSize-10, c3);
         } else{
          curShape = rectPattern( cellSize-10, c3);
         }
         shapeMatrix[i][j]= curShape;  //store in 2D array
     } //end of inner loop (cols)
  } //end of outer loop (rows) 
  return shapeMatrix;
}

```
###Populate2DArray - with Color input-paramters
It might be better to move the endpoint colors for the lerpColor function outside this function, so they can be passed into the function. When the colors are set inside the function, we would need a new function each time we want to use different colors, it's like the colors are hard-coded into this function.  This means we'd need to change the function signature to add the parameters, then, within the function we'd remove the code where we were initializing those colors.  


```java
 Populate2DArray(PShape[][],int rows, int cols, int cellSize, color c1, color c2)
```

###Program using PopulateGradientGrid
In the code example project below, the following code shows how we call the new function:  So, basic  
PShape[][] shapeMatrix = new PShape[rows][cols]; Populate2DArray(shapeMatrix , rows, cols, cellSize);


```java
//this code is in setup()

  int rows = 6;
  int cols = 6;
  int cellSize = width/cols;
  
  //Declare and Initialize 2D Matrix by calling refactored code in new function

PShape[][] shapeMatrix = new PShape[rows][cols] ; Populate2DArray(shapeMatrix , rows, cols, cellSize);


  
  //Code below displays each shapeMatrix item at the corresponding: row, col / x, y position. 
  
  int xPos=0; //variables to control where rectangle is drawn
  int yPos = 0;
  for( int i=0; i< rows; i++){
    for( int j=0; j< cols; j++){
        //Display Shape
         //draw the shape
        PShape curShape=shapeMatrix[i][j];
        shape( curShape, xPos, yPos);
         
         xPos += cellSize; //increment for drawing the next column
    } //end of inner loop (cols)
    yPos +=cellSize; //move yPos for drawing next row
    xPos = 0;
  } //end of outer loop (rows) 
} //end of setup

PShape vertexPattern1( float len, color c1 ){
  PShape s =  createShape( RECT, 0,0, len, len);
  s.setFill(c1);
  return s;
}
```
###Logic to render each PShape at a given x,y location 
//This code should also be refactored into a function so we can call it multiple times to have the shapeMatrix drawn at different initial x,y positions.  This is done in the following section: Function: [DisplayShapeMatrix()](/function-displayshapematrix.md)


