#Function: PopulateGradientGrid( ) 

The code in the previous sections needs should be refactored so it's using functions, this will allow us to separate the code-logic: designing the shape-color units, from the code-logic for: displaying the shape-color patterns 



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



#Function: DisplayShapeMatrix( )