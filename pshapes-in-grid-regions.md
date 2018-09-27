#PShapes in Grid Regions

In the previous section we created a function: displayShapes, to take a 1 Dimensional array of PShapes, the cellSize and the number of rows and columns in our canvas.  
```
displayShapes( PShape[] shapes, float cellSize,  int rows, int cols)
```
###Select Grid Regions - to define patterns
As we look to increase the complexity of our design, one approach would be to add logic to our nested for-loops to identify regions in each grid, where we could selectively display some portion of shapes in one of our shapes lists.

The image below shows a grid, with the (i,j) indexes for drawn in each cell.  The yellow section represents a region that we'd like to add items to.

We can define this region as having index values: `( i < 3  && j < 3 ) `

![](/assets/Screenshot 2017-09-21 14.00.02.png)

We could use logic like this to define what shapes are drawn within a region.  The logic is defined within the nested for-loops:  

`if( i < rows/2 && j < cols/2){  //draw region1 shapes   }`

###Design Based on Grid Regions 
We can see that the design below is more interesting than those previously shown. So how can we create this type of pattern where the overall design shows 4 different regions of patterns?
The next section will discuss logic to create this region-based designs. 

![](/assets/Screenshot 2017-09-22 14.51.04.png)



###Grid Logic - Select Grid Region based on i,j index values: 
In the code below, we add logic within the nested for-loops to select cells within a region.  This will get to be complex if we try to add design logic using this approach.


```java

void drawGrid(int rows, int cols, int size ){
   int xPos = 0;
   int yPos =0;
  for(int i=0;i< rows; i++){
    for( int j=0; j< cols; j++){
      if( i < rows/2 && j< cols/2){  //logic for region1
          fill(40,255,255); //yellow
          rect( xPos, yPos, size, size); //draw a yellow square for each cell in  region1
          drawLines( xPos, yPos, i, j, size);
      }
      drawLines( xPos, yPos, i, j, size);
      xPos += size;
    } //end inner for-loop: j
    xPos=0;
    yPos += size;
  } //end outer for-loop: i
 } //end drawGrid
 
 //function to draw cell boundries and i,j values
 void drawLines( int xPos,int yPos, int i, int j, int size){
   line( xPos, yPos, xPos+size, yPos); //horizontal lines
      line( xPos, yPos, xPos, yPos+size);
      textSize(14);
      textAlign(CENTER);
      fill(0);
      text( "( " + i  +", " + j + " )", xPos+(size/2) , yPos + (size/2));
}
 
 ```
 
 
 