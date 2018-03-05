#2D Arrays using lerpColor and Map

The example code below shows how we can use the i, j indexes of a for-loop to create and display a grid color gradient using: lerpColor( ) and map( ).  


###Example Code 
```java
  
  //the following code is in the Procesing Setup function
  colorMode(HSB, 360, 100,100); //corresponds to the color selector
  int rows = 6;
  int cols = 6;
  int cellSize = width/cols;
  int[][] intMatrix = new int[rows][cols];//2D array of ints
  int xPos=0; //variables to control where rectangle is drawn
  int yPos = 0;
  color c1=color(157, 83, 56);
  color c2 = color(258, 66, 96);
  for( int i=0; i< rows; i++){
    for( int j=0; j< cols; j++){
         int k = i + j;
         intMatrix[i][j]= k;
         float kFraction = map( k, 0, (rows-1) + (cols-1),0.0, 1.0);
         
         color c3 = lerpColor(c1, c2, kFraction);
         fill( c3 ); ///use map? max of k is 10
         rect(xPos, yPos, cellSize, cellSize);
         xPos += cellSize; //increment for drawing the next column
    } //end of inner loop (cols)
    yPos +=cellSize; //move yPos for drawing next row
    xPos = 0;
  } //end of outer loop (rows) 

  
```
###Grid Gradient using lerpColor( ) and map( )
The image below shows i,j values and the corresponding lerpColor fractional amount that was calculated using the map function in the code above.

![](/assets/Screen Shot 2018-02-14 at 9.25.25 AM.png)
  
  


