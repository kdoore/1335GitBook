#Mini-Preview of Shapes  
###Transforms: Translate and Scale

If we want to get a preview of our designs, we can make a mini version below the canvas area where we are designing our grid pattern.  We'll use Processing Transform Functions, to move the origin, then a single for-loop to draw each PShape in our arrays.  

We'll need to change the project canvas size: `size(800,800)`, To create space for our mini-preview below the artwork area.  Also, we'll need to change how we calculate the cellSize for our grid, since we're no longer using the full canvas width:

The steps to create the mini-pattern preview are the same as the logic for creating a normal grid: 2 nested for-loops to position designs across columns and down rows.  The only difference here is that we're going to translate the origin to the x,y position as the first step, this way we can put the grid wherever we want.  Second, we want to scale the grid smaller, so we'll pass in a scaleFactor parameter - this will scale the entire canvas smaller, if the scaleFactor is smaller than 1. We'll use pushMatrix() and popMatrix() to wrap this logic, this will prevent our transforms from impacting other code in our program.

NewCanvasSize = scaleFactor * CanvasSize:
If scaleFactor = .20, then
160 = .20 * 800;  //mini canvas dimension is 160x160

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

![](/assets/Screenshot 2017-09-22 14.14.26.png)