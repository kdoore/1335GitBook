#Pattern Preview - Transforms: Translate and Scale

If we want to get a preview of our designs, we can make a mini version below the canvas area where we are designing our grid pattern.  We'll use Processing Transform Functions, to move the origin, then a single for-loop to draw each PShape in our arrays.  

We'll need to change the canvas size, so it's larger to give space for our mini-preview.  Also, we'll need to change how we calculate the cellSize for our grid, since we're no longer using the full canvas width:

###Code to create mini pattern preview

    ```java
   void setup(){
   size( 800,800);
   int artBoard = 600; //new variable for artwork size
   int rows = 6
   int cols = 6;
   int cellSize = artBoard/rows;
   
   shapes1 = new PShape[rows * cols ];  //initialize array
   populateShapeList1(shapes1, cellSize);
   //call function to draw mini-grid
   drawMiniGrid(shapes1, 50,650,cellSize, rows, cols, .20, "Shapes1");
 
   }
    
    void drawMiniGrid(PShape[] shapes, int xPos, int yPos, float size, int rows, int cols, float scaleFactor, String label){
  pushMatrix();  //take a snapshot of current transform matrix
      translate( xPos, yPos);
      pushMatrix(); //remember translate ( ) position
      int x =0;
      int y=0;
      int shapeIndex=0;
      scale( scaleFactor );
      for( int i=0; i<rows; i++){
        for( int j=0; j< cols; j++){
        shape( shapes[shapeIndex], x,y);
        x += size;
        shapeIndex++;
        }
        x=0;
        y+= size;
      }
      popMatrix(); //undo scale, keep transform
  fill(160,255,255);
  text(label, 0,-10);   
  popMatrix();  //restore transformation matrix 
}

```

![](/assets/Screenshot 2017-09-22 14.02.40.png)