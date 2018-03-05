#Function: PopulateGradientGrid( ) 

The code in the previous sections needs should be refactored so it's using functions, this will allow us to separate the code-logic: designing the shape-color units, from the code-logic for: displaying the shape-color patterns 

Notice, there are no xPos, yPos variables used in PopulateShapeMatrix, instead, this function only populates our 2D data-structure, the layout and positioning in grid configuration will be done using a different function: displayShapeMatrix( )

```java

PShape[][] PopulateShapeMatrix(int rows, int cols, int cellSize){
  PShape[][] shapeMatrix = new PShape[rows][cols];
  
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
###PopulateGradientGrid - with Color input-paramters
It might be better to move the endpoint colors for the lerpColor function outside this function, so they can be passed into the function. When the colors are set inside the function, we would need a new function each time we want to use different colors, it's like the colors are hard-coded into this function.  This means we'd need to change the function signature to add the parameters, then, within the function we'd remove the code where we were initializing those colors.  

```java
PShape[][] PopulateShapeMatrix(int rows, int cols, int cellSize, color c1, color c2)
```

#Function: DisplayShapeMatrix( )


```java

void displayShapeMatrix(PShape[][] shapes, int xPos, int yPos, int rows, int cols, int size){  pushMatrix();  translate( xPos, yPos);   int x=0;   int y=0;      for( int i=0; i< rows; i++){        for( int j=0; j< cols; j++){          shape(shapes[i][j], x, y);          x += size;        }          x =0;        y += size;      }  popMatrix();}
```

