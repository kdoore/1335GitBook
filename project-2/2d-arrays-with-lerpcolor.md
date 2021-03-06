# 2D Arrays with lerpColor

The example code below shows how we can use the i, j indexes of a for-loop to create and display a grid color gradient using: lerpColor\( \) and map\( \). In each 2D array element, we're simply storing the value that we calculate for k, each time the inner for-loop code is executed, using the loop index variables: int k = i + j;

## Diagonal Patterns using k

We can notice that the values of k in the grid forms 2 patterns:

* Pattern1: k values across diagonal lines \(from lower-left to upper-right\) have the same value for k. We can use k to determine color, where each item along a diagonal will have the same color.  
* Pattern 2: k increases along diagonal \(from upper-left to lower-right\) k ranges from min value of: `k = 0`, to max value: `k = rows+cols-2`. We can use this information to create a color gradient along that diagonal, since lerpColor can calculate a color gradient based on a linear mapping between 2 colors.  

## Example Code

```java
  //the following code is in the Procesing Setup function
  //colorMode(HSB, 360, 100,100); //corresponds to the color selector

  void setup(){
  size(600, 600);
  colorMode(HSB, 360, 100, 100);
  int rows = 6;
  int cols = 6;
  int cellSize = width/cols;
  int[][] intMatrix = new int[rows][cols];//2D array of ints
  int xPos=0; //variables to control where rectangle is drawn
  int yPos = 0;
  color c1=color(157, 83, 56); //gradient color1
  color c2 = color(258, 66, 96); //gradient color2

  //nested for loops to calculate color gradient
  //and to draw shape in grid-layout
  for( int i=0; i< rows; i++){  //outer loop
    for( int j=0; j< cols; j++){ //inner loop
         int k = i + j; //calculate k using i,j index values
         intMatrix[i][j]= k;

         //calculate color and set fill
         float kFraction = map( k, 0, (rows-1) + (cols-1),0.0, 1.0);
         color c3 = lerpColor(c1, c2, kFraction);
         fill( c3 ); ///use map? max of k is 10

         //draw shape
         rect(xPos, yPos, cellSize, cellSize);

         //move to next column's x Position
         xPos += cellSize; //increment for drawing the next column
    } //end of inner loop (cols)
    yPos +=cellSize; //move yPos for drawing next row
    xPos = 0;
  } //end of outer loop (rows)
```

## Grid Gradient using lerpColor\( \) and map\( \)

The image below shows i, j values and the corresponding lerpColor fractional amount that was calculated using the map function in the code above.

![](../.gitbook/assets/screen-shot-2018-02-14-at-9.25.25-am.png)

