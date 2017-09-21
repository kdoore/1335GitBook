#PShapes in Grid Regions

In the previous section we created a function: displayShapes, to take 1 array of PShapes, the cellSize and the number of rows and columns in our canvas.  
```
displayShapes( PShape shapes, float cellSize,  int rows, int cols)
```
###Pattern in Grid Regions
As we look to increase the complexity of our design, one approach would be to add logic to our for-loops to identify regions in each grid, where we could selectively display some portion of shapes in one of our shapes lists.

The image below shows a grid, with the (i,j) indexes for drawn in each cell.

![](/assets/Screenshot 2017-09-21 14.00.02.png)

