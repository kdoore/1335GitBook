#Create 2D Array of PShapes
In the code below, we'll modify our [simple 2D arrays project](/2d-arrays-with-lerpcolor.md) so that we're now creating PShape objects for each 2D Array element (instead of using processing rect()), then we'll display those PShape in a second step of the process.

###PShape[ ][ ] ShapeMatrix
In the code below, we'll create a 2D array of PShapes using the Processing PShape methods, we'll use the calculated gradient color to PShape: setFill( color ) method for each PShape. Then we'll before display each PShape using the PShape: shape( PShape, x, y ) method 



```java

  int rows = 6;
  int cols = 6;
  int cellSize = width/cols;
  PShape [][]shapeMatrix = new PShape[rows][cols];
  //int[][] intMatrix = new int[rows][cols];//2D array of ints
  int xPos=0; //variables to control where rectangle is drawn
  int yPos = 0;
  color c1=color(157, 83, 56);
  color c2 = color(258, 66, 96);
  for( int i=0; i< rows; i++){
    for( int j=0; j< cols; j++){
         int k = i + j;
         //calculate fill color
         float kFraction = map( k, 0, (rows-1) + (cols-1),0.0, 1.0);
         color c3 = lerpColor(c1, c2, kFraction);
         
        //create the shape 
        PShape curShape = rectPattern( cellSize-10, c3);
         
         //store shape in 2D array
         shapeMatrix[i][j]= curShape;  //store in 2D array
        ///display shape
         shape(curShape, xPos, yPos); 
           
         xPos += cellSize; //increment for drawing the next column
    } //end of inner loop (cols)
    yPos +=cellSize; //move yPos for drawing next row
    xPos = 0;
  } //end of outer loop (rows) 
}

//function to create a PShape rect
PShape rectPattern( float len, color c1){
  PShape s = createShape( RECT, 0,0, len, len);
  s.setFill(c1);
  return s;
}

```


###Alternate PShapes Grid-Pattern
In the code segments below, we use additional logic, is the value of k odd or even, calculated using modulus `k % 2`  Where we draw a circle or rectangle if odd or even, still using the color gradient logic.  

    ![](/assets/Screen Shot 2018-03-05 at 9.16.50 AM.png)    

```java

////code inside nested for-loop

PShape curShape;
if( k %2==0){
//create Shape and setFill
curShape = cirPattern( cellSize-10, c3);
} else{
curShape = rectPattern( cellSize-10, c3);
}


//function to create a PShape circle
PShape cirPattern( float len, color c1){
  PShape s = createShape( ELLIPSE, len/2,len/2, len, len);
  s.setFill(c1);
  return s;
}

```

